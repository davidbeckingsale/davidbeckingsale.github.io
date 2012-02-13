---
layout: post
title: Aggresive Resize - Make tmux windows as big as possible
status: publish
type: post
excerpt: Stop tmux constraining windows to the size of the smallest client viewing the window
---

Via [Practical Tmux][pt]:

> Aggressive Resize
> 
> By default, all windows in a session are constrained to the size of the
> smallest client connected to that session, even if both clients are looking at
> different windows. It seems that in this particular case, Screen has the better
> default where a window is only constrained in size if a smaller client is
> actively looking at it. This behaviour can be fixed by setting tmux's
> aggressive-resize option.
> 
> setw -g aggressive-resize on

Great if you are connected to a session on both a laptop and a desktop machine.

[pt]: http://mutelight.org/articles/practical-tmux
