Due not next monday but monday after next  

Fork: what it do?  

In UNIX:  

1 process, then a tree of processes  

OS for fork and exit  

Process contol block: all relevant info about a process  

Has user context and kernel thread structure *???*  

Process has:  
* PID
* File Descriptor Table
* Registers
* Memory space
  * Local Desc. Table (dont worry about it)
  * Memory
* Kernel stack
* ESP (POints at bottom of kernel stack)  

Kernel stack: 
* ???

When creating new process, need to copy over: 
* FDT (need to modify slightly)
  * Make sure we have a reference count number
  * Modify close so only edit FDT when no more references to it *???*  
* Registers (part of kernel stack)
* LDT (has base address of local, not copied!!)
* Content of memory
* Kernel stack
* Kernel ESP will be different, but in same *relative* space  

Exec: 
* PID
* FDT
* Registers (x)
* LDT (x)
* Memory (x)
* Kernel stack (x)
* ESP kernel (x)  

Threads share memory space, processes have their own  

PCB  
* Data struct in OS comtaining info needed to manage process
  * Needed for scheduling, etc.  

struct UserContext (user.h)  
* Mem. 

Kernel Thread

Pointer Interrupt_State ~= ESP  

When making a child thread, should it be detatched?  
* No, needs to be attatched to keep tree intact. That way, parent knows it has a child  




Using mutex

Put a lock on an increment to make it atomic  

```

mutex_lock 

what we wish to lock

mutex_unlock

```  

sys_fork() slide has it 

Use interrupt_state instead Current_thread
* Other stuff may be in it
* Using curr_thread only works if fork returns w/o being interrupted, which is impossible  

Sys_exec()
* spawn() has some good tips  

File reference count needs to be locked! 


lookup_thread() for how to go through all threads for sys_exit  

close()
* 


Need to find a location for reference count  
* do this in vfs  

Recommended order to start
* fork()
* exec()
* exit()