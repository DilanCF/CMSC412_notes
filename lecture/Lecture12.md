# CMSC412 Lecture 12  
> 10-10  

*Watching March 12, 2019 Panopto lecture*  

## CPU Scheduling  

![Alt text](img/Lecture12/image-1.png)  

Managing states and budgeting processes  

Before: Threads. Now, we assume that we are managing processes  

Any process in ifs lifetime goes through certain states  
* Ready
  * A Process has recieved all recsources except for CPU 
  * In ready queue   
* Running 
  * In the running queue
  * No process in running state ever?
    * Yes, interrupt, deciding which process to give control
    * Apart from that, there is only one process per CPU
    * Kernel is not considered a process, and does not need to be scheduled
  * What can happen?
    * Complete process and go to terminated
    * Interrupt comes in and cpntrol is taken away
      * From here, go to ready state until control is given back OR, if IO needed, go to waiting ASOASF
* Terminated
  * Restore state of process

Scheduling means 
* Selecting a procss in a ready queue
  * This is a policy question
  * Do many tjhings (May be done atomically)
* Decide on a time quantum (if applicable)
* Restore the ame state of the process
  * When in reayd, this states remains in GPR (General purpose registers)  
* Change IC 

Typically, a process is gonig trhough this V loop  

![Alt text](img/Lecture12/image-2.png)  

We throuhg this ^ loop of bursts, running and waiting constantly  

Everytime we come into ready state, then to running, how long can we run until we need to wait to IO?
* Assume no interrupts

Typically, can talk of CPU burst as time a process can use the CPU  
IO burst is the IO request we make  

During IO, we go to the outside devices which are much slower than the CPU  

We get into waiting state and wait for longer times than CPU cycles  
* Inherently IO will take longer  

Depending on application one burst will dominate the other  
* ^ Computations, ^ CPU bursts
* ^ Device handling, ^ IO bursts  

Word processing
* IO bound  
  * While doing this, backgorund processes are displaying characters, GUI, etc.

Weather app
* CPU bound
* Many sensors, a lot of data that needs to be processes  

Buisness app
* IO bound
  * Ledgers, book keeping  

IRL, most processes are IO bound  

![Alt text](img/Lecture12/image-3.png)  

Burst in miliseconds is very small. Most burst lie less than 8 miliseconds  

![Alt text](img/Lecture12/image-4.png)  

Which one is selected depends on algo, queue order, etc.  

When would the scheduler come into effect?  
* When a process is running and goes into waiting state  

Scheduler needs to come in when the process relinquishes control  

1 and 4 are the voluntary actions  

Preemptive  
* WHenever, whatever you are doing, you are forced to stop  
* Comes from outside source ???


![Alt text](img/Lecture12/image-5.png)  

Dispatcher comes in to perform these ^ operations  

There is no saved PC value! What do?  
* Start with PC value that th entry point was when we started the scheduler  

If, in between, there is an interrupt, it is not a part of the dispatch latency  

WHat should a policy try to achieve?  
* WHen we are selecting a process to exec next, we should try to keep the smallest time  
* We want to keep our devices as busy as possible

Keep in mind the kind of env. where this technology was made
* Shared kernel with one mainframe  
* Based on CPU usage, people were charged
* Turnaround time  

All these things influence how we implement things / how things are done today  

![Alt text](img/Lecture12/image-6.png)  

*He starts to draw on a board that I can't see in the video :(*  

![Alt text](img/Lecture12/image-7.png)  

Observation: Every one of these has to do with TIME  

![Alt text](img/Lecture12/image-8.png)  

Naive approach: First come first serve  

Here, we are concerned with how long each process spends in the waiting queue  

FCFS is the fairest since the burst times are still the same

![Alt text](img/Lecture12/image-9.png)  

Now, if we order it from shortest to longest task, average waiting times decrease dramatically  

![Alt text](img/Lecture12/image-10.png)  

Asking the user does not work, since user either does not know length or lies to gain priority  

![Alt text](img/Lecture12/image-11.png)  

![Alt text](img/Lecture12/image-12.png)  

SJF is a nonpreemptive process  
* Assume that, once we are given CPU, we involuntarily relinquish it ???

We can monitor how long the previous bursts were and predict the next one from this  

Predict next CPU burst on previous and an exponential averaging  

