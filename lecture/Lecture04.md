# CMSC412 Lecture 4  
> 9-7  

## Geek OS  

*Today*: Compact overview of GeekOS  

![Alt text](img/Lecture04/image.png)  

![Alt text](img/Lecture04/image-1.png)  

APIC: ... Interrupt controller  

4 CPUs that have a shared bus. Bus moves the bits around. If an interrupt needs to be moved from one CPU to the other, use the bus  

*Remember*: INterrupt == HW  

How does a CPU know an interrupt on the bus is its own?  
* Bus has to have address lines. That way, if interrupt is in CPU0's address, CPU0 knows it has an interrupt   

diskc: kernel image, functioning in virtual environment  

![Alt text](img/Lecture04/image-2.png)  

Protected mode can only be reached *from* user mode  
* Has 4 privilege levels  

![Alt text](img/Lecture04/image-3.png)  

What do segment descriptor tables contain? 
* Global and local descriptor tables  
* Interrupt descriptor table  

Segment descriptor points to a segment with starting point and  

![Alt text](img/Lecture04/image-4.png)  

IDT: Int. desc. table  
* Has 256 entries, one for each interrupt  

INterrupt gate points to int. handler  

![Alt text](img/Lecture04/image-5.png)  

All general purpose registers are 32 bits in GeekOS  

eflag contains current state of execution  

![Alt text](img/Lecture04/image-6.png)  

Disable/restore interrupts 
* There are certain functions that we carry out that we don't want to stop in the middle of process  

![Alt text](img/Lecture04/image-7.png)  

Calibration: Ensure all have the same value  

Allocating CPU to process, allocate for fixed amount of time. Based on number of CPU ticks  

![Alt text](img/Lecture04/image-8.png)  

![Alt text](img/Lecture04/image-9.png)  

Supports are specified, and are accessed by IO instr  

![Alt text](img/Lecture04/image-10.png)  

Keyboard data is used as input  

No output to the keyboard, therefore no output register  

![Alt text](img/Lecture04/image-11.png)  

Keyboard must just send characters at any key pressed  

![Alt text](img/Lecture04/image-12.png)  

IDE is essentially a bus. Used to transfer data  

Whatever we transfer is 16b  

PIO: Programmed Input Output  

DMA: Direct Memory Access  

Cylinder? Head? ~~So no head?~~  
* Will discuss later in semester  

![Alt text](img/Lecture04/image-13.png)  

Device driver does the conversion  

![Alt text](img/Lecture04/image-14.png)  

Will not be using DMA too much  

![Alt text](img/Lecture04/image-15.png)  

During setup, interrupts are handled by the BIOS  

Change to OS of CPU

![Alt text](img/Lecture04/image-16.png)  

![Alt text](img/Lecture04/image-17.png)  

GPF: General Protection Fault  

![Alt text](img/Lecture04/image-18.png)  

![Alt text](img/Lecture04/image-19.png)  

mutex: Mutual Exclusion  

![Alt text](img/Lecture04/image-20.png)  

![Alt text](img/Lecture04/image-21.png)  

![Alt text](image-22.png)  

![Alt text](image-23.png)  

![Alt text](image-24.png)  

UC: User context  

We are trying to create an image that, when called with run, will execute  

User SS: Stack Segment  

![Alt text](img/Lecture04/image-25.png)  

User process does not have access to the kernel space. Therefore, must have process that can call something in the kernel *???* (Slide 31)  

![Alt text](img/Lecture04/image-26.png)  

We want program to run in a deterministic manner  

Many mechanisms for this require OS support  

Atomic action *???*  

If, due to Atomic action, there are instructions we cannot execute. We need to wait. How?  
* Spinlock  

![Alt text](img/Lecture04/image-27.png)  

We are waiting for the eax (GPR) to become 0. Once it is, we turn it to 1  

![Alt text](img/Lecture04/image-28.png)  

![Alt text](img/Lecture04/image-29.png)  

![Alt text](img/Lecture04/image-30.png)  

Mutual exclusion *???*  

![Alt text](img/Lecture04/image-31.png)  

![Alt text](img/Lecture04/image-32.png)  

WDYM by switch?  
* Switch of a task  

Kernel task, user task, wtc. 

What happens at scheduling? 

Why would an incomplete thread give up the CPU?  
* May be waiting on something  

Low-lvl interrupt handling  

![Alt text](img/Lecture04/image-33.png)  

![Alt text](img/Lecture04/image-34.png)  

How long will this ^ take?  
* Ans: very Fast (TM)  

![Alt text](img/Lecture04/image-35.png)  

VFS: Virtual File System  

![Alt text](img/Lecture04/image-36.png)  

How often do we use direct access?  

Sequential is the most common way of reading files  

![Alt text](img/Lecture04/image-37.png)  

![Alt text](img/Lecture04/image-38.png)  

Specify the path and the mode we will be accessing the file  

FIle systems are collections of directories  

![Alt text](img/Lecture04/image-39.png)  

![Alt text](img/Lecture04/image-40.png)  

![Alt text](img/Lecture04/image-41.png)  

![Alt text](img/Lecture04/image-42.png)  

FAT: File Allocation Table  

![Alt text](img/Lecture04/image-43.png)  

![Alt text](img/Lecture04/image-44.png)  

![Alt text](img/Lecture04/image-45.png)  

![Alt text](img/Lecture04/image-46.png)  

![Alt text](img/Lecture04/image-47.png)  

![Alt text](img/Lecture04/image-48.png)  

![Alt text](img/Lecture04/image-49.png)  

![Alt text](img/Lecture04/image-50.png)  

![Alt text](img/Lecture04/image-51.png)  

Where does this notify exec operate?  
* Whoever made the request, i.e the user
* However, it does not go to the user, instead to the OS  

![Alt text](img/Lecture04/image-52.png)  

Cache: Memory that can store data that can be trickled down to slower devices  

![Alt text](img/Lecture04/image-53.png)  

![Alt text](img/Lecture04/image-54.png)  