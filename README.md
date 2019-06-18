# Migration from Monolith to MicroServices via DDD approach readiness

Please fill-up the following questionnaire, it's mandatory to have essential understanding to go to next stage.

* How many standalone or monolithic service(s) are going to be re-architectured?

> You need to confirm how many systems there to re-architecture, try to list or draw a diagram to demonstrate what’s the core capability these monolith provide, and why you need to break it out. In my opinion there should contain these 3 aspect of viewpoints but not only.


Here is an example to explain why to do it.

|System Name	|Business Capability	|Force	|
|---	|---	|---	|
|City Weather information System	|Collect and persist daily weather information. Calculate history data and provide open data usage. Integrate with several government system to build up data exchange lifecycle	|The legacy monolith runs for more than 20 years, without clear understanding. The source code size is too huge, download, dev and test take too much time to wait, programmers waste time on waiting. Would like to build team in small size, per team owns a specific business context, and split it out from the monolith.	|
|Online EC shopping	|Contains several classic online shopping functions, and always be challenged at hot event days	|Embrace the event day, dealing with high concurrent access on specific business, such as DM presenting, shopping cart putting items, or payment gateway transactions.	|
|Nitch economic marketing	|provide quick change funcitions to support A/B testing marketing needs	|Way to embrace rapidly change, per function is designed in seperately	|

* How many domain experts will join the re-architecture journey? Per-monolith per(or)multiple experts?

> Regarding domain experts, there shouldn’t be only BA(Business analyst), SA(System analyst), or Customer but also the whole services’ stakeholders, such as operation engineer, developer, CxO, marketing, BD(Business Development), Sales ...etc 



> The first step to step in breaking the monolith is to collaborate team’s knowledge, you may leverage a centralized wiki to use the “Ubiquitous Language”, traditionally we use it in OOAD like “Glossary”.


Here is an example : 

|Ubiquitous Language in specific context	|Term in English 	|Term in Mandarin	|Term in any other local language	|
|---	|---	|---	|---	|
|Payment	|Payment	|付款	|	|
|Member	|Member	|會員	|	|

* Is there an architectural diagram of these legacy systems?

> In order to have a concrete understanding about the monolith, recommend to prepare the following diagrams. it’s not must to have but recommend to do.



|Diagram type	|Usage	|Example	|
|---	|---	|---	|
|Deployment Diagram	|To have an overview to know whole system, recommend to provide 2-level of depth on this. First level focus on physical deployment, so server farm, networking devices, RDBMS, others are essential components, besides to address what's the communication protocol, port between each connected components. The second-level we may focus on "Deployed Artifact", such as Java war/jar file, or other platform artifacts ( *.zip, *.dll). **This the only way to know what the "composite status in one physical machine or vm".**	|http://www.agilemodeling.com/artifacts/deploymentDiagram.htm	|
|Package Diagram	|This is an engineering level topic, to well protect the newly designed service project stack, to understand what's the dependency relationship with legacy monolith. Such as Java project, we often use Maven or Gradle to deal with project/module dependencies.	|http://agilemodeling.com/artifacts/packageDiagram.htm	|
|Use case Diagram	|Well, it should be rarely exist there,and most of these diagram are out of date, you can just ignore it	|http://www.agilemodeling.com/artifacts/useCaseDiagram.htm	|
|ICONIX Robustness Diagram	|To have a quick look to know what's the business flow go through by boundary, controller, and entities	|http://agilemodeling.com/artifacts/robustnessDiagram.htm	|
|Collaboration Diagram	|**UML collaboration**/communication **diagrams** like**UML** sequence **diagrams**, are used to explore the dynamic nature of your software. **Collaboration diagrams** show the message flow between objects in an OO application, and also imply the basic associations (relationships) between classes.	|http://agilemodeling.com/style/collaborationDiagram.htm	|

* What's the communication protocol among the current system architecture? (ex: DB-Link, File, API, Client SDK…etc )
* Which approach is preferred to do the re-architecutre? Big Bang or Iterative & Incremental, Why?
* Before the re-architecture process, how do you ensure the re-architectured function well as usual? Any approach or mechanism to protect? 
* Can you figure out the severity level when services down? ( 5 to 1, 5 is the most serious) Can you explain what's the impact?
* Can you figure out the services operation SLA on different architecture style, such as request/response, fire and forget (a.k.a asynchronized interaction)… etc.
* Behind the distributed Microservices architecture, there will be data aggregation issue. Is there any real-time inquiry use case that need to aggregate raw data among multiple microservices?
* How do you collect domain knowledge? If by document(s), how to make these document(s) "Be Live"?
* How do you from up the dev team? Per domain a team (a.k.a Function team within Bounded Context) or any other approach? 
* What's the max number of team members?
* Will each team have rights to make decision(s) on technology adoption? 
* Any specific non-functional requirements should be addressed in the new microservices architecture?
* When will you launch the re-architecture project?