if alpha is 0, tn does not make a difference, recent history does not matter ???  

SJF, assume all jobs given, and giving control of CPU to jobs in defined order, not taking any away.  
* If new job arrives:
  * Take away controol from currntly running job and give to new job  

![Alt text](img/Lecture12/image-13.png)  

Last bullet is why we call it exponential  

![Alt text](img/Lecture12/image-14.png)  

![Alt text](img/Lecture12/image-15.png)  

*Look up a video on this ^ or sumn*

![Alt text](img/Lecture12/image-16.png)  

If a new process comes in and has higher priortiy, preempt and do the new one  

IN the SRTF, it is a preemptive process.  

Priority is either preemp or non preemp 

SJF cannot be preemptive ???

![Alt text](img/Lecture12/image-17.png)  

Assume that all of these came all at once.  Lower the number, higher the priority  

Even though P4 had the lowest length, also had lowest priority, thus we do it last  

![Alt text](img/Lecture12/image-18.png)  

*Video lookup*  

* Bunch of processes in ready queue  
* Take one, giv CPU for quantum time
  * Did not finish in time due to interurpt
* Continue regardless, putting it into the back of the queue  

This ensures that each process gets the same amount of time  

![Alt text](img/Lecture12/image-19.png)  

![Alt text](img/Lecture12/image-20.png)  

*Video from March 12 stops here*

![Alt text](img/Lecture12/image-21.png)  

![Alt text](img/Lecture12/image-22.png)  

![Alt text](img/Lecture12/image-23.png)  

![Alt text](img/Lecture12/image-24.png)  

![Alt text](img/Lecture12/image-25.png)  

![Alt text](img/Lecture12/image-26.png)  

![Alt text](img/Lecture12/image-27.png)  

![Alt text](img/Lecture12/image-28.png)  

![Alt text](img/Lecture12/image-29.png)  

![Alt text](img/Lecture12/image-30.png)  

![Alt text](img/Lecture12/image-31.png)  

![Alt text](img/Lecture12/image-32.png)  

![Alt text](img/Lecture12/image-33.png)  

![Alt text](img/Lecture12/image-34.png)  

![Alt text](img/Lecture12/image-35.png)  

![Alt text](img/Lecture12/image-36.png)  

![Alt text](img/Lecture12/image-37.png)  

![Alt text](img/Lecture12/image-38.png)  

![Alt text](img/Lecture12/image-39.png)  

![Alt text](img/Lecture12/image-40.png)  

![Alt text](img/Lecture12/image-41.png)  

![Alt text](img/Lecture12/image-42.png)  

![Alt text](img/Lecture12/image-43.png)  

![Alt text](img/Lecture12/image-44.png)  

![Alt text](img/Lecture12/image-45.png)  

![Alt text](img/Lecture12/image-46.png)  

![Alt text](img/Lecture12/image-47.png)  

![Alt text](img/Lecture12/image-48.png)  

![Alt text](img/Lecture12/image-49.png)  

![Alt text](img/Lecture12/image-50.png)  

![Alt text](img/Lecture12/image-51.png)  

![Alt text](img/Lecture12/image-52.png)  

![Alt text](img/Lecture12/image-53.png)  

![Alt text](img/Lecture12/image-54.png)  

![Alt text](img/Lecture12/image-55.png)  

![Alt text](img/Lecture12/image-56.png)  

![Alt text](img/Lecture12/image-57.png)  

![Alt text](img/Lecture12/image-58.png)  

![Alt text](img/Lecture12/image-59.png)  

![Alt text](img/Lecture12/image-60.png)  

![Alt text](img/Lecture12/image-61.png)  

![Alt text](img/Lecture12/image-62.png)  

![Alt text](img/Lecture12/image-63.png)  

![Alt text](img/Lecture12/image-64.png)  

![Alt text](img/Lecture12/image-65.png)  

![Alt text](img/Lecture12/image-66.png)  

![Alt text](img/Lecture12/image-67.png)  

![Alt text](img/Lecture12/image-68.png)  

![Alt text](img/Lecture12/image-69.png)  

![Alt text](img/Lecture12/image-70.png)  

![Alt text](img/Lecture12/image-71.png)  

![Alt text](img/Lecture12/image-72.png)  

![Alt text](img/Lecture12/image-73.png)  