# CMSC412 Lecture 3  
> 9-5  

## X-86 Architecture  

*Last time*:  
Basic functions of the CPU  

*Today*:  
Take CPU details for the CPU we will use in this class (x86)  

ONe thing we did not talk about was the memory from last time  

![Alt text](img/Lecture03/image.png)  

The manufacturer decides the size of memory  

Each cell in the array has a specific address  

The integer becomes 

Access to a system memory is one at a time  

Who accesses the memory?
* Applications  

Memory controller to which an address is sent via a bus or comm. method  

How many bits req.? 
* All mem structs have integer power of 2 number of cells
* 2^n cells, # bits = n  

Access is made presenting n bits and RW flag  

Also need to specify what needs to be written in memory cell  

![Alt text](img/Lecture03/image-1.png)  

Can treat each cell as independent  

Take logical view: contiguous blocks of 2^k cells and name it a block  

Take address and split in 2: Block number and displacement within block  

Read address space in this way  

Block size != power of 2, divide by block size and look at quotient  

**Important ^^^**  

Mapping of address spaces  

![Alt text](img/Lecture03/image-2.png)  

Why? 
* Assign addresses for subroutines  

The essential req. for mapping is given address A in space A, must find a unique address in B   

Even cell sizes may be different with proper mapping  
* For now, 4-byte cell sizes  

4 GB mem, how many cells are there?  
How many bits of memory will I require?  
* 30 bit address  

Map every address to every unique address  

![Alt text](img/Lecture03/image-3.png)  

With this, can simply use lookup able  

Reducing size of this table, use blocks  

Use mapping of every block as a contiguous block  

This means the displacement does not change  

Address space is a virtual concept. Must be mapped to physical in order to be used  

**This is a general mapping concept!!**  

The better you know how the details work, the better programmer you will be  
> AA, 2023  

Most of the latest archs are backwards compatible  

![Alt text](img/Lecture03/image-4.png)  

![Alt text](img/Lecture03/image-5.png)  

CPU has to have many registers (GPR) 
* Registers instructions typically use  

There is a flag register, may keep something about the state, etc.  

Machine must have instruction counter  

E- prefix: 32 bits  
* If not, 16 bits  

Segment reg  

Any time something goes to memory, starts at the higher space and grows down   
* Our prerogative 
What you can do in HW is much faster than in SW  
* SW has instructions, thus slowing it down  

![Alt text](img/Lecture03/image-6.png)  

![Alt text](img/Lecture03/image-7.png)  

2 Levels of translation:  
* Segmentation and translation (paging)  

Anytime you write any program, Logical->physical space is done by hardware  

Doing the translation has a page table, converts to page table  

We are translating from virtual to linear , from linear to physical space  

The logical space has segments and offset  

The two sides don't have to be same size when doing mapping  

Take logical address and convert to linear address as a 32b unsigned int  

Then we get physical address  

![Alt text](img/Lecture03/image-8.png)  

![Alt text](img/Lecture03/image-9.png)  

Lower the number, higher the privilege  

![Alt text](img/Lecture03/image-10.png)  

Here ^, we see the structure of various registers  

![Alt text](img/Lecture03/image-11.png)  

![Alt text](img/Lecture03/image-12.png)  

GDTR, LDTR point to start of each table  

![Alt text](img/Lecture03/image-13.png)  

![Alt text](img/Lecture03/image-14.png)  

Each executing can have up to 6 registers  *???*  

We take these addresses and mapping them  

![Alt text](img/Lecture03/image-15.png)  

GDT, LDT- Global and Local Descriptor Table  

INdex into table pointed by GDTR and LDTR  

![Alt text](img/Lecture03/image-16.png)  

![Alt text](img/Lecture03/image-17.png)  

The interrupt enable flag can be set to 0 or 1 to enable/disable interrupts  
* Many of these bits are set by the hardware  

![Alt text](img/Lecture03/image-18.png)  

![Alt text](img/Lecture03/image-19.png)  

Going back, 3 tables highlighted. These are the registers that control these  

![Alt text](img/Lecture03/image-20.png)  

Page directory: Directory that translated pages to page block *???*  

Page number to page frame
![Alt text](img/Lecture03/image-21.png)  

![Alt text](img/Lecture03/image-22.png)  

![Alt text](img/Lecture03/image-23.png)  

Paging: Linear -> Physical  

![Alt text](img/Lecture03/image-24.png)  

Remember: logical address has segment and offset  

Lin. addr is 32 bits, divided in 3. (Dir, table, off)  

Bits in offset depends on size of page (4k, 4Meg)  

Going to 22 bit size, table is ignored. 4k = 12 bits for offset, table becomes 10 bits  

All of this happens in HW for every access in memory  
* This is why we use bit arithmetic instead of traditional (Schoolbook) arithmetic  

Anything coming from the registers must be very fast  

Linear address is 32 bits  

![Alt text](img/Lecture03/image-25.png)  

Segment has certain amount of bits  

![Alt text](img/Lecture03/image-26.png)  

GDT is common among all. Local is not. Local must change with each new segment  

![Alt text](img/Lecture03/image-27.png)  

Segment limit is arbitrary  

P bit- Segment is absent?? 
* No, means its not in the memory, it is not initialized  
* OS has to come in and adjust as needed  

![Alt text](img/Lecture03/image-28.png)  

![Alt text](img/Lecture03/image-29.png)  

HW does addressing differently based on size  

Most of these ^ are set by hardware  

![Alt text](img/Lecture03/image-30.png)  

![Alt text](img/Lecture03/image-31.png)  

![Alt text](img/Lecture03/image-32.png)  

System call: activates again. Call to a call gate can call a procedure  
* In doing this, privileges are checked  

![Alt text](img/Lecture03/image-33.png)  

![Alt text](img/Lecture03/image-34.png)  

![Alt text](img/Lecture03/image-35.png)  

![Alt text](img/Lecture03/image-36.png)  

![Alt text](img/Lecture03/image-37.png)  

Non-maskable: Cannot disable them (embedded opcode, exceptions, etc.)  

![Alt text](img/Lecture03/image-38.png)  

![Alt text](img/Lecture03/image-39.png)  

Amount of time between interrupts: 1/2 ms  

![Alt text](img/Lecture03/image-40.png)  

![Alt text](img/Lecture03/image-41.png)  

![Alt text](img/Lecture03/image-42.png)  

Current state of any task is captured here in the Task State Segment (Slide 52)  

![Alt text](img/Lecture03/image-43.png)  

![Alt text](img/Lecture03/image-44.png)  

![Alt text](img/Lecture03/image-45.png)  

Task == Process  

![Alt text](img/Lecture03/image-46.png)  

![Alt text](img/Lecture03/image-47.png)  

![Alt text](img/Lecture03/image-48.png)  

![Alt text](img/Lecture03/image-49.png)  

![Alt text](img/Lecture03/image-50.png)  

![Alt text](img/Lecture03/image-51.png)  

![Alt text](img/Lecture03/image-52.png)  




























































I hecking LOVE when professors fly through slides and read off the slides verbatim for half the class!!!!!