Microservices Notes

Microservices vs Monoliths

Monolith is code that exists in one place, on one server, using one host, where it's easy to understand how different parts interact, and everything is in one location and therefore simpler. The benefits are great for small teams and small businesses who don't anticipate much web traffic. However, monoliths are difficult to maintain, and require legacy code maintenance- updating them isn't easy. They also are not scalable, because of how they were planned.

Microservices solve some of the problems Monoliths face- they are services that are small enough that teams of people can work on them, and don't rely much on other services or databases to function, this allows changes to one section to be much easier.
If not implemented correctly however microservices can take the difficult aspects of both Monoliths and services and become incredibly challenging to work with. Proper planning is key.

Challenges of Microservices:
Developer Productivity- how do devs talk to eachother
Complex interactions
Deployment- you will need to automate
Monitoring- need a centralized place to view the logs

E-Commerce - os non-trivial and actively maintained

Architecture of Microservice:
-autonomous, they own their data, independently deployable

Augment a monolith to add the microservice, or decompose a monolith to extract microservices

Mitigate Data Ownership Limitations:
    -define service boundaries well, minimize the need to aggregate data
    -Caching: improved perfomance, improved availability
    -Identify "seams" in database

Microservices can be upgraded without needing the clients to upgrade

Make additive changes- new endpoints, new properties on DTO's

Create automated tests that ensure older clients are supported
Beware of shared code as it results in tight coupling

For Example in ECommerce:
Catalog, Basket, Ordering, Identity, Marketing, Location are all separate microservices that will be kept apart rom eachother.
    We were doing similar stuff for the banking app

Building Microservices:

Run it in variety of environments: locally for devs, staging for testers to try it out in a production-like environment, production to host the app for end users

Hosting options: virtual machines (costly), Platform as a service (serverless), Containers(portabe, run anywhere including locally)

Get used to the idea of testing your code on different OS

Creating a new Microservice:
    create a new source control repository per microservice
    continuous integration build, which runs automated tests

Tests, 3 to know:
    Unit Tests- fast to run, high code coverage
    Service-level tests- test a single serviec in isolation, mock collaborators (harder to write than unit tests)
    End-to-end Tests- shows how the code runs together. Production-like environment, but can be fragile.

Microservice Template: create a template so all the microservices work the same. Standardize these:
    -logging
    -health checks
    -configuration
    -authentication
    -build scripts
All these things increases consistency, reduces time creating microservices. Increased developer productivity
Ability to run the microservice in isolation.

Communication between Microservices:
Can microservies call whatever microservices they want?
    this can result in tangeled dependencies, cascading failures, poor performance

Microservices should publish to an "event bus", then to other microservices
API gateway: a middleman between front end and microservices that routes the communications

microservices subscribe to things on the event bus

Synchronous Communication- when you want a response following a request from a microservice.

RESTful APIs- represent information as "resources"
use standard HTTP methods, like GET POST PUT

Asynchronous Communication:
when a customer submits an order, they can get a 202 accepted that shows that its been accepted but not finished yet. this is asynchronous

Message Types: Commands and Events

Resilient Communication Patterns:
implement retries with back-off
Circuit breaker- if errors are detected it stops the code from continuing and messing up more things

Securing Microservices:
Encryption, authentication, authorization

Sensitive Data:
The catalog part of the Ecommerce isn't sensitive, but the ordering service IS- holds history of customer and personal info

Encryption in transit- use standard algorithms
Transport Layer Security
SSL Certificates
Certificate management

Encryption at rest
disk encryption, Key management, encrypt backups too

Authentication- we need to know who is calling our service to determine if they are allowed to receive information

HTTP Authorization Options: username&password- requires password storage
API key- key per client

Using an Identity Server
Use Industry standard protocols (OAuth 2.0 & OpenID Connect)
    - recommended to learn more about these before implementing them...

Authorization: not only who is calling but what they can do. We need authorization frameworks. Consider carefully what people are allowed to do via endpoints

Don't rely on a SINGLE technique, combine multiple layers of protection so if one fails users are protected.

Arrange penetration testing & automated secruity testing, attack detection by configuring alerts, auditing to know who did what when

Delivering Microservices:

Automated Deployment- no more manual deployment!
- should be reliable and repeatable process to update many microservices

Release Pipeline:
Build -> Unit Tests -> Deploy microservices -> service tests -> deploy to QA -> End-to-end tests -> release gate -> deploy to production

Deploy to different environments. Devs debug locally, QA does end to end tests, manual tests, pen testing, perfomance testing. Production does per customer, per region

Parameterize your deployments... in your config file in JSON format

Summation:
Automate deployments
Create a release pipeline
    -deploy to different environments, run automated tests
Upgrade microservices
    rolling updates, blue-green swap


Microservices need to be Observable with centralized logs, health check endpoints



