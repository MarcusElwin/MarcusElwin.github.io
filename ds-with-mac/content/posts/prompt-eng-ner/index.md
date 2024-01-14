---
title: Prompt Engineering for Named Entity Recognition (NER)
seo_title: Prompt Engineering NER
summary: Prompt Engineering Tips & Tricks for Named Entity Recognition (NER)
description: 
slug: prompt-eng-ner
author: Marcus Elwin

draft: false
date: 2024-01-14T16:23:42+01:00
lastmod: 
expiryDate: 
publishDate: 

feature_image: 
feature_image_alt: 

categories:
    - "Prompt Engineering"
tags:
    - "Large Language Models (LLMs)"
    - "Generative AI"
    - "Prompt Engineering"
    - "NER"
series:

toc: true
related: true
social_share: true
newsletter: false
disable_comments: false
---

**2023** was the year of *exploration*, *testing* and *proof-of-concepts* or deployment of smaller LLM-powered workflows/use cases for many organizations. Whilst 2024 will likely be the year where we will see even more production systems leveraging LLMs. Compared to a traditional ML system where data (examples, labels), model and weights are artifacts. Prompts used for driving a certain behavior of an assistant or agent are one of the **main** artifacts. 

Therefore many of the large players as well as academia have provided guides on how to prompt LLMs efficiently:
1. :computer: [OpenAI Prompt Engineering](https://platform.openai.com/docs/guides/prompt-engineering)
2. :computer: [Guide to Anthropic's prompt engineering resources](https://docs.anthropic.com/claude/docs/guide-to-anthropics-prompt-engineering-resources)
3. :computer: [Principled Instructions Are All You Need for Questioning LLaMA-1/2, GPT-3.5/4](https://arxiv.org/abs/2312.16171)
4. :computer: [Prompt Engineering Guide](https://www.promptingguide.ai/)

Many of these guides are quite **generic** and can work for many different use cases. However, there are very few guides mentioning best practices for constructing prompts for *Named Entity Recognition (NER)*. OpenAI has for instance a [cookbook](https://cookbook.openai.com/examples/named_entity_recognition_to_enrich_text) for `NER`  as well as [this](https://arxiv.org/pdf/2305.15444.pdf) and [this](https://arxiv.org/pdf/2310.17892.pdf) paper which both suggested a method called `Prompt-NER`. In this article, we will discuss some techniques that might be helpful when using LLM for NER use cases. To set the stage we will first start with defining what *Prompt Engineering* and *Named Entity Recognition* actually are.


## Prompt Engineering
Prompt Engineering sometimes feels more like an *art* compared to *science* but there are more and more best practices showing up (see some of the references in the previous section). 

See one definition below for `Prompt Engineering`:

{{< notice info >}} 
Prompt engineering is a relatively new discipline for developing and optimizing prompts to efficiently use language models (LMs) for a wide variety of applications and research topics. Prompt engineering skills help to better understand the capabilities and limitations of large language models (LLMs).

Prompt engineering is not just about designing and developing prompts. It encompasses a wide range of skills and techniques that are useful for interacting and developing with LLMs. It's an important skill to interface, build with, and understand the capabilities of LLMs. You can use prompt engineering to improve the safety of LLMs and build new capabilities like augmenting LLMs with domain knowledge and external tools.
— <cite>Prompt Engineering Guide[^1]</cite>

[^1]: The above quote is excerpted from https://www.promptingguide.ai/
{{< /notice >}}

Like any other artifact prompts may be outdated or "drift" which is why it is important to have systems in place to do:
* _Experiment_ tracking of prompts
* _Evaluating_ your prompts (either via "_golden dataset_" approach, LLM-based _evals_ or both)
* _Observability_ of how your prompts are being used
* _Versioning_ of your prompts. 

## Named Entity Recognition (NER)
Extracting `entities` or `tags` from data can be very useful for many different domains and businesses and can be used for many different things such as *classification, _knowledge retrieval_, _search_* etc.

See one definition below for `Named Entity Recognition`:

{{< notice info >}} 
**Named Entity Recognition (NER)** is a task of Natural Language Processing (NLP) that involves identifying and classifying named entities in a text into predefined categories such as person names, organizations, locations, and others. The goal of NER is to extract structured information from unstructured text data and represent it in a machine-readable format. Approaches typically use **BIO** notation, which differentiates the beginning (B) and the inside (I) of entities. O is used for non-entity tokens.
— <cite>Prompt Engineering Guide[^2]</cite>

[^2]: The above quote is excerpted from https://paperswithcode.com/task/named-entity-recognition-ner
{{< /notice >}}

Below is an example of the **BIO** notation:
{{< highlight shell "linenos=inline, style=monokai" >}}
Mac [B-PER]
Doe [I-PER]   
ate [O]
a [O]
hamburger [O] 
at [O]
Mcdonalds [B-LOC]
{{< / highlight >}}

However, the BIO notation does not make sense for all use case. Let's say that if you are interested in extracting _food_ entities then _hamburger_ above might be a key entity or tag that you want to predict. You can add any labels you like for your NER task as long as you have labeled entities to use.

Usually, a "typical" NER pipeline [^3] comprises the following steps:
1. `tokenizer`: Turn text into *tokens*
2. `tagger`: Assign part of speech tags
3. `parser`: Assign *dependency* labels
4. `ner`: Detect and label named entities

[^3]: Language Processing Pipelines from https://spacy.io/usage/processing-pipelines

Solving NER systems has previously been done by using:
1. Rule-based systems
2. Statistical & ML systems
3. Deep-Learning systems
4. Mix of (1) - (3).

Where [spacy](https://spacy.io/) and Transformer architectures from e.g. [HuggingFace](https://huggingface.co/) such as *BERT*, *XLM-ROBERta* have been the go-to methods.

Before we start with prompt engineering let's create an example of where we want to employ this. 

In the following section we will assume the following:
1. We are a food tech startup that provides and sells custom smart purchase lists to retailers from online food recipes.
2. We want to extract the following type of entities: `FOOD`, `QUANTITY`, `UNIT`, `PHYSICAL_QUALITY`, `COLOR`
3. When we have the `entities` we want to populate smart purchase stores with recommendations on where to get the food.

The example [recipe](https://www.carolinescooking.com/chashu-pork/#recipe) that we will be using:

{{< highlight markdown "linenos=inline, style=monokai" >}}

### Chashu pork (for ramen and more)
Chashu pork is a classic way to prepare pork belly for Japanese dishes such as ramen. 
While it takes a little time, it's relatively hands off and easy, and the result is delicious.

### Ingredients
2 lb pork belly or a little more/less
2 green onions spring onions, or 3 if small
1 in fresh ginger (a chunk that will give around 4 - 6 slices)
2 cloves garlic
⅔ cup sake
⅔ cup soy sauce
¼ cup mirin
½ cup sugar
2 cups water or a little more as needed

### Instructions
Have some string/kitchen twine ready and a pair of scissors before you prepare the pork. 
If needed, trim excess fat from the outside of the pork but you still want a later over the
...
{{< / highlight >}}

## Technique #1 - Use `temperature 0.0`
LLMs are *non-deterministic* by nature and different generations of using e.g. chat completions APIs from e.g. `OpenAI` will return different responses. However, one way to mitigate this is to use the `temperature` parameter often provided in these types of APIs. In short, the *lower* the temperature, the more **deterministic** the results in the sense that the highest probable next token is always picked [^4]. Do notice that this is still not a guarantee for deterministic output. Rather the *best try effort* to always select the *most likely token* as model output.

This is of course useful in a NER case where you would like the same or similar input to produce the same or similar output.

{{< notice tip >}} 
**Tip 1**: Use `0.0` as `temperature` to get more `deterministic` output.
{{< /notice >}}

[^4]: LLM Settings from https://www.promptingguide.ai/introduction/settings

## Technique #2 - Set `seed` for your runs
Recently OpenAI added the functionality to set the [seed](https://cookbook.openai.com/examples/reproducible_outputs_with_the_seed_parameter) to make runs more reproducible. If all other params are set to the same value e.g. `temperature=0` etc, `seed` is set and the `system_fingerprint`[^5] then output will be mostly deterministic.

[^5]: The fingerprint represents the backend configuration that the model runs with.

{{< notice tip >}} 
**Tip 2**: Set `seed` of each API call e.g. `seed=42` to get more `deterministic` output.
{{< /notice >}}

Both the previous section and this section were more focused on model parameters. The following sections will instead focus on what `Prompt Engineering` techniques we can use to extract named entities.

## Technique #3 - Use clear instructions 
Next step is to use `clear` instructions to the agent normally:
* `System` prompt is used for instructions
* `User` prompt to provided context and data
* (`Assistant`) prompt to provide examples

Starting with a prompt like the below:
{{< highlight markdown "linenos=inline, style=monokai" >}}

System:
You are a food AI assistant that is an expert in natural language processing
and especially name entity recognition.

User:
Extract all food related entities from the recipe below in backticks:
```{recipe}```
...
{{< / highlight >}}

We get the following output:
{{< highlight markdown "linenos=inline, style=monokai" >}}

#### extract_food_entities
I will now proceed to extract all the food-related entities from the given recipe.

#### extract_food_entities
The food-related entities present in the recipe are as follows:

* Pork belly
* Green onions
* Fresh ginger
* Garlic
* Sake
* Soy sauce
* Mirin
* Sugar
* Water
* Rice

These entities cover the main ingredients used for the Chashu pork recipe.
{{< / highlight >}}

<TODO: Add improved prompt>

## Technique #4 - Use `function` or `tools` API
When we use `functions` or `tools` we prompt the model to provided input arguments for an actual function in a downstream manner. The functions will also be part of the system prompt. Many of the latest models have been fine-tuned to work with function calling and thus produce valid `JSON` output in that way. 

In order to define a function we defina a `jsonSchema` as below:

{{< highlight json "linenos=inline, style=monokai" >}}

{
    "name": "extract_food_entities",
    "description": "Your a food AI assistant. Your task is to extract food entities from a recipe based on the json schema. You are to return the output as valid json.",
    "parameters": {
      "type": "object",
      "properties": {
        "food-metadata": {
          "type": "object",
          "properties": {
            "food": {
              "type": "string",
              "description": "The name of the food item"
            },
            "quntity": {
              "type": "string",
              "description": "The quantity of the food item"
              
            },
            "unit": {
              "type": "string",
              "description": "The unit of the food item"
            },
            "physicalQuality": {
              "type": "string",
              "description": "The physical quality of the food item"
            },
            "color": {
              "type": "string",
              "description": "The color of the food item"
            }
          },
          "required": [
            "food", 
            "quntity",
            "unit",
            "physicalQuality",
            "color"
          ]
        }
      },
      "required": [
        "food-metadata"
      ]
    }
  }
{{< / highlight >}}


## Technique #5 - Use domain prompts 
Exercitation non excepteur officia eu sed irure tempor ex laborum sed cupidatat mollit elit reprehenderit nostrud. Laboris voluptate minim eu lorem ad eu do sit culpa.

## Technique #6 - Use Chain-of-Thought
Exercitation non excepteur officia eu sed irure tempor ex laborum sed cupidatat mollit elit reprehenderit nostrud. Laboris voluptate minim eu lorem ad eu do sit culpa.

## Technique #7 - Use Prompt Chaining
Exercitation non excepteur officia eu sed irure tempor ex laborum sed cupidatat mollit elit reprehenderit nostrud. Laboris voluptate minim eu lorem ad eu do sit culpa.


## Closing Remarks
Exercitation non excepteur officia eu sed irure tempor ex laborum sed cupidatat mollit elit reprehenderit nostrud. Laboris voluptate minim eu lorem ad eu do sit culpa.