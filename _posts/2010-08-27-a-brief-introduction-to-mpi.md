---
layout: post
title: A Brief Introduction to MPI 
tags: - Tech 
status: publish 
type: post 
published: true 
---

My final year at university is approaching and I need to undertake a project. My project is going to involve high performance computing - namely message passing, and more specifically the Message Passing Interface. In order to begin to grasp the concepts of the MPI specification, I decided to present my current body of knowledge in this post

The Message Passing Interface is a specification, created by the MPI Forum. The purpose of the specification was to create a standard that would be widely used for message passing programs. The specification provides no implementation - it just describes the operations that are needed for message passing. The first draft was standardised in 1994 but the MPI Forum have continued to meet and refine the specification, resulting in MPI-2, which was standardised in 1996. MPI uses a number of concepts that may require more explanation. I will start with a simple example program and then explain it following the code listing: 

{% highlight c %}    
     /*
      "Hello World" MPI Test Program
     */
     #include <mpi.h>
     #include <stdio.h>
     #include <string.h>
     
     #define BUFSIZE 128
     #define TAG 0
     
     int main(int argc, char *argv[])
     {
       char idstr[32];
       char buff[BUFSIZE];
       int numprocs;
       int myid;
       int i;
       MPI_Status stat; 
     
       MPI_Init(&argc,&argv); /* all MPI programs start with MPI_Init; all 'N' processes exist thereafter */
       MPI_Comm_size(MPI_COMM_WORLD,&numprocs); /* find out how big the world is */
       MPI_Comm_rank(MPI_COMM_WORLD,&myid); /* and this processes' rank is */
     
       /* At this point, all programs are running equivalently, the rank distinguishes
          the roles of the programs in the SPMD model, with rank 0 often used specially... */
       if(myid == 0)
       {
         printf("%d: We have %d processors\n", myid, numprocs);
         for(i=1;i<numprocs;i++)
         {
           sprintf(buff, "Hello %d! ", i);
           MPI_Send(buff, BUFSIZE, MPI_CHAR, i, TAG, MPI_COMM_WORLD);
         }
         for(i=1;i<numprocs;i++)
         {
           MPI_Recv(buff, BUFSIZE, MPI_CHAR, i, TAG, MPI_COMM_WORLD, &stat);
           printf("%d: %s\n", myid, buff);
         }
       }
       else
       {
         /* receive from rank 0: */
         MPI_Recv(buff, BUFSIZE, MPI_CHAR, 0, TAG, MPI_COMM_WORLD, &stat);
         sprintf(idstr, "Processor %d ", myid);
         strncat(buff, idstr, BUFSIZE-1);
         strncat(buff, "reporting for duty\n", BUFSIZE-1);
         /* send to rank 0: */
         MPI_Send(buff, BUFSIZE, MPI_CHAR, 0, TAG, MPI_COMM_WORLD);
       }
     
       MPI_Finalize(); /* MPI Programs end with MPI Finalize; this is a weak synchronization point */
       return 0;
     }  
{% endhighlight %}

The fist thing of interest is the mpi header file, which is included in line 4. All mpi programs need this line in order to compile. The next item of note is the function MPI_Init() - this function must be called at the start of every MPI program, before any of the other MPI functions are used. This initialises the execution environment ready for other functions to be called. The functions MPI_Comm_size and MPI_Comm_rank are used in order to determine the number of total processors and the id of this processor. Each processor is given a rank, which is an integer in the range 0 - n-1, where n is the number of processors. Moving to the if else statement, the rank of the processor, which is stored in myid is used to determine what the program should do. Rank 0 is typically used as a master process, gather results from the others. Inside these blocks the MPI_Send and MPI_Recv functions are used. The master process sends a message to each of the other processors in turn. Once a process has received its message, it prints a string and then sends a message back to the master process. The master process receives all these messages. Following this, the MPI_Finalize function is called. This terminates the MPI execution environment. This is the last MPI function to be called, and no others may be called after it. This post is only intended to be a very brief and simple introduction,in line with my current state of knowledge. As my knowledge grows,expect more detailed and specific posts in a similar vein. Please feel free to comment if you think there are things I should elaborate on, or if you have any helpful tips. For more information, please see these links: 

*   [LLNL MPI Tutorial][1]
*   [MPI_Send][2]
*   [MPI_Receive][3]

 [1]: https://computing.llnl.gov/tutorials/mpi/
 [2]: http://www.mcs.anl.gov/research/projects/mpi/www/www3/MPI_Send.html
 [3]: http://www.mcs.anl.gov/research/projects/mpi/www/www3/MPI_Recv.html
