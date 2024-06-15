---
title: Intent Detection using LLMs
seo_title: Intent Detection using LLM
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

In today’s digital landscape, product teams are increasingly incorporating AI-driven features powered by *Large Language Models (LLMs)*. These advanced capabilities enhance various system components, including search, question-answering, and data extraction. 

However, a crucial preliminary step in delivering the right feature at the right time is accurately *routing* and interpreting user *actions*. Understanding user intent is therefore fundamental to the success of any LLM and Retrieval-Augmented Generation (RAG) based solution.

In this blog post, we will delve into how LLMs :robot: can be utilized to effectively detect and interpret user intent from a diverse range of queries.

## What is intent detection and why does it matter?
**Intent Detection** or *intent recognition* is an NLP technique used to identify the purpose or goal behind a user's query. Historically, this type of classification problem has been very important in <cite>search and recommendation engines [^1]</cite>.

Some key aspects of intent detection include:
- **Natural Language Understanding**: i.e. understanding the *meaning* behind what a user is saying.
- **Context Analysis**: i.e. considering the context in which the user query is in to accurately detect the intent. The context here could be a document, a part of a document, in a chat etc.
- **Classification**: i.e. assigning pre-defined labels or categories to a user's input and predicted intent.

As you can imagine this is a crucial step for an LLM-based system using e.g. RAG for various reasons such as:
- **Improving the user experience**: by understanding users we can *tailor* responses and actions to meet individual needs. But also improve the efficiency and relevancy of the responses to the user's query by *personalization*.
- **Automation**: knowing or predicting the intent can lead to the automation of certain pre-defined routines or tasks based on the user's query.
- **Feature Activation**: intent detection can be used to *route* the user to various parts of our system based on the predicted intent and thus incorporate *context* to respond to user queries promptly.

You may have heard about <cite>_semantic routing_[^2]</cite>, which is an adjacent concept. TLDR; use intent detection to route your users to relevant features or parts of your system to provide them with a tailored and timely experience.

[^1]: [Papers With Code, Intent Detection](https://paperswithcode.com/task/intent-detection)
[^2]: [Langchain, Route Logic Based on Input](https://python.langchain.com/v0.1/docs/expression_language/how_to/routing/)

## Intent Detection Method(s)
Now that we know what *intent detection* is, what it can be used for and why it is important.

Let's delve a bit further into various methods for detecting intent:

{{<mermaid>}}
graph LR
    A[Intent Detection Methods]

    A --> B[Rule-based Methods]
    B --> B1[Predefined Rules]
    B --> B2[Keyword Matching]

    A --> C[Traditional NLP Methods]
    C --> C1[Bag-of-Words]
    C --> C2[TF-IDF]

    A --> D[Classification Models]
    D --> D1[Naive Bayes]
    D --> D2[SVM]
    D --> D3[Random Forests]

    A --> G[Sequence Models]
    G --> G1[RNN]
    G --> G2[LSTM]
    G --> G3[GRU]

    A --> E[Transformer-based Methods]
    E --> E1[BERT]
    E --> E2[GPT]
    E --> E3[SetFit]
    E --> E4[FastFit]

    A --> F[Large Language Models]
    F --> F1[GPT-4o]
    F --> F2[Haiku]
    F --> F3[Mistral Large]
{{</mermaid>}}

A rough classification of these various methods is the following:
- Rule-based
- Traditional NLP methods
- Classification models 
- Sequence models
- Transformer-based models
- Large Language models

We will not look into all the details of these various methods. If you want to learn more, numerous great sources are available online for each type of method/algorithm mentioned.

However, see the table below, with some pros and cons of these various methods:
 
| **Method**                  | **Pros**                                                        | **Cons**                                                        |
|-----------------------------|-----------------------------------------------------------------|-----------------------------------------------------------------|
| **Rule-based Methods**      | - Simple to implement and interpret <br> - Easy to maintain for small sets of rules | - Limited flexibility and scalability <br> - Requires manual updates for new intents and vocabulary |
| **Traditional NLP Methods** (Bag-of-Words, TF-IDF) | - Simple and effective for basic text classification <br> - Quick and computationally inexpensive | - Ignores word order and context <br> - Can lead to loss of meaning |
| **Classification Models** (Naive Bayes, SVM, Random Forests) | - Generally more accurate than rule-based systems <br> - Can handle a variety of inputs | - Requires feature engineering <br> - May not capture complex linguistic nuances |
| **Sequence Models** (RNN, LSTM, GRU) | - Effective for capturing context and handling long sequences <br> - Good at modeling temporal dependencies in text | - Computationally intensive <br> - Requires large datasets |
| **Transformer-based Methods** (BERT, GPT, SetFit, FastFit) | - State-of-the-art performance in many NLP tasks <br> - Capable of understanding complex context and nuances | - Requires significant computational power <br> - Needs substantial training data |
| **Large Language Models** (GPT-4o, Haiku, Mistral Large) | - High accuracy and versatility in various applications <br> - Can handle a wide range of tasks without extensive retraining | - Very computationally expensive <br> - Potential issues with bias and interpretability |            |

## Intent Detection Using LLM(s)
Now that we know what `Ìntent Detection` is and why it is useful, let's look at a *real-world* example of how you could `detect` intent using LLMs.

In this example, we will operate a fictional recipe chatbot where people can in a QA fashion ask questions about a recipe and also get recipe recommendations. Our end-users, can either chat in the context of a `recipe` or a more general `QA` context. 

This means that we have two distinct `ContextTypes` to consider based on the user's actions:
1. `RECIPE`: queries in the context of a recipe 
2. `GENERAL`: more general queries not strictly connected to a specific recipe.


After talking with our product team and some clients, we understand that to a start we need to be able to detect the following `IntentTypes`:
1. `RECIPE_QA`: Question and answer about a recipe 
2. `RECIPE_SUGGEST`: Suggestions or changes to a recipe
3. `RECIPE_TRANSLATE`: Translate a recipe, or parts of a recipe in some way or form
4. `RECIPE_EXPLAIN`: Explain a recipe in more detail i.e. what type of cuisine is this etc.
5. `GENERAL_QA`: General QA with the chatbot
6. `GENREAL_RECOMMENDATION`: Queries related to getting recipe recommendations 

To spice :fire: it up a bit we will be using `TypeScript` for this example, mainly as I have been doing quite a lot of `TS` and `JS` lately at my current workplace.

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
            foodContextType: z.nativeEnum(FoodContextType))
            .describe('Type of context the user is in'),
            foodIntentType: z.nativeEnum(FoodIntentType))
            .describe('Predict food related intent'),
            reasoning: z.string()
            .describe('Reasoning around the predicted intent')
        })
      )
});

