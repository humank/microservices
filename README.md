# Migration from Monolith to MicroServices readiness

Please fill-up the following questionnaire, it's mandatory to have essential understanding to go to next stage.

### How many standalone or monolithic service(s) are going to be re-architectured?

> You need to confirm how many systems there to re-architecture, try to list or draw a diagram to demonstrate what’s the core capability these monolith provide, and why you need to break it out. In my opinion there should contain these 3 aspect of viewpoints but not only.


Here is an example to explain why to do it.

|System Name	|Business Capability	|Force	|
|---	|---	|---	|
|City Weather information System	|Collect and persist daily weather information. Calculate history data and provide open data usage. Integrate with several government system to build up data exchange lifecycle	|The legacy monolith runs for more than 20 years, without clear understanding. The source code size is too huge, download, dev and test take too much time to wait, programmers waste time on waiting. Would like to build team in small size, per team owns a specific business context, and split it out from the monolith.	|
|Online EC shopping	|Contains several classic online shopping functions, and always be challenged at hot event days	|Embrace the event day, dealing with high concurrent access on specific business, such as DM presenting, shopping cart putting items, or payment gateway transactions.	|
|Nitch economic marketing	|provide quick change funcitions to support A/B testing marketing needs	|Way to embrace rapidly change, per function is designed in seperately	|

### How many domain experts will join the re-architecture journey? Per-monolith per(or)multiple experts?

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

### What's the communication protocol among the current system architecture? (ex: DB-Link, File, API, Client SDK…etc )

> Point out all the communication protocol(s), no matter it is DB-Link, File, API over HTTP SOAP 1.x or higher, over HTTP by JSON request/response format, Client SDK, RMI/IIOP... etc.

> You may found one tricky fact, that most of  the communication protocol are specific-vendor technical injection. Recommend to re-consider to “Communicate by contract”, it’s a good way to escape from legacy technical debt. If there are still need to collaborate with others which couldn’t be changed now, try to translate it at “ API Gateway”. Amazon API gateway is a good fit to help on this issue. https://aws.amazon.com/api-gateway/

> So, the new communication protocol will be guide to use a classic HTTP/HTTPS protocol with readable request/response body, which release team’s innovation ability, choose appropriate technology to implement without legacy lock.

### Which approach is preferred to do the re-architecutre? Big Bang or Iterative & Incremental, Why?

