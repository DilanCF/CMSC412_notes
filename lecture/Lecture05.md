# CMSC412 Lecture 5  
> 9-12  

## Structures    

We will discuss basic concepts and further details  

*Today*: Operating systems structures  

Main purpose is to isolate HW from users and provide capabilities that users can, er, use  

![Alt text](img/Lecture05/image.png)  

Batch interface: System that executes a large set of commands via a pipeline  
* Comes from earlier days of computing  

One of the major things for users is to perform IO  

Can we write a program that has no IO?  
* Yesn't. Some IO can only be machine-readable  

![Alt text](img/Lecture05/image-1.png)

When we go to disk drives, sector-organized. We want to have some structure on top to make it more readable  

2 types of communication:
* Interprocess communication

How do we communicate with different processes? 
* Will go over later  

Processes have independent memory spaces  

Error detection: OS responsibility?  
* Yes and no. OS has to detect them, then depending on which program is running, either OS handles it or it provides facilities for it  

![Alt text](img/Lecture05/image-2.png)  

Users do not participate in resource allocation, it requests it  

Becomes an internal function of the OS  

Accounting is used for:  
* Servers (Keep track of which user uses how much)
* Diagnostic (Personal computer)  

Resources of system should only be used by those who are authorized to use it  

![Alt text](img/Lecture05/image-3.png)  

System call: Call by user process to make use of OS services  

![Alt text](img/Lecture05/image-4.png)  

![Alt text](img/Lecture05/image-5.png)  
> shell (NOT Bash!!)  

![Alt text](img/Lecture05/image-6.png)  

Desktop interface became more practical in the 80s  

![Alt text](img/Lecture05/image-7.png)  

![Alt text](img/Lecture05/image-8.png)  

Can we make direct system calls?  
* Yes, but we'd need to set a lot of things up, and APIs exist anyway  

![Alt text](img/Lecture05/image-9.png)  

How many system calls are here? ^  
* "Lots" -Agrawala, 2023  

![Alt text](img/Lecture05/image-10.png)  

![Alt text](img/Lecture05/image-11.png)  

Lots of system calls that may be used  

Few are reserved  

There is a number associated with the system call  
* Found in interrupt descriptor table  

![Alt text](img/Lecture05/image-12.png)  

![Alt text](img/Lecture05/image-13.png)  

Pros: 
* Passing pointer is more flexible, number of parameters found are according to the ones that correspond to the system call  

Cons:
* Passing params to register, finite amount of registers  

![Alt text](img/Lecture05/image-14.png)  

![Alt text](img/Lecture05/image-15.png)  

Has to allow these kinds of processes to be made  

Dump memory  

![Alt text](img/Lecture05/image-16.png)  

![Alt text](img/Lecture05/image-17.png)  

Share memory?
* Special provisions must be made by the OS to make this happen
* Will discuss this later  

![Alt text](img/Lecture05/image-18.png)  

![Alt text](img/Lecture05/image-19.png)  

![Alt text](img/Lecture05/image-20.png)  

![Alt text](img/Lecture05/image-21.png)  

When the execution is completed, control goes back to shell  

![Alt text](img/Lecture05/image-22.png)

BSD: Berkley Software Distribution  

![Alt text](img/Lecture05/image-23.png)  

![Alt text](img/Lecture05/image-24.png)  

Registry: Store a lot of configs and other information  
* Entries in the registry can be up to the 100s of thousands  

![Alt text](img/Lecture05/image-25.png)  

![Alt text](img/Lecture05/image-26.png)  

![Alt text](img/Lecture05/image-27.png)  

![Alt text](img/Lecture05/image-28.png)  

![Alt text](img/Lecture05/image-29.png)  

Biggest difficulties come from background compatibility  

![Alt text](img/Lecture05/image-30.png)  

Some codes that will be run often need to be optimized as much as possible. Therefore, must be written in assembly  

Porting: MOving from one OS system to the other  

![Alt text](img/Lecture05/image-31.png)  

![Alt text](img/Lecture05/image-32.png)  

Even though this is layered, all levels have access to the BIOS  

![Alt text](img/Lecture05/image-33.png)  

![Alt text](img/Lecture05/image-34.png)  

![Alt text](img/Lecture05/image-35.png)  

![Alt text](img/Lecture05/image-36.png)  

![Alt text](img/Lecture05/image-37.png)  

We have microkernel for method-passing  

![Alt text](img/Lecture05/image-38.png)  

![Alt text](img/Lecture05/image-39.png)  

![Alt text](img/Lecture05/image-40.png)  

![Alt text](img/Lecture05/image-41.png)  

![Alt text](img/Lecture05/image-42.png)  

![Alt text](img/Lecture05/image-43.png)  

![Alt text](img/Lecture05/image-44.png)  

![Alt text](img/Lecture05/image-45.png)  

How do we figure out which processes is taking up the most resources?  
* We can do profiling to find out where we are taking the most time  

![Alt text](img/Lecture05/image-46.png)  

Bottlenecks does not let other processes run  

![Alt text](img/Lecture05/image-47.png)  

![Alt text](img/Lecture05/image-48.png)  

![Alt text](img/Lecture05/image-49.png)  

SYSGEN: Customizes the version of the OS that supports the HW supplied  

