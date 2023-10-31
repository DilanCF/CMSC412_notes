# CMSC412 Lecture 13  
> 10-17  

*Watching March 28, 2019 Panopto lecture*  
**NOTE**: These notes will use the 2019 slides since the 2023 slides differ quite significantly from the recording. AKA didn't record the lecture properly last week 

## Memory Management  

![Alt text](img/Lecture14/image-1.png)  

![Alt text](img/Lecture14/image-2.png)  

![Alt text](img/Lecture14/image-3.png)  

When we are trying to design memory, what are we trying to achieve?  

Large address space: We don't want to be limited by the memory as programmers  
* For many decades, the programming and requirement doubles every year (Moores law)  

We can have HW that helps us reach these things  

Executing partially loaded programs since we don't have everything in main memory
* Can we really do this?
  * To exec an instruction, how much mem do we access?
    * Enough for the instruction possibly
  * We don't really care where the other parts are as long as we can access them when we need them
  * We need to do the memory management so we can load and unload from the secondary storage
  * ll the info of he memory space we have exists on the secondary storage  
The programs that we have written and the address spaces that we're operating in, any image of tht must be loaded into secondary

This is related to dynamic relocatability, where we need to be able to move stuff around when we need them.  
* Since we are trying to manage the finite real memory, we better be flexible!  

If we look at typical web server, how many concurrent requests may we handle?
* mUst we have separate copies of the code for the system to handle for each instance?  
  * Too big!

Need one copy everyone shares  

Called per-user code  

New tabs == new process, esp. with Chrome  

How to make the common code appear in both stacks? 
* This is the essence of sharing  

Protection means no ~~disintegrations~~ unauthorized actions  <sub>as you wish</sub>  

User's have exclusive rights over their memory, barring the OS  

![Alt text](img/Lecture14/image-4.png)  

![Alt text](img/Lecture14/image-5.png)  

![Alt text](img/Lecture14/image-6.png)  

The CPU has access only to the main memory and its local cache and registers  

For now, just assume all caches as the same, since they behave functionally the same, but with differing performances  

Protection must be done in HW  
* Must protect every access  

![Alt text](img/Lecture14/image-7.png)  

We have a base and limit register. IN the memory, we can have multiple processes
* Each process is given an address space
* slice of ech of the processes must be < real memory
* Whole process must stay in the memory  

The address space that the program sees goes from 0 to some number  

Each has a base register that helps us see the space for ech process  

The base addresses are offset from the space of the OS, and they are stored to the CPU  

Size of the request is less than the limit  

We can have the limits specified in the VM, or in the real space  

LImit reg: Test in Virtual address space. Must mke sure dress that we wish to issue is less than it  

![Alt text](img/Lecture14/image-8.png)  

Steps: 

1. CPU issues address
2. If addr. is greater than or equal to base, we continue
3. if the address is less than the base and the limit combined, then we can go to memory
4. Keep in mind the trap for addressing errors (too small, OOB, etc.)

![Alt text](img/Lecture14/image-9.png)  

This is all done in the VM for the particular process

Each binding maps one address space to the other  

A lot of this address space mapping goes on all the time  

![Alt text](img/Lecture14/image-10.png)  

Binding: Take any address and assign it to a particular address space  

Absolute code refers strictly to the virtual address space of the process

![Alt text](img/Lecture14/image-11.png)  

![Alt text](img/Lecture14/image-12.png)  

LOgical memory space is bound to separate physical memory space
* Key to memory management  

![Alt text](img/Lecture14/image-13.png)  

*Look up video on MMU*  

![Alt text](img/Lecture14/image-14.png)  

As long you are consistent, this is good to use  

DLLs that we have in Windows are OS libraries that help with this  

Suppose we were bringing in and dynamically linking code  

We locate it somewhere in the memory  

All we have is the relocation register pointing to its location to help us find it  

When we go to the DLL, once we have loaded it into memory, we just need the relocation register location to make it work  

![Alt text](img/Lecture14/image-15.png)  

![Alt text](img/Lecture14/image-16.png)  

![Alt text](img/Lecture14/image-17.png)  

Limited real space with large program?
* Overlays! 

A user implements this overlay, no special support from HW at all  

![Alt text](img/Lecture14/image-18.png)  

Backing store: Secondary storage (HDD, etc)  

Phys memory space can now surpass main memory  

We have to be able tyo take the image that is stored in memory, roll it out, and put a new one in  

![Alt text](img/Lecture14/image-19.png)  

Does the swapped...?
* If it was done at load time, will come back to physical addresses  

![Alt text](img/Lecture14/image-20.png)  

Swapping *can* be a time consuming process  

![Alt text](img/Lecture14/image-21.png)  

Context switch time can include the swapping time  


![Alt text](img/Lecture14/image-22.png)  

