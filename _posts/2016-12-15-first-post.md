---
title: Starting out with Jekyll
date: 2016-12-15 21:08:37 -0500
tags: [jekyll]
---

This is my first blog post! I'm excited to be working with Jekyll and Sass to produce this blog and hope to be able to provide lots of useful content.

Mostly, I expect to focus on computer science and programming. I'm working on several big projects right now, so I'll be focusing on status updates
on all of them and tutorials/explanations of things I've figured out. Some math and cybersec content will be forthcoming. Also there will be random musings on music, politics, literature, etc. periodically. Hope you enjoy!

### Jekyll

Writing this site has been my first experience with Jekyll for static content generation. I'd been considering writing a blog for a while using Django as a backend, but I figured I'd give this a try. Jekyll is essentially a static HTML generator with lots of awesome features. For a full introduction, read the [offical tutorial](http://jekyllrb.com/docs/home/), but I'm going to endeavor here to give a brief explanation of what Jekyll is all about and why it's so awesome.

Jekyll uses the popular markup format Markdown to format text and then compiles everything together into a static website. There are two tremendous advantages to this: ease of use and speed. Firstly, Jekyll is a lot easier to manage than a more complex application framework with databases and backends and lots of code. Jekyll apps are 99% content. Secondly, since Jekyll compiles to static HTML, this means that there's a massive speedup to loading pages. Jekyll uses a templating engine called Liquid that allows it to have almost programming-level like capabilities while compiling.

A blog post in Jekyll starts out like this (this is what I used for this article):

{% highlight yaml %}
---
title: Starting Out with Jekyll
date: 2016-12-15 08:04:37 -0500
layout: blog
tags: [jekyll]
---
{% endhighlight %}

This information is what Jekyll calls **front matter** in the YAML format. It tells Jekyll the important information about your post.

Next, your post file has some Markdown: the actual content of your post. This will look something like this:

{% highlight md %}
# This is a nice heading!

* And a list too...
* Look how nice this is :)
{% endhighlight %}

This file should be saved with a name like `_posts/2016-12-15-first-post.md` in order for Jekyll to correctly put it in its place. All we have to do now is define a layout and we're good to go! I hope I've piqued your interest. Read the tutorial if you want to keep going!
