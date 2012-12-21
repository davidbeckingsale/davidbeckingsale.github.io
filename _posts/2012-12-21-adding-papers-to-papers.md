---
layout: post
title: Adding PDFs to Papers2 with maid
status: publish
type: post
excerpt: Using the great <code>maid</code> gem, it's easy to automatically add PDFs to Papers2.
---

Often, when processing journal RSS feeds, I'll find quite a few articles that I
want to read.  I use [Papers2][papers] to manage my papers, so the first thing
I need to do is import these newly-downloaded files.

The [`maid`][maid] gem makes this easy to do automatically. I've added the
following rule to my `rules.rb` file:

    rule 'Add PDFs to Papers2' do
      dir('~/Downloads/*.pdf').each do |path|
        is_paper = `mdfind -onlyin ~/Downloads/ computing`
    
          if is_paper.include?(path)
            `open -a Papers2 "#{path}"`
          end
      end
    end

It's not perfect, but it _is_ perfectly functional. Every time I run `maid
clean`, any PDFs that contain the word "computing" will be automatically
imported into Papers. Obviously the word used to select papers will vary
depending on your field, but the rule is trivial to modify.

[maid]: https://github.com/benjaminoakes/maid
[papers]: http://www.mekentosj.com/papers/
