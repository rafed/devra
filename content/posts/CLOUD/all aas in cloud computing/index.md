---
title: All Kinds of "AAS" in Cloud Computing
date: 2020-06-11
tags: [cloud, software engineering]
image: "aas-vs.jpg"
---

From an end users perspective, there are three kinds of aaS in cloud computing. By aaS I mean "as a Service". They aaS-es are:

1. [IaaS - Infrastructure as a service](#iaas-infrastructure-as-a-service)
1. [PaaS - Platform as a service](#paas-platform-as-a-service)
1. [SaaS - Software as a service](#saas-software-as-a-service)

As businesses are moving more towards the cloud, understanding the differences between the types of services and also knowing some of the service providers is essential. This article provides a brief intro to these services.

> The examples of each service listed below is not an exhaustive list nor the best service provider of that category. They are merely services that I know of or have used in the past.

## IaaS (Infrastructure as a service)

IaaS is when you rent physical machines (i.e. infrastructural components such as storage, ram, CPU, routers) and use them remotely without having to manage them (such as ensuring electric supply, dedicated internet, air cooling, wire management, replacing damaged machines).

IaaS service providers:
- [GCP: Cloud Compute Engine](https://cloud.google.com/compute)
- [AWS: Elastic Cloud Compute (EC2)](https://aws.amazon.com/ec2/)
- [Azure: Virtual machines](https://azure.microsoft.com/en-us/services/virtual-machines/)

IaaS is all about building your system from scratch without having your machines on site. You need to manage all your rented machines though which can be a hassle for many developers who do not know infrastructure management. This where PaaS comes in.

## PaaS (Platform as a service)

PaaS is a way to provide a customer with the finished software environment. The environment is ready for deploying your app without the hassle of installing/managing dependencies yourself. Just deploy your app and go! 

Usually PaaS = IaaS + [Operating system + Database management]. 

PaaS service providers:
- [GCP: App Engine](https://cloud.google.com/appengine)
- [AWS: Elastic Beanstalk](https://aws.amazon.com/elasticbeanstalk/)
- [Heroku](https://www.heroku.com/)

The following are some sub-categories of PaaS.

#### DbaaS (Database as a service)

You get ready to use databases, that can automatically scale when load increases.

DbaaS service providers:
- [GCP: BigQuery](https://cloud.google.com/bigquery)
- [Amazon RDS](https://aws.amazon.com/rds/)
- [Directus](https://directus.io/)

#### FaaS (Function as a service/Serverless)

FaaS is a service that allows you to execute code in response to events. You typically deploy simple functions. FaaS is commonly used in building microservices.

FaaS service providers:
- [GCP: Cloud Functions](https://cloud.google.com/functions)
- [AWS: AWS Lambda](https://aws.amazon.com/lambda/)
- [Microsoft Azure: Azure Functions](https://azure.microsoft.com/en-us/services/functions/)

## SaaS (Software as a service)

SaaS is a method of software delivery where you use a service via an online subscription.

Since SaaS is about delivering software, it can be targeted towards both developers and end-users (IaaS and PaaS is only for developers).

Examples of SaaS are endless. I'll roughly go through them.

#### Bots as a service

Make a chatbot for your platform without coding:
- [Chatfuel](https://chatfuel.com/)
- [Manychat](https://manychat.com/)

#### STaaS (Storage as a service)

- [Google Drive](https://www.google.com/drive/)
- [Dropbox](https://www.dropbox.com/)

#### Caas (Commerce as a service)

- [Shopify](https://www.shopify.com/)
- [Wordpress](https://wordpress.org/)
- [BigCommmerce](https://www.bigcommerce.com/)

#### MaaS (Messaging as a service)

- [Sendgrid](https://sendgrid.com/)
- [Mailchimp](https://mailchimp.com/)
- [Twilio- SMS & emails](https://www.twilio.com/)

#### Survey as a Service

- [Qualtrics](https://www.qualtrics.com/)
- [SurveyMonkey](https://www.surveymonkey.com/)

The list of SaaS can go on and on, but you should get a general idea.