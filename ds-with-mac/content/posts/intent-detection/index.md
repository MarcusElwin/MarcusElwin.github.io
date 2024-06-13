---
title: Intent Detection
seo_title: Intent Detection
summary: 
description: Learn more about Intent Detection and how we can predict user intent using Langchain and LLMs.
slug: intent-detection
author: Marcus Elwin

draft: false
date: 2024-06-13T20:28:39+02:00
lastmod: 
expiryDate: 
publishDate: 

feature_image: 
feature_image_alt: 

categories:
    - "Intent Detection"
    - "Classification"
tags:
    - "Large Language Models (LLMs)"
    - "Machine Learning"
    - "RAG"
    - "Routing"
    - "TypeScript"
series:

toc: true
related: true
social_share: true
newsletter: true
disable_comments: false
---

Ex do est exercitation minim ullamco irure ex labore nostrud sit ea reprehenderit. Velit dolor quis est quis cupidatat consectetur exercitation commodo sed reprehenderit voluptate anim lorem exercitation mollit sint magna minim. Commodo occaecat magna consequat sit est duis tempor ut aliquip incididunt tempor sit nostrud. Ipsum aliqua nisi nisi ipsum aliquip sed quis laboris occaecat ipsum consectetur culpa dolore ad aliqua ullamco.

## What is intent detection and why does it matter?
__TODO__

## Intent Detection Method(s)
__TODO__

## Intent Detection Using LLM(s)
Now that we know what `Ìntent Detection` is and why it is useful, let's look at a real-world example of how you could `detect` intent using LLMs.

In this example, we will operate a fictional recipe chatbot where people can in a QA fashion ask questions about a recipe and also get recipe recommendations. For our end-users, they can either chat in the context of a `recipe` or in a more general `QA` context. This means that we have two distinct `ContextTypes` to consider based on the user's actions:
1. `RECIPE`: queries in the context of a recipe 
2. `GENERAL`: more general queries not strictly connected to a specific recipe.


After talking with our product team and some clients, we understand that to a start we need to be able to detect the following `IntentTypes`:
1. `RECIPE_QA`: Question and answer about a recipe 
2. `RECIPE_SUGGEST`: Suggestions or changes to a recipe
3. `RECIPE_TRANSLATE`: Translate a recipe, or parts of a recipe in some way or form
4. `RECIPE_EXPLAIN`: Explain a recipe in more detail i.e. what type of cuisine is this etc.
5. `GENERAL_QA`: General QA with the chatbot
6. `GENREAL_RECOMMENDATION`: Queries related to getting recipe recommendations 

To spice it up a bit we will be using `TypeScript` for this example, mainly as I have been doing quite a lot of `TS` and `JS` lately at my current workplace:

The libraries we will be using:
* `@langchain/openai`
* `@langchain/core`
* `zod`

To start with, let's see what `entities` we have to deal with, `TS` we use `enums` to enumerate these:

{{< highlight typescript "linenos=inline, style=monokailight" >}}
/* Enum for chat context */
export enum FoodContextType {
    RECIPE = "RECIPE"
    GENERAL = "GENERAL"
}

/* Enum for chat intent */
export enum FoodIntentType {
    RECIPE_QA = "RECIPE_QA"
    RECIPE_SUGGEST = "RECIPE_SUGGEST"
    RECIPE_TRANSLATE = "RECIPE_TRANSLATE"
    RECIPE_EXPLAIN = "RECIPE_EXPLAIN"
    GENERAL_QA = "GENERAL_QA"
    GENERAL_RECOMMENDATION = "GENERAL_RECOMMENDATION"
}
{{< / highlight >}}

As `intentDetection` is a `classification` problem we want to use an LLM to predict what the user intent is based on the following:
- `context`: the context the user is in
- `userQuery`: the actual user question or queries.

`Intent` can also be of multiple meanings i.e. only allowing or deducing a single intent might be wrong. For instance, look at the query below:
> "Please recommended me a french cooking recipe with instructions in french":
Some intent we can deduce based on the query is the following:
1. `GENERAL_RECOMMENDATION`: the user clearly wants to cook :fr: 
2. `RECIPE_TRANSLATE`: the user clearly wants to cook French food in French:fr: :fr:

