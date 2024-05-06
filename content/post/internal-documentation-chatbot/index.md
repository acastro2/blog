---
title: "Internal Documentation Chatbot"
date: 2023-09-30T22:47:24-05:00
image: ""
description: ""
draft: true
---

Lately, AI has captured my attention, a sentiment that seems to resonate far and wide, especially since ChatGPT made its release. It’s like having a clever copilot always at the ready, sharpening my skills and making the daily work grind a tad more enlightening. It's enabled me to be a better problem-solver, software architect, and coworker in general.

But, there was this itch I couldn’t scratch. ChatGPT was clueless about the specifics of my job because it didn't have knowledge about the company's internal documentation. Sure, there were methods to enable ChatGPT on it from the get-go, but none of them were a walk in the park.

Then, LlamaIndex came along and it felt like someone handed me the keys to the kingdom. It got me thinking, why not build a chatbot for my company? A bot that’s powered by ChatGPT (or whichever model you fancy) and is well-versed in internal documentation. The real bargain is, we can now pull in documentation from anywhere, because today, everything is an API away.

## What is ChatGPT again?

In case you have been living under a rock for the past year:

[ChatGPT](https://chat.openai.com/) is like this very smart companion that materialized from OpenAI's labs, designed to chew on words and spit out coherent, human-like text. At its core, it's a model trained on a mountain of text data, making it quite the conversationalist. Whether you're drafting emails, coding, or just in need of a digital buddy to chat with, ChatGPT is up for the task. It's not just a step, but a leap toward making machines get the gist of our human chatter.

## And what is LlamaIndex?

[LlamaIndex](https://www.llamaindex.ai/) it’s the bridge that takes your LLM applications from good to mind-blowing by injecting a dose of your own data into the mix. It does that in three steps:

* Data Ingestion: Picture a massive funnel that swallows down all the data you've got, be it from APIs, PDFs, documents, or SQL, and preps it to play nice with large language models.

* Data Indexing: Once it’s got your data, it files it away in a digital cabinet, ready to be summoned whenever needed. It's like having a super organized librarian who knows exactly where each piece of info is stashed.

* Query Interface: This is where the magic happens. You throw a question into LlamaIndex, and it filters through your data, associating with the large language model, to hit you back with a knowledge-packed answer. It's like having a smart, data-savvy buddy ready to dive into a sea of information to fetch the pearls of wisdom you need.

## The Idea



Ready to dive into the nitty-gritty of setting this up with AWS Lambdas, LlamaIndex, AWS Lex, and DynamoDB?

<<Diagram>>

## Data Crawling

Implementing the data crawler lambda and orchestrating it with cloudwatch triggers is a breeze. The only thing you need to do is to define the data source and the data destination. The data source can be a URL, a PDF, a document, or an API. The data destination is a DynamoDB table. The crawler will fetch the data from the source and store it in the destination table.

```python
```

Here I implemented this interface so you can extend that to support any other data sources you can think of.

### Processing and storing the data

LlamaIndex requires a few stores for it to work:

* Document stores: where ingested documents (i.e., Node objects) are stored,
* Index stores: where index metadata are stored,
* Vector stores: where embedding vectors are stored.
* Graph stores: where knowledge graphs are stored (i.e. for KnowledgeGraphIndex).

However, this is all abstracted away from you and LlamaIndex supports a ton of databases to store your data: https://gpt-index.readthedocs.io/en/latest/core_modules/data_modules/storage/vector_stores.html for you to store you data on.

I decided to store these in DynamoDB (because its probably my favorite NoSQL database).

Processing and persisting the data is very easy:

```python
```

## Now the magic: Querying the data

Now I have created another AWS Lambda only for querying the data. <<I need to explain how to query the data, because I don't really understand it well>>

```python
```

## The Chatbot

For my use case, I would like to render this chatbot in a web UI from another internal application we have. I'm not the strongest frontend developer, hence, I decided to start from something that is already built and extend it, I selected this really nice repository to start from https://github.com/mckaywrigley/chatbot-ui-lite. It's a really nice chatbot UI built with React, Redux and Tailwind.

However, I wanted to make this more future proof, because I can see the potential for it to grow, hence, I decided to use AWS Lex to interface between the lambda and the UI.

> AWS Lex is a service that allows you to build conversational interfaces into any application using voice and text. Lex provides the advanced deep learning functionalities of automatic speech recognition (ASR) for converting speech to text, and natural language understanding (NLU) to recognize the intent of the text, to enable you to build applications with highly engaging user experiences and lifelike conversational interactions. With Amazon Lex, the same deep learning technologies that power Amazon Alexa are now available to any developer, enabling you to quickly and easily build sophisticated, natural language, conversational bots (“chatbots”).

The key reason why I decided to use AWS Lex, is because I can setup the LlamaIndex query lambda as the fallback functionality for Lex. So, if Lex doesn't understand the user's input, it will call the LlamaIndex query lambda to try and find an answer. However, I can build intentions on top of Lex that will allow me to create more complex interactions with the user, like for example:

* Schedule a topic for our internal office hours
* Request a new feature in some application, which will create a ticket in Jira ticket for the correct team to pick up
* <<think of other examples>>

All of these can be accomplished with AWS Lex, and I can use the LlamaIndex query lambda as a fallback for more general questions.

However, I would like to make it clear, that if you don't have the intention of extending this as a chatbot, you can put the query lambda behind an API Gateway and call it directly from the UI.

But enough talk, lets look at some code, the repository above talks directly with ChatGPT, so we need to implement a new interface to talk with AWS Lex.

```typescript
```

{{< buy_me_coffee >}}
