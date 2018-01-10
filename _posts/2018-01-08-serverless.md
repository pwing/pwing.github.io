---
layout: post
title:  "Moving on from RESTful microservices - Serverless Architectures"
date:   2017-12-19 
categories: serverless, aws
---
So the stuff you had/have to handle when doing microservices are things like:
- a git repo per microservice
- building an uberjar (with an embedded web server).
- server config so your microservice listens on a particular port.
- swagger doc for your microservice.
- docker config to define a container for your microservice.
- ec2 instances or other vms to deploy your microservices to.
- kubernetes or mesos admin of docker containers.
- api gateway.

AWS Lambda etc. as a higher level compute service abstracts away the web server, and we can now just focus on developing our business logic as functions.  Besides reducing the number of devops tasks required to manage microservices in production, there's a strong likelihood of using AWS Lambda being much cheaper, as you only pay for when the function runs, not when it's not.  We no longer need to have servers running idle, waiting for requests.  A comparison of costs can be found [here](https://www.trek10.com/blog/lambda-cost/).

As businesses have moved from on-premise to the cloud to save money, we can now potentially save even more money by going serverless.  
With recent innovations such as AWS Lambda, Azure Functions and Google Cloud Functions, it is now possible to develop a back end architecture without having to worry about microservices architecture.  Previously, each microservice (typically with a RESTful http api) would have been developed as a separate "web application server" to be deployed and run as docker containers on virtual machines.  The problem there is that you have to manage those containers and vms, using something like mesos or kubernetes and/or doing additional aws configuration.

AWS Lambda etc as compute services mean that we no longer have to think of microservices as standalone servers - a RESTful API can be made by defining the api on the Amazon API Gateway, which can then be linked to the AWS Lambda functions to call.  As well as Function as a Service (FaaS), serverless architecture is also comprised of Backend as a Service (Baas), where we can reuse other people's services/ functions e.g AWS Cognito for authentication, and so save time and money.

As Serverless is still fairly new (e.g. AWS Lambda launched in 2014), there's going to be lot of new patterns and practices and tooling to become established and mature.  [Serverless Framework](https:/serverless.com) seems to be one of the more popular tools to help with FaaS development, not only with AWS Lambda but other environments too.

[Yan Cui has given a talk on AWS Lambda, with many interesting points, which shows that it can work very well in production](https://vimeo.com/221105875)

Some benefits of serverless are:
- thinking more about functions will encourage programming in a functional style, which will be cleaner.
- cheaper, as you're not paying for your server when it's idle.
- cheaper, as you don't have to maintain your servers, e.g. security patches - the provider does it for you.
- faster development - can reuse other services such as cognito or dynamodb.
- faster development - even less monolithic that microservices, a function can be built and deployed quickly without being grouped with other change sets.
- event driven - being reactive to events makes a serverless app more efficient (no idle time and is asynchronous).

Some limitations are:
- Local Testing - whilst functions can be tested locally, integration testing will have to be done by testing against cloud environments, unless there's a way to instantiate a "lambda environment" locally.
- Loss of Control - configuration, performance, security. 

Overall, the cost aspect will push people to use Serverless and the technologies to support this move will mature.

### References ###
- ["What is Serverless?" by Mike Roberts and John Chapin](http://www.oreilly.com/programming/free/what-is-serverless.csp?intcmp=il-prog-free-info-lgen_new_site_using_serverless_architectures) - this gives a good overview of Faas and Baas.
- [Amazon's web page on lambda](https://aws.amazon.com/lambda/)
- [Amazon's web page on serverless](https://aws.amazon.com/serverless/)
- [Yan Cui's talk on AWS Lambda](https://vimeo.com/221105875)
