---
layout: post 
title: Emacs require-final-newline and delete-trailing-whitespace (on save) 
tags: 
- Emacs 
status: publish 
type: post
published: true
---

Here are two useful features I have recently added to my emacs configuration: **Final Newline** ``(setq-default require-final-newline t)`` This makes sure that all files are saved with a final newline character. This is useful for programming, since it is a requirement of some languages. **Delete Trailing Whitespace (on save)** ``(add-hook 'before-save-hook 'delete-trailing-whitespace)`` Another useful feature for writing code in emacs, helps keep things tidy by deleting trailing whitespace every time you save a file.
