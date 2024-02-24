---
title: AI Odyssey February Edition
seo_title: AI Odyssey February Edition
summary: 10 AI, ML and Data Science related things that excited me during February 2024.
description: 
slug: ai-odyssey-february-24
author: Marcus Elwin

draft: false
date: 2024-02-24T14:40:39+01:00
lastmod: 
expiryDate: 
publishDate: 

feature_image: 
feature_image_alt: 

categories:
    - AI
    - Machine Learning
    - Data Science
tags:
    - AI
    - ML
    - DS
series:

toc: true
related: true
social_share: true
newsletter: false
disable_comments: false
---

The month of February 2024, is soon wrapping up, and boy what a month it has been! In this post, I will introduce a new _series_ called _AI Odyssey_ where I will highlight the top **10** things such as models, announcements, releases, libraries, tools, papers and similar, within the AI, ML and DS space :robot: that have excited me the most. 

Without any inherent order or importance let's start this post!

## 1. Google releases Gemini 1.5 Pro
### What
On February, 15th, 2024 Google announced the release of [Gemini 1.5](https://blog.google/technology/ai/google-gemini-next-generation-model-february-2024/#sundar-note) just one week after rolling out Gemini 1.0 Ultra. Gemini 1.5 is a new LLM with some interesting properties:
* Dramatically enhanced performance (according to Google)
* Which is more efficient and comparable to Ultra whilst requiring less computing
* Based on a <cite>Mixture-of-Experts (MoE) architecture[^1]</cite>
* That is Multi-modal (similar to CPT-4-V)
* Improved _In-Context_ learning skills from long prompts, without needing fine-tuning
* With a standard context window of **128,000** tokens, that can be extended to **1** million tokens. 

Let that sync in a bit **1 million** tokens which is roughly **700,000+**. A "regular" book :book: has somewhere between 250-300 words per page. This would mean that you can use a book of between 2300+ pages as context to the Gemini 1.5 Pro model. 

For instance, you could feed in the entire _Lord of the Rings_ and _The Count of Monte Cristo_ at the same time as both of these books are roughly **1200** pages. 

What is further highlighted in [Google technical report](https://storage.googleapis.com/deepmind-media/gemini/gemini_v1_5_report.pdf) is
> Gemini 1.5 Pro is built to handle extremely long contexts; it has the ability to recall and reason over fine-grained information from up to at least 10M tokens. 

In terms of training the setup seems to be similar to the other Gemini models:
> Like Gemini 1.0 Ultra and 1.0 Pro, Gemini 1.5 Pro is trained on multiple 4096-chip pods of Google’s TPUv4 accelerators, distributed across multiple datacenters, and on a variety of multimodal and multilingual data. Our pre-training dataset includes data sourced across many different domains, including web documents and code, and incorporates image, audio, and video content.

Based on its multi-model capabilities Gemini 1.5 Pro manages to learn the _Kalamang_ languages:
> Given a reference grammar book and a bilingual wordlist (dictionary), Gemini 1.5 Pro is 
> able to translate from English to Kalamang with similar quality to a human who learned from the same materials.

Finally, in terms of performance, the paper also mentions:
> Our extensive evaluations with diagnostic and realistic multi-modal long-context benchmarks show 
> that 1.5 Pro is able to maintain **near-perfect recall** on multi-modal versions of needle-in-a-haystack
> (see Section 4.2.1.2) and is able to effectively use its context to retrieve and reason over large amounts of data

I always get a bit skeptical (I guess it is the DS in me) when I hear that metrics are close to 100% or near-perfect as this normally means that you are overfitting or doing something wrong. However, it is still very impressive in comparison to GPT-4-V on the same dataset. While be exciting to see more benchmarks on this going forward.

[^1]: Similar to the Mixtral model launched last year: https://mistral.ai/news/mixtral-of-experts/

### Why it interests me
For many people building Generative AI applications, hallucinations are a big issue. What people do to mitigate this is to present more relevant content using e.g. _Retrieval Augmented Generation_ (RAG), using _Guardrails_ or _fine-tuning_ the LLM to make it more domain-specific. 

Having access to **1M+** context window will for instance open up use cases to reason and ask questions around multiple documents (as there might be some dependency amongst each document). There are also speculations that the pricing of Gemini 1.5 Pro could be potentially **10x** cheaper than GPT-4[^2]. If that is the case you would get a similar or potentially better performant LLM at the price of **gpt-3.5-turbo**.

[^2]: Source: https://www.reddit.com/r/singularity/comments/1avzrp7/gemini_15_will_be_20x_cheaper_than_gpt4_this_is/

### Additional resources
1. [Gemini 1.5 Pro Announcement](https://blog.google/technology/ai/google-gemini-next-generation-model-february-2024/#sundar-note)
1. [Gemini 1.5 Pro Technical Report](https://storage.googleapis.com/deepmind-media/gemini/gemini_v1_5_report.pdf)

## 2. Google releases Gemma
__TODO__

### What
__TODO__

### Why it interests me
__TODO__

### Additional resources
__TODO__

## 3. OpenAI releases SORA
__TODO__

### What
__TODO__

### Why it interests me
__TODO__

### Additional resources
__TODO__

## 4. Predibase announces LoRA Land
__TODO__

### What
__TODO__

### Why it interests me
__TODO__

### Additional resources
__TODO__

## 5. Stability AI announces Stable Diffusion 3
__TODO__

### What
__TODO__

### Why it interests me
__TODO__

### Additional resources
__TODO__

## 6. Astral releases `uv` uber fast `Python` packaging 
__TODO__

### What
__TODO__

### Why it interests me
__TODO__

### Additional resources
__TODO__

## 7. Ollama releases `OpenAI` compatibility
__TODO__ 

### What
__TODO__

### Why it interests me
__TODO__

### Additional resources
__TODO__

## 8. Chain-of-Thought Reasoning Without Prompting
__TODO__

### What
__TODO__

### Why it interests me
__TODO__

### Additional resources
__TODO__

## 9. SiloAI completes training of Poro
__TODO__

### What
__TODO__

### Why it interests me
__TODO__

### Additional resources
__TODO__

## 10. Qroq - extremely fast LLM serving using LPUs
__TODO__

### What
__TODO__

### Why it interests me
__TODO__

### Additional resources
__TODO__
