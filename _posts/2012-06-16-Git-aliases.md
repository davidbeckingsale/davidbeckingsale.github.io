---
layout: post
title: Git Aliases
status: publish
type: post
excerpt: How setting up a few simple aliases can make working with git a little bit more efficient.
---

Working with `git` necessarily involves a lot of command repetition. Checking the status of files, adding files to the staging area, checking diffs, and committing files. These are commands that you are going to issue many times a day. As soon as you are working with remote repos you can throw in a few more -- pushing and pulling for starters.

Having a core set of frequently used commands is not a problem, and highlights the simple commands that allow you to use `git` effectively. With a few aliases in our shell configuration, we can cut down the time it takes to issue these commands, and more efficiently work with git on the command line.

## In your shell
The first thing I do is alias the `git` command to `g`. Moving from 3 letters to one is not a huge difference, but it does start to add up, especially when combined with some of the following shortcuts.

## In your `.gitrc`
This set of aliases belong in your `.gitrc` file, where you can set up shorter aliases for all of `git`'s subcommands. These need to go under `[aliases]` in your .gitrc:
	
	s status
	c commit
	a add
	p push
	
With these aliases in place, `git commit` becomes `git c`, or even `g c` if you have already aliased `git` to `g` in your shell configuration.
	
## Back in your shell
The next tip comes from Peepcode's [Advanced Git][ag] screencast, where they talk about adding even shorter git alisases to your shell configuration. Basically, you just take out the space between git and your subcommand. For example, I would alias `ga` to `g a`, which would in turn perform a `git add`. Not needing to type the spaces doesn't sound like a big improvement, but as I said before, it all adds up.

[ag]: https://peepcode.com/products/advanced-git