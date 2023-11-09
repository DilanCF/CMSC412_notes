# CMSC412 Lecture 17  
> 10-26  

## Virtual memory 2 electric boogalo
<sub>yeah i know i made that joke before kiss my ass</sub> 

![Alt text](img/Lecture16/image-28.png)  

Basic issue: page replacement algorithm  
* Ibjective: page access time is dependment on page fault rate  
  * Want to reduce this given same noumber of ages existing

We start with reference string that identifies page numbers  

Given algo, how will it act  

![Alt text](img/Lecture16/image-29.png)  

More memory, less page faults  

![Alt text](img/Lecture16/image-30.png)  

How to asses? 

There ar 3 page frames avaialable  

Anytime we need to roll in a page (replace) mark as page fault with star  

First 3 are all page faults since the frames are all empty at first  
* 4th is a page fault since 2 does not exist  
* We continue replacing the oldest number that exists within the frames until the reference string has been satisfied  

![Alt text](img/Lecture16/image-31.png)  

Anomaly of *FIFO* systems  

![Alt text](img/Lecture16/image-32.png)  

![Alt text](img/Lecture16/image-33.png)  

Here, we first have the 3 essential page faults. After this, we have 2 trying to butt in. Out of 7, 0, and 1, which one should be replaced?  

* 1 is used 12 steps away
* 0 is used after this step
* 7 is used 16 steps away  

Therefore, we'd replace 7, since we won't use it for a long time  

REMEMBER: This is merely a measure of how well your algorithm works, and cannot be implemented IRL (you cant see the future)

You continue, doing the same process whenever you encounter a page fault  

In the ref string,how many essential faults are there?  
* Determine how many different paes are there in page string
  * IN our example, there are 6 (0,1,2,3,4,7)
  * We MUST have a page fault for each of these (They have to be brought in for the first time at some time during all this)  

![Alt text](img/Lecture16/image-34.png)  

As we increase memory (page frames), we have the same amount of page faults or less  

![Alt text](img/Lecture16/image-35.png)  

First three are essential faults  

When 2 wants to join the party, we look through our frames and see when they were used  

* 1's frame was just used
* 0's frame was used 1 step ago
* 7's frame was used 2 steps ago  

Therefore, we replace with 7's frame  

We can therefore treat this as a stack, whereby we add the new number on the top, pushing the bottom one out if necessary  

Suppose we had 4 page frames  
* We still maintain frame order  
* Pulling any new page on top  
  * If already there, put it on top  

If we have 2 instead of 3, what would the stacks look like?  
* No lol  
* All we are doing is changing the depth of the stack 
* By adding more frames, we only impact the bottom elements  
* This is why it results in equal or better performance only  

Where do we mainain this?   

![Alt text](img/Lecture16/image-36.png)  

![Alt text](img/Lecture16/image-37.png)  


I fell aslepp LUL
![Alt text](img/Lecture16/image-38.png)  

![Alt text](img/Lecture16/image-39.png)  

![Alt text](img/Lecture16/image-40.png)  

![Alt text](img/Lecture16/image-41.png)  

![Alt text](img/Lecture16/image-42.png)  

![Alt text](img/Lecture16/image-43.png)  

![Alt text](img/Lecture16/image-44.png)  

![Alt text](img/Lecture16/image-45.png)  

![Alt text](img/Lecture16/image-46.png)  

![Alt text](img/Lecture16/image-47.png)  

![Alt text](img/Lecture16/image-48.png)  

![Alt text](img/Lecture16/image-49.png)  

![Alt text](img/Lecture16/image-50.png)  

![Alt text](img/Lecture16/image-51.png)  

![Alt text](img/Lecture16/image-52.png)  

![Alt text](img/Lecture16/image-53.png)  

![Alt text](img/Lecture16/image-54.png)  

![Alt text](img/Lecture16/image-55.png)  

![Alt text](img/Lecture16/image-56.png)  

![Alt text](img/Lecture16/image-57.png)  

![Alt text](img/Lecture16/image-58.png)  

![Alt text](img/Lecture16/image-59.png)  

![Alt text](img/Lecture16/image-60.png)  

![Alt text](img/Lecture16/image-61.png)  

![Alt text](img/Lecture16/image-62.png)  

![Alt text](img/Lecture16/image-63.png)  

![Alt text](img/Lecture16/image-64.png)  

![Alt text](img/Lecture16/image-65.png)  

![Alt text](img/Lecture16/image-66.png)  

![Alt text](img/Lecture16/image-67.png)  

![Alt text](img/Lecture16/image-68.png)  

![Alt text](img/Lecture16/image-69.png)  

![Alt text](img/Lecture16/image-70.png)  

![Alt text](img/Lecture16/image-71.png)  

![Alt text](img/Lecture16/image-72.png)  

![Alt text](img/Lecture16/image-73.png)  

![Alt text](img/Lecture16/image-74.png)  

![Alt text](img/Lecture16/image-75.png)  

![Alt text](img/Lecture16/image-76.png)  

![Alt text](img/Lecture16/image-77.png)  

![Alt text](img/Lecture16/image-78.png)  

![Alt text](img/Lecture16/image-79.png)  

![Alt text](img/Lecture16/image-80.png)  

![Alt text](img/Lecture16/image-81.png)  

![Alt text](img/Lecture16/image-82.png)  

![Alt text](img/Lecture16/image-83.png)  

![Alt text](img/Lecture16/image-84.png)  