To model this we want to use `zod` (which is somewhat similar to `Pydantic` in Python). Luckily for us, many LLM(s) are good at `functionCalling` and extracting `structuredOutput` based on a provided schema.

A `zod` object for our task could look like the below:
{{< highlight typescript "linenos=inline, style=monokailight" >}}
import { z } from 'zod';

const zDetectFoodIntentResponse = z.object({
    foodIntent: z
      .array(
        z.object({
            inputType: z.nativeEnum(FoodContextType))
            .describe('Type of context the user is in'),
            intentType: z.nativeEnum(FoodIntentType))
            .describe('Predicte food related intent'),
            reasoning: z.string()
            .describe('Reasoning around the predicted intent')
        })
      )
});

/* Infer type */
type FoodIntentDetectionResponse = z.infer<typeof zDetectFoodIntentResponse>;
{{< / highlight >}}

Many modern LLMs have no support tool calling / structured output out-of-the-box, and using orchestrating libraries such as `langchain` makes it very easy to get started. Langchain released fairly recent updates to how to do structured output extraction and function calling across several different LLM providers. See more about it [here](https://blog.langchain.dev/tool-calling-with-langchain/).

To continue, next step is to create our `prompt` and build or `chain` of one or several `LLM` calls. If you want to see some tips and tricks on how to do multiple LLM calls for data extraction tasks see my other [blogpost](https://dswithmac.com/posts/prompt-eng-ner/). And if you like me are a fan of `DSPy` check my other [post](https://dswithmac.com/posts/ner-dspy/). Anyhow, on the initial starting point of our prompt:

{{< highlight typescript "linenos=inline, style=monokailight" >}}
export const FoodIntentDetectionPromptTemplate = `
You are an expert restauranteur and online TV chef.
Based on the provided 'context' and 'userQuery', predict the users 'intent'.
Make sure to follow the instructions.

# Instructions
1. Only use the 'foodContextTypes' specified in the schema.
2. Use the 'foodContextType' to determine what type of 'context' the user is in.
3. Based on the 'foodContextType' and 'userQuery' predict the 'foodIntentType'.
4. If the 'userQuery' is uncertain, unclear, or irrelevant use 'GENERAL_QA' as the default intent.

# Food Context Input Type
{foodContextType}

# User Context
{context}

# User Query
{userQuery}
`
{{< / highlight >}}

As prompt engineering is still more of an art than a science (if you are not using frameworks such as `DSPy`) you likely need to refine a prompt such as the above for your use case. Anyhow, for this example, this is good enough and let's proceed with building our chain.

First we define a helper class to keep track of our chat messages:

{{< highlight typescript "linenos=inline, style=monokailight" >}}
import { ChatPromptTemplate } from '@langchain/core/prompts'
import { ChatOpenAI } from '@langchain/openai'

/* MessageRole enum */
export enum MessageRole {
    ASSISTANT = 'ASSISTANT'
    SYSTEM = 'SYSTEM'
    USER = 'USER'
}

/* Messages object */
export class Messages {
    id: string;
    content: string
    recipe: string
    role: MessageRole
}
}
{{< / highlight >}}

Then we build our `predictIntent` function:

{{< highlight typescript "linenos=inline, style=monokailight" >}}
async predictIntent(messages: Messages)
: Promise<FoodIntentDetectionResponse> {
    // unpack message
    const { content, recipe, role } = message;

    // get userContext
    const userContext = (content == null && recipe != null): recipe ? content; 

    // deduce foodContextType from message
    const foodContextType = !recipe ? FoodContextType.GENERAL : FoodContextType.RECIPE ;

    // get user question
    const userQuery = ...;

    // build chain
    const llm = new ChatOpenAI({
        temperature: 0,
        modelName: 'gpt-3.5-turbo',
        openAIApiKey: process.env.apiKey

    });

    const = chain = ChatPrimptTemplate
    .fromTemplate(FoodIntentDetectionPromptTemplate)
    .pipe(llm.withStructuredOutput(zDetectFoodIntentResponse));

    // invoke chain and parse response
    const response = await chain.invoke(({
        context: userContext ?? '',
        foodContextType,
        userQuery: userquery ?? '' 

    }));

    const parsedResponse = zDetectFoodIntentResponse.safeParse(response);

    if (!parsedResponse.success) {
        throw new Error('Failed to parse response...');
    }

    return parsedResponse.data;


}
{{< / highlight >}}