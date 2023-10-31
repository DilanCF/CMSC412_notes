# CMSC412 Lecture 13  
> 10-17  

*Watching March 28, 2019 Panopto lecture*  
**NOTE**: These notes will use the 2019 slides since the 2023 slides differ quite significantly from the recording. AKA didn't record the lecture properly last week 

## Memory Management  

![Alt text](image-1.png)  

![Alt text](image-2.png)  

![Alt text](image-3.png)  

When we are trying to design memory, what are we trying to achieve?  

Large address sapce: We dont want to be limited by the memory as programmers  
* For many decades, the programming and requirement doubles every year (Moores law)  

We can have HW that helps us reach these things  

Executing partially loaded programs since we don't have everything in main memory
* Can we really do this?
  * To exec an instruction, ho much mem do we access?
    * Enough for the intruction possibly
  * We dont really care where the other parts are as long as we can access them when we need them
  * We need to do the memory mnagement so we can load and unload from the secondary torage
  * ll the info of he memory space we have exists on the secondary storage  
The programs that we have written and the address spaces that we're operating in, any image of tht must be loaded into secondary

This is realted to dynamic relocatability, where we need to be able to move stuff around when we need them.  
* Since we are trying to manage the finite real memory, we better be flexible!  

If we look at typical webserver, how many concurrent requests may we handle?
* mUst we have seperate copeis of the code for the systme to handle for each instance?  
  * Too big!

Need one copy everyone shares  

Called per-user code  

New tabs == new process, esp. with Chrome  

How to make the common code appear in both stacks? 
* This is the essence of sharing  

Protection means no ~~disintegrations~~ unauthorized actions  <sub>as you wish</sub>  

User's have exclusive rights over their memory, barring the OS  


![Alt text](image-4.png)  

![Alt text](image-5.png)  

![Alt text](image-6.png)  

The CPU has access only to the main memory and its local cache and registers  

For now, just assume all chaches as the same, since they behave functionally the same, but with differing performances  

Protection must be done in HW  
* Must procect every access  

![Alt text](image-7.png)  

We have a base and limit register. IN the memory, we can have multiple processes
* Each process is given an address space
* slice of ech of the proceses must be < real memory
* Whole process must stay in the memory  

The address space that the program sees goes from 0 to some number  

Each has a base register that helps us see the space for ech process  

The base addresses are offset from the space of the OS, and they are stored to the CPU  

Size of the request is less than the limit  

We can have the limits specified in the VM, or in the real space  

LImit reg: Test in Virtual address space. Must mke sure dress that we wish to issue is less than it  

![Alt text](image-8.png)  

Steps: 

1. CPU issues address
2. If addr. is greater than or equal to base, we continue
3. if the address is less than the base and the limit combined, then we can go to memory
4. Keep in mind the trap for addressing errors (too small, OOB, etc.)

![Alt text](image-9.png)  

This is all done in the VM for the particular process

Each binding maps one address space to the other  

A lot of this address space mapping goes on all the time  

![Alt text](image-10.png)  

Binding: Take any addrress and asign it to a particular addres space  

Absolute code refers strictly to the virtual address space of the process

![Alt text](image-11.png)  

![Alt text](image-12.png)  

LOgical memory space is boundd to seperate physical memory space
* Key to memory mnagement  

![Alt text](image-13.png)  

*Look up video on MMU*  

![Alt text](image-14.png)  

As long you are consistent, this is good to use  

DLLs that we have in Windows are OS ibraries that help with this  

Suppose we were bringing in and dynamically linking code  

We locte it somewhere in the memory  

All we have is the relocatoin register pointing to its location to help us find it  

When we go to the DLL, once we have loaded it into memory, we just need the relocation register location to make it work  

![Alt text](image-15.png)  

![Alt text](image-16.png)  

![Alt text](image-17.png)  

Limited real space with large program?
* Overlays! 

A user implements this overlay, no special support from HW at all  

![Alt text](image-18.png)  

Backing store: Secondary sorage (HDD, etc)  

Phys memory space can now surpass main memory  

***28:58***

we have to be able tyo take the image that is stored in memory, roll it out, and put a new one in  

![Alt text](image-19.png)  

Does the swapped...?
* If it was done at load time, will come back to physical addresses  

![Alt text](image-20.png)  

Swapping *can* be a time consuming process  

![Alt text](image-21.png)  

Context switch time can include the swapping time  


![Alt text](image-22.png)  

[Short video on 2x buffering](https://www.youtube.com/watch?v=qdeBmEnv_bI&ab_channel=CS186Berkeley)  

mem to mem copy, must have the space, and since we are copying to the kernel, the kernel will require the same amount of space as well  

![Alt text](image-23.png)  

![Alt text](image-24.png)  

If we have multiple processes, processor knows the start addresses and assigns spaces accordingly and contiguously  

![Alt text](image-25.png)  

![Alt text](image-26.png)  

![Alt text](image-27.png)  

Hole continues to change  

Say at the end of this chart, process 9 ends. We now have 2 spaces free, but not contiguous. In order to remedy this, we'd need to do a memory to memory move  

We want to make sure the holes we have are as large as possible ;)  

For allocated spaces we need to keep track of
* Process it belongs to
* Beginning address
* Limit (?)  

For holes we need to keep track of
* Beginning
* Size  

With 10 holes, how do we choose where to allocate?
* First hole that is more than the size, then allocate  
* Keep the holes ordered by size and find best fit
* " and find worst fit  

What are we trying to do?
* Avoid mem->mem move
* Biggest holes  

Therefore worst fit is best (acc. to Prof, but video below doesn't line up with that, so who tf knows)   

[Video on First vs Best vs Worst Fit](https://www.youtube.com/watch?v=HBQZ5rlaN-s&ab_channel=ShrutiP)

![Alt text](image-28.png)  

***46:42***

![Alt text](image-29.png)  

![Alt text](image-30.png)  

![Alt text](image-31.png)  

![Alt text](image-32.png)  

![Alt text](image-33.png)  

![Alt text](image-34.png)  

![Alt text](image-35.png)  

![Alt text](image-36.png)  

![Alt text](image-37.png)  

![Alt text](image-38.png)  

![Alt text](image-39.png)  

![Alt text](image-40.png)  

![Alt text](image-41.png)  

![Alt text](image-42.png)  

![Alt text](image-43.png)  

![Alt text](image-44.png)  

![Alt text](image-45.png)  

![Alt text](image-46.png)  

![Alt text](image-47.png)  

![Alt text](image-48.png)  

![Alt text](image-49.png)  

![Alt text](image-50.png)  

![Alt text](image-51.png)  

![Alt text](image-52.png)  

![Alt text](image-53.png)  

![Alt text](image-54.png)  

![Alt text](image-55.png)  

![Alt text](image-56.png)  

![Alt text](image-57.png)  

![Alt text](image-58.png)  

![Alt text](image-59.png)  

![Alt text](image-60.png)  

![Alt text](image-61.png)  

![Alt text](image-62.png)  

![Alt text](image-63.png)  

![Alt text](image-64.png)  

![Alt text](image-65.png)  

![Alt text](image-66.png)  

![Alt text](image-67.png)  

![Alt text](image-68.png)  

![Alt text](image-69.png)  

![Alt text](image-70.png)  

![Alt text](image-71.png)  

![Alt text](image-72.png)  

![Alt text](image-73.png)  

![Alt text](image-74.png)  

![Alt text](image-75.png)  

![Alt text](image-76.png)  

