---
layout: post
title: Journaling with DayOne 
status: publish
type: post
excerpt: Kickstarting my DayOne journal by importing old ohlife entries.
---
Yesterday, I took the plunge and invested a whole ~£4.50 buying [DayOne][d1] for both OS X and iOS. The app is billed as 
> The easiest to use journal / diary / text logging application for the Mac...

and I think that is probably true. So far, I've only written about six (short) entries over two days, but I'm really enjoying the simple, clean, interface. 

What I think will become a key feature for me are the reminders. I used to use [ohlife][ol] for keeping a journal, something I stuck with for a just over a month, and one of the best features there were the daily email reminders to make an entry. However, whilst it was easy to hit reply and submit your entry, I don't think a mail client is where most people do their best writing -- certainly not their most intimate.

The first thing I did when I installed DayOne was to work out how to import my old ohlife entries, something that currently needs to be done using the `dayone` command line tool. It is very simple to use, and the [sample script][doexample] they provide, along with Brett Terpstra's [post][bt] on using DayOne from the command line had me well on my way to getting my old entries imported.

The ohlife export file simply contains all your entries, with a simple date, content format. I whipped up a quick ruby [script][dabgh] to parse my file and create the new entries and I was done.

Flicking through these old entries (from last August) really highlighted the benefits of keeping some kind of daily log of thoughts/feelings/actions, and it was really interesting to read through some of my old entries, knowing that things I was worrying about had turned out fine, and how things I'd wanted to happen have now come to pass.

I'm feeling quite positive that DayOne will help me log enough about each day to be able to look back in 6 months or a year and (hopefully) feel good about what I have done since then!

[d1]: http://dayoneapp.com/
[ol]: http://ohlife.com/
[doexample]: https://gist.github.com/977766
[bt]: http://brettterpstra.com/logging-with-day-one-geek-style/
[dabgh]: https://github.com/davidbeckingsale/ohlife-to-dayone.rb
