---
layout: post
title:  "NodeJS Pros and cons"
date:   2014-03-08 10:03:00
categories: java
---

While working on NodeJS, I found these pros and cons quite useful to remember. 

1. NodeJS Asynchronous event driven IO helps concurrent request handling, but does not provide scalability. 
2. Javascript is fun but not easy to integrate with relational database. 
3. Reusable code for server and client but a lot of nested callbacks.
4. NPM is already large but not easy for starter. 
5. Active Open source community but not suited for CPU intensive tasks.

In general, use Node.js when you have highly I/O-bound operations that don’t use much CPU. Use Java/.NET when you need to calculate things and use a lot of CPU. Don’t use Node.js solely on the reasoning that it’s much faster and performs way better than Java/.NET.



