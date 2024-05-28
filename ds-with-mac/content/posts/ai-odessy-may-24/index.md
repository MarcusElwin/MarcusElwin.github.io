---
title: Ai Odessy May Edition
seo_title: Ai Odessy May 24
summary: 10 GenAI, ML and Data Science-related announcements that excited me during May 2024.
description: 
slug: ai-odessy-may-24
author: Marcus Elwin

draft: false
date: 2024-05-26T18:49:05+02:00
lastmod: 
expiryDate: 
publishDate: 

feature_image: 
feature_image_alt: 

categories:
    - GenAI
    - AI
    - ML
    - DS
tags:
series:
    - AI Odessy

toc: true
related: true
social_share: true
newsletter: false
disable_comments: false
---

_Cillum tempor enim consequat officia sunt esse eiusmod anim cupidatat velit velit nulla do tempor duis aute dolore lorem deserunt. Fugiat lorem excepteur ex labore nisi aliqua commodo ut ipsum veniam sint nulla dolor cillum aliqua aliqua. Et consequat incididunt consectetur eu laboris reprehenderit occaecat dolore voluptate ad duis. Fugiat laboris adipiscing non aute reprehenderit irure minim ea fugiat incididunt minim eu mollit cupidatat ipsum magna._

* Gemini 1.5 Flash
* Project Astra
* GPT-4o
* Pydantic Logfire
* Snowflake Arctic Embed
* Nomic Embed
* xLSTM: Extended Long Short-Term Memory
* KAN: Kolmogorov-Arnold Networks
* Mapping the Mind of a Large Language Model
* ~~NuNER-v2.0~~

## 1. Google releases Gemini 1.5 Flash
### What :dart:
__TODO__

### Why it caught my attention :eyes:
__TODO__

### Addition

## 2. OpenAI releases GPT-4o (omni)
### What :dart:
__TODO__

### Why it caught my attention :eyes:
__TODO__

### Addition

## 3. Snowflake Releases Arctic Embed
### What :dart:
__TODO__

### Why it caught my attention :eyes:
__TODO__

### Addition

## 4. xLSM: Extended Long Short-Term Memory
### What :dart:
__TODO__

### Why it caught my attention :eyes:
__TODO__

### Addition

## 5. KAN: Kolmogorov-Arnold Networks
### What :dart:
__TODO__

### Why it caught my attention :eyes:
__TODO__

### Addition_

## 6. Antrophic sees :eyes: into the mind of an LLM :brain:
### What :dart:
__TODO__

### Why it caught my attention :eyes:
__TODO__

### Addition

