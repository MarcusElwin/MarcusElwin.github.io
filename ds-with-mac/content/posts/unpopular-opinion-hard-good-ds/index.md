---
title: Unpopular Opinion - It's harder than ever to be a good data scientist
seo_title: Unpopular Opinion - It's harder than ever to be a good data scientist
summary:  It is an understatement to say that AI, particularly the Data Science profession, is changing drastically with the introduction of GenAI and Large Language Models. In today's GenAI-driven world, being a good data scientist is more challenging than ever. In this article, I will summarize some of my thoughts and experiences working in traditional data science and, recently, AI engineering.
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

Over the past **6+ years** (and nearly a **decade** being involved with AI), I've worked across various industries and companies of all sizes, from large corporations 🏢 to agile startups 🚀. This experience has given me a front-row seat 🎟️ to the diverse structures and maturity levels of data science teams and their adjacent roles. Like many data professionals, I recently transitioned to *AI engineering* 🤖, focusing on the practical deployment of GenAI and Large Language Models (LLMs) in production environments over the past year.

The data science landscape has evolved rapidly 🌐, especially with the rise of GenAI and LLMs. While these advancements have opened new doors 🚪, they have also made it more challenging than ever to be a **"good"** data scientist. From managing high expectations in organizations with little to no data strategy 🏗️ to navigating the hype that has turned everyone into self-proclaimed "AI specialists" 🧑‍💻, the role of a data scientist is more complex than it once was.

In this article, I'll share my thoughts and experiences on the challenges data scientists face today. We'll look at what it means to be a **V-shaped data scientist**t 📊, how data quality issues impact performance ⚠️, the importance of deep domain knowledge 🧠, and the blurred lines between *DataOps, MLOps, AIOps*, and traditional *DevOps* 🔄. My goal is to shed light on the realities of this profession and why the path to becoming a genuinely skilled data scientist is more demanding than ever.

**Disclaimer**: The quotes may or may not be inspired by real people. All images are AI generated.

## What is a good Data Scientist?
> So you say you want to do Deep Learning, we don't do any learning here. Rather unlearning. So, focus on Data Engineering instead.  
> — **Random Employer in 2015**

When I began my career in data science, my work primarily involved using **R** and **SQL** to conduct statistical analysis for the stock exchange, focusing on trading behavior. The cutting-edge computer vision and deep learning algorithms I had studied felt distant from my day-to-day reality at the time. However, as my career progressed, I had the opportunity to apply deep learning techniques and deploy them in real-world production environments. This evolution mirrors a broader shift in the expectations placed on data scientists, which have expanded from traditional machine learning to deep learning and now GenAI and Large Language Models (LLMs).

