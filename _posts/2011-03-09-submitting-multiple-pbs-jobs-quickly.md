---
layout: post
title: Submitting multiple PBS jobs quickly
tags:
- MPI
- Programming 
status: publish
type: post
excerpt: Submitting multiple jobs into a scheduling system like PBS can be a bit of a chore, so it's good to automate it with a shell script.
published: true
---

When you're running parallel programs you will often want to submit lots of jobs with slightly different parameters, for example, different numbers of nodes or different input parameters. It gets really tedious to do this by hand, so what I have been doing recently is writing bash scripts to submit the jobs for me. The easiest way to do this is to put your submission command inside a for loop and then use the counter variable for your varying parameters. The following snippet is a script to submit lots of copies of the same job, but running on different numbers of nodes. 

{% highlight bash %}
#!/bin/bash
for a in {1..25} do
		echo "cd $PBS\_O_WORKDIR" >> fw$a.sh 
		echo >> fw$a.sh 
		echo "mpirun graph-parallel 3000" >> fw$a.sh 
		qsub -V -l nodes=$a:ppn=1 fw$a.sh 
done
{% endhighlight %}

I use echo to build up the file containing the job, and at the end of each submission, add it to the queue using qsub. If you are having to submit a lot of jobs this is definitely something to look in to.