## 7. NuNER-v2.0
### What :dart:
[NuMind](https://numind.ai/) has released a new LLM: _NuNER-v2_ that specializes in _Named Entity Recognition_ which is a successor to their previously launched [NuNER](https://www.numind.ai/blog/a-foundation-model-for-entity-recognition). 

As part of this release, they have released the following models (all available on _HuggingFace_):
- NuNER 2.0
- NuNER Zero
- NuNER Zero Span
- NuNER Zero-4k

As mentioned by NuMind on LinkedIn:
> NuNER 2.0 is the successor of NuNER, an NER-specific embedding model. It is meant to be fine-tuned in a few-shot setting (typically 100 examples). We find that it works quite better than the original NuNER (typically +4% in F-score).

<br>

> NuNER Zero is a zero-shot NER model, based on the GLiNER architecture. Thanks to the dataset we use, we find that it achieves +3.1% token-level F-score over GLiNER-large-v2.1 on GLiNERS's benchmark (see plot bellow). A nice feature of this model is that it is a *token classifier* which means it can detect arbitrary long entities (GLiNER-large-v2.1 is limited to 12 tokens per entity).

In the paper in [3], the below prompt is what is used to annotate data (for pre-training) with the help of an LLM [^1]. The authors estimate that  in `95%` of the cases the concept associated with the extracted entity is **sensible**:

[^1]: In the paper the LLM used is `gpt-3.5-turbo`.

{{< highlight python "linenos=inline, style=monokailight" >}}
The goal is to create a dataset for entity recognition. Label
as many entities, concepts, and ideas as possible in the
input text. Invent new entity types that may not exist
in traditional NER Tasks such as more abstract concepts
and ideas. Make sure the entity concept is not part of
speech but something more meaningful. Avoid finding
meaningless entities.
Output format (separate entities with new line):
entity from the text <> entity concept <> description of
entity group/concept
Input:
[INPUT SENTENCE]
{{< / highlight >}}

For `NuNER-v2` and the other model `derivatives` mentioned, one can assume that the approach is similar [^2]. This is what is mentioned in the LinkedIn Post in [2]:

> In a nutshell: we created a new LLM-annotated dataset based on C4 and Pile (using the procedure of our paper https://lnkd.in/dnbNfEbf). This dataset is larger and substantially more diverse than before. We then trained a variety of NER models on it and found out that they work pretty well!

The architecture used in the paper in [3] is the following:
![NuNER](/nuner_arch.png "NuNER uses 2 separate sub-networks: (1) NuNER network of interest and which encodes input text as a sequence of vectors. (2) Concept encoder which encodes concepts as vectors. The embeddings of both of these networks are then compared to get the logits for the network. RoBERTa-base is the underlying transformer used for both networks. Source: paper in [3]")

In the paper in [3] the authors also compare `NuNER` to `gpt-3.5-turbo` and `gpt-4`:
![Alt text](/nuner_vs_llm.png "Comparison of NuNER to LLMs. Dashed lines indicates in-context learning and solid lines indicate fine-tuning. Source: paper in [3].")

Would be interesting to see how `NuNER-v2` and its siblings fairs against `gpt-4-turbo` or `gpt-4o` in terms of information extraction. Given that it is supposed to be better than `NuNER`.

[^2]: `gpt-4-turbo` has also been known to be a good data annotator but is probably not used due to the higher cost incurred. However, `gpt-4o` could be an option here.

The key takeaway (imho) from the paper in [3] is:
> NuNER demonstrates that LLM-annotated data can effectively reduce the need for extensive human annotations while achieving high performance in NER tasks. Where the diversity and size of the pre-training dataset significantly impact NuNER's performance.

Initial results using _NuNER_ zero in various domains look promising:

![NuNER Zero vs GliNER-v2.1-large.](/nuner_performance.jpeg "NuNER Zero shows better performance (F1 score) in various different domains, in terms of finding entities compared to the baseline GLInER-v2.1-large model. Source: LinkedIn Post in [2]")

### Why it caught my attention :eyes:
* Typically many companies have information extract or NER use cases, often you want structured JSON as output from an LLM. To pass this further to other parts of your system.
* _NuNER-v2_ is a specialized LLM that you can *finetune* with a relatively small dataset i.e. only ~100 examples in your domain. 
* Using LLMs for data annotation and doing _knowledge distillation_ is an interesting practice to leverage both LLMs and _task specific foundation models_.

### Additional resources :computer:
1. [A Foundation Model for Entity Recognition](https://www.numind.ai/blog/a-foundation-model-for-entity-recognition)
2. [LinkedIn Post](https://www.linkedin.com/posts/etiennebcp_new-sota-ner-models-from-numind-yc-s22-activity-7193643817709826048-gyzQ/?utm_source=share&utm_medium=member_android)
3. [NuNER: Entity Recognition Encoder Pre-training via LLM-Annotated Data](https://arxiv.org/abs/2402.15343)
4. [GLiNER: Generalist Model for Named Entity Recognition using Bidirectional Transformer](https://arxiv.org/abs/2311.08526)

## 8. Nomic Embed gpt4 quality embeddings locally
### What :dart:
__TODO__

### Why it caught my attention :eyes:
__TODO__

### Addition

## 9. Pydantic Logfire tracing :eyes:
### What :dart:
__TODO__

### Why it caught my attention :eyes:
__TODO__

### Addition

## 10. Project Astra :robot:
### What :dart:
__TODO__

### Why it caught my attention :eyes:
__TODO__

### Addition

