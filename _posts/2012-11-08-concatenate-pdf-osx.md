---
layout: post
title: Concatenate PDF files on OSX
status: publish
link: http://gotofritz.net/blog/howto/joining-pdf-files-in-os-x-from-the-command-line
type: post
---

> It turns out that from Tiger onwards, OSX ships with a Python script that does exactly what you need. The script is already executable, and Python is pre-installed on OS X, so all you need to do to run it is opening the Terminal and typing
>
>     "/System/Library/Automator/Combine PDF Pages.action/Contents/Resources/join.py" -o PATH/TO/YOUR/MERGED/FILE.pdf /PATH/TO/ORIGINAL/1.pdf /PATH/TO/ANOTHER/2.pdf /PATH/TO/A/WHOLE/DIR/*.pdf
