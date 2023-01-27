---
title: "Kafka Retries Go"
date: 2023-01-24T22:44:14-06:00
#draft: true
---

When doing event-driven applications using Kafka, in the consumer side, after you receiving the Kafka message, your application needs to do something with it. For this blog post lets name this part "Processing the message".

But wait, lets get everybody to the same page, what is Kafka again?

Apache Kafka is a distributed streaming platform that allows applications to process, store, and analyze large streams of data in real-time. It is designed to handle high volume, high throughput, and low latency data streams.

In Kafka, a consumer is an application that reads messages from one or more topics. Consumers subscribe to one or more topics and consume the messages that are produced to those topics. Consumers keep track of the offset of the messages that they have consumed, so that they can pick up where they left off in case of failures or restarts. Consumers can also be part of a consumer group, where each consumer in the group is assigned a subset of the partitions for a topic, allowing for parallel consumption of the data.

Now that we are all in the same page, lets create an example:

We work on a company named ACME, and we have a Kafka topic which receives a new message every time a new Customer is created and this Customer needs to receive an email saying that his account is now fully created and that they need to verify the email.

When we read something like "when something happens" do "something else", always think about events! Events, in Kafka are messages!

So now, we are going to create this microservice that will:

1. Receive this new customer message from Kafka
2. Compose a nice email
3. Send it to the customer
4. Add a new message to another topic saying that the message was sent!

Lets diagram that for more visibility:

{{<mermaid>}}
graph LR
    A[Customer App] -->|New Customer| B[(Customer Registration\n Topic)]
    subgraph Verify Email App
    C[Consume Message] -.-> |1| B
    C -->|1| D[Compose Email]
    D <-.-> E[(Email Templates)]
    C -->|2| F[Send Email]
    F -.-> G{{SMTP}}
    C -->|3| H[(Email Sent)]
    end
{{</mermaid>}}

Cool, but, this is a blog post about retries right? Where are the retries in all of it?

Well, any part of the processing can go wrong, lets name a few things that can go wrong:

* The email template database might be down.
* The template persisted inside of it might be invalid.
* The SMTP server might be down or drop a message.
* The application might compose the SMTP message badly and the SMTP server reject it.
* Producing the message to the other Kafka topic might return an error in the Kafka's server side.

Some of these errors require code/data changes, for example, to fix the template we need to update it, to correct the way the app is composing the SMTP message we need to make a code change. There's no real good way of retrying that since it will probably require manual intervation.

However, the other ones could be tried. The database might be temporarely down, producing the message might have error out out of flakiness and the SMTP server could be overloaded at that time but should be back up now.

## Enter Kafka Consumer Retries!

After this very long introduction, this problem is something that I face daily in several of our microservices. Kafka is a topic, and as such, doesn't provide retry mechanism built in. I tried multiple software architectures for retrying message processing, none of them are ideal and finally I found one that is the easiest to deal with.

### But first, let me share some background of what I tried

#### AWS SQS

I'm a strong AWS advocate, and the first thing that came to mind when thinking **retries** was almost instantaneously AWS SQS.

Let's remember what is AWS SQS again:

Amazon Simple Queue Service (SQS) is a fully managed message queuing service that enables decoupling and scaling of microservices, distributed systems, and serverless applications. SQS automatically retries failed messages with a backoff algorithm, allows for specifying a maximum retries before moving to a dead-letter queue and supports a maximum message size of **256 KB**.

So, AWS SQS is amazing, and allows for resiliency and decoupling easily and with retries backed in. But that last sentence is the real problem: SQS only goes to 256 KB while Kafka messages can have all the way up to 1 MB by default, and can even be more than that!

But then you tell me "OK Alex, but that's not a big deal", well it kinda is, because we have no good way of controlling the message size, it can grow and break your application without you even realizing! And by that time you will have lost messages or will have a big production incident in your hands.

#### Kafka

Yes, that's exactly it, since SQS its a problem, why not use Kafka itself?

I tried to spin up an application Kafka topic that's internal only to the application itself where the application would push to and in case of a failure it would enqueue it again with a new `count` attribute in the header, let me diagram that to make more sense:

{{<mermaid>}}
sequenceDiagram
    Application -->> Kafka Topic: Consume new Customer Message
    Application -->> Internal Kafka Topic: Produce message with header "count = 0"
    Application -->> Internal Kafka Topic: Consume message
    Note over Application: Process message
    Note over Application: Error Processing
    Application -->> Internal Kafka Topic: Produce message with header "count = 1"
    Application -->> Internal Kafka Topic: Consume message
    Note over Application: Process message
    Note over Application: Error Processing
    Application -->> Internal Kafka Topic: Produce message with header "count = 2"
    Application -->> Internal Kafka Topic: Consume message
    Note over Application: Process message
    Note over Application: Error Processing
    Application -->> DLQ Kafka Topic: Produce message
{{</mermaid>}}

