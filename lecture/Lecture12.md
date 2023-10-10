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

We throuhg this &#8593 loop of 

![Alt text](img/Lecture12/image-3.png)  

![Alt text](img/Lecture12/image-4.png)  

![Alt text](img/Lecture12/image-5.png)  

![Alt text](img/Lecture12/image-6.png)  

![Alt text](img/Lecture12/image-7.png)  

![Alt text](img/Lecture12/image-8.png)  

![Alt text](img/Lecture12/image-9.png)  

![Alt text](img/Lecture12/image-10.png)  

![Alt text](img/Lecture12/image-11.png)  

![Alt text](img/Lecture12/image-12.png)  

![Alt text](img/Lecture12/image-13.png)  

![Alt text](img/Lecture12/image-14.png)  

![Alt text](img/Lecture12/image-15.png)  

![Alt text](img/Lecture12/image-16.png)  

![Alt text](img/Lecture12/image-17.png)  

![Alt text](img/Lecture12/image-18.png)  

![Alt text](img/Lecture12/image-19.png)  

![Alt text](img/Lecture12/image-20.png)  

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