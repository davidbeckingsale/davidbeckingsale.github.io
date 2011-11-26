---
layout: post
title: Configuring Xmonad
tags: - Tech
status: publish
type: post
published: true
---

Following the submission of my xmonad config to the xmonad reddit, I wanted to write a post that explained what I have done in a bit more detail.

[Xmonad][1], my window manager of choice, lies at the very heart of my config. It is accompanied by [conky][2] and [dzen][3], 2 utilities very much at home with this minimalistic tiling WM. Conky provides a way to display information, which is used to display the CPU information, RAM information, network information, and the time. Conky is controlled with a simple textfile. In my config, this is ".conky_bar"

Dzen provides the actual bars for information to reside in. The bar at the top of the screen is actually 3 separate items: a dzen bar for workspace and window information, the conky powered bar for stats and finally trayer provides a system tray. I used the zenburn colour scheme as the basis of my theme. I like dark themes, but sometimes find that black (#000000) based themes can be a little too dark. The lighter grey of zenburn is a perfect choice,¬ and the fact that the colour scheme has been built up for a number of years has provided me with a good palette to use as the base for my config. 

Building my config allowed me to develop a greater understanding of xmonad and Haskell, as well as letting me gain some experience with conky. I think the most important thing to emphasise about my config, is that the majority of it is very simple, and purely aesthetic. If you use xmonad, I would imagine you are already using your own config. If not, or if you would just like some more ideas, I strongly recommend you take a look at the [xmonad config archive][4]. If you decide you want to build up a configuration of your own there are a few tips that I would like to share: 
*   Find or create a colour scheme. Simple is often best.
*   Make use of simple keybindings for your frequent tasks (this is less related to the aesthetics of your setup and more to usability). For more information about my config please see [here][5].

 [1]: http://www.xmonad.org
 [2]: http://conky.sourceforge.net/
 [3]: http://sites.google.com/site/gotmor/dzen
 [4]: http://haskell.org/haskellwiki/Xmonad/Config_archive
 [5]: http://www.davidbeckingsale.com/blog/projects/xmonad-config
