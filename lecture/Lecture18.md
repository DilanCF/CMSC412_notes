# CMSC412 Lecture 18  
> 10-31  

## Virtual Memory

Fundamental notion:  Being able to map an address space to any other
* Given N address and an address space, must be able to map to another one
* If not available, must have mechanism to get it from a different place (Secondary storage)
  * May also store in main memory?
  * Commercial operating systems: more complexity  
  * Why is RL messier than examples in textbook?
    * Environment that our system will be in is unknown 
      * User, programs to be run, etc.
    * Must have a General Purpose solution

For a commercial system, a virtual memory system, must decide:
* Segmentation? Paging? Both?
* Page size?
* Page fault policy?
* ASOASF

Also need to consider HW support  

Windows page size: 12b or 32b  
* Wanted to see that the intel HW supports this kind of environment  

Say we decide paging, segmentation or no?  

* Segmentation comes down to HW support and ???  

![Alt text](img/Lecture18-19/image-59.png)

In most of these things, make the page size == page on disk or sector on disk ???  

Concerned with how to handle pages!!  

Swapping: Take out all pages alloc to a process and put it in storage to free space up for other processes  

![Alt text](img/Lecture18-19/image-60.png)

Pageout daemon and works like clock algo
* For each page, we support one extra bit  

When paging out, just put it on a free page list
* Do not change contents!
* If e get a reference to it, jst find it in list  

![Alt text](img/Lecture18-19/image-61.png)

Say the machine has 32MB of memory
* what number of free pages? Portion of memory for free pages?
* Determined by `lotsfree`
  * How big is `lotsfree`?
    * 1/3 at first, ???

![Alt text](img/Lecture18-19/image-62.png)

![Alt text](img/Lecture18-19/image-1.png) 

Overloaded: Too many page faults  
* Swapping avoid us entering thrashing condition!  

So much paging done that ??? becomes low  

![Alt text](img/Lecture18-19/image-2.png)  

![Alt text](img/Lecture18-19/image-3.png)  

Based on 4.3 UNIX  

![Alt text](img/Lecture18-19/image-4.png)  

*Look this up*  

The primary ach on which this was implemented was ???

HW did not provide modified bit. Why?
* we dunno lol  

![Alt text](img/Lecture18-19/image-5.png)  

![Alt text](img/Lecture18-19/image-6.png)  

Instead of just getting page that the default is on, we get some more along with it ???

![Alt text](img/Lecture18-19/image-7.png)  

![Alt text](img/Lecture18-19/image-8.png)  


## Mass Storage

![Alt text](img/Lecture18-19/image-9.png)  

So far, we have talked about CPU and memory, etc.  

The complete addr. space has to be somewhere

Since we cant have large main memory, we must have secondary storage  

Having offline ones

Magnetic disks remain "dominant" for the past few decades
* Secondary because hey are not connected to the CPU ???  

In order to read or write, must remain under the head  

![Alt text](img/Lecture18-19/image-10.png)  

![Alt text](img/Lecture18-19/image-11.png)  

![Alt text](img/Lecture18-19/image-12.png)  

![Alt text](img/Lecture18-19/image-13.png)  

How long does it tak to go over the track?  
* Seek time

???
* Rotation delay
  * Max can be the time it takes to rotate once, min once

![Alt text](img/Lecture18-19/image-14.png)  

![Alt text](img/Lecture18-19/image-15.png)  

![Alt text](img/Lecture18-19/image-16.png)  

![Alt text](img/Lecture18-19/image-17.png)  

![Alt text](img/Lecture18-19/image-18.png)  

![Alt text](img/Lecture18-19/image-19.png)  

![Alt text](img/Lecture18-19/image-20.png)  

![Alt text](img/Lecture18-19/image-21.png)  
Can we do better than just estimating averages?
* Only if we know where everything is beforehand  

Transfer time depends on where we are making transfer from  

These days, most disk drives have their own cache
* Whenever you request sector, whole track copy is stored in the cache  

![Alt text](img/Lecture18-19/image-22.png)  

What does solid state mean?
* Solid state parts: No electromechanical movement 
* Made to be plug n' play  

![Alt text](img/Lecture18-19/image-23.png)  

![Alt text](img/Lecture18-19/image-24.png)  

100TB drives not as popular due to failure rate  

SSD have limited read write capability  

![Alt text](img/Lecture18-19/image-25.png)  

![Alt text](img/Lecture18-19/image-26.png)  

![Alt text](img/Lecture18-19/image-27.png)  

![Alt text](img/Lecture18-19/image-28.png)  

![Alt text](img/Lecture18-19/image-29.png)  

![Alt text](img/Lecture18-19/image-30.png)  

![Alt text](img/Lecture18-19/image-31.png)  

![Alt text](img/Lecture18-19/image-32.png)  

![Alt text](img/Lecture18-19/image-33.png)  

![Alt text](img/Lecture18-19/image-34.png)  

![Alt text](img/Lecture18-19/image-35.png)  

![Alt text](img/Lecture18/image-36.png)  

![Alt text](img/Lecture18/image-37.png)  

![Alt text](img/Lecture18/image-38.png)  

![Alt text](img/Lecture18/image-39.png)  

![Alt text](img/Lecture18/image-40.png)  

![Alt text](img/Lecture18/image-41.png)  

![Alt text](img/Lecture18/image-42.png)  

![Alt text](img/Lecture18/image-43.png)  

![Alt text](img/Lecture18/image-44.png)  

![Alt text](img/Lecture18/image-45.png)  

![Alt text](img/Lecture18/image-46.png)  

![Alt text](img/Lecture18/image-47.png)  

![Alt text](img/Lecture18/image-48.png)  

![Alt text](img/Lecture18/image-49.png)  

![Alt text](img/Lecture18/image-50.png)  

![Alt text](img/Lecture18/image-51.png)  

![Alt text](img/Lecture18/image-52.png)  

![Alt text](img/Lecture18/image-53.png)  

![Alt text](img/Lecture18/image-54.png)  

![Alt text](img/Lecture18/image-55.png)  

![Alt text](img/Lecture18/image-56.png)  

![Alt text](img/Lecture18/image-57.png)  

![Alt text](img/Lecture18/image-58.png)  

