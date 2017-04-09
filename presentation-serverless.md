# Presentation Serverless Framework

### Title

Going Serverless: **Code Without Infrastructure**

### Summary

Write and deploy code without worrying about compilation, networks, infrastructure and servers. Is it too good to be true? In this talk we'll examine serverless architecture (especially on AWS) and why there's so much hype about it at the moment.

### Outline

Intro

- About me
- PageUp is hiring

What is serverless

- Stateless compute containers
- IAAS -> PAAS -> FAAS (Functions as a service)

Hosting options

Start talking through the hosting models? On site pets, cloud pets, cloud cattle, docker, now serverless. 

Why serverless

* No pet servers (less maintenance)
* No images to maintain
* Microservices! SoA
* Isolated deployments
* Pay per invocation vs. pay to have server always running

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
* Connection pooling

What we learnt

* Load testing
* Use Dynamo only for key / value store, don't query
* Come up with a usage model / pattern
* Don't introduce caching until needed
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

Serverless architecture is all the rage in the development community at the moment, for developers it means is that we get to write modules or functions, zip them up and upload them to a cloud provider to run on some configured events. Serverless architecture can be described as code that is run in stateless compute containers that are event-triggered, ephemeral (may only last for one invocation), and fully managed by a 3rd party. That sounds like a bit of a mouthful so let's unpack that a bit. 

Stateless compute containers - Virtual machines are an example of a stateful compute container, they manipulate data and save it back into the virtual machine image. On the other hand docker containers are an example of stateless compute containers, once you create the container and the code it will run, it should never be modified. If it needs access to state it reaches out to another service like a mapped host share, database or cache.

Event-triggered means an event needs to trigger the code to execute, as opposed to an application where code is constantly running and checking for input. Examples of an event may include an API call, a file being saved or a message being placed on a queue.

Ephemeral means that the code is executed once for this event then shut down. This is a significant difference to traditional execution models where an application or a website is maintained in a long running application. Windows IIS websites are run in a thread called an application pool, these application pools are costly to start up, often taking minutes so most application pools will run for an extended period of time like hours or days. All the time that it's running you will be paying running costs for it, Serverless services can significantly save costs by only running when needed.

And fully managed by a 3rd party means we don't need to worry about maintaining hardware or operating systems. No security updates to install or environments to configure, you just write the code and deploy it. For this reason serverless architectures are sometimes know as Functions-as-a-service.



So why is serverless so exciting? Well the golden ticket for most companies is time to market. The sooner you can bring an idea to your customers as a real product the sooner you can start marking money, and you gain a significant competitive advantage by being the first to market. Serverless is about reducing the effort (and usually cost) required to develop software. By managing hardware and operating systems at scale, Cloud providers can often provide much cheaper operations and infrastructure than doing it in house, as a software developer your expertise is in writing code, and serverless frees you up from worrying about how it's run. 

Servers that are carefully managed and continuously upgraded are known as pet servers. Pet servers require significant attention and effort to ensure they're constantly performing correctly, and if things go wrong they require a lot of effort to replace. In contrast cattle servers are servers that are spun up as needed and then destroyed, they require less maintenance and if something is going wrong with the server, you kill it and start another one. 

Teams are getting leaner and organisations are understanding the value of focusing on doing what you do best and outsourcing the rest. The rise of Cloud computing has meant this is affordable for everyone. Before virtualisation and Cloud technologies, servers were carefully managed and upgraded, teams were dedicated to the correct configuration and running of the infrastructure to host applications and replacing them was costly. We call those pet servers, they take a lot of maintenance and we care for them over their long lifetime. Then virtualisation came about, companies like Amazon's AWS offered Infrastructure as a Service (IaaS) - no more physical servers to buy and manage, you just install your virtual machines on their bare metal. Rather than managing pet servers, you could define a server image then spin up an instance of that server and kill it as needed. This meant that scaling an application could become much more affordable. Rather than buying and maintaining 10 expensive machines to handle the peak load times, you could run just one virtual server then start more up as needed and shut them down when load decreases. 

But maintaining the server images still requires ongoing time and effort. Someone needs to be monitoring security patches for the operating system and required stack in the image and recreating the image as necessary. Microsoft's Azure Cloud offering focuses on Platform as a Service (PaaS) to abstract away the operating system and hosting stack. You provide them with a compiled .NET application and they manage running it and scaling it. This is very similar to Serverless, except that with PaaS it's expected that your code will be constantly running like a traditional web server application. Serverless is sometimes known as Functions as a Service (FaaS). When you deploy code to a Serverless architecture it doesn't need to know whether it's a web service or any other type of application. It's just a function that you configure to run when certain events occur, and once that thread is finished your code stops executing, you now only need to pay per invocation rather than for a server to be constantly running.

Other benefits to using Serverless are that each function is independently deployable, meaning we can make small isolated changes to one part of the system and deploy them, this becomes increasingly important when you have a team of people working on different areas of the system. Rather than needing to coordinate a deployment of multiple different changes to multiple areas of the system and testing them in collaboration, we just deploy the part we need.

Serverless architecture is helping the rapid delivery of microservices. These are small, isolated but compossible services that perform help enable the rapid delivery of features while improving maintainability of the system as a whole.



AWS's Lambda functions are by far the most recognised Serverless offering, but there are other competitors in the market, including [Google Cloud Functions](https://cloud.google.com/functions/), [Microsoft Azure Functions](https://azure.microsoft.com/en-us/services/functions/), [IBM OpenWhisk](https://developer.ibm.com/openwhisk/) with an [open source implementation](https://github.com/openwhisk/openwhisk?cm_mc_uid=14550632011514612454806&cm_mc_sid_50200000=1466841331), [Iron.io](http://iron.io/), and [Webtask](https://webtask.io/).

Serverless requires an event to trigger the execution and scaling of your functions, for AWS there are many events that can be configured, including API Gateway

S3

- Kinesis
- SNS
- DynamoDB
- CloudWatch and more...



For years developers have been relegated to a thin slice of the development lifecycle. Business Analysts wrote requirements, Project Managers coordinated the tasks and process, Testers checked the quality of the solution, Operations managed the deployment and hosting and the Support team triaged the issues coming in. But times have changed and business have realised the value in having a team of Developers who are cross-functionally skilled and able to take on many tasks. At PageUp where we I work our development teams consist of 4-8 developers and a product owner, that's about it. Within the team we collaborate on the upcoming roadmap of work, the requirements and UX if necessary, the architecture and solution design for each project and the process to deliver it. We do all our own testing and when we build new microservices it's up to us to design the infrastructure necessary to host it and to deploy it, manage the uptime of it and fix any bugs. By placing this responsibility on the development team we are able to think through the entire project when working at each stage, e.g. we consider development and maintenance when designing requirements and we think about monitoring and support when developing, there's no throwing over the fence at any stage, we own all of the solution so we better get it right. It's a good way to work. But it does mean we get stretched pretty thin. We all come from a technical development background, but we're broadening our skills into requirements gathering, agile iteration mastery, as well as infrastructure and network support. So when technologies like Serverless come along, we see huge value in them. 

Serverless is simply about running code without having to worry about what it's running on or where it's running. It's the dream of being able to write code and deploy it without having to get the infrastructure team involved. 

Serverless doesn't actually mean there are no servers.

