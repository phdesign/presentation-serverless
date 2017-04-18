# Presentation Serverless Framework

### Title

Going Serverless: **Code Without Infrastructure**

### Summary

Write and deploy code without worrying about compilation, networks, infrastructure and servers. Is it too good to be true? In this talk we'll examine serverless architecture (especially on AWS) and why there's so much hype about it at the moment.

### Outline

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



## Demo

Walk through creating an S3 based lambda using the AWS console.

Walk through creating an api based lambda using serverless framework

## v2

Serverless architecture is all the rage in the development community at the moment, and for good reason. Serverless offers benefits for everyone from self funded startups to global corporates. In this session we're going to take a look at what serverless is, the benefits of using serverless over traditional long running applications, the serverless ecosystem including hosting providers, we'll take a bit more of a deep dive in AWS's serverless Lambdas, we're even going to try writing a lambda and deploying it to see just how easy they are to create, and then we'll close out with some discussion on the challenges of using serverless.

But first, a little about me. I'm a Technical Lead at PageUp, where we build SaaS solutions for HR, including recruitment, performance reviews and professional development / learning. At PageUp we're breaking apart our monolithic .NET app into microservices to enable us scale faster and deliver innovative new solutions quickly. A recent project my team worked on involved adding access restrictions to our training library so that clients could customise which of their employees could see specific learning activities. We built this using AWS serverless technologies which helped us deliver it faster and independently from the monolith app, meaning our team wasn't constrained by the monthly release cycle, in fact we were deploying to production multiple times per day.

### 1. What is serverless

So what is Serverless? The term serverless can be used in reference to the Serverless Framework, which is a toolset for managing AWS lambda function, we'll look at that framework later but for now I'll be using the term to describe the more general Serverless computing or Serverless architecture.

Serverless has been described as "[Code that] is run in stateless compute containers that are event-triggered, ephemeral (may only last for one invocation), and fully managed by a 3rd party." More simply put, Serverless describes functions or modules that are run on demand.

Stateless compute containers mean that a serverless function or module is not allowed to maintain state between invocations, this means that serverless code needs to be either pure functions, ~~which is a function that has no side effects and whose return value is always the same given the same input,~~ or it needs to store state in a separate system like a distributed cache or database. 

Event triggered means that serverless functions respond to an external configured event, rather than continuously running and checking for input. Later on we'll cover some of the types of events that can typically be configured.

Ephemeral means that the code is executed once for this event then shut down. This is a significant difference to traditional execution models where an application or a website is maintained in a long running application. .NET IIS websites are run in a thread called an application pool, these application pools are costly to start up, usually taking minutes so most application pools will run for an extended period of time like hours or days. Serverless functions are designed to start as quickly as possible, execute the code and shutdown.

And fully managed by a 3rd party means we don't need to worry about maintaining hardware or operating systems. No security updates to install or environments to configure, you just write the code and deploy it. Managing the operating environment and scaling of servers is completely managed for you.

As a point of clarification, I've mentioned serverless functions a few times now, but to be clear, serverless code can be a single function or a collection of modules and functions like any application. Typically we try to keep the size of our serverless code as small as possible, following a single responsibility principle.

Also, serverless is a very misleading term. There are of course servers running the code, it's just that the servers and scaling is fully managed for you.

### 2. Why Serverless?

By only executing as needed to respond to an event, serverless code can be very cheap to run. This is extremely beneficial for new startups or companies trying innovative products where they need to be able to fail fast, but also be setup to succeed if the product is successful. For an idea of cost, AWS bills by request, by how long your code runs for and by how much memory it's allocated. There's a perpetual free tier of 1 million requests and 400,000 GB-seconds per month. So, as an example, for 3 million requests to an AWS serverless function, that runs for 1 sec and uses 512MB of memory, it would cost approximately $18.34 per month.

Another big benefit of serverless is that scaling is completely managed for you. Unlike virtual machines or docker containers where you would specify a minimum number of instances to be running, a maximum amount of instances, and a trigger to determine when to start new instances, the provider handles all of this for you. 

Other benefits to using Serverless are that each function is independently deployable, meaning we can make small isolated changes to one part of the system and deploy them. This becomes increasingly important when you have teams of developers working on different areas of the system. Rather than needing to coordinate a deployment of multiple different changes to multiple areas of the system and testing them in collaboration, we just deploy the part we need.

Serverless computing can significantly increase a companies time to market, which can give you a big competitive advantage. Often being the first to market with a new offering means you can dominate the market, and the sooner you put your software into customers hands the sooner you can start realising profit from it. 

