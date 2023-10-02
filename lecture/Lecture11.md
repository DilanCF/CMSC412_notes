# CMSC412 Lecture 11  
> 10-3  

*Watching 2019 Panopto lecture*  

## Deadlocks  

*We already covered some of the first portion in the previous lecture, but I'm gonna start from the beginning anyways becaouse FYATHYRIO*  

![Alt text](image.png)  

Deadlocks occur when there are a colleciton of processes that cannot make progreess  

![Alt text](image-1.png)  

![Alt text](image-2.png)  

The model we work with ^  

We ask for resource, and wait for OS to give us resource  
* While we wait for that resource, we are in a queue  
* ewach recourse type has certain amount of instances  

By definiton, no one process will hold onto a resource forever  

In practice, this may happen though  

![Alt text](image-3.png)  

From here, we can see that the first mutex locks its mutex, and the other does the same for the second one. Then, each tries to get the others' lock. However, since they have each gotten the one that the other is trying to get, they get blocked waiting for the other to release their respective locks  

![Alt text](image-4.png)  

This one is called a "livelock" since the program does something constantly forever instead of waiting whilst being locked. Let's look at thread 1, where it locks `lock1`. Then, it tries to lock `lock2`. However, ~~bitch-ass~~ thread 2 already locked it, so the check that thread 1 does fails, and it goes to the else statement where it releases its first lock from the beginning. Since we are in a `while` loop, however, now ~~dumbass smooth brain~~ thread 1 tries it again , where it obviously fails again and again. The reason this is a livelock and NOT a deadlock is because the thread is actually doing something, its just not making any progress ![generating god seed](image-45.png).  

![Alt text](image-5.png)  

ALL of these must be held in order for deadlock to occur. If even one of these is not true, deadlock cannot occur

![Alt text](image-6.png)  

![Alt text](image-7.png)  

Individual instances of the resources are represented as mini squares in the bigger resource square  

When there is an edge from Process->Resource, that is a Request  

When there is an edge from Resource->Process, that is a Grant/Hold  

![Alt text](image-8.png)  

R<sub>2</sub> holds 2 instances of itself. R<sub>4</sub> holds 4 of itself. P<sub>1,2</sub> are both holding both of the instances of R<sub>2</sub>. P<sub>1</sub> resuests R<sub>1</sub> while R<sub>1</sub> itself is granting P<sub>2</sub>, which in turn is requesting R<sub>3</sub>, which in turn is granting P<sub>3</sub> *whew*.  

<sub>oh and also R<sub>4</sub> is all alone veri sed</sub>  

Note that, since there is no cycle in this graph, we can confidently say there is no deadlock possible. However, the inverese is NOT true.  
* If there is a cycle, there MAY or MAY NOT be a deadlock possible  

![Alt text](image-9.png)  

Here, we see that P<sub>1</sub> is waiting for R<sub>1</sub>, which is granting P<sub>2</sub>, which is waiting for R<sub>3</sub>, which is granting P<sub>3</sub>, which is waiting for R<sub>2</sub>, which is busy granting P<sub>1,2</sub>. Since both P<sub>1</sub> and P<sub>2</sub> are waiting for their respective resources, they are stuck, and we have deadlock.  

<sub>and R<sub>4</sub> is still all alone veri supa mega sed</sub>  

![Alt text](image-10.png)  

Here, we have another cycle. However, as aforementioned, this does not guarantee a deadlock. As we can see, P<sub>2</sub> has all it needs and releases R<sub>1</sub>, which in turn grants P<sub>1</sub>, freeing up an instance in R<sub>2</sub>, which in turn allows R<sub>2</sub> to grant P<sub>3</sub>'s request, and P<sub>4</sub> is completed and everyone is veri happi <sub>except for R<sub>4</sub> and R<sub>3</sub> who were killed offscreen apparently</sub>  

![Alt text](image-11.png)  

These explain how to find deadlocks in cyclic graphs

![Alt text](image-12.png)  

4 methods:  
1. Prevention
2. Aviodance
3. Allow & Recover
4. Ignore  

![Alt text](image-13.png)  

![Alt text](image-14.png)  

Making each of the reqs. for dealock false: 
* Mutual exclusion:
  * Make the resources sharable
  * Not possible in some cases (printer)
* Hold & Wait:
  * Try to do no hold & wait
  * Try to give process all the resources it needs at once before it executes
* No Preemption:
  * Make preemption to be true
  * Done using time time quantum method
  * Time Quantum Method: Allocate time to each process. When time is over, resources must be released  
* Circular wait:
  * Number all resources  

E.g: 
1. CPU
2. Printer
3. Scanner

   * Therefore, process can request resources in increasing order. If any process tries to request a #1 resource after requesting and being granted a #4 resource, it is ~~told to fuck off~~ not given the resource  


![Alt text](image-15.png)  

We dont guarantee prevention, we merely avoid it  

![Alt text](image-16.png)  

Essentially, what order can processes be done/ granted resources s/t everyone is completed AND there is no deadlock?
* This is what we need to answer to find the *safe state*  

![Alt text](image-17.png)  

![Alt text](image-18.png)  

Deadlock is only a subset of unsafe states. There could possibly be no deadlock yet we are in an unsafe state  

![Alt text](image-19.png)  

![Alt text](image-20.png)  

![Alt text](image-21.png)  

![Alt text](image-22.png)  

![Alt text](image-23.png)  

So, cycle != Guaranteed deadlock. HOWEVER, it is still possible for a deadlock to happen, and even more pertinent to this context, a cycle in the graph would mean that we are in an unsafe state *???*. Therefore, we want to avoid cycles at all costs  

![Alt text](image-24.png)  

I already did the walkthrough, and I p much understand what to do on pen and paper, so I don't really need to go through these :sunglasses:

![Alt text](image-25.png)  

![Alt text](image-26.png)  

![Alt text](image-27.png)  

![Alt text](image-28.png)  

![Alt text](image-29.png)  

![Alt text](image-30.png)  

**Im pretty sure there is a typo here, P<sub>2</sub> and P<sub>0</sub> need to be switched around since we go back and check in on P<sub>0</sub> after we finish with P<sub>4</sub>. Though it may be an arbitrary order, idk**

![Alt text](image-31.png)  

![Alt text](image-32.png)  

Avoidance: Make sure that a process is allocated resources only if doing so will not cause us to go to unsafe state  

![Alt text](image-33.png)  

This is NOT the same as a resource-allocation graph  

![Alt text](image-34.png)  

This ^ shows us that we have a deadlock, since we have a cycle: 

P<sub>1</sub>->P<sub>2</sub>->P<sub>3</sub>->P<sub>4</sub>->P<sub>1</sub>  

Note: This is only for single instance of resource

![Alt text](image-35.png)  

We need to do a slightly different version of the bankers algo.  

The main difference between Bankers and Detection is that in Banker's, we know beforehand the maximum resources that each process needs in order to function correctly. Based on the max and how many resources are avaliable, we determine if we can complete the i<sup>th</sup> process. If not, we continue untill enough resources are available to complete it. The detection algorithm works off of requests. IOW, we already have resources allocated (just like in Banker's), however we are asking for additional resources with no regard as to whether it is the max amount of resources that the particular process needs.  

![Alt text](image-36.png)  

![Alt text](image-37.png)  

![Alt text](image-38.png)  

![Alt text](image-39.png)  

![Alt text](image-40.png)  

![Alt text](image-41.png)  

![Alt text](image-42.png)  

