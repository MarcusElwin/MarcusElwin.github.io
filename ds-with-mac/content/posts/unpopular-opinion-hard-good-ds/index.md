---
title: Unpopular Opinion - It's harder then ever to be a good data scientist
seo_title: Unpopular Opinion - It's harder then ever to be a good data scientist
summary:  It is an understatement, that AI and particularly the Data Science profession is chaning drastically, with the introduction of GenAI and Large Language Models. In today’s GenAI driven world, being a good data scientist is more challenging than ever before. In this article I will summarize some of my thoughts and experience working with both traditional Data Science and recently AI Engineering.
description: Some thoughts and experiences working as a "traditional" Data Scientist and now recently as more of an AI engineer.
slug: unpopular-opinion-hard-being-good-ds
author: Marcus Elwin

draft: false
date: 2024-10-20T16:52:55+02:00
lastmod: 
expiryDate: 
publishDate: 

feature_image: 
feature_image_alt: 

categories:
    - "Data Science"
    - "Career Advice" 
tags:
    - "Data Science"
    - "Large Language Models"
    - "Ai Engineering"
series:

toc: true
related: true
social_share: true
newsletter: false
disable_comments: false
---

Over the past **6+ years** (and nearly a *decade* being involved with AI), I’ve worked across various industries and companies of all sizes, from large corporations to agile startups. This experience has given me a front-row seat to the diverse structures and maturity levels of data science teams and their adjacent roles. Like many data professionals, I recently made the transition to AI engineering, focusing on the practical deployment of GenAI and Large Language Models (LLMs) in production environments over the past year.

The data science landscape has evolved rapidly, especially with the rise of GenAI and LLMs. While these advancements have opened new doors, they have also made it more challenging than ever to be a “good” data scientist. From managing high expectations in organizations with little to no data strategy, to navigating the hype that has turned everyone into self-proclaimed “AI specialists,” the role of a data scientist is more complex than it once was.

In this article, I’ll share my thoughts and experiences on the challenges data scientists face today. We’ll look at what it means to be a *V-shaped data scientist*, how data quality issues impact performance, the importance of deep domain knowledge, and the blurred lines between DataOps, MLOps, AIOps, and traditional DevOps. My goal is to shed light on the realities of this profession and why the path to becoming a truly skilled data scientist is more demanding than ever.

## What is a good Data Scientist?
When I began my career in data science, my work primarily involved using **R** and **SQL** to conduct statistical analysis for the stock exchange. The cutting-edge computer vision and deep learning algorithms I had studied felt distant from my day-to-day reality at the time. However, as my career progressed, I had the opportunity to apply deep learning techniques and deploy them in real-world production environments. This evolution mirrors a broader shift in the expectations placed on data scientists, which have expanded from traditional machine learning to include deep learning and now GenAI and Large Language Models (LLMs).