To understand why serverless computing is such a revolution, it's useful to review how it's come about with a quick history of Cloud computing. 

### 3. Serverless Ecosystem

There are a number of serverless providers available at the moment, with varying levels of maturity. Probably the two best known offerings are AWS's Lambdas and Microsoft Azure Functions. But Google and IBM are also playing the field. 

AWS supports JavaScript via Node.js, Python, Java and C#. Microsoft Azure Functions support JavaScript, C#, F#, Python, PHP, Bash, Batch and PowerShell scripts, while Google Cloud Functions only currently support JavaScript. 

All of them have very similar offerings, but we're going to focus a bit more on AWS which my team have been developing with recently.

AWS Lambda's can be configured to respond to any of the following events, and the list is continuously growing. API Gateway, S3, Kinesis, SNS, DynamoDB, CloudWatch and more…

We'll look at a couple of use cases for these events. Firstly, using API Gateway we can build a RESTful API to respond to web requests without needing a web server. 

// TODO: Serverless use cases

// TODO: Serverless Framework

### 4. Serverless challenges

There's a lot of benefits to going Serverless, and there are companies building entire product backends with serverless and managed offerings, but let's take a look at a few challenges when using serverless. Serverless offerings have only been around for the last 3 years or so, so while they're gaining a lot of traction, the technology is still very new and developers are still exploring the right, and wrong usages of it and the tooling around them is still developing. The Serverless Framework is still only beta, as is Google Cloud Computing.

An important point to be aware of is that serverless functions are usually time limited. For AWS Lambdas they are usually limited to run for up to 5 minutes, this means they're not suitable for long running tasks. But they can be used effectively to break down long running tasks into many smaller tasks and place them on a queue to processed but subsequent functions. It's also worth noting that there is a Concurrent Execution Limit for AWS Lambdas, by default this is a maximum of 600 concurrent Lambdas executing in any one region.

Startup time can be a problem for some serverless functions. As there really are servers and provisioning happening under the hood it makes sense for the providers to stop processes that aren't being used, so when you hit a serverless function for the first time it can be a bit slow to respond, anywhere from a few hundred milliseconds for node or python to potentially a few seconds for java. Once warm though, subsequent hits will be faster. For AWS the instance is usually shutdown after about 5 minutes of inactivity. It's worth noting this for serverless functions used in blocking UI calls as every millisecond can count when the user is waiting.

Authentication isn't a challenge, in fact it's pretty well supported on AWS, it's just something to be aware of. Generally your serverless functions can be blissfully unaware of authentication, it is usually handled further up the stack and the relevant information like user id passed down. For example, API Gateway can manage authentication, either to a managed service or to a lambda that does the custom authentication check, this authentication approval can then be cached for performance, we can assume that if the user passes the same token for the next 5 minutes that they are still authenticated. 

Many people see a code editor in a cloud console and object to serverless functions as it circumvents all the good practices we've learnt from decades of coding, like source control, unit testing and continuous integration. But improved tooling is making it easier to bring all those good practices to serverless functions. While you can edit your serverless code directly in the browser, it's much better to manage it as a project folder on your local system where you can use your favourite source control, then use tools like Serverless Framework to manage the deployment and even local testing of the functions. For our project we managed to replicate an entire local development environment, so we could test our serverless APIs running on a local machine, we also had a fully automated test suite that ran over the code, and finally we had an automated continuous integration and delivery environment where once we committed and pushed a change to either the code or the configuration, our test suite would build on Travis and deploy immediately. For API driven serverless functions this works pretty seamlessly. The challenges increase when you're trying to locally replicate other event triggers like file stream processing.

Statelessness is often seen as a good thing, for a long time developers relied on things like session or application state to maintain state across multiple web requests. This would help, for example, if you had a multi page signup form. You didn't want to commit the partially complete form to the database yet because the user might cancel, but you need to remember what they entered on the previous screens. Nowadays we have richer JavaScript front ends or mobile apps that can manage collecting pages of information before sending it off to the server, so a lot of state is unnecessary, but by habit we still rely on it. Have stateless requests can be a mind shift for some, but ultimately it results in better applications that are easier to manage. 

## v1







Servers that are carefully managed and continuously upgraded are known as pet servers. Pet servers require significant attention and effort to ensure they're constantly performing correctly, and if things go wrong they require a lot of effort to replace. In contrast cattle servers are servers that are spun up as needed and then destroyed, they require less maintenance and if something is going wrong with the server, you kill it and start another one. 

