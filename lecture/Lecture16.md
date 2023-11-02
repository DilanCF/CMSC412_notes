# CMSC412 Lecture 16  
> 10-24  

## Virtual memory  

![Alt text](image-1.png)  

We have to recognize whats going on  

WHole program must be in memory  

If we make provision so tht without havnig whole program in mem @ exec, we could still crry on with execution of programs  

Starting point: Ability to execute partilly loaed programs

decouploing the address space that a program is structured in and the physical address space  

![Alt text](image-2.png)  

By mapping at runtime, can decouple the two 

WHy do we need logicla address space to be larger?  
* We as programmers need to facilitate any bloating that occurs  
* Typically, the demand we place we put on emmeory doubles every 3-5 years  
* OUr ablilty to have that much memory on phycisal hardware cannot keep up with demand  

Are we wasting this spce in virtaul memory space?  
* We are writing  in higher level language that is then translated to machine language
  * Adds overhead  
* Can always write smaller languages, but requires lower-level languages  

Raspberry Pi and Arduino have pretty large memories but still require tight code  

If wiritng in higher -lvl lagnuages is inefficietn, why do we sill use them?
* Human factor: human efficiency is important  

Whatever time we leave on the table is made up for in how well humans can write code thanks to modern programming languages  

![Alt text](image-3.png)  

Virtual address space: All that the compilers are dealing with  
* Address spaces

Everything is with respect to an address space  

We want to have an address sapce to bemappped in th end  

Maintainning tables is one way to do address translation  

What do we keep in memory?
* up to implementation  

![Alt text](image-4.png)  

Even when we are talking about virtual address sapc, it needs to exist somewhere
* USually secondary storage  

From which, whenever we needany part, we take it in  

The full copy of virtual memory space exists on the secondary storage  

We should be able to bring back in from secondary into physical emmory  

![Alt text](image-5.png)  

What wre we doing at the beginnnign?

Bring in entire process and swap entire space when we have a new process  

![Alt text](image-6.png)   

Shared in 2 virtaul address spaces  

SHared paces must be reentrant and occupy same spaces in virtual spaces  

![Alt text](image-7.png)  

When we do this kind of swapping, due to the address space needint to be contiguous, we could get external fragmentation  

Even though total amoun of free space is larger, since it is not contiguous, we cannot make use of it  

![Alt text](image-8.png)  

We load a page only when a reference to the page is made  

I/O to secondar storage is significantly slower  

When is a page needed?  
* When a reference is made to it  

Wht kind of address does the exec of a program require?
* Bring instruction in, operands, store operands in emmroy  

This instruction, while it is executing, try to get an operand 
* Operand not in operand? Cannot cnotinue  
  * Page fault occurs in the middle of execution  
* Must repeat instruction by rolling back state to the beginning of instruction

Interrupt detected in HW
* Done by the MMU  

***21:40***

![Alt text](image-9.png)  

![Alt text](image-10.png)  

![Alt text](image-11.png)  

![Alt text](image-12.png)  

![Alt text](image-13.png)  

![Alt text](image-14.png)  

![Alt text](image-15.png)  

![Alt text](image-16.png)  

![Alt text](image-17.png)  

![Alt text](image-18.png)  

![Alt text](image-19.png)  

![Alt text](image-20.png)  

![Alt text](image-21.png)  

![Alt text](image-22.png)  

![Alt text](image-23.png)  

![Alt text](image-24.png)  

![Alt text](image-25.png)  

![Alt text](image-26.png)  

![Alt text](image-27.png)  

![Alt text](image-28.png)  

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

![Alt text](image-77.png)  

![Alt text](image-78.png)  

![Alt text](image-79.png)  

![Alt text](image-80.png)  

![Alt text](image-81.png)  

![Alt text](image-82.png)  

![Alt text](image-83.png)  

![Alt text](image-84.png)  

