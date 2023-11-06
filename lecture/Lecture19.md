# CMSC412 Lecture 16  
> 11-2  

## Secondary storage  


![Alt text](img/Lecture18/image-26.png)  

![Alt text](img/Lecture18/image-27.png)  

![Alt text](img/Lecture18/image-28.png)  

![Alt text](img/Lecture18/image-29.png)  

![Alt text](img/Lecture18/image-30.png)  

![Alt text](img/Lecture18/image-31.png)  

![Alt text](img/Lecture18/image-32.png)  

![Alt text](img/Lecture18/image-33.png)  

Picking up from last class  

We talked about the kind of structures thats disks have  

Number all the sectors as large, 1D arrays  

Say there is this view that is maintained  

First sector: Last sector  

Floppy disks had a hole that aligned with a cover that also had a hole  
* Used as reference  

In the same way, our disks have a "reference" for when memory starts
* Arbitrary  

Goal: Arrange things s/t contiguous things are reached quickly  

Most of the drivers we have will have bad sectors  
* Yield head crashes
  * When the head of the reader scratches the disk itself  
* Surface is not as smooth  

Three has to be a lower level formatting s/t the tracks are identified  

At the manufacturer, they have to decide how big the sectors are  

Header of each sector identified by the sector number  

Bad sectors have replacement sectors  

Not necessarily contiguous on the disk  

![Alt text](img/Lecture18/image-34.png)

How to issue command ot a specific device via scsi bus?
* Must have address field  

Everything is implemented in HW  

![Alt text](img/Lecture18/image-35.png)  

![Alt text](img/Lecture18/image-36.png)  

![Alt text](img/Lecture18/image-37.png)  

SAN typically fairly local
* Specialized for movement of information between servers  

Different communications for different purposes

![Alt text](img/Lecture18/image-38.png)  

Controller that has these protocols, we can make requests from anywhere  

??? 22~ in video

![Alt text](img/Lecture18/image-39.png)  

How is scheduling the disk different from the other scheduling we have done? 
* CPU scheduler, mem. scheduler, etc.  

Three components in any transfer

Goal: Make operations as fast as possible  

Rotational delay: how fast the disk is rotating  
* Scheduler cannot really impact this  

Accessing sector in sequence, ???  

Who controls whether we read sequentially or not?
* Program itself

We can control the seek time  

![Alt text](img/Lecture18/image-40.png)  

Any kind on optimization only makes sense with many requests  

Only time we can optimize anything is by reordering things around

![Alt text](img/Lecture18/image-41.png)  

Where does thi happen?  

Software based device driver  

^ Sequence of tracks we will access  

200 tracks  

In what order should we process them?

![Alt text](img/Lecture18/image-42.png)  

Min maxxing forsenInsanse

Minimize seek time  
* Unsuccessful here  

![Alt text](img/Lecture18/image-43.png)  

Pro: Start off quick, then slow down?  

Built in bias to addresses that are closer to the middle  

![Alt text](img/Lecture18/image-44.png)  

![Alt text](img/Lecture18/image-45.png)  

![Alt text](img/Lecture18/image-46.png)  



![Alt text](img/Lecture18/image-47.png)  

![Alt text](img/Lecture18/image-48.png)  

![Alt text](img/Lecture18/image-49.png)  

![Alt text](img/Lecture18/image-50.png)  

What can we do about the rotational delay?  
* Very difficult since we don't have the right information  

how much does the disk queueing impact OS performance?
* Higher level question  

![Alt text](img/Lecture18/image-51.png)  

Each sector has pre-defined size  

DIsk IO done in blocks  

File IO done in clusters  

![Alt text](image-1.png)

![Alt text](img/Lecture18/image-52.png)  

IO commands, instead of gong through file system, goes to controller
* May be beneficial in databases and such  

![Alt text](img/Lecture18/image-53.png)  

MBR: **M**aster **B**lock **R**ecord

Who does the drive numbering?
*BIOS  

BIOS keeps track of configuration and to where to go to get the boot partition in order to start the computer  

![Alt text](img/Lecture18/image-54.png)  

Where we keep the copy of the virtual memory space on secondary storage  

Swap space: We know a lot about the structure of the information coming in  
* Overwriting DN make sense  

![Alt text](img/Lecture18/image-55.png)  

RAID SHADOW LEGENDS!!!  

We have disk drives that are fairly inexpensive  
* Multiple drives can give us better reliability  

![Alt text](img/Lecture18/image-56.png)  

![Alt text](img/Lecture18/image-57.png)  

![Alt text](img/Lecture18/image-58.png)  

Automatic replication of data is common nowadays  

![Alt text](image-2.png)  

![Alt text](image-3.png) 

![Alt text](image-4.png)  

![Alt text](image-5.png)  

![Alt text](image-6.png)  

![Alt text](image-7.png)  

Make the update of this disk an atomic action  