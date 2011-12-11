---
layout: post
title: Adding notes to Simplenote via the command-line and Dropbox 
tags:
- commandline
- notes
- simplenote
- snippet
- Tech
status: publish
type: post
excerpt: I forked out for a premium Simplenote account because I was happy with the app and found the service it provides useful. However, for quick snippets the web-interface isn't the quickest thing to use, so I decided to try and write some kind of shell function to let me capture notes from the terminal.
published: true
---

I forked out for a premium [Simplenote][1] account because I was happy with the app and found the service it provides useful. Most people these days are coming around to the benefits of plain text, and Simplenote makes it easy to keep plaintext in sync across multiple devices.

However, for quick snippets, in what I imagine to be [Notational Velocity][2] style, the web-interface isn't the quickest thing to use. Since a premium account allows you to sync all your notes to/from Dropbox, I decided I would try and write some kind of shell function to help me out.

Here it is:
{% highlight bash %}
    note() {
        echo "$@[2,10000]" > ~/Dropbox/notes/$1
    }
{% endhighlight %}
    
I can now type
{% highlight bash %}
    notes my_note.txt write blog post about this 
{% endhighlight %}
and that will create a note in the folder in my Dropbox that syncs with Simplenote. The `[2,10000]` range for putting the args into quotes is a bit hacky, but I wasn't sure how else I could do it, and a quick bit of googling didn't really help. I also wanted to avoid having to type quotes on the command line when I was trying to capture a note.</p> 
Not bad for 5 minutes work, now I just have to remember to use it!

 [1]: http://simplenoteapp.com/
 [2]: http://notational.net/
