---
layout: post
title:  "Zero Defect?"
date:   2013-07-09 21:00:00
categories: agile
---

People talk about working on support projects and dealing with lots of defects on development cycle, but with Agile development methodology,  there are several strategies that may help you to achive zero defects on your project.

**Test Driven Development.** Nice side effect of TDD is a unit tests suite. You have tests for new code, and you have unit tests for old code. More tests — less bugs. 

**Continuous integration.** Instant feedback helps to identify problems early and fix them early. It saves time (and money) and reduces bugs in production. 

**Automated regression** functional tests suite. Unit tests are good, but you need something else. Functional tests emulates user behavior and find user interface errors, integration errors, etc. Needles to say you should have continuous integration in place to succeed with automated functional tests. 

**Root cause analysis.** There are several ways to fix a bug. You may just hack the code and apply a patch (please, don’t do it at home!). You may think deeper and fix the bug nicely. Also you may look into the root of the problem and fix it. Yes, it may take time, but you will prevent future bugs from this domain. 

**High development skills.** Ironically, high skills do not always reduce bugs rate in production. “Stars” may be strong in some areas (business layer), but may not polish things. It may lead to many small bugs, especially on UI.