Teams are getting leaner and organisations are understanding the value of focusing on doing what you do best and outsourcing the rest. The rise of Cloud computing has meant this is affordable for everyone. Before virtualisation and Cloud technologies, servers were carefully managed and upgraded, teams were dedicated to the correct configuration and running of the infrastructure to host applications and replacing them was costly. We call those pet servers, they take a lot of maintenance and we care for them over their long lifetime. Then virtualisation came about, companies like Amazon's AWS offered Infrastructure as a Service (IaaS) - no more physical servers to buy and manage, you just install your virtual machines on their bare metal. Rather than managing pet servers, you could define a server image then spin up an instance of that server and kill it as needed. This meant that scaling an application could become much more affordable. Rather than buying and maintaining 10 expensive machines to handle the peak load times, you could run just one virtual server then start more up as needed and shut them down when load decreases. 

But maintaining the server images still requires ongoing time and effort. Someone needs to be monitoring security patches for the operating system and required stack in the image and recreating the image as necessary. Microsoft's Azure Cloud offering focuses on Platform as a Service (PaaS) to abstract away the operating system and hosting stack. You provide them with a compiled .NET application and they manage running it and scaling it. This is very similar to Serverless, except that with PaaS it's expected that your code will be constantly running like a traditional web server application. Serverless is sometimes known as Functions as a Service (FaaS). When you deploy code to a Serverless architecture it doesn't need to know whether it's a web service or any other type of application. It's just a function that you configure to run when certain events occur, and once that thread is finished your code stops executing, you now only need to pay per invocation rather than for a server to be constantly running.

Serverless architecture is helping the rapid delivery of microservices. These are small, isolated but compossible services that perform a single operation help enable the rapid delivery of features while improving maintainability of the system as a whole.





Serverless requires an event to trigger the execution and scaling of your functions, for AWS there are many events that can be configured, including API Gateway, which allows you to accept RESTful HTTP requests, trigger a Lambda to run then return the result. This allows us to build fully managed RESTful web services, and by abstracting the API configuration from the running code, we could maintain multiple backwards compatible versions of our API talking to the one codebase. Other event sources include CloudWatch, CodeCommit, DynamoDB, Kinesis, S3 and SNS. Using CloudWatch you can configure code that is run based on metrics or alarms from another system, or a common example is using an S3 event to trigger a function. S3 is a file storage system from AWS, so you could configure that every time an image is saved into a specific location in S3 then a Lambda is triggered that creates multiple thumbnails or resizes of the image and save them away. 



One of the challenges with Lambda is managing the configuration of all the interconnected systems. It's possible to create a lambda and author it through the AWS web console, then create the required API Gateway configuration to trigger the invocation of the lambda, but the configuration can get complex, especially if authentication or caching needs to be involved. This is why serverless toolsets are starting to be developed, the most well known of which is called Serverless Framework. 



For years developers have been relegated to a thin slice of the development lifecycle. Business Analysts wrote requirements, Project Managers coordinated the tasks and process, Testers checked the quality of the solution, Operations managed the deployment and hosting and the Support team triaged the issues coming in. But times have changed and business have realised the value in having a team of Developers who are cross-functionally skilled and able to take on many tasks. At PageUp where we I work our development teams consist of 4-8 developers and a product owner, that's about it. Within the team we collaborate on the upcoming roadmap of work, the requirements and UX if necessary, the architecture and solution design for each project and the process to deliver it. We do all our own testing and when we build new microservices it's up to us to design the infrastructure necessary to host it and to deploy it, manage the uptime of it and fix any bugs. By placing this responsibility on the development team we are able to think through the entire project when working at each stage, e.g. we consider development and maintenance when designing requirements and we think about monitoring and support when developing, there's no throwing over the fence at any stage, we own all of the solution so we better get it right. It's a good way to work. But it does mean we get stretched pretty thin. We all come from a technical development background, but we're broadening our skills into requirements gathering, agile iteration mastery, as well as infrastructure and network support. So when technologies like Serverless come along, we see huge value in them. 



Another concept that complimentary to Serverless is Backend as a Service. The idea being that you build rich mobile or web front ends that compose managed backend services rather than any custom code. E.g. using hosted databases that are accessible by an API, hosted Authentication services and hosted file storage. Serverless functions an compliment this approach but augmenting the hosted services with some custom code only when necessary. For example, you could use save data directly into AWS DynamoDB tables, then have a Lambda function that triggers when data in the database is changed and responds to that event.