The role of a “good” data scientist has continuously evolved, and so have the titles and responsibilities. Depending on the company or industry, a data scientist might focus on anything from statistical modeling to full-stack AI deployment. (See more on this under Issue #3). Despite these variations, there are core skills that I believe are essential for data scientists to thrive in today’s dynamic industry.

This brings us to the concept of the “V-shaped Data Scientist.”

{{<mermaid>}}
graph TD;
    A[Data Scientist]
    B[Logical Thinking, Mathematical & Statistical Fundamentals]
    C[Domain and Business Understanding]
    D[System Design and Architecture Skills]
    E[Ownership of End-to-End Application Stack]
    F[Intellectual Curiosity and Continuous Learning]

    A -->|Core Skills| B
    A -->|Differentiators in AI application| C
    A -->|Crucial for AI Systems| D
    A -->|Beyond Proficiency in Modeling| E
    A -->|Essential for Keeping Up-to-Date| F

    B -->|Critical for| G[Verifying AI-Generated Content]
    C -->|Leads to| H[Solving Actual User-Centric Use Cases]
    D -->|Includes| I[Monitoring, Tracing, Drift Detection]
    E -->|Reduces Need For| J[Building Custom Models]
    F -->|Enables| K[Adaptation to Rapid Industry Changes]

    G -.->|In context of| J
    I -.->|Supports| E
    K -.->|Necessitates| C
    H -->|Benefits from| D
{{</mermaid>}}

As I see it, there are five key areas where a successful data scientist must be versatile:

1.	**Logical Thinking, Mathematical & Statistical Fundamentals**: A solid understanding of these principles is the foundation for building reliable models and verifying outputs.

2.	**Domain and Business Understanding**: Knowing the industry context ensures that data solutions address real-world problems and create value.

3.	**System Design and Architecture Skills**: Building scalable and maintainable systems requires a grasp of system architecture, especially for deploying AI models.

4.	**Ownership of End-to-End Application Stack**: From data preprocessing to model deployment, owning the entire workflow allows for seamless integration and maintenance.

5.	**Intellectual Curiosity and Continuous Learning**: The rapidly changing field demands a passion for continuous learning to stay current with emerging trends and technologies.

These skills form the core of a “V-shaped” data scientist, who combines depth in specific areas with broad capabilities across the entire data or ML workflow.


{{<mermaid>}}
pie
    title Skills of a V-shaped Data Scientist
    "Deep Expertise in AI & ML" : 30
    "Programming & System Development" : 20
    "Data Engineering" : 20
    "Business Acumen" : 20
    "Ethics & Governance" : 10
{{</mermaid>}}

For more on the concept of the V-shaped data scientist, check out my detailed article in [[1](https://medium.com/gopenai/v-shaped-data-scientist-in-the-era-of-generative-ai-b29f1bca93b7)].

## Issue #1 - High expectations but no data or data strategy
AI is now on every board and company wish list. Since the inception of ChatGPT in late 2022, there’s been a rush to become “AI-driven,” with many businesses eager to integrate AI capabilities into their products. It may seem easier than ever to implement AI using Large Language Models (LLMs), but the reality is far more complex.

As a data scientist working to bring ML systems or LLMs into production, I’ve encountered several key challenges that reveal a gap between expectations and reality. Regardless of whether we call it AI, ML, or LLM, the success of these technologies hinges on having a solid foundation in place. 

Here are some of the main issues:

**No Data** 🏗️:
* *The Data Pipeline Dilemma*: Without data, even the most advanced AI models are useless. Many companies underestimate the importance of having robust data pipelines that can collect, clean, and prepare data for analysis. As a data scientist, you may find yourself spending more time convincing the organization to invest in data engineers or analytics engineers who can help build these essential pipelines.
  
* *Scattered and Unstructured Data:* Companies may also have data, but it is often siloed, inconsistent, or poorly structured, making it difficult to use effectively for AI applications.
  
**No Data Strategy** 🧭:
* *Data Without Direction*: Simply having data is not enough. If there’s no clear strategy on how to leverage this data, you might face significant roadblocks. For example, sensitive data that cannot be used freely, or a lack of data governance, can lead to major compliance and privacy issues. Without a strategic approach, data science efforts might not result in meaningful insights or business value.
  
* *Becoming Truly Data-Driven:* A proper data strategy means having a clear understanding of what data is needed, how it will be collected, and how it can drive the company’s goals. Without this, data scientists end up solving problems that don’t matter, or worse, creating solutions that no one will use.

**No AI Strategy** 🎯:
* *“We Need AI, But We Don’t Know Why”*: This is a common scenario. Many companies feel pressured to adopt AI simply because it’s the latest trend, without any clear understanding of how it fits into their business model. Implementing AI without a clear use case is like building a solution in search of a problem. For example, creating a fancy Text2SQL bot or chatbot might sound great, but without a clear vertical or objective, it’s unlikely to yield significant benefits.
  
* *Defining Real-World Use Cases*: An effective AI strategy should map out specific business problems where AI can offer a competitive advantage. Without this focus, data science projects can end up as expensive experiments that don’t deliver ROI.

**No Labeling Strategy 🏷️**:
* *The Need for Accurate Evaluation*: Even though LLMs are remarkably capable, you still need to evaluate their outputs, and this often requires labeled data. While it’s tempting to rely on the “LLM as a judge” approach, this can lead to misleading conclusions if the model isn’t properly benchmarked.
  
* *Ownership and Management of Labels*: Labeling data is a critical part of many AI workflows, especially for tasks requiring supervised learning. This means someone needs to take ownership of the labeling process, ensuring quality, consistency, and relevance. Without a clear labeling strategy, data scientists are left trying to generate signals from data they don’t fully understand, leading to a confusing and ineffective model development cycle.
  
* *Synthetic Data vs. Real Labels*: There’s been growing interest in using generated or synthetic data to fill gaps, and while this can be helpful, it’s not a cure-all. If you’re generating data without understanding the underlying patterns, you might end up reinforcing biases or missing key insights, which can lead to flawed models.

These challenges highlight a common theme: **high expectations but a lack of foundational support**. Companies eager to adopt AI must first address these fundamental issues by investing in data infrastructure, developing clear strategies, and fostering a culture that understands the importance of quality data. Otherwise, the gap between expectations and reality will continue to widen, making it harder for data scientists to deliver meaningful results. I think this is also a key reason why many Data Scientists quits and progress to do something else e.g. Data Engineering[[2](https://analyticsvidhya.com/blog/2019/12/5-key-reasons-data-scientists-quit-jobs/)][[3](https://www.omdena.com/blog/why-data-scientists-leave-their-jobs)]. *Luickly*, more and more companies are starting to understand this and employees a <cite>CAIO or *Chief AI Officer*[^1]</cite>.

[^1]: Read more here: https://www.forbes.com/sites/jackkelly/2024/05/28/the-rise-of-the-chief-ai-officer/


## Issue #2 - AI, GenAI and LLM hype everyone are now "AI" specialists
__TODO__

## Issue #3: The Inconsistent Nature of Data Science Roles Across Companies
__TODO__

## Issue #4: The Data Quality Problem
__TODO__

## Issue #5: The need for deep domain knowledge 
__TODO__

## Issue #6: DataOps, MLOps, AIOps, LLMOPs or just DevOps? 
__TODO__

## Issue #7: The Impact of Rapid Technological Change

## References
1. Elwin, M. (2024). V-shaped Data Scientist in the Era of Generative AI. Medium. Available at: https://medium.com/gopenai/v-shaped-data-scientist-in-the-era-of-generative-ai-b29f1bca93b7
2. Analytics Vidhya. (2020). 5 Key Reasons Why Data Scientists Are Quitting their Jobs. Retrieved from: https://www.analyticsvidhya.com/blog/2019/12/5-key-reasons-data-scientists-quit-jobs/
3. Omdena. (2023). Top 3 Reasons Why Data Scientists Are Leaving Their Jobs. Retrieved from: https://www.omdena.com/blog/why-data-scientists-leave-their-jobs 