# microservices
Before you make a decision to migrate monolith to microservices, there is an essential readiness for microservices pre-work.

## Please fillup the following questionaire, it's mandatory to have essential understanding to go to next stage.

- How many standalone or monolithic service(s) are going to be re-architectured?
- How many domain experts will join the re-architecture journey? Per-monolith per(or)multiple experts?
- Is there an architectural diagram of these legacy systems?
- What's the communication protocol among the current system architecture? (ex: DB-Link, File, API, Client SDK…etc )
- Which approach is preferred to do the re-architecutre? Big Bang or Iterative & Incremental, Why?
- Before the re-architecture process, how do you ensure the re-architectured function well as usual? Any approach or mechanism to protect? 
- Can you figure out the severity level when services down? ( 5 to 1, 5 is the most serious) Can you explain what's the impact?
- Can you figure out the services operation SLA on different architecture style, such as request/response, fire and forget (a.k.a Asynchronized interaction)… etc.
- Behind the distributed Microservices architecture, there will be data aggregation issue. Is there any real-time inquiry use case that need to aggregate raw data among multiple microservices?
- How do you  collect domain knowledge? If by document(s), how to make thess document(s) "Be Live"?
- How do you from up the dev team? Per domain a team (ak.a Function team within Boundex Context) or any other approach? 
- What's the max number of team members?
- Will each team have rights to make decision(s) on technology adoption? 
- Any specific non-functional requirements shoud be addressed in the new microservices architecture?
- When wull you launch the re-architecture project?
