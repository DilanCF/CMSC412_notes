# CMSC412 Lecture 7  
> 9-19  

## Threads  

![Alt text](img/Lecture07/image.png)

This is the entity that processes control. Managed by the OS by the processes  

Each process has its address space, stacks, heaps, etc.  

How does OS manage it? Through Process Control Block (PCB)  
* Must keep track of the management of the process  

![Alt text](img/Lecture07/image-1.png)  

Even with one CPU, we can give control to different processes for extremely small periods of time  
* This is due to multiprocessing 

Not matter how fast a processor is, in a finite amount of time, only a finite amount of instructions can be done  

Amount of memory that exists can be very small  

Suppose we had second CPU. Can it also execute instructions in the same address space?  
* Yes, but needs its own PC  

Is there a logical inconsistency on this?  
* No  

Suppose we have one process, with multiple CPUs
* Causes clobbering  

There *are* dangers, just not logical ones  

![Alt text](img/Lecture07/image-2.png)  

What is cache doing/do?
* Copy of address space  

![Alt text](img/Lecture07/image-3.png)  

![Alt text](img/Lecture07/image-4.png)  

![Alt text](img/Lecture07/image-5.png)  

Threads are part of A process  

Address space belongs to process, NOT thread  

they work collaboratively so nothing is clobbered  

Threads run within the application  

What must we do to create a thread? 
* Specify PC 

![Alt text](img/Lecture07/image-6.png)  

![Alt text](img/Lecture07/image-7.png)  

![Alt text](img/Lecture07/image-8.png)  

Distinction between *Parallelism* and *concurrency*  

Para: do two tings at the same time
conc: Do multiple things one at a time switching rapidly

![Alt text](img/Lecture07/image-9.png)  

We can take any process, stop it for an arbitrary length of time with no impact on functionality  
* If we have a process T1, we may share to T2 or T3
* Synchronization reqs. come into play


Anytime you use computers to interact with IRL, timing becomes an important factor  

![Alt text](img/Lecture07/image-10.png)  

How many PCs can we have? assign different PCs to different threads  

To run any thread, we need at least one CPU  

![Alt text](img/Lecture07/image-11.png)  

Hardware supported threads may have different registers  

How much can we speedup?  

![Alt text](img/Lecture07/image-12.png)  

There is a serial portion and a parallel portion  

![Alt text](img/Lecture07/image-13.png)  

One processor can have 8 threads
* this is HW supported  

Unit of CPU management is becoming a thread  

User threads
* Application to the kernel looks like a signal process  

How would an application manage threads at an application level?  
* This application only runs when the OS gives control to the particular process  
  * Now, it acts as multiple  

We are saying, for any application, the user has to handle it ??? (Slide 18) 
Controlling threads at user level, there is a module that handles this  
User knows better how to use the threads for the application  

Kernel threads
* Visible to kernel

User "
* Not visible to OS
* App specific  

![Alt text](img/Lecture07/image-14.png)  

![Alt text](img/Lecture07/image-15.png)  

![Alt text](img/Lecture07/image-16.png)  

Mapping responsibility falls on either one (depends)  

![Alt text](img/Lecture07/image-17.png)  

![Alt text](img/Lecture07/image-18.png)  

![Alt text](img/Lecture07/image-19.png)  

When writing programs, we use the API to the thread lib. that at runtime can carryout the mapping  

![Alt text](img/Lecture07/image-20.png)  

POSIX is a specification of how the API should work, NOT the actual moving parts themselves  

![Alt text](img/Lecture07/image-21.png)  

![Alt text](img/Lecture07/image-22.png)  

PThreads may be a kernel thread, or not. Depends on how it is called  

![Alt text](img/Lecture07/image-23.png)  

![Alt text](img/Lecture07/image-24.png)  

![Alt text](img/Lecture07/image-25.png)  

![Alt text](img/Lecture07/image-26.png)  

![Alt text](img/Lecture07/image-27.png)  

Language processors are providing support to split stuff up into multiple threads  
* What must compiler know about program in order to do that
  * Are there sections of the program that can be run independently

![Alt text](img/Lecture07/image-28.png)  

Most OS control degree of multiprogramming  
* Number of threads is bound by thread pool  

![Alt text](img/Lecture07/image-29.png)  

![Alt text](img/Lecture07/image-30.png)  

![Alt text](img/Lecture07/image-31.png)  

![Alt text](img/Lecture07/image-32.png)  

![Alt text](img/Lecture07/image-33.png)  

![Alt text](img/Lecture07/image-34.png)  

![Alt text](img/Lecture07/image-35.png)  

![Alt text](img/Lecture07/image-36.png)  

![Alt text](img/Lecture07/image-37.png)  

![Alt text](img/Lecture07/image-38.png)  

![Alt text](img/Lecture07/image-39.png)  

![Alt text](img/Lecture07/image-40.png)  

![Alt text](img/Lecture07/image-41.png)  

These will be stored where we keep track of the tasks, TSS

![Alt text](img/Lecture07/image-42.png)  

![Alt text](img/Lecture07/image-43.png)  

All these are handled by the operating system  

![Alt text](img/Lecture07/image-44.png)  

