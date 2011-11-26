---
layout: post
title: Debugging MPI with GDB 
tags:
- MPI
- Programming
status: publish
type: post
published: true
---

I have been writing some MPI code recently, and as is often the case with C I found I was getting some segfaults. As anyone who programs with MPI knows, debugging is non-trivial because of the parallel nature of the programs. I didn't want to have to pack the program full of printf statements to try and diagnose the problem, so I looked into debugging. While I was searching I came across a great [FAQ][1] on the OpenMPI site containing instructions for using GDB to debug parallel programs. Firstly I compiled my code with the -g flag, don't forget this or else the info you can get from gdb will be severely limited. After compiling the code, load it with [code light="true"] mpirun -np 4 xterm -e gdb my\_mpi\_application [/code] replacing xterm with your terminal application of choice. This command will spawn 4 xterms running gdb, ready for you to debug your program. Each instance of gdb will correspond to a different MPI "processor", so it is easy to debug the program by using breakpoints and print commands, just as you would if you were debugging a serial application with gdb. It is important to note that I did all this debugging locally, spawning multiple copies of the program on my laptop, your success with this method on a cluster or similar machine may vary and the FAQ above does offer some alternative methods for getting this to work. Debugging like this is best suited to small errors where you only need to run a few instances of this program -- I wouldn't recommend spawning 30 gdb sessions and trying to debug like that!

 [1]: http://www.open-mpi.org/faq/?category=debugging#serial-debuggers
