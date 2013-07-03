---
layout: post
title:  "Welcome to Jekyll!"
date:   2013-06-30 14:01:03
categories: jekyll update
---

Static HTML and Blog aware ruby framework [Jekyll][jekyll] is really awesome and useful. You can migrate your blog side with Jekyll and upload to GitHub Pages. 


Steps to start and run your static pages blog site to localhost.


1. Download and install, On Max OS X, Open Terminal and run following command.
	{% highlight ruby %}
	sudo gem install jekyll
	{% endhighlight %}

2.  Now create new website/blog site with jekyll, this command will create a defined folder structure.  
	{% highlight ruby %}
	jekyll new myblog.github.com
	{% endhighlight %}

3.  You can add/update posts and start jekyll, 
 	{% highlight ruby %}
	jekyll serve
	{% endhighlight %}

4. Now browse to http://localhost:4000 and see your site locally.

5. When you add or update any thing on site contents, you just need to build jekyll and change will reflect on browser.
 	{% highlight ruby %}
	jekyll build
	{% endhighlight %}

	
You'll find this post in your `_posts` directory - edit this post and re-build (or run with the `-w` switch) to see your changes!
To add new posts, simply add a file in the `_posts` directory that follows the convention: YYYY-MM-DD-name-of-post.ext.

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll's GitHub repo][jekyll-gh].

[jekyll-gh]: https://github.com/mojombo/jekyll
[jekyll]:    http://jekyllrb.com
