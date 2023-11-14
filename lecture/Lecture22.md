# CMSC412 Lecture 22  
> 11-14  

## File systems 2: The Squeakquel 

![Alt text](img/Lecture22/image-1.png)  

What IS a file?
* Logical storage unit that is primarily user defined  

Structure that we impose on the data that we want to store for a long time  

How to organize it, how to store it, etc.  

We typically organize these things into a collection  
* Called directory or file folders  

One of the simplest things we must do is to find the file  
* Must give it a symbolic name
* Self-descriptive  
  * Program should then be able to find it on secondary storage
* Based on symbolic name, should be able to find the particular file  

Does using folders help?
* Depends on convention used when naming files
  * File names must be unique  

One way in which to organize it to have convention for all file names  

Collection of files in directory that keeps track of what files are in there
* Must be abele to search directory 
* Create
* Read
* etc. (See slide ^)

![Alt text](img/Lecture22/image-2.png)  

![Alt text](img/Lecture22/image-3.png)  

Have directory that is for all users 

How do we know that the file name is unique system wide as a user?  
* Sol: 2 lvl

![Alt text](img/Lecture22/image-4.png)  

![Alt text](img/Lecture22/image-5.png)  

Go even further beyond  

Start naming files after the path name  

![Alt text](img/Lecture22/image-6.png)  

Curren directory concept useful in order to make programs portable 
* As you use the programs, and change directories, you can still access the files relative to the current files ???

![Alt text](img/Lecture22/image-7.png)  

![Alt text](img/Lecture22/image-8.png)  

Why have multiple names?  
* Have multiple users make changes on the same directory  ???

![Alt text](img/Lecture22/image-9.png)  

We are introducing another dir. entry type  

![Alt text](img/Lecture22/image-10.png)  

How many times would we need to cycle round with the name avi and book?  

Garbage collection can help avoid cycles  

![Alt text](img/Lecture22/image-11.png)  

![Alt text](img/Lecture22/image-12.png)  

With any volume, will have its own file system as a structure  

Will work with one overall file system at a mount point  

![Alt text](img/Lecture22/image-13.png)  

![Alt text](img/Lecture22/image-14.png)  

Sharing should be done in a controlled manner  

What kind of structures for controlled access to files would be the best?
* Should we be able to specify on user to user basis what they can do to the file that we own?

Keeping track and maintaining consistency become challenges  
* most extensive way to hav file control is to specify on each user basis
  * Called "Access control list"  

What are different access we can share with others?
* Read, R/W, exec only  

![Alt text](img/Lecture22/image-15.png)  

![Alt text](img/Lecture22/image-16.png)  

Must have failure modes for files systems  

All WWW ar stateless  
* Each request is stateless

![Alt text](img/Lecture22/image-17.png)  

For most of the cloud based storage systems, consistency is maintained transparently  

![Alt text](img/Lecture22/image-18.png)  

![Alt text](img/Lecture22/image-19.png)  

![Alt text](img/Lecture22/image-20.png)  

![Alt text](img/Lecture22/image-21.png)  

![Alt text](img/Lecture22/image-22.png)  

![Alt text](img/Lecture22/image-23.png) 

Now we are talking about the mechanisms to perform this  
* Want to do this transparently  

Any info about the file system must be on secondary storage  

Everything that is modified mus be put back without corruption of data  

![Alt text](img/Lecture22/image-24.png)  

![Alt text](img/Lecture22/image-25.png)  

![Alt text](img/Lecture22/image-26.png)  

Device controller: HW that carries out device driver commands  

Basic file system can retain certain copies in the buffers or caches and can supply them when needed  

![Alt text](img/Lecture22/image-27.png)  

This is a layered style for structure!!  

![Alt text](img/Lecture22/image-28.png)  

Standards specify how certain things should be built
* With them, any programs that follow the same standard will play nice with each other  

![Alt text](img/Lecture22/image-29.png)  

When any request comes in, there must be some part of it in memory  

![Alt text](img/Lecture22/image-30.png)  

Partition: Portion of disk that we treat as independent  

MBR: MAster boot record  

What does the disk look like? 
* Linear array of blocks  

![Alt text](img/Lecture22/image-31.png)  

![Alt text](img/Lecture22/image-32.png)  

FCB- File control block  

![Alt text](img/Lecture22/image-33.png)  

![Alt text](img/Lecture22/image-34.png)  

Can we, by bringing in information into memory, improve the system?
* For all systems, must open file that precede any file  

Need to check if file has been opened by somebody 
* Why do we need 2 per process open file tables?  
  * Done so since different processes may be accessing it sequentially ???  

Must all files have current location concept?  
* Vast majority of accesses to file are sequential  

Keep track of current location in file  

![Alt text](img/Lecture22/image-35.png)  

Must the entry in the system table also be deleted?
* Depends on who is using it
  * If any file closes it, the count of active users goes down  

![Alt text](img/Lecture22/image-36.png)  

![Alt text](img/Lecture22/image-37.png)  

![Alt text](img/Lecture22/image-38.png)  

![Alt text](img/Lecture22/image-39.png)  

![Alt text](img/Lecture22/image-40.png)  

Storing stuff contiguously benefits us when we read things sequentially  

![Alt text](img/Lecture22/image-41.png)  

![Alt text](img/Lecture22/image-42.png)  

![Alt text](img/Lecture22/image-43.png)  

External frag: Allocation scheme is cont., but space free is not contiguous 
* Of the space that isn't allocated to anything  

Internal frag: Unused space that has already been allocated to you

![Alt text](img/Lecture22/image-44.png)  

Do we really need to read each block to get to the next one?  
* Yes  

![Alt text](img/Lecture22/image-45.png)  

![Alt text](img/Lecture22/image-46.png)  

![Alt text](img/Lecture22/image-47.png)  

How big can we make this table?  
* Depends on the volume that we support  

WHatever is the number of blocks, we should use them  

![Alt text](img/Lecture22/image-48.png)  

![Alt text](img/Lecture22/image-49.png)  

![Alt text](img/Lecture22/image-50.png)  

![Alt text](img/Lecture22/image-51.png)  

Similar to 2 lvl paging  

![Alt text](img/Lecture22/image-52.png)  

![Alt text](img/Lecture22/image-53.png)  
