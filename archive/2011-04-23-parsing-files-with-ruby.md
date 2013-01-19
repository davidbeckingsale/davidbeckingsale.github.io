---
layout: post
title: Parsing Files with Ruby
status: publish
type: post
excerpt: I'm coming to the end of my final year project, and have been running a lot of performance tests. This involves crunching a lot of data in order to generated some graphs. I knocked up a little Ruby script to make this process a bit easier.
published: true
---

I'm coming to the end of my final year project, and have been running a lot of performance tests. This involves running the same program on multiple node configurations. The result of all this is a *lot* of text ending up in a lot of files. The programs don't just spit out a runtime, they dump a lot of information related to the solution the process has calculated. Because of the large amount of text that I would have had to trawl through, I decided to try and do it with a script. I've been learning a little bit of Ruby on Rails recently, so I decided to give that a whirl. It's nothing special, just a quick and dirty regex script with Ruby. It's a nice way to see how Ruby can interact with system type stuff. The code I used was: 

{% highlight ruby %}
file=ARGV.first
decomp_regex = /\s[0-9]+\sdomains\s-\s([0-9]+)\sx\s0-9]\sdecomposition/ 
time_regex = /\sCPU\stime\swas:\s([0-9]?[0-9]+|[0-9]+)/

File.readlines(file).each do |line| 
	if (m = decomp_regex.match line) 
		print m[1] 
	end 
	if (m = time_regex.match line) 
		print ",#{m[1]}\n" 
	end
end
{% endhighlight %}

Like I said, nothing fancy. Just searches for lines of the form "25 domains - 5 x 5 decomposition" and rips out the first number of the "N x N" and prints it. The second regex looks for lines like "CPU time was: 903.231", and takes the time and puts that after the first number. This basically is generating lines like "5, 903.321" which are used for plotting in gnuplot. It's not big and it's not clever, but it's saved me a bunch of time over the past couple of days generating files for plotting.
