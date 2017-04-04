# Presentation Serverless Framework

### Title

* Going Serverless: **Code Without Infrastructure**
* Build apps without infrastructure
* Adventures into Serverless
* Going Serverless
* Hey you! Drop that server. 
* Code without servers

### Summary

Write and deploy code without worrying about compilation, networks, infrastructure and servers. Is it too good to be true? In this talk we'll examine serverless architecture (especially on AWS) and why there's so much hype about it at the moment.

### Outline

Intro

- About me
- PageUp is hiring

What is serverless

Overview of Serverless technologies

Stateless compute containers

IAAS -> PAAS -> FAAS

Functions as a service

Hosting options

Pay per invocation

Why serverless

* No pet servers
* No images to maintain
* Microservices! SoA
* Isolated deployments

Lamdba needs an event source

* API Gateway
* S3
* Kinesis
* SNS
* DynamoDB
* CloudWatch and more...

Serverless Framework

* API Gateway
* Lambda
* Dynamo

Demo (backup if there's no internet etc…)

Monitoring

Problems you'll face

* Setup local test environment
* Warmup time
* Authentication

SQL Projection

What we learnt

* Load testing
* Use Dynamo only for key / value store, don't query
* Come up with a usage model / pattern
* Don't introduce caching until
* Would use ElasticSearch instead of SQL

https://twitter.com/VilleImmonen/status/722324840435302400

> Serverless architecture is such a silly name. Of course there are servers, just not ones you need to watch and micromanage all the time
>
> \- @VilleImmonen

> [Code that] is run in stateless compute containers that are event-triggered, ephemeral (may only last for one invocation), and fully managed by a 3rd party.
>
> \- Mike Roberts (ThoughtWorks)

> A serverless architecture approach replaces long-running virtual machines with ephemeral compute power that comes into existence on request and disappears immediately after use. 
>
> \- Thoughtworks Tech Radar

## v1

Serverless architecture is all the rage in the development community at the moment, for developers what it means is that we get to write modules or functions, zip them up and upload them to a cloud provider to run on some configured events. Serverless architecture can be described as code that is run in stateless compute containers that are event-triggered, ephemeral (may only last for one invocation), and fully managed by a 3rd party. That sounds like a bit of a mouthful so let's unpack that a bit. 

Stateless compute containers - Virtual machines are an example of a stateful compute container, they manipulate data and save it back into the virtual machine image. On the other hand docker containers are an example of stateless compute containers, once you create the container and the code it will run, it should never be modified. If it needs access to state it reaches out to another service (e.g. mapped host share, database or cache).

Event-triggered means an event needs to trigger the code to execute, as opposed to an application where code is constantly running and checking for input. Examples of an event may include an API call, a file being saved or a message being placed on a queue.

Ephermeral means that the code is executed once for this event then shut down. This is a significant difference to 



Why use Serverless



For years developers have been relegated to a thin slice of the development lifecycle. Business Analysts wrote requirements, Project Managers coordinated the tasks and process, Testers checked the quality of the solution, Operations managed the deployment and hosting and the Support team triaged the issues coming in. But times have changed and business have realised the value in having a team of Developers who are cross-functionally skilled and able to take on many tasks. At PageUp where we I work our development teams consist of 4-8 developers and a product owner, that's about it. Within the team we collaborate on the upcoming roadmap of work, the requirements and UX if necessary, the architecture and solution design for each project and the process to deliver it. We do all our own testing and when we build new microservices it's up to us to design the infrastructure necessary to host it and to deploy it, manage the uptime of it and fix any bugs. By placing this responsibility on the development team we are able to think through the entire project when working at each stage, e.g. we consider development and maintenance when designing requirements and we think about monitoring and support when developing, there's no throwing over the fence at any stage, we own all of the solution so we better get it right. It's a good way to work. But it does mean we get stretched pretty thin. We all come from a technical development background, but we're broadening our skills into requirements gathering, agile iteration mastery, as well as infrastructure and network support. So when technologies like Serverless come along, we see huge value in them. 

Serverless is simply about running code without having to worry about what it's running on or where it's running. It's the dream of being able to write code and deploy it without having to get the infrastructure team involved. 

Serverless doesn't actually mean there are no servers.

Teams are getting leaner and organisations are understanding the value of focusing on doing what you do best and outsourcing the rest. The rise of Cloud computing has meant this is affordable for everyone. AWS initially offered Infrastructure as a Service (IaaS) - no more physical servers to buy and manage, you just install your virtual machines on theirs. Azure focuses on Platform as a Service (PaaS) to abstract away the operating system, you just give us your compile .NET application and we'll run it on a Windows IIS server. Serverless can be seen as Functions as a Service (FaaS) - don't even worry about IIS, apache or the transport layer, just give us some code to run and tell us when to run it. 