[Short video on 2x buffering](https://www.youtube.com/watch?v=qdeBmEnv_bI&ab_channel=CS186Berkeley)  

mem to mem copy, must have the space, and since we are copying to the kernel, the kernel will require the same amount of space as well  

![Alt text](img/Lecture14/image-23.png)  

![Alt text](img/Lecture14/image-24.png)  

If we have multiple processes, processor knows the start addresses and assigns spaces accordingly and contiguously  

![Alt text](img/Lecture14/image-25.png)  

![Alt text](img/Lecture14/image-26.png)  

![Alt text](img/Lecture14/image-27.png)  

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

![Alt text](img/Lecture14/image-28.png)  

![Alt text](img/Lecture14/image-29.png)  

Why would there be internal fragmentation?  
* Managing memory, we need to see the granularity we want to use  
  * byte by byte?

Larger the chunk we manage, the less details we keep track of  

We can easily split the address to describe the chunk number  

If we are going to organize a memory with 4k chunks, and we are given 4097 bytes, we will need 2 chunks  

The 4095 bytes contribute to the fragmentation  

Strict limit on internal frag if we are doing the alloc and mem management and can locate any available chunk with an address space  
* May be done with paging  

Limiting the maximum size of fragmentation to size of chunk  

![Alt text](img/Lecture14/image-30.png)  

We create pre-defined partitions at setup time. THis is how we do it if not done dynamically  

All swapping tht is done must be done with respect to the partition  

DMA: Direct Memory Access  

MOs of the devices have a device driver and controller  

TYpically, all IO controlled by OS in response to system calls made by processes  

Swapping generated by kernel itself  

Typically, 2 dominant types of IO we can do  

1. Programmed IO
   1. Only way we want to operate is to handle it through interrupts  
   2. Essential unit of transfer is byte or word  
   3. CPU supplies the address on the disk, and reding is done at a set amount of time 
   4. Request goes to dev controller, and if head is not at that cylinder, we move it
   5. Wait for sector to take it, read sector into buffer in the device control 
   6. Transfer information one word at a time
2. DMA
   1. Device onrolll sits on the same bus as the memory
   2. device controller can write directly to the memory
   3. Instead of asking for a single sector, can ask for bigger section of file
   4. can specify where in the memory this should be put
   5. Still need to specify location
   6. Device controller will read sector by sector, bring to buffer
   7. Since we have access to memory, we don't interrupt and write directly
   8. whn done, then we interrupt CPU  

When the device controller goes through memory, who is making the request?  
* Typically the CPU  

Stealing memory cycles from CPU  

In our case, when we say we need to latch it to the memory, we specify where this IO would bring things in  

![Alt text](img/Lecture14/image-31.png)  

Programs have ben bound to address space  
* Thought of as a continuous segment of space

Creating an executable image, we combine all them and fitting to address space at run time

Can treat each as a segment  

Treating the logical address space as a collection of segments  

Each has continuos space, but each is different form the other  

![Alt text](img/Lecture14/image-32.png)  

All of these are now much closer to ach other  

![Alt text](img/Lecture14/image-33.png)  

![Alt text](img/Lecture14/image-34.png)  

Changing logical vew of address space  

![Alt text](img/Lecture14/image-35.png)  

In the previous archs, for large programs, large chunks  

My segment abel has an entry for that segment, etc.  

![Alt text](img/Lecture14/image-36.png)  

![Alt text](img/Lecture14/image-37.png)  

![Alt text](img/Lecture14/image-38.png)  

Segmentation supports sharing  

![Alt text](img/Lecture14/image-39.png)  

![Alt text](img/Lecture14/image-40.png)  

![Alt text](img/Lecture14/image-41.png)  

![Alt text](img/Lecture14/image-42.png)  

![Alt text](img/Lecture14/image-43.png)  

![Alt text](img/Lecture14/image-44.png)  

![Alt text](img/Lecture14/image-45.png)  

![Alt text](img/Lecture14/image-46.png)  

![Alt text](img/Lecture14/image-47.png)  

![Alt text](img/Lecture14/image-48.png)  

![Alt text](img/Lecture14/image-49.png)  

![Alt text](img/Lecture14/image-50.png)  

![Alt text](img/Lecture14/image-51.png)  

![Alt text](img/Lecture14/image-52.png)  

![Alt text](img/Lecture14/image-53.png)  

![Alt text](img/Lecture14/image-54.png)  

![Alt text](img/Lecture14/image-55.png)  

![Alt text](img/Lecture14/image-56.png)  

![Alt text](img/Lecture14/image-57.png)  

![Alt text](img/Lecture14/image-58.png)  

![Alt text](img/Lecture14/image-59.png)  

![Alt text](img/Lecture14/image-60.png)  

![Alt text](img/Lecture14/image-61.png)  

![Alt text](img/Lecture14/image-62.png)  

![Alt text](img/Lecture14/image-63.png)  

![Alt text](img/Lecture14/image-64.png)  

![Alt text](img/Lecture14/image-65.png)  

![Alt text](img/Lecture14/image-66.png)  

![Alt text](img/Lecture14/image-67.png)  

![Alt text](img/Lecture14/image-68.png)  

![Alt text](img/Lecture14/image-69.png)  

![Alt text](img/Lecture14/image-70.png)  

![Alt text](img/Lecture14/image-71.png)  

![Alt text](img/Lecture14/image-72.png)  

![Alt text](img/Lecture14/image-73.png)  

![Alt text](img/Lecture14/image-74.png)  

![Alt text](img/Lecture14/image-75.png)  

![Alt text](img/Lecture14/image-76.png)  