![Way to divide monolith](https://martinfowler.com/bliki/images/microservice-verdict/path.png)
Recommend to divide monolith in I&I  (Iterative & Incremental), because of we may lack of whole business understanding, keep it in baby step, re-programming with test protection. You may always be challenged this approach could take several year(s) to fully transform monolith into microservices, it doesn’t matter.


> We develop microservices for business fulfillment, for stable supporting business, not for credits, or acting histories on resume. Without robust functionality, microservices are just a technical stack without meaning.


When you have several team(s) to breakout monolith into microservices at the same time, ensure to clarify the business context via stakeholders and domain experts confirmation. There is an fluent way to discover business flow by critical business event pipeline, so called **Event Storming workshop.**

Event Storming, is founded by Alberto Brandolini a couple years ago, take a look on this. 
https://www.youtube.com/watch?v=NGXl1D-KwRI 

If you want to know a sample to run EventStorming and implement on AWS platform, here you go : 
https://github.com/humank/EventStormingWorkShop 

### Before the re-architecture process, how do you ensure the re-architectured function well as usual? Any approach or mechanism to protect? 

![Software Testing Pyramid](http://thelatestsoftwaretestingnews.co.uk/wp-content/uploads/2018/07/Screen-Shot-2018-07-04-at-10.35.26.png)

It all about test. Traditionally modifying any legacy function without protection of test, just like 

> Walk a tightrope.


We know it’s an ideal assumption that all the systems were developed with tests to prove functions run as business expectation, but in fact, it is rare. While you attempt to break out monolith, if there is no such resources for you to write more unit tests to cover the protection, at least you need to have automation UI test for stable delivering.

Most benefits from Unit tests (70%), and then Integration test(20%), UI test (10%)... 
Encourage to do Unit test when re-develop specific functions, encourage do it with Test Driven Design(TDD).

### Can you figure out the severity level when services down? ( 5 to 1, 5 is the most serious) Can you explain what's the impact?


Example : 

|
Disaster severity	|
Subsystem	|
Failure Impact	|
|---	|---	|---	|
|
★★★★★	|Account	|Customer will no longer to do transaction.  Operator couldn't retrieve accounting reports.  Agent couldn't register any new comer account	|
|
★★★★★	|User Service	|Customer & Operator can't login platform to perform any action	|

Besides , you can also have a Two-Dimension table to show up the co-relationships between each service

|Service Name	|A	|B	|C	|D	|E	|
|---	|---	|---	|---	|---	|---	|
|A	|	|V	|V	|	|	|
|B	|V	|	|V	|V	|	|
|C	|V	|V	|	|	|	|
|D	|	|V	|	|	|	|
|E	|	|	|	|	|	|

By doing this, you know the **“hub & spoke” co-relationship. It’s useful to control the dependencies propagating, and way to design an Open-host-service pattern. The Open-host-service pattern comes from Domain Driven Design, it is used to when you want to open your system for integration • Protocol that gives access to your system as a set of services • Open for everyone that needs to integrate with your system • New services can be added on request but need to serve a “general” purpose.**

You can always find out the top 3 or 5 services take most important roles, and knowing there should be some fluent way to have a resiliency design.

How to design service with resilience non-functional attribute? 

> recommend to watch this video : @https://youtu.be/gET51_C3k5s


Patterns for Resilient Architecture Design , by Adrian Hornsby @AWS
https://medium.com/@adhorn/patterns-for-resilient-architecture-part-1-d3b60cd8d2b6 
https://medium.com/@adhorn/patterns-for-resilient-architecture-part-2-9b51a7e2f10f
https://medium.com/@adhorn/patterns-for-resilient-architecture-part-3-16e8601c488e
https://medium.com/@adhorn/patterns-for-resilient-architecture-part-4-85afa66d6341


### Can you figure out the services operation SLA on different architecture style, such as request/response, fire and forget (a.k.a asynchronized interaction)… etc.

When breaking out monolith to microservices, all the traffics are remote invoked, it’s good to know the business functions expectation to design the process with appropriate tech stack adopt in.


* request/response in 2 seconds or less than
* Service healthy thresholding mechanism
* Async call, consuming rate, when should all the pending request to be solved, if no, how to response the consequence
* Dead letter Queue design-  https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-dead-letter-queues.html

### Behind the distributed Microservices architecture, there will be data aggregation issue. Is there any real-time inquiry use case that need to aggregate raw data among multiple microservices?

***Frankly speaking, if there will be one or more real-time inquiry use case(s) which need to aggregate raws data among multiple microservices, I’d like to recommend to merge these use cases in a new one “Microservice”, it’s high cohesion.***

If the inquiry result could be in Eventually consistency, you could leverage CQRS pattern  with raw data aggregation design, or event driven pipeline fork mechanism to deal with raw data from different context.


> refer to : Implementing Event-Driven architectures with AWS Event Fork Pipelines - https://aws.amazon.com/blogs/compute/enriching-event-driven-architectures-with-aws-event-fork-pipelines/



### How do you collect domain knowledge? If by document(s), how to make these document(s) "Be Live"?

***Traditionally we leave the document(s) in powerpoint, wiki, word, excel, or any other format but not in “Source Code”.***
However, by doing this way, the systems will challenge the maturity of Document management. documents are always out-of-sync with source code. The requirement document(s) couldn’t reflect the business intent, either well guide developer to develop program. ***A living document is “the One”, which is desired by the development team.***

A living document for team, which stands for “reflect the requirement in time, sync up with source code”. It’s great to adopt “Behavior-Driven-Design” to collaborate domain experts with developer team. Let’s say using Ubiquitous Language in gherkin style statement ( Given/When/Then), mitigate the gap between non-technical team and developer team.


> For more BDD introduction? take a look :  https://cucumber.io/docs

> 10 minutes to know BDD : https://cucumber.io/docs/guides/10-minute-tutorial/

### How do you from up the dev team? Per domain a team (a.k.a Function team within Bounded Context) or any other approach? 

Recommend to form up team by function not by component. Each team owns a service with clear bounded context. In AWS we called this as 2-Pizza team, all the functions in bounded context could be served by team members. If can’t, try to have a virtual function team to deliver the service(s).

### What's the max number of team members?

2 pizza team size, not too much people, usually it’s a 5 -7 ppl team.

### Will each team have rights to make decision(s) on technology adoption? 

Exactly, encourage each team takes most appropriate technology to solve business problem.
For data persistence? There is not only one RDBMS solution, you can have multiple choice, let’s say DB freedom.
For programming platform ? ***There will be no centralized tech stack to obey, just pick what you need if the communication protocol is based on “Contract, not technology.”***

### Any specific non-functional requirements should be addressed in the new microservices architecture?

I think this is not only for microservices, but all the service design worth to do. Figure out it and help to make technology stack adoption decision, always need to consider trade-off between tech and business.

### When will you launch the re-architecture project?

Please try to have your own answers regarding the questionnaire as below, get “consensus” not “compromise” from team, stakeholders, and get support from higher decision maker. Never do this migration without support.
