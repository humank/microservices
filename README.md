# Migration from Monolith to MicroServices via DDD approach readiness
Please fill-up the following questionnaire, it's mandatory to have essential understanding to go to next stage.

* How many standalone or monolithic service(s) are going to be re-architectured?

> You need to confirm how many systems there to re-architecture, try to list or draw a diagram to demonstrate what’s the core capability these monolith provide, and why you need to break it out. In my opinion there should contain these 3 aspect of viewpoints but not only.


Here is an example to explain why to do it.

|System Name	|Business Capability	|Force	|	|
|---	|---	|---	|---	|
|City Weather information System	|Collect and persist daily weather information. Calculate history data and provide open data usage. Integrate with several government system to build up data exchange lifecycle	|The legacy monolith runs for more than 20 years, without clear understanding. The source code size is too huge, download, dev and test take too much time to wait, programmers waste time on waiting. Would like to build team in small size, per team owns a specific business context, and split it out from the monolith.	|	|
|Online EC shopping	|Contains several classic online shopping functions, and always be challenged at hot event days	|Embrace the event day, dealing with high concurrent access on specific business, such as DM presenting, shopping cart putting items, or payment gateway transactions.	|	|
|Nitch economic marketing	|provide quick change funcitions to support A/B testing marketing needs	|Way to embrace rapidly change, per function is designed in seperately	|	|


* How many domain experts will join the re-architecture journey? Per-monolith per(or)multiple experts?

> Regarding domain experts, there shouldn’t be only BA(Business analyst), SA(System analyst), or Customer but also the whole services’ stakeholders, such as operation engineer, developer, CxO, marketing, BD(Business Development), Sales ...etc 



> The first step to step in breaking the monolith is to collaborate team’s knowledge, you may leverage a centralized wiki to use the “Ubiquitous Language”, traditionally we use it in OOAD like “Glossary”.


Here is an example : 

|	|	|	|	|
|---	|---	|---	|---	|
|	|	|	|	|
|	|	|	|	|
|	|	|	|	|
|	|	|	|	|
|	|	|	|	|

* Is there an architectural diagram of these legacy systems?
* What's the communication protocol among the current system architecture? (ex: DB-Link, File, API, Client SDK…etc )
* Which approach is preferred to do the re-architecutre? Big Bang or Iterative & Incremental, Why?
* Before the re-architecture process, how do you ensure the re-architectured function well as usual? Any approach or mechanism to protect? 
* Can you figure out the severity level when services down? ( 5 to 1, 5 is the most serious) Can you explain what's the impact?
* Can you figure out the services operation SLA on different architecture style, such as request/response, fire and forget (a.k.a Asynchronized interaction)… etc.
* Behind the distributed Microservices architecture, there will be data aggregation issue. Is there any real-time inquiry use case that need to aggregate raw data among multiple microservices?
* How do you collect domain knowledge? If by document(s), how to make these document(s) "Be Live"?
* How do you from up the dev team? Per domain a team (a.k.a Function team within Bounded Context) or any other approach? 
* What's the max number of team members?
* Will each team have rights to make decision(s) on technology adoption? 
* Any specific non-functional requirements should be addressed in the new microservices architecture?
* When will you launch the re-architecture project?




