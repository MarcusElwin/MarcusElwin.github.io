---
title: AI Odyssey February Edition
seo_title: AI Odyssey February Edition
summary: 10 AI, ML and Data Science-related announcements that excited me during February 2024.
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
    - AI Odessy

toc: true
related: true
social_share: true
newsletter: false
disable_comments: false
---

The month of **February 2024**, is soon wrapping up, and boy what a month it has been! In this post, I will introduce a new _series_ called _AI Odyssey_ where I will highlight the top **10** announcements (_in my humble opinion_) in terms of models, releases, libraries, tools, papers and similar, within the AI, ML and DS space :robot: that have excited me the most. 

Without any _inherent_ order or _importance_ let's start this post!

## 1. Google releases Gemini 1.5 Pro
### What :dart:
On February, 15th, 2024 Google announced the release of [Gemini 1.5](https://blog.google/technology/ai/google-gemini-next-generation-model-february-2024/#sundar-note) just one week after rolling out Gemini 1.0 Ultra. Gemini 1.5 is a new LLM with some interesting properties:
* Dramatically enhanced performance (according to Google).
* More efficient and comparable to Ultra whilst requiring less computing.
* Based on a Mixture-of-Experts (MoE) architecture[^1].
* Multi-modal LLM (similar to _GPT-4V_).
* Improved _In-Context_ learning skills from long prompts, without needing fine-tuning.
* With a standard context window of **128,000** tokens, that can be extended to **1** million tokens. 

Let that sink in a bit **1 million** tokens which is roughly **700,000+**. A "regular" book :book: has somewhere between _250-300_ words per page. This would mean that you can use a book of between **2300+** pages as context to the Gemini 1.5 Pro model. 

For instance, you could feed in the entire _Lord of the Rings_ and _The Count of Monte Cristo_ at the same time as both of these books are roughly **1200** pages. 

What is further highlighted in [Google technical report](https://storage.googleapis.com/deepmind-media/gemini/gemini_v1_5_report.pdf) is:
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

I always get a bit _skeptical_ (I guess it is the DS in me) when I hear that metrics are close to 100% or near-perfect as this normally means that you are overfitting or doing something wrong. However, it is still very impressive in comparison to GPT-4V on the same dataset. While be exciting to see more benchmarks on this going forward.

[^1]: Similar to the Mixtral model launched last year: https://mistral.ai/news/mixtral-of-experts/

### Why it interests me :eyes:
* For many people building Generative AI applications, hallucinations are a big issue. What people do to mitigate this is to present more relevant content using e.g. _Retrieval Augmented Generation_ (RAG), using _Guardrails_ or _fine-tuning_ the LLM to make it more domain-specific. 

* Having access to **1M+** context window will for instance open up use cases to reason and ask questions around multiple documents (as there might be some dependency amongst each document). 

* There are also speculations that the pricing of Gemini 1.5 Pro could be potentially **10x** cheaper than GPT-4[^2]. If that is the case you would get a similar or potentially better performant LLM at the price of or cheaper than **gpt-3.5-turbo**.

[^2]: [Reddit post](https://www.reddit.com/r/singularity/comments/1avzrp7/gemini_15_will_be_20x_cheaper_than_gpt4_this_is/)

### Additional resources :computer:
1. [Gemini 1.5 Pro Announcement](https://blog.google/technology/ai/google-gemini-next-generation-model-february-2024/#sundar-note)
1. [Gemini 1.5 Pro Technical Report](https://storage.googleapis.com/deepmind-media/gemini/gemini_v1_5_report.pdf)

## 2. Google releases Gemma
### What :dart:
On February, 21st, 2024 Google announced the release of [Gemma](https://blog.google/technology/developers/gemma-open-models/) a family of lightweight, Open models also roughly a week after releasing Gemina 1.5 Pro :point_up: . 

The Gemma release included the following:
* Gemma 2B & Gemma 7B (great for consumer-size GPU)
* Toolchains for inference and supervised fine-tuning (SFT) across all major frameworks: _JAX_, _PyTorch_, and _TensorFlow_ through native _Keras 3.0_
* Integration into the Hugging Face ecosystem (2 base models & 2 fine-tuned ones)
* The Gemma model architecture is based on the transformer decoder.
  
Looking at the technical paper _Gemma_ in its base form seems to fair well against _Mistral_ and _LLaMa_ in terms of QA, Reasoning, Math / Science and Coding:

![Results Gemma](/res_gemma.png "Language understanding and generation performance of Gemma for different capabilities VS other open source models LLaMa and Mistral. The image was sourced from Gemma Techincal Report.")

Also looking at the [LLM Leaderboard](https://huggingface.co/blog/gemma) Gemma is ranking highly in comparison to other 7B models. While be interesting to see when we start to see some more fine-tuned versions of Gemma.

Finally, it is also cool to see the quick integration with the Keras library as well where it is as simple as the below to start testing Gemma:
{{< highlight python "linenos=inline, style=monokai" >}}
# load model
gemma_lm = keras_nlp.models.GemmaCausalLM.from_preset("gemma_2b_en")
# generate text
gemma_lm.generate(What is the meaning of life", max_length=512)
{{< / highlight >}}
### Why it interests me :eyes:
* Fun to see that **Google** is back on the open models track after releasing Gemini 1.5. Pro, that seems to be very performant. 
* It will be interesting to see what other fine-tuned models that will start to pop up in a while.

### Additional resources :computer:
1. [Gemma Announcement](https://blog.google/technology/developers/gemma-open-models/)
2. [Gemma Techincal Report](https://storage.googleapis.com/deepmind-media/gemma/gemma-report.pdf)
3. [Welcome Gemma - Google's New Open LLM](https://huggingface.co/blog/gemma)
4. [Introducing Gemma models in Keras](https://developers.googleblog.com/2024/02/gemma-models-in-keras.html)

## 3. OpenAI releases SORA
### What :dart:
On February, 15th, 2024 OpenAI released _SORA_ AI model (text-to-video) that can generate "realistic" and "imaginative" scenes from natural language.

Some properties of SORA:
* Diffusion model jointly trained on videos and images of various lengths, ratios and resolution
* Uses a transformer architecture
* Input data as _patches_ similar to tokens

![Viz of input patches](/sora.png "Example of input patches that are constructed from compressing videos in a lower latent space. Image is sourced from SORA Technical Report.")

According to OpenAI:
> Sora is able to generate complex scenes with multiple characters, specific types of motion, and accurate details of the subject and background. The model understands not only what the user has asked for in the prompt, but also how those things exist in the physical world
> ...
> Sora serves as a foundation for models that can understand and simulate the real world, a capability we believe will be an important milestone for achieving AGI


### Why it interests me :eyes:
* The demo videos using a fairly simple prompt look very impressive, and I think there are a bunch of use cases for gaming, marketing and filmmaking with something like SORA. After it has been "battle" tested of course. 
* The ability to simulate and understand the real world (at least as an initial foundation) is very interesting if and when we do end up with AGI.

### Additional resources :computer:
1. [SORA](https://openai.com/sora)
2. [SORA Techincal Report](https://openai.com/research/video-generation-models-as-world-simulators)

## 4. Predibase announces LoRA Land
### What :dart:
On February, 20th, 2024 Predibase announced that they had fine-tuned a bunch of Open-Source LLMs (25 to be exact), based on Mistral. Where these fine-tuned models managed to beat GPT-4 on a couple of benchmarks and domains. 

The remarkable thing here, apart from the allegedly high performance, is that the serving of these models all work on a single GPU. 

Predibase mentions the following, regarding LoRA [^3]:
* **25** task-specialized LLMs, and fine-tuned using Predibase
* For a cost of **$8.00** on average :dollar:

![LoRA land benchmarks vs GPT-4](/lora_land_bench.png "LLM Benchmarks: 25 fine-tuned Mistral-7b adapters that outperform GPT-4. Image from Predibase.")

### Why it interests me :eyes:
* You should not sleep on fine-tuning, often a fine-tuned task-specific model can be a more generalized model.
* A more cost-efficient way of serving custom LLMs using Predibase, requiring less computing and giving you more control.

[^3]: Low-rank Adapter (LoRA) finetuning is a method that reduces memory
requirements by using a small set of trainable parameters, often termed adapters, while not updating
the full model parameters that remain fixed.

### Additional resources :computer:
1. [LoRA Land: Fine-Tuned Open-Source LLMs that Outperform GPT-4](https://predibase.com/blog/lora-land-fine-tuned-open-source-llms-that-outperform-gpt-4)
2. [LoRA Land](https://predibase.com/lora-land)
3. [QLoRA: Efficient Finetuning of Quantized LLMs](https://arxiv.org/abs/2305.14314) 

## 5. Stability AI announces Stable Diffusion 3
### What :dart:
On February 22nd, 2024 Stability AI announced that they have released (in an early preview) "Stable Diffusion 3". Like SORA this is a text-to-image model.

What is mentioned in the release:
* Range of models from 800M to 8B parameters
* Combination of diffusion transform architecture and flow matching 

No technical report is out yet, but will be interesting to dive deeper when it gets released. 
### Why it interests me :eyes:
* For similar reasons as SORA 

### Additional resources :computer:
1. [Stable Diffusion 3 Annoucment](https://stability.ai/news/stable-diffusion-3)
2. [Scalable Diffusion Models with Transformers](https://arxiv.org/abs/2212.09748)
3. [Flow Matching for Generative Modelling](https://arxiv.org/abs/2210.02747)

## 6. Astral releases `uv` uber fast `Python` packaging 
### What :dart:
On February, 15th, 2024 the company behind [Ruff](https://docs.astral.sh/ruff/) i.e. Astral released `uv`. Which is an extremely fast Python package manager and resolver.

See some benchmarks below:

![uv: Python packaging in Rust](/uv.png "Left is the package resolver. Right is installation. According to Astral uv provides a speed-up of 10-100x. Image from Astral.")

What `uv` is:
* Extremely fast Python package installer and resolver
* Written in Rust and works as a drop-in replacement of e.g. pip
* Up to 10x faster compared to e.g pip without a caching 
* Up to 100x fast compared to e.g. pip with caching
* `uv` can also be used for `virtual` environment management 
* Inspired by [Rye](https://github.com/mitsuhiko/rye).
  
### Why it interests me :eyes:
* I like the vision of a "Cargo"[^4] for Python i.e. improve the experience of the somewhat fragmented `Python` ecosystem 
* Poetry is a great alternative to e.g. Conda or `pip` but it is not perfect
* Still early days for `uv` but will definitely try it and see how it takes off 

[^4]: Package manager for Rust

### Additional resources :computer:
1. [uv: Python packaging in Rust](https://astral.sh/blog/uv)
2. [Github for uv](https://github.com/astral-sh/uv)

## 7. Ollama releases `OpenAI` compatibility
### What :dart:
On February, 8th, 2024 the team behind Ollama, announced that Ollama now supports OpenAI Chat Completions API.
This also coincided with the announcement from HuggingFace to support the OpenAI Chat completions API. Trying different models both open and closed source, seems to be easier than ever!

An example of how to use this via the OpenAI client is shown below:

{{< highlight python "linenos=inline, style=monokai" >}}
from openai import OpenAI

client = OpenAI(
    base_url = 'http://localhost:11434/v1',
    api_key='ollama', # required, but unused
)

response = client.chat.completions.create(
  model="llama2",
  messages=[
    {"role": "system", "content": "You are a helpful assistant That is an export in human life existential questions."},
    {"role": "user", "content": "Why is 42 seen as the meaning of life?"},
  ]
)
print(response.choices[0].message.content)
{{< / highlight >}}

### Why it interests me :eyes:
1. No need to change how you invoke LLMs whether it be open or closed source.
2. Make it easier for ML developers to try different models and parsing results in a similar way.

### Additional resources :computer:
1. [Ollama: OpenAI compatibility](https://ollama.com/blog/openai-compatibility)
2. [From OpenAI to Open LLMs with Messages API on Hugging Face](https://huggingface.co/blog/tgi-messages-api)

## 8. Chain-of-Thought Reasoning Without Prompting
### What :dart:
On February, 15th, 2024 researchers from Google Deepminde released a paper called "Chain-of-Thought Reasoning Without Prompting".

The main thesis is the following:
> Can LLMs reason effectively without prompting? And to what extent can they reason? We find that, perhaps surprisingly, there exists a task-agnostic way to elicit CoT reasoning from pre-trained LLMs by simply altering the decoding procedure.!

Illustration of their approach below:
![Chain-of-Thought Reasoning Without Prompting](/cot_ex_prompt.png "Overview of CoT-decoding. Using alternative top k tokens to elicit reasoning. Image from Chain-of-Thouight Reasoning Without Prompting paper.")

Some initial points from the paper:
* Input is using the standard question-answer (QA) format: `Q:[question]\nA:`.
* CoT decoding offers an alternative way to elicit reasoning capabilities from pre-trained LLMs without explicit prompting. 
* Model demonstrates increased confidence in the final, answer when a CoT reasoning path is present in the decoding process.

It is a sound and interesting approach to focus more on using the "intrinsic" reasoning capabilities of an LLM rather than influencing its reasoning via CoT-prompting.

And some additional points from the paper:
* They also found that higher values of 𝑘  (in terms of top k tokens to do CoT-decoding from) typically result in improved model performance.
* Another noteworthy observation is that CoT-decoding can better reveal what LLMs’ intrinsic strategy in solving a problem, without being influenced by the external prompts which could be biased by the prompt designers.
* Experiments were using PaLM-2 and Mistral-7B.

### Why it interests me :eyes:
* _Prompt Engineering_ sometimes feels more of an art compared to a science where small slight changes can fool an LLM fairly easily.
* Cleaver way of using the intrinsic capabilities of pre-trained LLMs.
* Looking forward to more "clever" ways of pushing accuracy from an LLM without having to too much on prompt engineering.

### Additional resources :computer:
1. [Chain-of-Thought Reasoning Without Prompting](https://arxiv.org/abs/2402.10200)

## 9. SiloAI completes training of Poro
### What :dart:
On February 20th, 2024 Silo AI announced that they have finalized training of their Poro family of models. These models were first announced last year in [November](https://www.silo.ai/blog/poro-a-family-of-open-models-that-bring-european-languages-to-the-frontier).

As mentioned by Silo AI in their post:
> The completion of training Poro functions as a proof point for an innovative approach in developing AI models for languages with scarce data resources. Poro outperforms all existing open language models on the Finnish language, including FinGPT, Mistral, Llama, and the BLUUMI 176 billion parameter model, among others.

Some key features of Poro 34B from the post:
* Poro Research Checkpoints will be available
* Poro 34B has **34.2** billion parameters and uses a [BLOOM](https://huggingface.co/docs/transformers/model_doc/bloom) architecture with [ALiBi](https://arxiv.org/abs/2108.12409) embeddings
* Multilingual capabilities: Poro is designed to process English and Finnish and has proficiency with a variety of programming languages. Additionally, it can perform translation between English and Finnish.
* Open source: Poro is freely available under the Apache 2.0 License
* Training details: Poro is trained using **512** AMD MI250X GPUs on the LUMI supercomputer in Finland.

### Why it interests me :eyes:
* Great seeing that Europe is stepping up its _Generative AI_ game, and the Nordics in particular!
* Interesting training approach with using a "low" resource language such as Finish together with English to derive cross-lingual signals for training. This is likely beneficial for other Nordic languages as well.
* More language-specific models i.e. models for Nordic languages vs General models may be better for certain use cases.

### Additional resources :computer:
1. [Europe's open language model Poro: A milestone for European AI and low-resource languages](https://www.silo.ai/blog/europes-open-language-model-poro-a-milestone-for-european-ai-and-low-resource-languages)
2. [Poro - a family of open models that bring European languages to the frontier](https://www.silo.ai/blog/poro-a-family-of-open-models-that-bring-european-languages-to-the-frontier)
3. [Europe’s open language model family Poro extends checkpoints, languages and modalities](https://www.silo.ai/blog/europes-open-language-model-family-poro-extends-checkpoints-languages-and-modalities)
4. [Poro Model Card](https://huggingface.co/LumiOpen/Poro-34B)

## 10. Groq - extremely fast LLM serving using LPUs
### What :dart:
On February 20, 2024, I started to hear a lot of buzz connected to the specialized chip manufacturer Groq showcased an impressive **500+** tokens/seconds ratio for serving LLMs. This mainly by using their specialized LPU chips.

An LPU or Language Processing Unit is:
> An LPU Inference Engine, with LPU standing for Language Processing Unit™, is a new type of end-to-end processing unit system that provides the fastest inference for computationally intensive applications with a sequential component to them, such as AI language applications (LLMs).

According to _Groq_ their chip overcomes the following challenges, for LLMs: 
1. Compute density
2. Memory bandwidth

When doing a small test it is fast:
![Groq and the meaning of life.](/groq.png "Testing Qroq chat interface with an impressive 500+ tokens/seconds. Served using LPUs.")

I think it is very interesting to see other more specialized chip providers show up, such as Groq. However, there are also other providers such as [graphcore](https://www.graphcore.ai/) offering IPUs [^5].

[^5]: Intelligence Processing Unit (IPU) technology, which is another ML-specialized chip.

### Why it interests me :eyes:
Serving both commercial and open LLMs can take quite some time for tricky applications.
* Groq and their LPU chips seem to push boundaries in terms of LLM serving and speed of inference.
* Nice with some alternatives to high-demand GPUs like the A100s and H100s

### Additional resources :computer:
1. [Groq Chat](https://groq.com/)
2. [https://wow.groq.com/artificialanalysis-ai-llm-benchmark-doubles-axis-to-fit-new-groq-lpu-inference-engine-performance-results/](https://wow.groq.com/artificialanalysis-ai-llm-benchmark-doubles-axis-to-fit-new-groq-lpu-inference-engine-performance-results/)
3. [Groq ISCA Paper 2020](https://wow.groq.com/groq-isca-paper-2020/)
4. [Groq ISCA 2022 Paper](https://wow.groq.com/isca-2022-paper/)
