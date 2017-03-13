---
layout: post
title:  "AWS lambda"
date:   2017-03-12 8:00:00
categories: nodejs
---

Cloud computing is the on-demand delivery of computing power, database storage, applications, and other IT resources through a cloud services platform via the internet with pay-as-you-go pricing. It has three main types that are commonly referred to as Infrastructure as a Service (IaaS), Platform as a service (PaaS) and Software as a Service (SaaS). Amazon Web Services (AWS) is a secure cloud services platform, offering to compute power, database storage, content delivery and other functionality to help businesses scale and grow.

Recently I had an opportunity to work on AWS EC2 and Lambda architecture and learn about its powerful way to run and manage applications. By Definition, AWS Lambda can run code without thinking about servers and you pay for only the compute time you consume. I mean, just write and upload your code in any supported language and Lambda takes care of everything required to run and scale that code.

This product is the perfect fit for our requirement because of its event based processing. We have many entry points which invoke based on certain events but runs small module. In Past in order to run these application modules, we had expensive distributed servers and 24/7 support but still, there was a lot of struggle in the whole process to keep the application responsive all the time irrespective of uses.

AWS Lambda helped us a lot in order to manage and run many small modules without worrying about whole applications. Now we have more control on independent lambda health which may affect one of the key features.