And it works, it trully does, but it have some pretty significant downsides.

Firstly, Kafka topics are not as trivial to setup as SQS, creating multiple Kafka topics can be somewhat cumbersome, and dealing with all these consumers and producers inside the code can get really messy.

Moreover, and yet again, Kafka doesn't support retries built in, this is because the Kafka protocol is designed for high-throughput and low-latency data streaming, and retries add overhead and complexity to the system.

#### Databases

Desperate times, desperate measures, right?

Moderns SQL databases support LOCKING mechanism you can leverage that to use a table records as a queue.

{{<mermaid>}}
sequenceDiagram
    Application -->> DB: Insert new row with process_times = 0 and created_at = now()
    loop process_times
    Application -->> DB: Query order by created_at where process_times < 2 top 1 row
    Application -->> DB: Lock row
    Note over Application: Process row
    Note over Application: Error Processing
    Application -->> DB: Update row process_times column +1
    end
{{</mermaid>}}

And, believe it or not, it works!

However, it isn't great. Databases are clearly not queues and using it as such is a strech.

* Databases are built for consistency using transactions, and it can be quite performant, but it will never performe as much as something like Kafka. Hence it can easily become a bottleneck.
* Managing all of this code can easily become problematic and is not a easily pattern to share accross your entire company.

### So, what now?

After trying all of the above, having some degree of success and several degress of failure and mostly being unsatisfied with the results I decided to look at how some other companies and frameworks are doing it.

There's very little resource about that in the internet (which is one of the reasons why I'm writing this blog post). However, one of the biggest frameworks we have in existence do have a retry mechanism: Spring!

Spring is an open-source Java framework that provides a comprehensive programming and configuration model for building modern enterprise applications through multiple modules and you pick the ones you need.

One of such modules is the Spring Kafka, which provides several ways to handle retries when consuming messages, such as using the RetryTemplate and RetryCallback interfaces from the Spring Retry library to define a retry policy, using the @KafkaListener annotation to configure retry behavior on a per-method basis or using AOP to handle retries by using a RetryInterceptor. Spring Kafka allows developers to choose the approach that best fits their use case, whether it is a global retry policy or a more fine-grained per-method retry configuration.

Has been a long time that I don't work with Java, and Spring code is far from easy to understand (its pretty advanced stuff), but after a deep dive of it, this is the very shallow understand I acquired from it:

Spring implements an Error Handler using a strategy for handling exceptions thrown by the consumers. When an exception that is not a `BatchListenerFailedException` (which Spring knows is impossible to retry) is thrown, the error handler will retry the batch of records **from memory**. To prevent a consumer rebalance during an extended retry sequence, the error handler pauses the consumer, polls it before sleeping for the back off interval for each retry, and calls the listener again. If the retries are exhausted, it invokes a Consumer Record Recoverer for each record in the batch. If the recoverer throws an exception or the thread is interrupted during its sleep, the batch of records will be redelivered on the next poll. The consumer is resumed regardless of the outcome before the error handler exits.

In my honest opinion this is a really elegant solution.

### Recreating it in Golang

I currently work (and love 💙) with Go, and, as far as my research went, I didn't find any rewwrite of the Spring Kafka+Retry framework in Golang, so, lets build our own!

Here, I want to point that there's one **key difference** in our implementation, I do really like the idea of pausing the Consumer and in case of something catastrophic happen it going back to the previous record of the batch. However, I don't really think that is necessary, I preferred to implement it by:

* Creating a Consumer that will read from the topic.
* Create a go channel that will handle the retries.
* If a message fail to process, send it to the retry channel.
* The main consumer continues to process the main topic while the other messages are retried
* If the retries exhaust it sends it to a persisted DLQ for later investigation

⚠️ The **key** assumption here is that your application don't strongly care the order of the messages, so you can keep retrying a message while progressing the topic, if that's **not** the case, you will need to stop the consumer!

{{< tabs >}}
{{% tab name="python" %}}
```python
print("Hello World!")
```
{{% /tab %}}
{{% tab name="R" %}}
```R
> print("Hello World!")
```
{{% /tab %}}
{{% tab name="Bash" %}}
```Bash
echo "Hello World!"
```
{{% /tab %}}
{{< /tabs >}}
