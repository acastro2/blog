---
title: "Internal Documentation Chatbot"
date: 2023-09-30T22:47:24-05:00
image: ""
summary: ""
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


{{< buy_me_coffee >}}
