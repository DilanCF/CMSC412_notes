# CMSC412 Lecture 9  
> 9-25  

*Watching 2019 recordings*  

## Synchronization  

![Alt text](image.png)  

Synchronization: Many techniques  

Why?:  
* Whenever we are talking about any of the modern computer systems, thre are multiple concurrencies
* When they are seperate, esy to manage
* But nowadays, almost all of them are sharing resources  

KEy Idea:  
* Permits us, when writing progs, to have certanity they ill behave  

We want certain ocnditions to be followed  

Critical Seciton:  
* All processes share memory. We want to ensure that the memory is not changed without letting the rest of the processes know  
* Therefore, each process will have its own critical section, where no other process may enter  

The executions of critical sections is such that when one process is accessing it ???, it knows it is allowed into its critical section  

Knwon as Mutually Exclusive (Mutex)  

Atomic action:  
* Action is atomic means whatever action it is, it must be done *completely*, or it doesnt get done at all  

IN the middle of the execution of this action, it cannot be interrupted  

Why atmoic?:
* Updating memory

There are some architectures where updating is done via more than one instruction  

interrupts that come about are part of the execution of instruction  

ANy outside interrupts, CPU only checks for it at the end of said atomic action  

Executino of every instuciton at a machine level is atomic!  
* Some exceptions ofc  

For practical purposes, go with the assumption that a machine instruciton is atomic  

Many times, we want to do more complex things that require atomic actions  

![Alt text](image-1.png)  

We want to assure that the program is functioning correctly when writing programs  
* Proving correctness  

Dijkstra formulated the semaphore structure in 1962  

Code with flags, essentially  

Semaphore can only be accessed via `wait()` and `signal()` (P & V respectively)  

`wait()`:
```python
P(Semaphore S)
{
    while(S <= 0)
    ; // no operation
    S--;
}
```  

`signal()`:
```python
V(Semaphore S){
    S++;
}
```

![Alt text](image-2.png)  

When we are trying to do synch, we try to communicate that all the processes are done  

If in CS, we need to let the other processes know  

We have synch points for any process, to go past the synch point, certain conditions must be met  
* Depend on all other processes as well  

These are means of communicating with the set of processes that are using that semaphore at once

![Alt text](image-3.png)  

These can be used for various different things, not only memory  

Remember!: We are assuming P and V are implemented at a machine level, and are therefore atomic  

![Alt text](image-4.png)  

If we initialize S to n, n processes can have access to the critical section  

![Alt text](image-5.png)  
> Implementing S as a binary semaphore^  

![Alt text](image-6.png)  

![Alt text](image-7.png)  

![Alt text](image-8.png)  

Suspending means taking the CPU away from the process, put it on a queue  

This is done by the wait and signal  


![Alt text](image-9.png)  

[Good explanation for semaphore with no busy waiting](https://www.youtube.com/watch?v=_DAIgCgvog0&ab_channel=a-cube)

![Alt text](image-10.png)  

![Alt text](image-11.png)  

Always must have wait before signal

![Alt text](image-12.png)  

[Video](youtube.com/watch?v=ufdQ0GR855M&ab_channel=NesoAcademy)

![Alt text](image-13.png)  

![Alt text](image-14.png)  

![Alt text](image-15.png)  

![Alt text](image-16.png)  

![Alt text](image-17.png)  

![Alt text](image-18.png)  

![Alt text](image-19.png)  

![Alt text](image-20.png)  

![Alt text](image-21.png)  

![Alt text](image-22.png)  