/* Infer type */
type FoodIntentDetectionResponse = z.infer<typeof zDetectFoodIntentResponse>;
{{< / highlight >}}

Many modern LLMs have no support tool calling / structured output out-of-the-box, and using orchestrating libraries such as `langchain` makes it very easy to get started. Langchain released fairly recent updates to how to do structured output extraction and function calling across several different LLM providers. See more about it [here](https://blog.langchain.dev/tool-calling-with-langchain/).

To continue, the next step is to create our `prompt` and build or `chain` of one or several `LLM` calls. If you want to see some tips and tricks on how to do multiple LLM calls for data extraction tasks see my other [blogpost](https://dswithmac.com/posts/prompt-eng-ner/). And if you like me are a fan of `DSPy` check my other [post](https://dswithmac.com/posts/ner-dspy/). Anyhow, on the initial starting point of our prompt:

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

First, we define a helper class to keep track of our chat messages:

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

    const = chain = ChatPromptTemplate
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

Not too hard right? Using this function we might get output such as the below for different queries:

Query 1:
> "Can give me a good dinner recommendation that is fairly quick and easy, preferably japanese?"

Output 1:
{{< highlight json "linenos=inline, style=monokailight" >}}
{
    "foodIntent": [
        {
            "foodContextType": "GENERAL",
            "foodIntentType": "GENERAL_RECOMMENDATION",
            "reasoning": "The user is asking for a recommendation of Japanese food that is easy and quick. Due to this, the predicted intent is GENERAL_RECOMMENDATION."
        }
    ]
}

{{< / highlight >}}

Query 2:
> "This recipe is great, but I would like to make it vegetarian, and also use the imperial system instead of the metrics system for the ingredients"

Output 2:
{{< highlight json "linenos=inline, style=monokailight" >}}
{
    "foodIntent": [
        {
            "foodContextType": "RECIPE",
            "foodIntentType": "RECIPE_QA",
            "reasoning": "The user ..."
        },
        {
            "foodContextType": "RECIPE",
            "foodIntentType": "RECIPE_TRANSLATE",
            "reasoning": "The user ..."
        },
    ]
}

{{< / highlight >}}


## Closing remarks
In this post, we explored *intent detection* in a bit more detail and why it is important for any AI or LLM-powered system. With the main goal of increasing the relevancy and accuracy of a user's query in a QA/search-based system.

We also demonstrated how you could use LLMs such as `gpt-4o` to detect *intent* in a fictional QA system. Intent detection is not just a technical necessity but a strategic advantage in building intelligent, user-centric LLM-powered systems.

Even if we used `gpt-4o` in this example, there are many relevant lower latency alternatives such as `haiku` from Antrophic. And if you have a few 100s of examples other transformer-based approaches such as `FastFit` or `SetFit` are also interesting. Thanks for reading and until the next time :wave:!