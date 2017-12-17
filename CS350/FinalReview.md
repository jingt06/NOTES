#CS350 Final Review

##I/O

- A device driver interacts with a device by reading/writing to the device's command, status and data registers
- For example: Sending data to an output device (polling)
   - Write data to the device's data register
   - Write "output" command to the device's command register
   - keep reading the device's status register until it is "completed"
   - Reset the status register so it can send the next piece of data
- Polling is not always desirable (why: waist CPU cycles when waiting for the devices complete.)

DMA (using Interrupt)

- Device can instead raise an interrupt when it is finished with the comamnd

1. save PC andd PC reset to exception handler
2. switchs CPU to kernel mode (prevledged mode)
3. save thread context on trap frame
4. calls mips\_trap, determines it is interrupt or syscall or excpetion
5. (if it is interrupt) call interrupt handler an it determines which devices fires the interrupt

###Accessing devices

- Special I/O instructions (x86)
- Memory-mapped I/O
   - Device registers have a memory address
   - Use standard "load" to read data from a device, and "store" to write data to devices 

### Direct Memory Access
- The "load" instruction read data one word at a time
   - This can be slow if we are trying to transfer a large amount of data
   - Also requires CPU to perform the transfer
-  **Direct Memory Access** (DMA) is a method to allow a separate controller to transfer data between a device and memory
   - DMA controller becomes bus master and performs the dta transfer on behalf of the CPUs
   - Instead of writing data into the data register, write the source/destination memory address into the address register     

(why not combine DMA and CPU polling: DMA will handle all data transfer, no need for cpu polling any more, otherwise it will cause conflict) 


####Disk 
- **Service time** is the sum of
   - **Seek time**: Moving the disk head to the right track/cylinder
   - **Rotational Latency**: Waiting until the sector spins to disk head
   - **Transfer time**: wait until all of the 

   
#### Disk Head Scheduling

- FCFS: no optimization but fair and no starvation
- SSTF (shortest seek time first): starvs but faster
- elevator: in between

#### Scheduling

- Want to minimize turnaround time
   - Arrival time
   - Run time
   - Start time
   - Finish time
- Turnaround time: f - a
- Response time: s - a

#### CPU scheduling

- Thread arrives when it is ready
- Runtime is the amount of time a thread runs until it blocks or finishes
- We can estimate a threads runtime by determining its tendency to block
   - A thread that blocks often is likely an interactive thread and has short runtiem
   - A thread that doesnt bloc ksi likely a computationally intensive thread with a long runtime
   - Sohuld we assign higher priority to interactive or non-interactive thread?
- **Multi-Level Feedback Queue** 
   - Assigns a priority level to a thread based on its previous behaviour
   - Possible problem: starvation, solution: periodically move low priority process to high high priority process queue

#### Multi-Core Scheduling
- Queue per core first  single ready queue
- Contention and Scalability
- Cache affinity
- Load imbalance


##File Systems

- File
  - Identified by an i-number
  - An i-numberis the index to an i-node array
-  i-node
  - Stores meta-information about the file
     - File type,permissions,length,last modified, etc.
  - Stores block pointers (direct/indirect block pointers)
- Bitmap nodes
  - Stores the availability of i-nodes and data blocks
- Super block
  - Meta-infomation of the entire file system( Number of inodes, whre the inode blocks begin, etc)   

- Given a file offset, know how to determine which block pointer must be accessed ot determine the block location
- Understand desgin decisions for a particular file system
   - Why not just have indirect pointers?
   - In what situations is an indexed file system more appropriate than a chained file system? 
- How are directories implemented
   - hard link vs soft link
   - referential integrity

- Given a file (/foo/bar), know all of the inodes/data block in order to open/read the file.


#Study your assignments
- Given a panic outpu, can you determine the cause of the error?