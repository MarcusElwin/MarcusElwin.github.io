---
title: Prompt Engineering for Named Entity Recognition (NER)
seo_title: Prompt Engineering NER
summary: Prompt Engineering Tips & Tricks for Named Entity Recognition (NER)
description: 
slug: prompt-eng-ner
author: Marcus Elwin

draft: false
date: 2024-01-21T16:23:42+01:00
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

**2023** was the year of *exploration*, *testing* and *proof-of-concepts* or deployment of smaller LLM-powered workflows/use cases for many organizations. Whilst 2024 will likely be the year where we will see even more production systems leveraging LLMs. Compared to a traditional ML system where data (examples, labels), model and weights are artifacts, prompts are the **main** artifacts. Prompts and prompt engineering are used for driving a certain behavior of an assistant or agent.

Therefore many of the large players as well as academia have provided guides on how to prompt LLMs efficiently:
1. :computer: [OpenAI Prompt Engineering](https://platform.openai.com/docs/guides/prompt-engineering)
2. :computer: [Guide to Anthropic's prompt engineering resources](https://docs.anthropic.com/claude/docs/guide-to-anthropics-prompt-engineering-resources)
3. :computer: [Principled Instructions Are All You Need for Questioning LLaMA-1/2, GPT-3.5/4](https://arxiv.org/abs/2312.16171)
4. :computer: [Prompt Engineering Guide](https://www.promptingguide.ai/)

Many of these guides are quite **generic** and can work for many different use cases. However, there are very few guides mentioning best practices for constructing prompts for *Named Entity Recognition (NER)*. OpenAI has for instance a [cookbook](https://cookbook.openai.com/examples/named_entity_recognition_to_enrich_text) for `NER`  as well as [this](https://arxiv.org/pdf/2305.15444.pdf) and [this](https://arxiv.org/pdf/2310.17892.pdf) paper which both suggested a method called `Prompt-NER`. 

In this article, we will discuss some techniques that might be helpful when using LLM for NER use cases. To set the stage we will first start with defining what *Prompt Engineering* and *Named Entity Recognition* are.


## Prompt Engineering
Prompt Engineering sometimes feels more like an *art* compared to *science* but there are more best practices showing up (see some of the *references* in the previous section). 

One definition of `Prompt Engineering` is shown below:

{{< notice info >}} 
Prompt engineering is a relatively new discipline for developing and optimizing prompts to efficiently use language models (LMs) for a wide variety of applications and research topics. Prompt engineering skills help to better understand the capabilities and limitations of large language models (LLMs).

Prompt engineering is not just about designing and developing prompts. It encompasses a wide range of skills and techniques that are useful for interacting and developing with LLMs. It's an important skill to interface, build with, and understand the capabilities of LLMs. You can use prompt engineering to improve the safety of LLMs and build new capabilities like augmenting LLMs with domain knowledge and external tools.
— <cite>Prompt Engineering Guide[^1]</cite>

[^1]: The above quote is excerpted from https://www.promptingguide.ai/
{{< /notice >}}

Like any other artifact prompts may be "outdated" or "drift" which is why it is important to have systems in place to do the:
* _Experiment_ tracking of prompts
* _Evaluating_ your prompts (either via the "_golden dataset_" approach, LLM-based _evals_ or both)
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

Below is an example of the **BIO** notation, which is a common format used for NER:
{{< highlight shell "linenos=inline, style=monokai" >}}
Mac [B-PER]
Doe [I-PER]   
ate [O]
a [O]
hamburger [O] 
at [O]
Mcdonalds [B-LOC]
{{< / highlight >}}

However, the BIO notation does not make sense for all use cases. Let's say that if you are interested in extracting _food_ entities then _hamburger_ above might be a **key** entity or tag that you want to predict.

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

Where [spacy](https://spacy.io/) and Transformer architectures from e.g. [HuggingFace](https://huggingface.co/) such as _BERT_, _XLM-ROBERta_ etc. have been the go-to methods or architectures.

Before we start with prompt engineering let's set the stage with an example use case. 

### Food Entities from recipes 
In the following section we will assume the following:
1. We are a food tech startup that provides and sells custom smart purchase lists to retailers from online food recipes.
2. We want to extract the following type of entities: `FOOD`, `QUANTITY`, `UNIT`, `PHYSICAL_QUALITY`, `COLOR`
3. When we have the `entities` we want to populate smart purchase lists with recommendations on where to get the food.

The example [recipe](https://www.carolinescooking.com/chashu-pork/#recipe) that we will be using:

{{< highlight markdown "linenos=inline, style=monokai" >}}

### Chashu pork (for ramen and more)
Chashu pork is a classic way to prepare pork belly for Japanese dishes such as ramen. 
While it takes a little time, it's relatively hands-off and easy, and the result is delicious.

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

## Technique #1 - Use `temperature=0.0`
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
The next step is to use `clear` instructions to the agent normally:
* `System` prompt is used for instructions
* `User` prompt to provide context and data
* (`Assistant`) prompt to provide examples

Starting with a prompt like the below:
{{< highlight markdown "linenos=inline, style=monokai" >}}

System:
You are a food AI assistant who is an expert in natural language processing
and especially name entity recognition.

User:
Extract all food-related entities from the recipe below in backticks:
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

You can also use the `Assistant` message to prompt with some examples:
{{< highlight markdown "linenos=inline, style=monokai" >}}

Assistant:
Example:
```json
{
  "food": "minced meat",
  "quantity": 500
  "unit": grams (g)
  "physicalQuality": "minced",
  "color": "brown"
}
```
...
{{< / highlight >}}

{{< notice tip >}} 
**Tip 3**: Use clear instructions.
{{< /notice >}}

## Technique #4 - Use `function` or `tools`
When we use `functions` or `tools` we prompt the model to provide input arguments for an actual function in a downstream manner. The functions will also be part of the system prompt. Many of the latest models have been fine-tuned to work with function calling and thus produce valid `JSON` output in that way. To define a function we define a `jsonSchema` as below:

{{< highlight json "linenos=inline, style=monokai" >}}

{
    "name": "extract_food_entities",
    "description": "You are a food AI assistant. Your task is to extract food entities from a recipe based on the JSON schema. You are to return the output as valid JSON.",
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
            "quantity": {
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
            "quantity",
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

The example output of using the `extract_food_entities` below is:
{{< highlight json "linenos=inline, style=monokai" >}}

{
    "food-metadata": {
        "food": "Pork Belly",
        "quantity": "2",
        "unit": "lb",
        "physicalQuality": "-",
        "color": "-"
    }
}
{{< / highlight >}}

{{< notice tip >}} 
**Tip 4**: Use `tools` or `function` calling with a `jsonSchema` to extract wanted metadata.
{{< /notice >}}

## Technique #5 - Use domain prompts 
As seen above using the `jsonSchema` above gives us metadata in a structured format that we can use for downstream processing. However, there are some limitations in the number of characters you can set in the description for each `property` in the `jsonSchema`. One way to give further instructions to the LLM is to add `domain-specific` instructions to e.g. the `system` prompt:

{{< highlight markdown "linenos=inline, style=monokai" >}}

System:
You are a food AI assistant who is an expert in natural language processing
and especially name entity recognition. The entities we are interested in are: "food", "quantity", "unit", "physicalQuality" and "color". 

See further instructions below for each entity:

"food": This can be both liquid and solid food such as meat, vegetables, alcohol, etc. 

"quantity": The exact quantity or amount of the food that should be used in the recipe. Answer in both full units such as 1,2,3, etc but also fractions e.g. 1/3, 2/4, etc. 

"unit": The unit being used e.g. grams, milliliters, pounds, etc. The unit must always be returned.

"physicalQuality": The characteristic of the ingredient (e.g. boneless for chicken breast, frozen for
spinach, fresh or dried for basil, powdered for sugar).

"color": The color of the food e.g. green, black, white. If no color is identified respond with colorless.

User:
Extract all food-related entities from the recipe below in backticks:
```{recipe}```
...
{{< / highlight >}}

Example output with this update prompt is shown below:
{{< highlight json "linenos=inline, style=monokai" >}}

{
    "food-metadata": {
        "food": "pork belly",
        "quantity": "2 lb",
        "unit": "pound",
        "physicalQuality": "raw",
        "color": "colorless"
    }
}

{
    "food-metadata": {
        "food": "green onions", 
        "quantity": "2",
        "unit": "pieces",
        "physicalQuality": "fresh",
        "color": "green"
    }
}
{{< / highlight >}}
{{< notice tip >}} 
**Tip 5**: Incorporate `domain` knowledge to help the LLM with extracting the entities you are looking for.
{{< /notice >}}

## Technique #6 - Use Chain-of-Thought
{{< notice info >}} 
Chain-of-Thought (CoT) is a prompting technique where each input question is followed by an intermediate reasoning step, that leads to the final answer. This shown to improve the the output from LLMs. There is also a slight variation of CoT called _Zero-Shot Chain-of-Thought_ where you introduce **“Let’s think step by step”** to guide the LLM's reasoning.
{{< /notice >}}

An update to the prompt now using *Zero-Shot Chain-of-Thought* would be:

{{< highlight markdown "linenos=inline, style=monokai" >}}

System:
You are a food AI assistant who is an expert in natural language processing
and especially name entity recognition. The entities we are interested in are: "food", "quantity", "unit", "physicalQuality" and "color". 

See further instructions below for each entity:

"food": This can be both liquid and solid food such as meat, vegetables, alcohol, etc. 

"quantity": The exact quantity or amount of the food that should be used in the recipe. Answer in both full units such as 1,2,3, etc but also fractions e.g. 1/3, 2/4, etc. 

"unit": The unit being used e.g. grams, milliliters, pounds, etc. The unit must always be returned.

"physicalQuality": The characteristic of the ingredient (e.g. boneless for chicken breast, frozen for
spinach, fresh or dried for basil, powdered for sugar).

"color": The color of the food e.g. green, black, white. If no color is identified respond with colorless.

Let's think step-by-step.

User:
Extract all food-related entities from the recipe below in backticks:
```{recipe}```
...
{{< / highlight >}}

By adding **“Let’s think step by step”** we can see some slight improvements for the extraction:
{{< highlight json "linenos=inline, style=monokai" >}}

{
    "food-metadata": {
        "food": "pork belly", "quantity": "2 lb",
        "unit": "ounce",
        "physicalQuality": "trimmed",
        "color": "colorless"
    }
}
{{< / highlight >}}
Trimmed is likely a better `physicalQuality` to describe the pork belly, instead of `raw`. This as the pork belly is sliced and used as a topping e.g. a bowl of ramen.

{{< notice tip >}} 
**Tip 6**: `Chain-of-thought` may improve performance, especially for fields that need some calculation or reasoning steps.
{{< /notice >}}

## Technique #7 - Use Prompt Chaining
{{< notice info >}} 
To improve the reliability and performance of LLMs, one of the important prompting engineering techniques is to break tasks into subtasks. Once those subtasks have been identified, the LLM is prompted with a subtask and then its response is used as input to another prompt. This is what's referred to as prompt chaining where a task is split into subtasks with the idea to create a chain of prompt operations.
— <cite>Prompt Engineering Guide[^6]</cite>

[^6]: The above quote is excerpted from https://www.promptingguide.ai/techniques/prompt_chaining
{{< /notice >}}

*Prompt Chaining* is somewhat similar to CoT here with the idea of breaking down the problem into sub-problems or tasks. However, the main difference here is that one prompt outputs its response from a previous prompt to the next prompt as refined context.

In our recipe example, we might construct a prompt looking like the below:

{{< highlight python "linenos=inline, style=monokai" >}}
CONTEXT_PROMPT = """
You are a food AI assistant who is an expert in natural language processing
and especially named entity recognition. The entities we are interested in are: "food", "quantity", "unit", "physicalQuality" and "color". 

Your task is to extract the entity, the value of the entity and the reasoning, 
for why the extracted value is the correct value. 
If you cannot extract the entity add "N/A".

Make sure to output the results according to the output format below.

<Food-Metadata>:
"<metadata>":
- Entity: // the actual entity i.e. pork, onions etc
- Value: // Value of the metadata field
- Reasoning: // Reasoning for why the entity is correct.

Let's think step-by-step.
"""
{{< / highlight >}}

The output from the first prompt is:
{{< highlight markdown "linenos=inline, style=monokai" >}}
"pork":
- Entity: food
- Value: pork belly
- Reasoning: The text mentions preparing pork belly for Japanese dishes such as ramen, and the recipe specifically calls for 2 lb of pork belly.

"green onions":
- Entity: food
- Value: green onions
- Reasoning: The text mentions using 2 green onions and specifies that 3 should be used if they are small.

"ginger":
- Entity: food
- Value: ginger
- Reasoning: The recipe specifies using 1 inch of fresh ginger.

"garlic":
- Entity: food
- Value: garlic
- Reasoning: The recipe specifies using 2 cloves of garlic.

"sake":
- Entity: food
- Value: sake
- Reasoning: The recipe calls for ⅔ cup of sake.

"soy sauce":
- Entity: food
- Value: soy sauce
- Reasoning: The recipe calls for ⅔ cup of soy sauce.

"mirin":
- Entity: food
- Value: mirin
- Reasoning: The recipe calls for ¼ cup of mirin.

"sugar":
- Entity: food
- Value: sugar
- Reasoning: The recipe calls for ½ cup of sugar.

"water":
- Entity: food
- Value: water
- Reasoning: The recipe specifies using 2 cups of water.
{{< / highlight >}}
We then use the output from the prompt above as input to our `extract_food_entities` prompt from before. This approach may be helpful when you have entities that need to be calculated with some reasoning around them or they may not be in the exact format that you have in your JSON schema.

{{< notice tip >}} 
**Tip 7**: `Prompt-Chaining` can help as an import pre-processing step to provide more relevant context.
{{< /notice >}}

## Closing Remarks
In this post, we have been walking through some useful prompt-engineering techniques that might be helpful when you deal with Named Entity Recognition (NER) using LLMs such as OpenAI. Depending on your use-case one or several of these techniques may help improve your NER solution. However, writing clear instructions, using CoT and or prompt chaining together with `tools` or `functions` tend to improve the NER extraction.