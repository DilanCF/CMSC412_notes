# CMSC412 Lecture 8  
> 9-21  

## Synchronization  

*No slides?*  
<img src=img/Lecture08/bitchless.png alt="drawing" width="200"/>

System consists of objects AND activities

Act>: Executional programs

Property of objects:
* Safety
  * Concern at many levels
  * security and protection
  * modifying things

Property of activity
* Liveness
  * Levels: messages
  * Will a prog execute?  

Violating safety
* scheduler can interleave or overlap threads 
  * Leads to storage corruption
  * violation of representation invariant
  * violation of protocol
    * Protocol: set of rules

![Alt text](img/Lecture08/image.png)  


![Alt text](img/Lecture08/image-1.png)  

Processes are independent, how can they share resources?
* Sharing CPU, memory, etc.  

These are essential for systematic function of computer  

Shared resources  

Responsibility of OS to protect these resources  
* Must be done in SW, there is a lot of information to handle

When something is done in HW, we do not carry it out in execution in Fetch decode exec system
* Ex. Memory setup  

Provides processes way to protect their own abstractions

Producer-consumer problem:
* 2 threads, one makes, one takes
* buffer in between

![Alt text](img/Lecture08/image-2.png)  

![Alt text](img/Lecture08/image-3.png)  

![Alt text](img/Lecture08/image-4.png)  

![Alt text](img/Lecture08/image-5.png)  
> Buffer from slides ^  

If counter is shared, we may get racing conditions  

![Alt text](img/Lecture08/image-6.png)  

![Alt text](img/Lecture08/image-7.png)  

![Alt text](img/Lecture08/image-8.png)  

![Alt text](img/Lecture08/image-9.png)  

![Alt text](img/Lecture08/image-10.png)  

But what happens when I run it again?  

![Alt text](img/Lecture08/image-11.png)  

![Alt text](img/Lecture08/image-12.png)  

![Alt text](img/Lecture08/image-13.png)  

![Alt text](img/Lecture08/image-14.png)  

![Alt text](img/Lecture08/image-15.png)  

![Alt text](img/Lecture08/image-16.png)  

Racing: Depending on the order in which you type stuff, you get different things for each execution  

Is copying an atomic action?
* ye lol  

Very rare that you interrupt something during instruction  

exec. of instruction is atomic  
* Counterpoint: divide by zero, improper opcode, stack smashing  

IN paging, we'll see how opcode goes to an address that is not available  

We don't want to make this visible to the program at all!  

How avoid this?
* Save state as it was before the start of instr
* Interrupt
* Resume

Still technically atomic  

From our example, we want this to be atomic  

Schedulers are time-dependent, and are therefore hard to debug  

![Alt text](img/Lecture08/image-17.png)  

But we run into the same issue!  

Question: If you run program with race condition, will you *Always* get unexpected result?

![Alt text](img/Lecture08/image-18.png)  


How to solve this issue?  
Answer:  
![Alt text](img/Lecture08/image-19.png)  

What interrupts can we not disable?  
* Hardware, firmware, stuff that goes through HW  

![Alt text](img/Lecture08/image-20.png)  

Mutex: Mutually exclusive  

Waiting for mutexes happens in the wait queue  

![Alt text](img/Lecture08/image-21.png)  

We have to make sure the mutex is atomic in order to ensure that nothing gets interrupted during the mutex init and stuff  

![Alt text](img/Lecture08/image-22.png)  

![Alt text](img/Lecture08/image-23.png)  

![Alt text](img/Lecture08/image-24.png)  

![Alt text](img/Lecture08/image-25.png)  

![Alt text](img/Lecture08/image-26.png)

![Alt text](img/Lecture08/image-27.png) 

![Alt text](img/Lecture08/image-28.png)  

![Alt text](img/Lecture08/image-29.png)  

![Alt text](img/Lecture08/image-30.png)  

Make sure CS is performed in a mutually exclusive manner  

How large can an atomic action be?  
* No limit on it  

If every thread has 100k CS, everyone will need to wait for it  

![Alt text](img/Lecture08/image-31.png)  

![Alt text](img/Lecture08/image-32.png)  

![Alt text](img/Lecture08/image-33.png)  

We run 2 threads, running synch. Will we get problems?  
* If T1 wants to block on A, but T2 has it, we run into deadlock  

![Alt text](img/Lecture08/image-34.png)  

Not easy to detect  

![Alt text](img/Lecture08/image-35.png)  

![Alt text](img/Lecture08/image-36.png)  

What often happens is that we get a cycle, as seen here ^

![Alt text](img/Lecture08/image-37.png)  

Must b executed in an atomic manner  

No other thread may enter during CS  

![Alt text](img/Lecture08/image-38.png)  

![Alt text](img/Lecture08/image-39.png)  

![Alt text](img/Lecture08/image-40.png)  

![Alt text](img/Lecture08/image-41.png)  

![Alt text](img/Lecture08/image-42.png)  
> May show up in exams!! ^  

![Alt text](img/Lecture08/image-43.png)  

![Alt text](img/Lecture08/image-44.png)  

![Alt text](img/Lecture08/image-45.png)  
> Combines 1 & 2  

![Alt text](img/Lecture08/image-46.png)  

![Alt text](img/Lecture08/image-47.png)  

![Alt text](img/Lecture08/image-48.png)  

![Alt text](img/Lecture08/image-49.png)  

If we have N processes, before entering CS, every process gets a number (akin to a bakery)  

![Alt text](img/Lecture08/image-50.png)  

![Alt text](img/Lecture08/image-51.png)  

Does the bakery algorithm work?
* ye lol  

Appropriate safety measure have been taken for this  

Theses are for a centralized method for shared memory  

Have glossed over other details  

![Alt text](img/Lecture08/image-52.png)  

![Alt text](img/Lecture08/image-53.png)  

![Alt text](img/Lecture08/image-54.png)  

![Alt text](img/Lecture08/image-55.png)  

![Alt text](img/Lecture08/image-56.png)  

![Alt text](img/Lecture08/image-57.png)  

![Alt text](img/Lecture08/image-58.png)  

![Alt text](img/Lecture08/image-59.png)  

