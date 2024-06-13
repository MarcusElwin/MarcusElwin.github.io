---
title: Running your Data Products Team as a F1 team
seo_title: Running Data your Data Products Team as a F1 team
summary: In formula 1 and for data product teams, the sum is greater than its parts.
description: 
slug: running-data-f1
author: Marcus Elwin

draft: false
date: 2023-09-01T21:58:08+02:00
lastmod: 2023-09-03T21:58:08+02:00
expiryDate: 
publishDate: 

feature_image:
feature_image_alt: 

categories:
    - Data Product Management
tags:
    - Data Products
    - Team Dynamics
series:

toc: true
related: true
social_share: true
newsletter: false
disable_comments: false

---

**Formula 1: Where Speed Meets Tech and Charisma** :racing_car:

[FIA Formula 1](https://www.formula1.com/) is an electrifying blend of fast cars, cutting-edge tech, and charismatic personalities. It's not unlike the dynamic atmosphere of a tech startup or scale-up.

Many, myself included, became avid F1 fans after watching ['Formula 1: Drive to Survive'](https://www.netflix.com/se-en/title/80204890) on Netflix.

In the midst of the 2023 season, [10](https://www.formula1.com/en/teams.html) teams compete, with *Redbull Racing* leading the *constructors* championship :crown:. They owe much of their success to superstar [Max Verstappen](https://sv.wikipedia.org/wiki/Max_Verstappen), but is it all due to him?

In this blog post, we delve into F1 and data product teams, uncovering intriguing parallels. Our goal: extract valuable insights for data product teams from the high-speed world of Formula 1.

Get ready for a thrilling ride!


## How is a F1 team organized?  

### Typical roles in a F1 team

| Role           | Role Description                           | # People |
| -------------- | ------------------------------------------ | -------- |
| Team Principal | The team's top decision-maker and leader.  | 1        |
| F1 Drivers     | Elite drivers who race for the team.       | 2        |
| Assistants     | Support staff for various team functions.  | 4-12     |
| Managers       | Oversee team operations and strategies.    | 10-20    |
| Engineers      | Design and optimize the race car.          | 51-211+  |
| Designers      | Create car designs and aerodynamics.       | 44-120   |
| Mechanics      | Maintain and service the race car.         | 20+      |
| Production     | Produce car components and equipment.      | 8-90     |
| Other          | Diverse roles such as PR, marketing, etc.  | 20-90    |


See the table above for the **9** most common roles in a Formula 1 team and depending on the size of the team normally <cite>~**170-600**[^1]<cite> people are involved in the daily operations of the team. 

#### Overview of what each person is in charge of:

* **Team Principal**: The directors of the team, some may come from car manufacturers or other are from private companies e.g. the team owners.

* **F1 Drivers**: The stars of the team driving the F1 cars. Normally there are 2 main drivers,  1 reserve driver and 1 simulation driver. The two main drivers tend to be bitter foes.

* **Assistants**: They are in charge of helping and organizing events, calendars and procedures.

* **Managers**: In charge of different groups and areas, leading teams, supervising and guiding.

* **Engineers**: Many different rules such as *race engineers*, *aerodynamics engineers* and *R&D engineers*. They make shit work. 

* **Designers**: Handle everything covering the design of the cars.

* **Mechanics**: What we normally see during the races, they change and repair components when the F1 drivers fucks up.

* **Production**: Responsible for producing and developing car parts.

* **Other**: Chefs, personal trainers,  web and media relations etc.

{{< notice note >}} 
More and more teams also employs data competencies such as *Data Scientist*, *Data Engineers*, *Analytics Engineers* to make the teams more successful in wind tunnel similations for aerodynamics, making sense of waste amounts of IoT data and even improving the teams strategies.
{{< /notice >}}

### Activities during a "normal" race week

{{<mermaid>}}
timeline
    title Formula 1 "Typical" Race Week
    Day 1 - 4
        : Travel
        : Logistics
        : Setup
        : Teardown plan
    Day 5 
        : Practice 1
        : Practice 2
    Day 6
        : Practice 3
        : Pre-Qualifying Show
        : Qualifying
        : Post Qualifying Show
    Day 7 
        : Race 
        : Post-Race Show
        : Pack-up
        : Race debrief
{{</mermaid>}}

The timeline above illustrates how a "regular" race week looks like for a Formula 1 team.

#### Day 1-4: Race Preparation

- Teams travel to the new race location, transporting and setting up cars, pits, and more.
- Thursday morning is dedicated to strategizing the teardown plan for Sunday.

#### Day 5: Race Practice

- Friday's race practice includes two sessions to collect live data, fine-tune simulations, and test new parts.
- Drivers familiarize themselves with the track, and engineers adjust cars based on data and feedback.
- In-depth tire compound degradation analysis is conducted.

#### Day 6: Race Qualifying

- Saturdays feature final practice (if not a sprint weekend) and qualifying sessions.
- Teams compete for grid positions, and cars enter parc fermé, limiting adjustments.
- Post-qualifying, the strategy team has precise data for simulations.
- Pre and post-shows add excitement.

#### Day 7: Race & Pack-Up

- Sunday is race day :racing_car::
- Teams work on cars for 5 hours before the formation lap.
- The race begins, and teams vie for points.
- Post-race, teams start pack-up following the Thursday plan.
- A debrief session helps iron out issues for the next race.

## How is a Data Products Team (DPT) organized?

### Digression Data Products?
To understand what a *data products* team is doing, it might be helpful to discuss what a *data product* is. We will not detail to any larger extent what a data product is in this article, but perhaps in future articles. 

However, as any sane person would do I did ask for help from *chatGPT*:

{{< notice note >}} 
A **data product** is essentially a product that derives its value primarily from data. Unlike traditional products or even most software products, data products are all about using data to provide *insights*, *solve problems*, or make *predictions*. They're like the intersection of technology and data science. 
{{< /notice >}}

Or in even more simple terms:

{{< notice note >}} 
A **data product** is something like your weather app that uses data to provide you with valuable information or services, and it's different from regular, physical products or services because it relies on data to function and deliver value.
{{< /notice >}}

### Typical roles in a Data Products Team

| Role                               | Role Description                                      | # People |
| ---------------------------------- | ----------------------------------------------------- | -------- |
| Area Leads / Engineering Directors | Oversee and guide technical domains and strategies.   | 1-4    |
| Engineering Managers               | Manage and support engineering teams effectively.     | 1-2      |
| Product Managers                   | Define product vision and guide development efforts.  | 1-3      |
| Data Scientists                    | Utilize data for insights and machine learning.       | 3-5      |
| Backend / Frontend Engineers       | Develop backend and frontend components of the product. | 5-10    |
| Designers                          | Create user-centric design for product interfaces.    | 1-2      |
| Other                              | Diverse roles such as QA, DevOps, etc.                | 5-10     |

**NB**: the roles and number of peoples above are in my experience more common in more *product* oriented companies, whilst at other companies some of these roles may have different names, or be more centralized.

#### Overview of what each person is in charge of:

* **Area Leads / Engineering Directors**: These folks are the true visionaries of the team, setting the high-level agenda based on the company's grand objectives. Depending on the company's mood, they might share the limelight with the CTO or VP of Engineering / Product.

* **Engineering Managers**: Ah, the coaches, the mentors, the team's cheerleaders, if you will. They're all about optimizing the execution of things and have a bizarre fascination with reducing the infamous "technical debt." Some more Data Science-focused companies might even sport a peculiar variant known as the "Data Science Manager."

* **Product Managers**: The gatekeepers of vision and roadmap. They hold no formal power but are expected to herd cats (read: teams and people) to get things done. Getting folks aligned and doing what they want? Just another day in the sweet spot.

* **Data Scientists**: The wizards, the data wranglers, the folks who make magic happen with data. They casually throw around terms like ML, LLMs, and AI, but deploying? Well, that's not always their cup of tea. Many of them prefer cozying up to Jupyter notebooks. Some companies even call them "AI Engineers," "ML Engineers," or the trendy "Generative AI Engineers." And hey, have you heard of the mystical "[Decision Scientist](https://chds.hsph.harvard.edu/approaches/what-is-decision-science/)"? No one's quite sure what makes them different from regular Data Scientists, but it's a mystery we're not solving today.

* **Backend / Frontend Engineers**: These are the swiss knives of engineering, skilled in crafting backend or frontend systems, APIs, and sculpting infrastructure with terraform. Oh, and they're best buds with the Engineering Managers because they share a common love for reducing "technical debt." If you're lucky, you might spot a rare species known as "full-stack" engineers. They're not exactly wizards, but they're more like those handy Swiss Army knives.

* **Designers**: The true artists of the digital realm, they're all about Figma and crafting user journeys. Sometimes, they're the mysterious outsiders, dwelling beyond the borders of the product team. Whatever you do, don't let them leave – you'd be lost without them.

* **Other**: These are the unsung heroes, often students in desperate need of cash :moneybag:. But also QA, Delivery, Marketing etc. Some companies go all out and hire data annotation firms, known for their *interesting* [practices](https://www.context.news/ai/ai-boom-is-dream-and-nightmare-for-workers-in-global-south).

### Activities during a "normal" business week

{{<mermaid>}}
timeline
    title Data Product Team "Typical" Week
    Day 1
        : Weekly team meeting
        : Feature Work
    Day 2
        : Standup/Checkin
        : Feature Work
    Day 3
        : Standup/Checkin
        : Feature Work
    Day 4
        : Standup/Checkin
        : Team Retro
        : Feature Work
    Day 5 
        : Standup/Checkin 
        : Demos
        : Grooming / Planning
{{</mermaid>}}

The timeline above illustrates a "regular" week a typical "product" team using some agile framework such as *kanban* or <cite>*scrum*[^2]<cite>, working in weekly sprints in my experience. 

#### Day 1: Weekly Preparations

- Teams kick off the week with a review meeting, setting priorities, and potentially launching new initiatives. Some companies rely on Directly Responsible Individuals ([DRIs](https://about.gitlab.com/handbook/people-group/directly-responsible-individuals/)) to lead initiatives, while others delegate to Product Managers or Engineering Managers.
- Feature work resumes, gaining momentum.

#### Day 2-4: Feature Work

- Teams focus on feature development, diving into initiatives with cross-functional collaboration.
- Daily standups or check-ins track progress and address blockers.
- Team retrospectives provide opportunities to evaluate work methods and discuss topics on a weekly or bi-weekly basis.

#### Day 5: Demos & Planning

- Feature work wraps up, with some brave souls merging changes into production on Fridays. Others take a more relaxed approach. :beer:
- Demo sessions are held, either internally or company-wide.
- Grooming and planning for the upcoming week ensure a smooth transition.



## What are some similarities between F1 and DPT?
Now that we know how both types of teams work, let's look at some simularities:

| **Similarities**                            | **Formula 1 Team**                                        | **Data Product Team**                                       |
|--------------------------------------------|-----------------------------------------------------------|--------------------------------------------------------------|
| 1. **Team Collaboration**                  | Diverse specialists collaborating effectively.            | Cross-functional teams working in harmony.                   |
| 2. **Data-Driven Decision-Making**         | Heavy reliance on data for optimization and strategy.    | Data informs product development and decision-making.        |
| 3. **Iterative Development**               | Constantly evolving car designs throughout the season.   | Regular product updates and enhancements based on feedback.  |
| 4. **Performance Optimization**            | Focus on maximizing car performance on the track.        | Optimization for efficient, scalable, and user-friendly products.|
| 5. **Risk Management**                    | Managing and mitigating race-day risks.                  | Robust risk management for data security and reliability.    |
| 6. **Real-Time Decision-Making**          | Swift, real-time decisions during races.                 | Agile adaptation to changing user needs and market conditions.|
| 7. **Continuous Learning**                | Learning and adjusting strategies from race to race.     | Continual improvement based on user feedback and data analysis.|
| 8. **Technology Integration**             | Embracing cutting-edge automotive innovations.           | Leveraging advanced technologies like ML and AI.            |
| 9. **Competitive Landscape**              | Competition against rival teams.                         | Competing in crowded markets, differentiating products.     |
| 10. **User Experience**                   | Prioritizing the driver's experience in the car.         | User-centered design for intuitive and engaging products.   |
| 11. **Strategic Planning**                | Developing race strategies aligned with goals.           | Creating product roadmaps aligned with business objectives. |
| 12. **Resource Management**               | Efficient management of budgets and personnel.           | Allocating resources effectively for product development.  |


## Learnings from F1 that can be applied to DPT?
When looking at how a F1 team is operating, there are mainly 3 key areas where a data product team can draw inspiration and learnings from:
* *Strategies for High-Performance Product Development*
* *Data-Driven Insights and User-Centricity*
* *Post-Launch Evaluation*

### Strategies for High-Performance Product Development

1. **Simulated Testing**: F1 teams extensively use simulations for various aspects. Data Product teams can benefit from more simulated testing alongside A/B or bandit testing.

2. **Real-Time Decision-Making Under Pressure**: F1 teams make quick decisions under race-day pressure. Data Product Teams face similar challenges, like deciding to implement chatGPT in response to a competitor.

3. **Pit-Stop Mentality (Rapid Change Execution)**: In F1, pit stops take less than <cite>3 seconds<cite>[^3], emphasizing rapid execution. Data Product teams might not have such urgency, but they can practice rapid execution through continuous planning.


4) **Precision and Attention to Detail**: A F1 team pay meticulous attention to detail in product development, as very small changes can mean winning or losing a race. Similar can be said about a Data Product Team, where your clients will notice if you pay attention to details and their needs.

### Data-Driven Insights and User-Centricity

1. **Driver Feedback (User Feedback)**: Data Product Teams collect user feedback through interviews or surveys. In F1, drivers are crucial customers, <cite>product "experts"<cite>[^4], and <cite>"evangelists"<cite>[^5]. They have daily access to drivers, frequently incorporating their input into the "product." The cadence of this information sets F1 apart. In short, treat your customers like F1 drivers for your product.

2. **Telemetry (User Analytics)**: F1 teams, like data product teams, monitor and gather real-time data on their cars, using a plethora of sensors for comprehensive insights. This informs their strategies and complements driver feedback. Data Product Teams excel in this area but can learn to measure even more user behavior.

### Post-Launch Evaluation

1. **Post-Race Analysis (Post-Launch Evaluation)**: After each race, F1 teams conduct post-race analyses to find improvements and insights for the next race. This is a weekly practice for them. Data Product Teams might do something similar after retrospectives or the completion of significant initiatives. The difference is F1's consistent weekly process, which Data Product Teams can learn from. In short, consider post-evaluation after each release if possible.

[^1]: Based on estimates [here](https://onestopracing.com/how-do-f1-teams-work/) note that this may vary in each team.
[^2]: Or a mix of both scrum and kanban knowns as *scrumban*, or plain good ol *waterfall* methodologies, read more [here](https://asana.com/resources/scrumban).
[^3]: This of course depends on the circuit, see more [here](https://en.wikipedia.org/wiki/Pit_stop#:~:text=A%20pit%20stop%20typically%20takes,stops%2C%20depending%20on%20the%20circuit.)
[^4]: The F1 drivers has an extraordinary feel for the car, what setup they should have and shouldn't have.
[^5]: If the F1 driver feels comfortable with the car i.e. product, they will perform if not they will let you know that you suck.
