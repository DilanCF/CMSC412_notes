# CMSC412 Lecture 13  
> 10-19  

*Watching October 19, 2023 Panopto lecture*  
**NOTE**: This lecture more or less picks up at the tail of the 2019 lecture, there may be some slides that are not covered here since they were already covered last time

## Memory Management 2 <sub>electric boogaloo</sub>  

Basic concept: We manipulate address spaces all the time!  

Mapping of addr space fomr one to other happens as we go along at many differen tplaces

translating one addr to another
* As long as we get a new unique addr for th one we are trying to convert, thats all that matters

Carry on till exec time  

Adress translatoin important!  

Need the mechanism  

Program preperation: Mapping done in sftware  

Runtime: Teansaltion done using HW  

addr trans: Address treated as individual binary number and contents are the word of the info coming throuhg  

Translation table: We are seeing one base and one limit register
* May have more  
* Ppoint a pointer to it

![Alt text](img/Lecture15/image-33.png)  

We have a bunch of modules and the lanbuage prep parts are treatong each module independently

If there are refecences outside of the modules, they are left as symbolic addresses (module, name, etc.)

runtime: everythingm must be resolved  
* All addresses must be resolved to some memory location

Can we retain this sructure througught?  

![Alt text](img/Lecture15/image-34.png)  

Must we create this linear address space map prior or at execution?  

Normally, prior  
* BY the time we reach execution, we reached linkage editor, references, assigned spaces in linear array, etc.  

BUT, can we do this at runtime?
* What will it take?  

We have to identify the address as 2 parts
1. Segment ID
2. Location in segment

Assume all within-segment IDs start at 0  

![Alt text](img/Lecture15/image-35.png)  

Many parts to a program  

Treat each as an independent segment  

Makes easer to manage  

![Alt text](img/Lecture15/image-36.png)  

Whatever the address space is, it is 2D  

Many segments with code within them  
* Linear arrays  

Key limiting factor is the ability to translate them  

![Alt text](img/Lecture15/image-37.png)  

Logical -> physical  

Each seg. contigous  

![Alt text](img/Lecture15/image-38.png)  

This translation is  process by process system  

![Alt text](img/Lecture15/image-39.png)  

Can we carry out address translation now?  
* NO
* Need the mechanism that finds the segment table and check s < STLR, then add the offset  

Code-sahring: Segment level 
* If provisions done  

Fit the whole segment space of different processes
* Now, fit addr. space of one process but multiple segments  

![Alt text](img/Lecture15/image-40.png)  

![Alt text](img/Lecture15/image-41.png)  

For a processes logcial address space, thet are mapped to phys address space at different locaiton and kept teack of in a segment table  

![Alt text](img/Lecture15/image-42.png)

one way: common editor, want to make sure no process has acces to any other process
* Specifically, all data kept in different segment  
* Reentrant code: No self modifying instrucitnos, DNH temporary data

If we have a single copy of editor, will the address trnas go properly?  
* must have seperate address table  

Depending on which of the two processes is in control, relevant segment table will be used  

Addr. for modufyable portion is in the data portion  

Must every segment of my process be resident @ exec time?  
* No

If we are executing in seg.1 and using memory in seg. 2 at one time, we dont care about the rest of the segments 

![Alt text](img/Lecture15/image-43.png)  

![Alt text](img/Lecture15/image-44.png)  

![Alt text](img/Lecture15/image-45.png)  

![Alt text](img/Lecture15/image-46.png)  

![Alt text](img/Lecture15/image-47.png)  

![Alt text](img/Lecture15/image-48.png)  

![Alt text](img/Lecture15/image-49.png)  

![Alt text](img/Lecture15/image-50.png)  

![Alt text](img/Lecture15/image-51.png)  

![Alt text](img/Lecture15/image-52.png)  

![Alt text](img/Lecture15/image-53.png)  

![Alt text](img/Lecture15/image-54.png)  

![Alt text](img/Lecture15/image-55.png)  

![Alt text](img/Lecture15/image-56.png)  

![Alt text](img/Lecture15/image-57.png)  

![Alt text](img/Lecture15/image-58.png)  

![Alt text](img/Lecture15/image-59.png)  

![Alt text](img/Lecture15/image-60.png)  

![Alt text](img/Lecture15/image-61.png)  

![Alt text](img/Lecture15/image-62.png)  

![Alt text](img/Lecture15/image-63.png)  

![Alt text](img/Lecture15/image-64.png)  

![Alt text](img/Lecture15/image-65.png)  

![Alt text](img/Lecture15/image-66.png)  

![Alt text](img/Lecture15/image-67.png)  

![Alt text](img/Lecture15/image-68.png)  

![Alt text](img/Lecture15/image-69.png)  

![Alt text](img/Lecture15/image-70.png)  

![Alt text](img/Lecture15/image-71.png)  

![Alt text](img/Lecture15/image-72.png)  

![Alt text](img/Lecture15/image-73.png)  

![Alt text](img/Lecture15/image-74.png)  

![Alt text](img/Lecture15/image-75.png)  

![Alt text](img/Lecture15/image-76.png)  

![Alt text](img/Lecture15/image-77.png)  

![Alt text](img/Lecture15/image-78.png)  

![Alt text](img/Lecture15/image-79.png)  

![Alt text](img/Lecture15/image-80.png)  

![Alt text](img/Lecture15/image-81.png)  
