---
layout: post
title: Logging Blog Ideas 
status: publish
type: post
excerpt: Easy capturing of blog ideas using Alfred.
---
Like most people these days, I'd like to blog more. A key part of that is finding things to write about. Whenever I had an idea, I would open up nvALT, find my list of ideas, then add a new idea to the bottom. None of those steps are too difficult, but they do cause a fairly lengthy disruption if you are in the middle of something else. To streamline the process, I used [Alfred][alfred], an application launcher from [Running With Crayons][rwc].

One great feature of Alfred is the ability to trigger a shell script, along with passing it an optional parameter. A simple shell script to log ideas would look something like this:

{% highlight bash %}
	echo "idea" >> ~/Dropbox/notes/blog_ideas.txt
{% endhighlight %}

Combining that with Alfred means that I can replace whatever is inside the quotes with a parameter that Alfred will pass to the script. The value this parameter takes will be whatever you type after the keyword you use to trigger your script. The actual script you need to put in Alfred looks something like this:

{% highlight bash %}
echo "- {query}" >> /Users/david/Dropbox/notes/blog_ideas.md 
    && echo "Added {query} to blog ideas…"
{% endhighlight %}

I use a hyphen at the start of the item because I maintain my file as a markdown list. The echo at the end gives me a [Growl][grwl] notification with whatever was added to my list of ideas.
I can now hit ⌘-Space to bring up Alfred, then type "blog capturing ideas with Alfred", and get a new line at the end of my ideas file.

[alfred]: http://www.alfredapp.com/
[rwc]: http://www.runningwithcrayons.com/
[grwl]: http://growl.info/
