---
layout: post
title: Emacs and org-mode for Getting Things Done
tags: 
- Emacs
status: publish
type: post
published: true
---

I have ranted about people trying to use emacs for everything, but I have recently been humbled by starting to use org-mode as my [GTD][1] solution. I previously used [Remember the Milk][2] and [Nirvana][3] for managing my todo lists, but after frequent internet connection problems I started to look for an offline GTD solution. Being an emacs user I had heard of [org-mode][4] before, but had never really got round to using it. I had made a few .org files with some outlines in but nothing of any significance. When I found out about people using it for GTD I tried my hardest to make it work for me, but I just found the setup intimidating. The flexibility of org-mode that is it's strong point was probably the one thing that made it hardest for me to use. I didn't want to have to decide how best to do things. I wanted a ready made system to type my tasks into, even if it didn't quite fit with the way that I work. I spent too much time worrying about my GTD system: how it should look, what it should do, what categories I needed. Should I put scheduled tasks into my todo lists or onto my calendar (I use Google Calendar, but Nirvana and RTM both support scheduled tasks). All these questions are rather unimportant. It's not what you system it, it's how you use it. I want to use the rest of this post to outline my system, and try and help anyone that feels lost about getting started using org-mode for GTD. 

### Getting started

I'm going to assume a basic familiarity (with org-mode), inasmuch as you can create items in outline mode, and know a little bit about turning an item into a task (hint: use C-c C-t). If you are a complete org nooby, then don't worry. Learning the basics is pretty [easy][5]. The first thing to do is set up your "agenda files". These are where org-mode will look when you ask it to show you a list of your current taks with the "org-agenda" command. The two files I use are gtd.org and someday.org -- this is a way of seperating my current projects and tasks from my someday projects. To add these files to the agenda, put the line \[code light="true"\] (setq org-agenda-files (list "~/Dropbox/org/gtd.org" "~/Dropbox/org/someday.org")) [/code] somewhere into your .emacs. 

### gtd.org

One of the things I struggled with most when starting out with org-mode as a gtd system was how to organise things. Taking a lot of tips from the gtd org [tutorial][6], I have organised my file in the following way: 
*   INBOX This is where things I capture go. 
*   TASKS These are single next action items
*   PERSONAL PROJECTS Personal projects, e.g, writing this post
*   WORK PROJECTS Projects relating to university: coursework, assignments and so on. 
Underneath these top level items will come keyworded items, representing tasks or projects. In the INBOX, items will have no keyword and will be waiting to be refiled into the appropriate section. INBOX is just a dumping ground where stuff that I capture gets sent. I will talk about capturing a bit later on. Under TASKS, I use two keywords: TODO, which is the default keyword org-mode uses for tasks, and WAITING, for any items where I am waiting on someone else. The two PROJECT categories will contain items with keyword PROJ as children. The tasks associated with these projects will the be TODO or WAITING items that are children of their parent project item. Here the flexibility of org-mode is great because it allows you arbitrary levels of taxanomically satisfying nesting :) I wouldn't recommend going overboard, but it can be useful to split up projects into a few subprojects if it gives greater clarity to whatever it is you are doing. The someday.org file contains task items that are keyworded SOMEDAY. I review this file weekly and move any items I want act on into the main gtd.org file. To help you get a feel for how it looks, here is a sample gtd.org file I have made up: [code light="true"] * INBOX * NEXT ** TODO Buy some milk :@errand: * PERSONAL PROJECTS ** PROJ Write blog post \***| TODO Add fake gtd.org file to post :@online: ** PROJ Build Rocket * WORK PROJECTS ** PROJ Some assignment [/code] 

### Typical workflow 

Workflow is a key part of any gtd system. The way I see it, there are three parts to workflow: viewing tasks, capturing new tasks, and actually doing them! To view tasks use the org-mode agenda function that I described how to set up earlier. To capture tasks I use org-modes capture feature, enabling me to capture anything and send it straight to the INBOX of my gtd.org file. Capture requires some setup, which is done through the variable org-capture-templates: \[code light="true"\] (setq org-capture-templates '(("t" "Todo" entry (file+headline "~/Dropbox/org/gtd.org" "INBOX") "* TODO %?\n %i\n") ("n" "Note" entry (file+datetree "~/Dropbox/org/notes.org") "* %?\nEntered on %U\n %i\n %a"))) [/code] Now when you invoke the command org-capture, you will be prompted for a template (etiher t or n using the above setup). Once you select the template, you can then enter the task information and save it with C-c C-c. To complete tasks you just need to do the work, before completing the item in your agenda file :) 

### More org related stuff

*   The clock is pretty useful if you want to record time spent working on a task. Move to the line containing the task and start the clock with C-c C-x C-i. The clock will remain running (even between emacs sessions) until you stop it with C-c C-x C-o, or complete the task.
*   Contexts are generally added with org-modes "tags", you can hit C-c C-c and then enter any tag you want for that item. 
*   Categories and other org-mode setup Something I don't fully understand yet. The main piece of advice I can give relates to both org-mode and GTD in general. Don't worry about the system. How you use your system is much more important. As long as you can capture tasks and projects successfully and remember to check your agenda, you have everything you need from your system. Whether this is org-mode, rtm, nirvana or any other gtd type app is not important. The key is the important habbits you need to acquire in order to use what are essentially just lists effectively.

 [1]: http://www.davidco.com/what_is_gtd.php
 [2]: http://www.rememberthemilk.com
 [3]: http://www.nirvanahq.com
 [4]: http://orgmode.org
 [5]: http://orgmode.org/worg/org-tutorials/index.html
 [6]: http://members.optusnet.com.au/~charles57/GTD/gtd_workflow.html
