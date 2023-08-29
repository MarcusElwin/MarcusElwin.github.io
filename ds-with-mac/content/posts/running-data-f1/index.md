---
title: Running your Data Products Team as a F1 team
seo_title: Running Data your Data Products Team as a F1 team
summary: In formula 1 and for data product teams, the sum is not greater than its parts.
description: 
slug: running-data-f1
author: Marcus Elwin

draft: false
date: 2023-08-24T21:58:08+02:00
lastmod: 
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
[FIA Formula 1](https://www.formula1.com/) is the ultimate combination of <cite>fast cars [^1]</cite>, the latest techology and eccentric drivers and team principals. Not to far off from the "normal" business environment :sweat_smile: at a tech startup or scale-up. Me like many other people where probably not big F1 fans until we saw [Formula 1 Drive To Survie](https://www.netflix.com/se-en/title/80204890) on Netflix a couple of years back. 

As of now in the middle of the 2023 session, there are [10](https://www.formula1.com/en/teams.html) Formula 1 teams competing with *Redbull Racing* leading the *constructors* championship followed by *Mercedes* and *Aston Martion* on second and third position. Red-bull is clearly enjoying the :crown: with their super star [Max Verstapen](https://sv.wikipedia.org/wiki/Max_Verstappen). But is all credit due to him, for their great success in the 2023 session?

In this blog post we will dig in to the inner workings of a F1 team, data products team and what similarities there are, to finally conclude on some learnings data product teams can take from F1.

## How is a F1 team organized?  

### Typical roles in a F1 team

| Role   | Role Description     | # People   |
| --------  | -------- | ------ |
| Team Principal | __TODO__ | 1 |
| F1 Drivers | __TODO__ | 2 |
| Assistants | __TODO__ | 4-12 |
| Managers | __TODO__ | 10-20 |
| Engineers | __TODO__ | 51-211+|
| Designers | __TODO__ | 44-120|
| Mechanics | __TODO__ | 20+|
| Production | __TODO__ | 8-90|
| Other | __TODO__ | 20-90|

The table above shows a rough grouping of different **9** common roles in a Formula 1 team. Depending on the size of the team normally ~**170-600** people are involved in operating a Formula 1 team. Below follows an overview of what each person is in charge of:

* *Team Principal*: The directors of the team, some may come from car manufactors or other are from private companies from e.g. the team owners.

* *F1 Drivers*: The stars of the team driving the F1 cars. Normally there is 2 main drivers,  1 reserve driver and 1 simulation driver. The two main drivers tend to be bitter foes.

* *Assistants*: They are in charge of helping and organzing events, calendars and procedures.

* *Managers*: In charge of different groups and areas, leading teams, supervising and guiding.

* *Engineers*: Many different rules such as *race engineers*, *aerodynamics engineers* and *R&D engineers*. They make shit work. 

* *Designers*: Handle everything covering the design of the cars.

* *Mechanics*: What we normally see during the races, they change and repair components when the F1 drivers fucks up.

* *Production*: Responsible for producing and developing car parts.

* *Other*: Chefs, personal trainers,  web and media relations etc.

{{< notice note >}} 
More and more teams also employs data competencies such as *Data Scientist*, *Data Engineers*, *Analytics Engineers* to make the teams more successful in wind tunnel similations for aerodynamics, making sense of waste amounts of IoT data and even improving the team strategies.
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

#### Day 1-4 Race preparations
During the 4 days before the race weekend the teams normally:
* Travel from the previous race location to the next
* Transport and ship cars, pits, motorhomes and garages
* Setup these on the new race location
* Use Thursday morning to setup their teardown plan for Sunday.

#### Day 5 Race Practice
On Friday's race practice starts where team:
* Collect live-data during 2 practice sessions, to adapt computer simulations and improve race strategies
* Testing new parts that have been proven in e.g. wind tunnels or simulations
* Drivers learning the track and together with data and feedback from drivers engineers adjust the cars in terms of balance and drivability
* Degradation analysis of different [tyre compounds](https://www.formula1.com/en/latest/article.the-beginners-guide-to-formula-1-tyres.61SvF0Kfg29UR2SPhakDqd.html) is also performed.

#### Day 6 Race Qualifying
During Saturdays the following events take place:
* Final practice if it is not [sprint-week](https://www.formula1.com/en/latest/article.explained-everything-you-need-to-know-about-the-2023-f1-sprint-format.583WHWKbWVVBemPKi6pJxH.html), where the team makes final adjustment and decides on their *qualifying strategy.*
* During qualifying session the teams compete for starting positions on the grid for race day, during qualifying the cars enters *parc ferme* until the start of the race, meaning that the team have limited ability to do changes to the car. 
* After qualifying session, strategy team have much more *accurate* data to run simulations on for race day. 
* There are also pre & post-shows during this day.

#### Day 7 Race & Pack-up
Finally Sunday arrives which is race day:
* Teams are allowed to touch their cars for up to 5 hours before the formation lap of the race
* Formation lap starts, and drivers often try to get there tyres up to temperature
* Race starts and all teams try to win as many points as possible
* Before the race is finished the teams beginning the *pack-up* according to the plan from Thursday
* Immediately after race each team has a *debrief* session to spot any issues for the next race

## How is a Data Products Team (DPT) organized?

### Digression Data Products?
To understand what a *data products* team is doing, it might be helpful to discuss what a *data product* is. We will not detail to any larger extent what a data product is in this article, but perhaps in future articles. However, as any sane person would do I did ask for help from *chatGPT*:

{{< notice note >}} 
A data product is essentially a product that derives its value primarily from data. Unlike traditional products or even most software products, data products are all about using data to provide insights, solve problems, or make predictions. They're like the intersection of technology and data science. So, in simple terms, a data product is something like your weather app that uses data to provide you with valuable information or services, and it's different from regular, physical products or services because it relies on data to function and deliver value.
{{< /notice >}}

### Typical roles in a Data Products Team

| Role   | Role Description     | # People   |
| --------  | -------- | ------ |
| Area Leads / Engineering Directors | __TODO__ | 1 - 4 |
| Engineering Managers | __TODO__ | 1-2 |
| Product Managers | __TODO__ | 1-3 |
| Data Scientists | __TODO__ | 3-5 |
| Backend / Frontend Engineers | __TODO__ | 5-10|
| Designers | __TODO__ | 1-2|
| Other | __TODO__ | 5-10|

* *Area Leads / Engineering Directors*: The directors of the team setting the high level vision and agenda based on the company objectives. Depending on company CTO might take some of these roles as well or VP of Engineering.

* *Engineering Managers*: Responsible for coaching, mentoring and developing the team and improving the *execution* of things. Often fascinated with reducing **"technical debt"**. Some more Data Science focused companies might have a variant called *Data Science Manager*.

* *Product Managers*: Responsible for the vision and roadmap for what to build in the team. Often teams gateway to clients. They are in the sweat spoot of having no *formal power*, but need to get people and other teams aligned and do what they want.

* *Data Scientists*: Data wizards, Data Wranglers that make magic happen with data. *ML*, *LLMs* & *AI* are buzzwords they use. Often in charge of building algorithms and or product logic, but not always deploying (many favor *jupyter notebooks*) them depending on the company. Also some companies might call them *AI Engineers*, *ML Engineer* or even *Generative AI Engineer* these days. You might also have seen [Decision Scientist](https://chds.hsph.harvard.edu/approaches/what-is-decision-science/) pop up in some companies. What they do differently from Data Scientist is still an unsolved mystery.

* *Backend / Frontend Engineers*: Engineers skilled in building backend or frontend systems, APIs, infrastructure via terraform and reducing **technical debt** (which is why they get along with the EM). If you are fortunate you may have some *full-stack* engineers in your team that can do both. Not like wizards, bit more like swizz knives.

* *Designers*: People skilled in figma and designing flows and user journeys. Often these tend to be outside of the product team, so if you have one don't let them leave.

* *Other*: Usually people labelling data, most often students needing money :moneybag:. Some companies also employ data annotation firms, with [questionable](https://www.context.news/ai/ai-boom-is-dream-and-nightmare-for-workers-in-global-south) practices.

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

The timeline above illustrates a "regular" week a typical "product" using some agile framework such as *kanban* or *scrum* team, working in weekly sprints in my experience. 

#### Day 1 Weekly preparations
Depending on what team you work in Mondays are usually used for:
* Weekly team meeting to sync on any spillover from last week, focus for team this week, and potentially startup of any new initatives. Some companies might use [DRIs](https://about.gitlab.com/handbook/people-group/directly-responsible-individuals/) to lead an inititive, often an engineer in the team. Whilst at other companies this responsibility might be more on the PM and or EM.
* Feature work is typically picked up again.

#### Day 2-4 Feature Work
During these days most of the focus is mainly on feature work:
* Feature work in 1 or more initatives, where data product teams tend to be cross-functional
* Daily standups or checkins to check progress and any blockers on deliveries
* Team retros to evaluate way of working or other topics that can be weekly or bi-weekly. Also good time for team to evaluate and complain.

#### Day 5 Demos & planning
Finally race day :car:...or demo day:
* Wrap of of feature work before end of week, brave souls merge to production on Fridays others relax :beer:
* Usually some demo session is hold, internal in the team or across the company
* Grooming and planning for next week is also typically done.

## What are some similarities between F1 and DPT?
So now that we know how a Formula 1 team and Data Product Team works, let's look at some simularities:

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
Below follows a table with some key-learnings a Data Product Team can draw from Formula 1:

| **Learnings for Data Product Teams**                        | **Derived from Formula 1 Teams**                     |
|------------------------------------------------------------|------------------------------------------------------|
| 1. **Continuous Improvement**                               | Embrace incremental improvements and feedback loops. |
| 2. **Data-Driven Decision-Making**                          | Prioritize data analytics for informed decisions.    |
| 3. **Cross-Functional Collaboration**                       | Leverage diverse skills within the team effectively. |
| 4. **Iterative Development**                                | Follow iterative development cycles for agility.     |
| 5. **Performance Optimization**                             | Optimize product performance and efficiency.         |
| 6. **Risk Management**                                     | Develop robust risk management strategies.           |
| 7. **Real-Time Adaptation**                                | Be agile and adaptable to changing circumstances.    |
| 8. **User-Centered Design**                                | Focus on creating products that solve user problems. |
| 9. **Strategic Planning**                                  | Develop clear product roadmaps aligned with goals.   |
| 10. **Resource Efficiency**                                | Allocate resources efficiently for product success.  |
| 11. **Competitive Positioning**                            | Continuously assess the competitive landscape.       |
| 12. **Focus on Performance and Value Delivery**             | Prioritize delivering high-performance products.     |



[^1]: Depending on track and circuit the drivers can reach up to 345km/h or 214mph, see more [here](https://www.autosport.com/f1/news/how-fast-is-an-f1-car-top-speeds-of-f1-indycar-motogp-and-more-4980734/4980734/)

