---
layout: post
title:  "Deploy To Openshift"
date:   2013-07-05 14:18:00
categories: cloud openshift
---

Looking for tips on what to build or where to go next? I've organized some helpful hints for you.

**Accessing your application**

Your application has one or more cartridges that expose a public URL. The Example link below to see your application:

{% highlight ruby %}
http://myapplication-durgeshvaishnav.rhcloud.com/
{% endhighlight %}

The application overview page provides a summary of your application and its cartridges.

**Making code changes**

OpenShift uses the Git version control system to manage the code of your application. Each cartridge has a single Git repository that you'll use to check in changes to your application. When you push a change to your Git repository we'll automatically deploy your code and restart your application if necessary.

Install the Git client for your operating system, and from your command line run
{% highlight ruby %}
git clone ssh://{ssh-key}@myapplication-durgeshvaishnav.rhcloud.com/~/git/myapplication.git/
cd myapplication/
{% endhighlight %}


This will create a folder with the source code of your application. After making a change, add, commit, and push your changes.

{% highlight ruby %}
git add .
git commit -m 'My awesome changes'
git push
{% endhighlight %}

When you push changes the OpenShift server will report back its status on deploying your code. The server will run any of your configured deploy hooks and then restart the application.