The role of a "good" data scientist has continuously evolved, and so have the titles and responsibilities. Depending on the company or industry, a data scientist might focus on anything from statistical modeling to full-stack AI deployment. (*See more on this under Issue #3*). Despite these variations, there are core skills that are essential for data scientists to thrive in today's dynamic industry.

This brings us to the concept of the "V-shaped Data Scientist."

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

1.  **Logical Thinking, Mathematical & Statistical Fundamentals**: A solid understanding of these principles is the foundation for building reliable models and verifying outputs.

2.  **Domain and Business Understanding**: Knowing the industry context ensures that data solutions address real-world problems and create value.

3.  **System Design and Architecture Skills**: Building scalable and maintainable systems requires a grasp of system architecture, especially for deploying AI models.

4.  **Ownership of End-to-End Application Stack**: From data preprocessing to model deployment, owning the entire workflow allows for seamless integration and maintenance.

5.  **Intellectual Curiosity and Continuous Learning**: The rapidly changing field demands a passion for continuous learning to stay current with emerging trends and technologies.

These skills form the core of a "V-shaped" data scientist who combines depth in specific areas with broad capabilities across the entire data or ML workflow.


{{<mermaid>}}
pie
 title Skills of a V-shaped Data Scientist
 "Deep Expertise in AI & ML": 30
 "Programming & System Development": 20
 "Data Engineering": 20
 "Business Acumen": 20
 "Ethics & Governance": 10
{{</mermaid>}}

For more on the concept of the V-shaped data scientist, check out my detailed article in [[1](https://medium.com/gopenai/v-shaped-data-scientist-in-the-era-of-generative-ai-b29f1bca93b7)].

## Issue #1 - High expectations but no data or data strategy
> We need to do AI, especially GenAI and LLMs. Our competitors are ahead of us with this AI thing. ChatGPT right? Make a chatbot. Make something cool. And by the way, we have no data available for the first year you work here. Privacy issues. GDPR.
> — **Random Manager in 2023**
>

{{< figure src="/pic_issue_1.png" alt="#Issue1" title="Fig 1. High expectations without any clear strategy, makes it hard for AI as well. Source: Author." style="display: block; margin-left: auto; margin-right: auto; width: 50%; max-width: 50%;" >}}

AI is now on every board and company wish list. Since the inception of ChatGPT in late 2022, there's been a rush to become "AI-driven," with many businesses eager to integrate AI capabilities into their products. Implementing AI using Large Language Models (LLMs) may seem more effortless than ever, but the reality is far more complex.

As a data scientist working to bring ML systems or LLMs into production, I've encountered several vital challenges that reveal a gap between expectations and reality. Regardless of whether we call it AI, ML, or LLM, the success of these technologies hinges on having a solid foundation in place. 

Here are some of the main issues:

**No Data** 🏗️:
* *The Data Pipeline Dilemma*: Even the most advanced AI models are useless without data. Many companies need to pay more attention to the importance of having robust data pipelines that can collect, clean, and prepare data for analysis. As a data scientist, you may spend more time convincing the organization to invest in data engineers or analytics engineers who can help build these essential pipelines.
  
* *Scattered and Unstructured Data:* Companies may also have data, but it is often siloed, inconsistent, or poorly structured, making it difficult to use effectively for AI applications.
  
**No Data Strategy** 🧭:
* *Data Without Direction*: Simply having data is not enough. You might face significant roadblocks without a clear strategy for leveraging this data. For example, sensitive data that cannot be used freely or a lack of data governance can lead to major compliance and privacy issues. Data science efforts might lack meaningful insights or business value without a strategic approach.
  
* *Becoming Truly Data-Driven:* A proper data strategy means clearly understanding what data is needed, how it will be collected, and how it can drive the company's goals. Without this, data scientists solve problems that don't matter or create solutions that no one will use.

**No AI Strategy** 🎯:
* *"We Need AI, But We Don't Know Why"*: This is a common scenario. Many companies feel pressured to adopt AI simply because it's the latest trend, without understanding how it fits into their business model. Implementing AI without a clear use case is like building a solution in search of a problem. For example, creating a fancy Text2SQL bot or chatbot might sound great, but without a clear vertical or objective, it's unlikely to yield significant benefits.
  
* *Defining Real-World Use Cases*: An effective AI strategy should map out specific business problems where AI can offer a competitive advantage. Without this focus, data science projects can become expensive experiments that don't deliver ROI.

**No Labeling Strategy 🏷️**:
* *The Need for Accurate Evaluation*: Although LLMs are remarkably capable, you still need to evaluate their outputs, which often require labeled data. While relying on the "LLM as a judge" approach is tempting, this can lead to misleading conclusions if the model isn't properly benchmarked.
  
* *Ownership and Management of Labels*: Labeling data is critical to many AI workflows, especially for tasks requiring supervised learning. This means someone needs to take ownership of the labeling process, ensuring quality, consistency, and relevance. Without a clear labeling strategy, data scientists are left trying to generate signals from data they don't fully understand, leading to a confusing and ineffective model development cycle.
  
* *Synthetic Data vs. Real Labels*: There's been growing interest in using generated or synthetic data to fill gaps, and while this can be helpful, it's not a cure-all. Creating or generating data without understanding the underlying patterns might reinforce biases or miss critical insights, leading to flawed models.

These challenges highlight a common theme: **high expectations but a lack of foundational support**. Companies eager to adopt AI must first address these fundamental issues by investing in data infrastructure, developing clear strategies, and fostering a culture that understands the importance of quality data. Otherwise, the gap between expectations and reality will widen, making it harder for data scientists to deliver meaningful results. I think this is also a key reason why many Data Scientists quit and progress to do something else e.g., Data Engineering[[2](https://analyticsvidhya.com/blog/2019/12/5-key-reasons-data-scientists-quit-jobs/)][[3](https://www.omdena.com/blog/why-data-scientists-leave-their-jobs)]. *Luickly*, more and more companies are starting to understand this and employees a <cite>CAIO or *Chief AI Officer*[^1]</cite>.

[^1]: Read more here: https://www.forbes.com/sites/jackkelly/2024/05/28/the-rise-of-the-chief-ai-officer/


## Issue #2 - AI, GenAI, and LLM hype everyone is now "AI" specialists
> AI, AI for real came in 2022 right with ChatGPT; I have done 5 courses in Prompt Engineering, which is not that hard, right? It works when I try on my oversimplified, non-realistic version of reality on my local machine, which does not consider scale or cost. So chop, chop, make it work. 
> — **Random Manager / non AI Co-worker in 2024**
>
{{< figure src="/pic_issue_2.png" alt="#Issue2" title="Fig 2. There are too many false AI prophets these days. Source: Author." style="display: block; margin-left: auto; margin-right: auto; width: 50%; max-width: 50%;" >}}

Since the launch of Large Language models like GPT, the AI landscape has experienced an explosion of interest, driving businesses to position themselves as "AI-driven" almost overnight. While the increased attention to AI has sparked innovation, it has also led to misconceptions and unrealistic expectations. Many organizations quickly jump on the AI bandwagon without truly understanding what it means to implement these technologies effectively.

Here are some key challenges this hype has created:

**The Rise of the Self-Proclaimed "AI Specialist" 🧑‍💻**:
* *Overnight Experts*: The commoditization of AI, primarily through LLMs, has made these powerful tools much more accessible. With platforms like Cursor[^2] simplifying coding tasks, it has become easier for anyone to claim technical expertise. This has led to a surge of people rebranding themselves as "AI specialists" after taking a short course in "Prompt Engineering" [^3] or reading a few blogs. However, knowing how to ask ChatGPT relevant questions doesn't make someone an expert in, say, finance, healthcare, or any other <cite>domain[^4]</cite>. This overconfidence and influx of self-proclaimed experts can dilute the quality of AI projects, leading to a false sense of competence that ultimately hampers real progress.
  
* *Misaligned Skills*: Companies often have teams that can use AI tools but need more expertise to build, fine-tune, or deploy robust models. This disconnect can lead to poorly executed projects that fail to deliver business value. For instance, I've seen scenarios where senior engineers dismiss AI as a "fad" because it threatens the traditional ways they've worked, a mental defense mechanism to avoid learning new skills. However, on the flip side, many organizations **can't or should** use a full-fledged data scientist or AI specialist from the start. Instead, they might be better off getting their data infrastructure in place and starting with simpler rule-based systems or hiring a well-rounded "AI Engineer" [^5] who can bridge the gap between full-stack engineering and AI deployment.

**Over-Reliance on Plug-and-Play AI Solutions 🔌**:
As many of you have undoubtedly noticed, AI—particularly Generative AI (GenAI)—has become increasingly commoditized. This means that AI can now be integrated into existing systems as a module or component, making it more accessible and widespread. While this democratization is a positive step for increasing AI adoption, it has also led to a surge in so-called **"OpenAI or GPT wrappers"**—applications that add a basic layer over pre-existing models, like ChatGPT, without offering significant value beyond the core functionalities.

Anyone can build a simple Retrieval-Augmented Generation (RAG) solution, but not everyone can build one that <cite>scales effectively[^6]</cite>. This over-reliance on plug-and-play solutions presents several key challenges:

* **The Illusion of Simplicity**: Plug-and-play tools can create a false sense of ease. Businesses might believe they can integrate AI quickly without understanding the complexities of deployment, scaling, or maintenance. For example, deploying an AI chatbot might seem as simple as plugging in an API. Still, issues such as handling real-time interactions, maintaining data security, and managing performance under high demand are far more complex than they appear.

* **Limited Customization and Differentiation**: Many of these solutions are quick to set up but offer little customization. Companies often end up with generic AI tools that don't differentiate them from competitors. For instance, there's no shortage of chatbots that simply wrap OpenAI's API, offering the same basic capabilities as ChatGPT without any unique features. Real differentiation comes from fine-tuning models, integrating domain-specific data, and building on top of the basic model to meet unique business needs.

* **Scalability and Performance Challenges**: While it's easy to prototype with a plug-and-play model, scaling that solution to real-world use cases can be different. Performance bottlenecks, cost inefficiencies, and data integration issues can arise, particularly when models are expected to handle large volumes of requests or complex queries. A basic RAG solution might work in a controlled environment. However, building one that can scale across multiple use cases requires significant engineering expertise, including optimized data pipelines, real-time monitoring, and robust infrastructure.

* **Security and Compliance Risks**: Plug-and-play solutions can lead to security vulnerabilities if not integrated thoughtfully. For example, a company that adds a pre-trained LLM without proper data handling protocols might inadvertently expose sensitive information. Additionally, Compliance with privacy regulations (like GDPR or CCPA) can be tricky when using third-party AI models, mainly if the model processes customer data directly.

**Thinking that LLMs are a universal tool or a panacea for everything ML-related** 🏥:
**Large Language Models (LLMs)** are potent tools—they excel at generating text, answering questions, and extracting information from unstructured data. However, they are not a one-size-fits-all solution for every machine learning problem. AI has been evolving since the 1950s, and various algorithms have been developed, each suited to specific tasks.

**Use LLMs Where They Shine**: LLMs are great for tasks like generating coherent text, summarizing content, language translation, and even providing conversational interfaces. These models are trained on vast datasets, allowing them to handle nuanced language processing and complex question-answering scenarios. They are ideal for cases where understanding and generating human-like text is crucial, such as customer service chatbots, document summarization, or extracting insights from large volumes of textual data.

**But Don't Overreach**: Despite their capabilities, LLMs are not well-suited for every problem. For instance, regression tasks, time series forecasting, and clustering are areas where traditional machine learning models often perform better, like linear regression, ARIMA, or k-means clustering. These tasks require models that can be tightly controlled, easily interpreted, and optimized for numerical precision, where LLMs may lack the necessary specificity or efficiency. Using LLMs for these problems can lead to overfitting, increased computational costs, and a lack of clarity in model performance.

**The Importance of Choosing the Right Tool**: One of the main advantages of traditional ML algorithms is their interpretability and ease of optimization. For example, if you need to predict sales over time, a time series model can provide more accurate predictions and allow you to understand seasonality and trends. Similarly, models like decision trees, support vector machines, or ensemble methods can be tuned more effectively than a massive LLM for classification tasks where the dataset is well-defined.

So, in short, next time you want to use an LLM for something ML already does better: **Trust your Data Scientist's or ML Engineers' judgment** 🧠; this is what they are trained for!

**The Misunderstanding of AI Capabilities vs. Business Needs 🏢**:
We've already discussed the hype vs. reality problem surrounding the AI craze. However, from a business perspective, there are several other misalignments between what AI can do and how companies attempt to use it:

* **The "Cool Factor" vs. Real Value Factor**: Many businesses pursue AI projects because they want to appear innovative without truly understanding how these projects align with their needs. For example, companies might invest in chatbots simply because they are trendy, without considering whether their customers prefer self-service solutions over direct human support. This often leads to projects that look impressive but don't generate real, lasting value.

* **Importance of Defining Clear Use Cases**: Successful AI implementation begins with identifying pain points and defining specific use cases where AI can add measurable value. Instead of investing in generic AI solutions, companies should prioritize projects that directly impact their bottom line, such as predictive maintenance in manufacturing or personalized recommendations in e-commerce. Without clear use cases, AI initiatives risk becoming expensive experiments with no clear ROI.

* **Communication Barriers**: There is often a disconnect between data scientists' technical knowledge and business leaders' strategic priorities. This misalignment can lead to underutilized AI projects or overpromised solutions that fail to meet expectations. Bridging this gap requires ongoing dialogue to ensure that AI projects align with business goals and address real-world challenges effectively.

* **The Role of Translational Roles**: Bridging the gap between technical teams and business units is essential. Roles like data translators or analytics leads can help set realistic expectations, articulate business needs to technical teams, and ensure that AI initiatives are developed with a clear understanding of their intended outcomes. These roles are vital in translating business problems into technical solutions and vice versa, preventing misalignment from the start.

These issues aren't going to disappear just because we're using LLMs. This is one reason why AI agents are not yet ready to replace coders or developers. As long as project managers and business leaders in 2024 struggle to communicate what they want to build, the most sophisticated AI (yeah, talking about you, Devin and similar coding agents) will still require skilled professionals to bridge these gaps and deliver meaningful, well-aligned solutions.

[^2]: https://www.cursor.com/
[^3]: Mark my words, you are not an "AI" specialist because you know some prompt engineering.
[^4]: Domain X here can be any domain you like; I'm not putting any weight here on whether certain domains can or should be completely automated.
[^5]: See a brief overview [here](https://www.coursera.org/articles/ai-engineer)
[^6]: A small RAG [playbook](https://jxnl.co/writing/2024/08/19/rag-flywheel/)

## Issue #3: The Inconsistent Nature of Data Science Roles Across Companies
> Data Scientist? What do you do? I mean, for real? Can't you help me with this dashboard and a SQL query to get my ad-hoc nonreusable insights that I will probably forget I asked about?
> — **Random Coverker in 2024**
>

{{< figure src="/pic_issue_3.png" alt="#Issue3" title="Fig 3. Unfortunate that you don't have as many arms as responsibilities. Source: Author." style="display: block; margin-left: auto; margin-right: auto; width: 50%; max-width: 50%;" >}}


Data Scientist was once hailed as the sexiest job of the 21st century [^7], but now AI Engineer seems to be taking that spot. However, even before this shift, it was often unclear what a Data Scientist was actually supposed to do. The responsibilities of a Data Scientist can vary widely depending on the company, industry, and even the team they're a part of. This inconsistency has led to confusion for both employers and professionals trying to build their careers.

**Different Interpretations of the Role**:

* **Product Analyst**: In some companies, Data Scientists function mainly as product analysts, focusing on tasks like A/B testing, user behavior analysis, and generating business insights. These roles emphasize statistical analysis and data visualization but might not involve any machine learning or predictive modeling.

* **Data Engineer**: At other companies, the role may lean heavily towards data engineering—building and maintaining data pipelines, integrating various data sources, and ensuring data quality. In these cases, the "Data Scientist" might spend most of their time working on ETL (Extract, Transform, Load) processes, with little opportunity to apply machine learning or advanced analytics.

* **Machine Learning Engineer**: Conversely, some companies expect their Data Scientists to act as ML Engineers, handling the end-to-end lifecycle of machine learning models. This can include everything from data preprocessing to model training, evaluation, deployment, and monitoring. These roles require a mix of software engineering and data science skills, often blending into what many now call "AI Engineering."

**Broadened Skill Requirements**: The role of Data Scientist has continued to evolve, and nowadays, professionals are often expected to have a grasp of:

* **AI Engineering and LLMs**: The rise of generative AI and LLMs (Large Language Models) has added a new layer of complexity. Today's data scientists are increasingly expected to understand how to fine-tune, deploy, and maintain these advanced models, even though their skill sets differ significantly from those of traditional data scientists.

* **Full-Stack Development**: Some companies seek "full-stack Data Scientists" who can build models and develop the front-end or back-end systems that deploy these models. This involves familiarity with programming languages, cloud services, and web frameworks, making it a steep learning curve for those entering the field.

**The Struggle with Undefined Roles**: I've experienced these variations firsthand across different organizations, and it's evident that the expectations for Data Scientists are still unclear. This inconsistency can lead to confusion when applying for jobs, as job titles might not accurately reflect the actual responsibilities. A "Data Scientist" at one company might be doing the work of a data analyst, while at another, they might be developing and deploying machine learning models as an ML Engineer.

**Skill Overload and Burnout**: The broadening of the role can lead to "skill overload," where professionals are expected to be proficient in everything from data cleaning and statistical analysis to model deployment and software development. This can make it challenging for individuals to specialize or find a niche, leading to job dissatisfaction and burnout.

**Shift Towards AI Engineering**: The demand for AI Engineers has been growing, particularly with the increased focus on deploying generative AI models. Companies seek professionals who can bridge the gap between traditional data science and software engineering, integrating AI into scalable, production-ready systems. This shift has caused some companies to redefine the role of Data Scientists or even replace it entirely with AI Engineers with a broader skill set.

**Navigating the Inconsistencies**: For those entering the field, it's crucial to understand these variations and choose a path that aligns with their interests and skills:

* **Seek Clarity During Job Applications**: When applying for roles, ask detailed questions during interviews to understand what the job will entail. Will you build models, analyze data, create pipelines, or deploy machine learning systems? This can help avoid misalignment between your expectations and the reality of the role.

* **Specialization vs. Generalization**: Consider whether you want to be a specialist (e.g., focusing on machine learning or data engineering) or a generalist who can handle multiple aspects of data science projects. Both paths have merits, but understanding your preferences can help guide your career development.

* **Leverage New Opportunities**: The rise of AI Engineering presents new opportunities for those willing to expand their skill sets. Learning about LLMs, cloud services, and deployment frameworks can open doors to exciting roles combining data science and software development.

[^7]: DS was the sexiest job at least [2012](https://hbr.org/2012/10/data-scientist-the-sexiest-job-of-the-21st-century)

## Issue #4: The Data Quality Problem
> Ah, data, my dear friend, foe, and partner. What would I do without you? Use LLMs to generate data, perhaps? But that can be bad, you say?  
> — **Random Data Scientist in 2024**
>

{{< figure src="/pic_issue_4.png" alt="#Issue4" title="Fig 4. Garbage in equals Garbage out. Source: Author." style="display: block; margin-left: auto; margin-right: auto; width: 50%; max-width: 50%;" >}}

Garbage in equals garbage out—let's repeat it: GIGO, GIGO. Data quality is and will remain a critical issue at many companies, even if you use all the cool LLM-based features available today. If there's no data strategy or plan to make data accessible, the quality of the model doesn't matter. From my experience, almost every place I've worked has had issues with data, whether it's about quality, accessibility, or integration.

There's a long-standing belief that a Data Scientist spends **80%** of their time cleaning data and only **20%** on actual analysis and modeling. This idea, popularized through various surveys, still holds some truth, even though things have drastically improved over recent years. For example, a study by CrowdFlower (now Figure Eight) found that data scientists typically spent around **60%** of their time on cleaning and organizing data, which contributed to the often-quoted "80/20" split when considering other data preparation tasks like data collection[[4](https://www.figure-eight.com/data-scientists-spend-most-time-cleaning-data/)][[5](https://www.forbes.com/sites/bernardmarr/2018/01/19/data-preparation-is-still-80-of-the-work-in-data-science-ai/)]. I don't think I have ever put 80% of my time on cleaning data but still, I have had to put a lot of time and effort into doing so.

However, it's still surprising that so many companies don't fully understand their data, where it resides, how it's generated, and its quality. Without a clear data management strategy, even the most advanced machine learning models will struggle to produce reliable, actionable insights. Why not use a data catalog solution you say? Well beats my comprehension.


## Issue #5: The need for deep domain knowledge 
> Aren't you a "scientist"? Shouldn't you know everything by heart, i.e., legal, finance, sourcing, etc.? It can't be that hard. I have worked with this for 10+ years, so I shouldn't have to tell you how the domain works; use ChatGPT. Why should I provide guidance and help you with labeling?
> — **Random Domain Expert 2022-2023**
>

{{< figure src="/pic_issue_5.png" alt="#Issue5" title="Fig 5. Data Scientists also needs to be Domain Scientists. Source: Author." style="display: block; margin-left: auto; margin-right: auto; width: 50%; max-width: 50%;" >}}

There is a massive potential for LLMs and LLM Agents. Who knows—this might be the cusp of achieving AGI (*Artificial General Intelligence*) or even ASI (*Artificial Superintelligence*). But, even with this optimism, I still see LLMs and agents having a hard time in their current form becoming genuine generalist problem solvers. This means that profound domain expertise will continue to be essential in the coming years. 

However, being a data scientist, it's challenging to be a legal or finance expert or possess in-depth knowledge of other adjacent domains. This is where collaboration becomes crucial. Working alongside domain experts will be even more critical, as their insights can guide the proper framing of problems, ensure that data-driven solutions are relevant, and help validate AI model outcomes.

### The Role of Domain Experts in AI Projects
* **Contextual Understanding**: Domain experts provide the context often missing in pure data analysis. For instance, a legal expert can help interpret regulatory data accurately, while a healthcare professional can ensure that AI models for medical diagnostics are clinically sound.

* **Fine-Tuning AI Models**: When building LLMs or other AI solutions, domain knowledge can aid in fine-tuning, ensuring that the models generate outputs that align with industry standards and real-world applications. Without this, even the best models may miss critical nuances.

* **Mitigating Risks and Ensuring Compliance**: In sectors like finance, healthcare, and law, there are strict compliance requirements. Domain experts can help data scientists navigate these regulations, ensuring that AI models are effective and legally compliant.

While LLMs and other AI tools continue to advance, deep domain knowledge remains crucial for success. For Data Scientists, collaboration with domain experts is not just a best practice—it's a necessity. The synergy between technical skills and domain expertise will drive innovative, effective, and responsible AI as we push toward more sophisticated AI solutions.

## Issue #6: DataOps, MLOps, AIOps, LLMOps, or Just DevOps?
> "Wait, so you're telling me I need to understand how data pipelines work, manage model deployment, optimize LLMs, AND maintain cloud infrastructure? I thought I just needed to train a model! Can we call it 'Ops' and pretend I know what I'm doing?" — **Random Data Scientist in 2024**
>

{{< figure src="/pic_issue_6.png" alt="#Issue6" title="Fig 6. Why not keep it simple and call it Ops? Source: Author." style="display: block; margin-left: auto; margin-right: auto; width: 50%; max-width: 50%;" >}}

I'm a big advocate of end-to-end (E2E) ML systems, and you can find more of my thoughts on this topic in my previous writings [[9](https://dswithmac.com/posts/testing-ml/)]. In these systems, the AI or ML component is often a small but critical part of a larger ecosystem that requires testing, monitoring, tracing, and other operational practices. This still holds for LLM-based systems, giving rise to the now-growing field of LLMOps. 

However, it can be rather discombobulating for practitioners to differentiate between MLOps, DataOps, AIOps, and LLMOps. Aren't these just variations of DevOps? In my experience, what you call it matters less than understanding the need to operationalize these stochastic systems effectively. It's crucial to focus on managing these systems in production, as it will always differ from experimentation or development (DEV) environments.

### Breaking Down the Terminology: What's the Difference?
* **DataOps**: Primarily focused on managing data pipelines and workflows. DataOps ensures that data is accessible, reliable, and clean, enabling smooth data ingestion, transformation, and integration. Effective DataOps practices are critical because consistent, high-quality data is the foundation for all AI models.
  
* **MLOps**: A blend of DevOps and machine learning, MLOps focuses on automating and streamlining the deployment, monitoring, and management of machine learning models. This includes version control, CI/CD pipelines, model monitoring, and scaling infrastructure. MLOps emphasizes reproducibility, scalability, and reliability, ensuring that models can be iteratively improved and seamlessly integrated into production systems.
  
* **AIOps**: Combines AI with IT operations to automate performance monitoring, anomaly detection, and alert management tasks. AIOps systems use machine learning to process large amounts of IT data and identify issues before they become critical, helping improve system reliability and reduce downtime. It's often seen as a way to use AI to monitor and maintain IT infrastructure efficiently.
  
* **LLMOps**: An emerging field specifically focused on operationalizing Large Language Models. It involves all the principles of MLOps but adds layers unique to LLMs, such as fine-tuning, prompt optimization, and managing model hallucinations. Since LLMs can be resource-intensive, LLMOps emphasizes infrastructure optimization, cost management, and real-time deployment challenges.

### Why These 'Ops' Matter for AI Success
* **End-to-End Integration**: Regardless of the terminology, the key is to think beyond just model development. This means seamlessly integrating your data pipelines, model training processes, deployment strategies, and post-deployment monitoring. Whether it's DataOps for managing data workflows, MLOps for machine learning lifecycle management, or LLMOps for overseeing large language models, the goal remains the same: reliable and scalable operations.

* **Monitoring and Maintenance**: AI models, especially those involving LLMs, are inherently stochastic and can behave unpredictably in production environments. Continuous monitoring and maintenance are essential to catch performance drifts, unexpected behavior, or data quality issues. This includes setting up alerts, tracing problems back to their source, and having protocols to handle model updates or rollbacks. For example, a model trained on static data may begin to underperform as new patterns emerge in live data, requiring retraining or fine-tuning.

* **Version Control and Experimentation Tracking**: An essential part of operationalizing ML systems is maintaining version control for models, datasets, and code. Experimentation tracking allows practitioners to compare different model versions, making reverting to previous iterations easier if new deployments fail. This practice ensures consistency and traceability across the AI lifecycle, which is especially important in regulated industries like finance or healthcare.
  
* **DevOps Practices Applied to AI**: At its core, MLOps, DataOps, and LLMOps are extensions of DevOps principles. They adopt the best practices of DevOps—such as Continuous Integration/Continuous Deployment (CI/CD), automated testing, and infrastructure as code (IaC)—and apply them to AI workflows. The main difference lies in the need to handle additional layers of complexity, such as data preprocessing, model training, and model performance monitoring. For instance, deploying a traditional software application might not require constant retraining, whereas AI models often do.

### Key Challenges in Operationalizing AI Systems
* **Data Drift and Concept Drift**: One of the most significant issues for production AI systems is data drift—when the data entering the model in production changes over time, leading to performance degradation. Detecting and managing this is a core aspect of MLOps and LLMOps, requiring automated monitoring systems and mechanisms to trigger retraining when necessary.
  
* **Infrastructure Scaling**: As models, especially LLMs, can be computationally expensive, scaling infrastructure becomes challenging. Companies must ensure their infrastructure can handle peak loads without incurring unsustainable costs. Solutions like autoscaling, serverless architectures, and distributed computing are often integrated to manage this effectively.
  
* **Cost Management**: The computational cost can be significant, particularly with LLMs. Practitioners must know how to optimize models, compress them, or implement cost-effective solutions such as on-demand cloud services to manage expenses without compromising performance.

While the terminology may vary, the principles remain consistent: AI systems require robust operational frameworks to function effectively in production. Whether it's called MLOps, DataOps, AIOps, or LLMOps, what matters is adopting a holistic approach to ensure these systems are scalable, reliable, and adaptable. After all, production environments are always different from development, and planning for those differences separates successful deployments from failed experiments.

## Issue #7: The Impact of Rapid Technological Change
> "Wait, so the new library/model or LLM isn't compatible with our current stack, but is it faster and cheaper? It can reason, you say... Awesome. I'll just figure out how to make it fit, like a square peg in a round hole." - **Problem-Solving EM, 2024**
>

{{< figure src="/pic_issue_7_v2.png" alt="#Issue7" title="Fig 7. Too many languages, frameworks and models to keep track off. Source: Author." style="display: block; margin-left: auto; margin-right: auto; width: 50%; max-width: 50%;" >}}

If you have chosen the path of a Data Scientist, you're likely someone who enjoys learning and experimenting with new technology. However, compared to a few years ago, the pace of change in this field has accelerated drastically. We see new research papers released almost daily and new libraries that promise to do things better than before. Emerging programming languages have also entered the mix—should you stick with `Python`, or explore newer ones like `Rust,` `TypeScript,` or even `Zig`? Regarding databases, should you continue using `Postgres` with `pgvector` enabled, or should you switch to a newer vector database like `Qdrant`?

The choices don't stop there. Should you buy or build? Fine-tune or prompt-engineer, especially as LLM capabilities continue to improve? What tasks are still considered core to Data Science? Sure, evaluation (evals) is essential, but how engaging is it to write evals all day? And with the rise of techniques like using LLMs as evaluators, is there even a need for traditional approaches anymore?

My point is that **technology**—and **Data Science** with it—continues to change rapidly. And we as practitioners need to stay ahead of the curve and adopt a continuous learning mind set. If you caught the recent announcements from Anthropic, demonstrating <cite>Claude taking over your computer [^8]</cite>, it raises an even bigger question: *do we still need programmers*, or will AI soon take over these tasks? We'll likely need to be present and involved, but filtering out what's genuinely relevant from the constant stream of new developments is becoming increasingly challenging.

### Key Challenges and Considerations
* **Overwhelming Choice of Tools and Technologies**: With the rapid release of new programming languages, frameworks, and libraries, Data Scientists face the daunting task of deciding which tools to invest their time. Should you learn Rust for performance benefits or stick to Python, which remains the industry standard for data science? Every new tool claims to be better, but not all are worth the investment.
  
* **Fragmentation and Integration**: The sheer number of tools can lead to fragmentation, where teams might struggle to integrate different systems. A new vector database might be faster, but if it doesn't play well with existing data pipelines, it can lead to more issues than it solves.
  
* **Evolving Skillsets**: The skillset required for Data Scientists continues to evolve. It's no longer just about building models; understanding how to fine-tune LLMs, manage data infrastructure, and even prompt engineering has become part of the job. This broadening of roles can lead to skill overload, where it's difficult to specialize in any area.
  
* **Balancing Innovation and Practicality**: The fast pace of change means that businesses often feel pressured to adopt the latest technologies, even if they don't fully understand their benefits. This can lead to premature adoption of tools that might not be the best fit, resulting in wasted resources and time. Finding the balance between staying innovative and sticking with practical, proven solutions is critical.
  
* **Filtering Noise from Genuine Innovation**: With the constant stream of new research, it's hard to distinguish what is genuinely innovative from what is just noise. Not every new paper or tool will be groundbreaking, and data professionals must develop a critical eye for what will benefit their work versus what is a distraction.
  
* **The Future of Programming Roles**: Technologies like Anthropic's Claude, which demonstrate AI taking over complex tasks like operating a computer, raise questions about the future of programming and data science roles. Will the role of a Data Scientist evolve into something entirely different, where human input is more about guiding and supervising AI systems rather than building them?

The rapid pace of technological change presents both opportunities and challenges. While it drives the field of Data Science forward, it also demands constant learning, adaptation, and discernment. Success will depend on navigating this evolving landscape, balancing innovation with practicality, and staying focused on core skills while remaining open to new possibilities.

[^8]: Claude computer use: [Anthropic News](https://www.anthropic.com/news/3-5-models-and-computer-use)

## Closing remarks

As the field of data science continues to grow and evolve, so do the challenges that come with it. The introduction of GenAI, Large Language Models, and the increasing demand for AI-driven solutions have brought new opportunities and heightened expectations. **Companies want to leverage AI to gain a competitive edge, but many still need the foundational strategies and support systems to make that a reality**.

For data scientists, ML Engineers, and recently AI Engineers, this means adapting to an ever-shifting landscape where skills once considered niche, such as understanding system architecture or working with domain experts, have become essential. **The days of focusing purely on building models are over** and have been over for some time. Success now requires a combination of technical prowess, strategic thinking, and adaptability.

However, the journey has its pitfalls. The hype around AI has created a perception that it's easier than ever to implement sophisticated solutions, leading to a rise in **"overnight experts"** and an over-reliance on plug-and-play tools. Navigating these waters means finding the right balance between innovation and practicality—knowing when to embrace the latest technologies and when to rely on tried-and-tested methods.

As AI continues to develop, so will the need for **robust DataOps, MLOps, and LLMOps frameworks** that ensure these systems are scalable, secure, and reliable. At the same time, the pace of technological change means data scientists must constantly learn and adapt, discerning genuine advancements from the noise.

In the end, being a **"good" data scientist in today's world** requires more than technical skill—it requires an understanding of the business landscape, a willingness to collaborate with diverse teams, and, above all, a drive to keep learning. Despite the challenges, those who can adapt and evolve with the field will find themselves at the forefront of an exciting and dynamic profession.

The future of data science is bright—just as soon as we figure out what the job entails, now and in the future. One day, you're cleaning data; the next, you're explaining to your boss why their AI chatbot can't "just read minds." But if you love learning new frameworks, battling tech buzzwords, and trying to convince everyone that data privacy is non-essential, congrats—you've chosen the right field. 

So grab your favorite Python package, keep an eye on the latest LLM breakthrough, and remember: **A great data scientist doesn't just solve problems—they convince everyone that they never created them in the first place**.


## References
1. Elwin, M. (2024). V-shaped Data Scientist in the Era of Generative AI. Medium. Available at: https://medium.com/gopenai/v-shaped-data-scientist-in-the-era-of-generative-ai-b29f1bca93b7
2. Analytics Vidhya. (2020). 5 Key Reasons Why Data Scientists Are Quitting their Jobs. Retrieved from: https://www.analyticsvidhya.com/blog/2019/12/5-key-reasons-data-scientists-quit-jobs/
3. Omdena. (2023). Top 3 Reasons Why Data Scientists Are Leaving Their Jobs. Retrieved from: https://www.omdena.com/blog/why-data-scientists-leave-their-jobs
4. CrowdFlower. (2016). Data Scientists Still Spend Most of Their Time Cleaning Data. Retrieved from: https://www.figure-eight.com/data-scientists-spend-most-time-cleaning-data/
5. Forbes. (2018). Data Preparation Is Still 80% of the Work in Data Science. Retrieved from: https://www.forbes.com/sites/bernardmarr/2018/01/19/data-preparation-is-still-80-of-the-work-in-data-science-ai/
6. JXNL. (2024). Scaling Retrieval-Augmented Generation (RAG) Solutions. Retrieved from: https://jxnl.co/writing/2024/08/19/rag-flywheel/
7. Harvard Business Review. (2012). Data Scientist: The Sexiest Job of the 21st Century. Retrieved from: https://hbr.org/2012/10/data-scientist-the-sexiest-job-of-the-21st-century
8. Coursera. (2023). Becoming an AI Engineer: What You Need to Know. Retrieved from: https://www.coursera.org/articles/ai-engineer
9. DS with MAC. (2023). Testing of ML Systems: A Practical Guide. Retrieved from: https://dswithmac.com/posts/testing-ml/
10. Anthropic. (2024). Claude and the Future of AI in Computing. Retrieved from: https://www.anthropic.com/news/3-5-models-and-computer-use