1 . A system uses **physical address** and **virtual addresses**. How many physical address spaces are there in a computer? How many virtual address spaces?

- One physical address space per machine and one virtual address space per process

2 . What is a simple method of address translation? How does this work? What are tis disadvantages?

- Dynamic relocation. 
- phyiscal address = paddr base(reloaction register) + virtual address.
- Disadvantagegs: external fragment.

3 .  In **dynamic relocation**, when does the value of the relocation register in MMU change?

- during each address switch (context switch to a thread of a different process)

4 . What are three algorithms that can be used to find an allocation space? Why whould anyone ever want to use the worst fit algorithm.

- worst fit, best fit, first fit.

5 . What is the difference between **external fragmentation** and **internal fragmentation**?

- External fragmentation are unused wasted memory outside of the allocated areas of memory, usually caused by dynamic relocation. Internal fragmentation are unused memory inside the allocated block of memory, usually caused by paging.

6 . What advantages does **paging** give over **dynamic relocation**?

- solve external fragentation problem (virtual address space need not to be physically contiguous in pysical address space) and it is a easy memory management by the kernel. 
- (**disadvantage**: internal fragmentation. page table may be huge.)

7 . How does the kernel use a page table to help translate virtual addresses to physical addresses?

-  Done by MMU
-  determines the page number ad offset of the vaddr.
-  checks whether the page number is larger than the value in the page tabel length register
-  if it is, the MMU raises an exception
-  otherwise, the MMU uses the page table to determine the frame number of the frame that holds the virtual page, and combines the frame number and ofset to determine the physical address.

8 . Given a virtual address and a page table, how do you calculate its physical address? In reverse?

-  Physical address = Pagetable[vaddr.page#] + vaddr.offset
-  Vitual address = frame#->page# + offset

9 . Describe how the OS uses the valid bit to determine which PTEs contain a valid page mapping.

- **valid bit**: is the process permitted to use this part of the address space
- if the valid bit is 1, the PTE contains a valid mapping.

10 . In address translation, what four roles does the OS(kernel) serve? What two roles does the MMU serve?

- Kernel:
    -  manage MMU state on address space switches
    -  create and manage page tabels
    -  manage (allocate/deallocate) physical memory
    -  handle exceptions raised by the MMU
- MMU(hardware):
    - translate virtual addresses to physical addresses
    - check for and raise exceptions when necessary
 
 11 . What happens whe na precess violates a protection rule checked by the MMU?
 
- The MMU will throw a exception, handled by kernel.

12 . What is the TLB? What does it stand for.

- **TLB**: Translate Lookaside Buffer. It is a fast, fully associative address translation cache. It can cache frequently/recent used page translation and a TLB hit avoids page table lookup from RAM.

13 . Why might the MMU need to invalidate the TLB? When would this happen?

- If MMU cannot distinguish TLB entries from different address spaces. Then the kernel must clear or invalidate the TLB on each address space switch.

14 . Why is it not a good idea to save/restore on context switches?

- Because the mapping may change between switches, for example, some frame (or data) may be swapped from physical memory.

15 . What is the difference between a **hardware-controlled TLB** and a **software-controlled TLB**? 

- In hardware-controlled TLB, everything is done by hardware (add to TLB or evicts an entry to make room for new one when TLB is full)
- In software-controlled TLB, MMU simply causes an exception, which triggers the kernel exception handler to run (Kenel determine the page-to-frame mapping and load into TLB), after the exception handler runs, the MMU retries the instruction that caused the exception.

16 . A range addresses starting at 0x0000000 is intentionally left empty. Why is this?

- address 0x0 are NULL which is used to indicate error conditions. Even small address, such as 0x8, should be avoided. Accessing a field from a structure through a NULL pointer (eg. as->base1 when as is NULL) will cause your program to dereference these small addresses.

17 . How does segmentaiton improve address translation? What is the motivation behind segmentation?

- We only need to allocate pages for valid segment of the address space. Do not map the rest of the address space. (Handle sparse address spaces)

18 . How do you translate a segmented and paged virtual address into a physical address? In reverse?

- Virtual address = seg + page + offset
- Get a corresponding page table by looking up seg number. (raise exception if seg too big)
- Get frame number from the pagetable and page number
- Combine frame number and offset to get physical address

19 . What are the three approaces for locating the kernel's address space? How do OS161 and Linux do this?

- **Kernel in physical space**: PROBLEM: difficult for kernel to avoid overwriting user program data accidently. Without TLB and MMU, hard(slow) for kernel to translate for user space pointer. 
- **Kernel in separate virtual address space**: 
   - ADVANTAGE: provide isolation between kernel and process
   - PROBLEM: 
      - Passing paramenter from user to kernel is expensive. 
      - Data passed from user to kernel are limited in size. (eg pass 1G data to kernel, but out of memory)
      - For very system call, context switch is needed to change the address space form other process address space to kernel address space. TLB will be flushed away (not desired).
- **Kernel mapped into portion of address space of every process**: application virtual addresses are easy for kernel to use. (LINUX and other operating systems use this approach)

20 . Describe the different parts of an **ELF file**. Why doesn't the ELF file describe the stack?

- ELF files contains a header describing the segments and segment images.
- ELF does not describe the stack since when the program are loaded into RAM, the stack is empty.

21 . What are the different **sections** in an **ELF fiel**. What are the different segments?

- Sections:
  - .text: program code
  - .rodata: read-only global data
  - .data: initialized global data
  - .bss: uninitialized global data
  - .sbss: small uninitialized global data
- Segments:
   - Text segment, containing the program code and any read-only data
   - Data segment, containing any other global program data

22 . Which kind of variables map to which section

- see answer above..

23 . The benefits of **multilevel page table** over single level page table

- The total memory needed for multilevel page table are less than the page table for single level page tabe. And for sparse address, second level page table are not required for them, so we can use less memory. Another benefit is the multiple second level page table can go to different location in memory (single page table need to be contiguous).

24 . Why **segmentation + paging**, not **paging + segmentation**

- If paging+segmentation are used, external fragmentation will occur at second level, and the address space will be partitioned in a arbitrary way.

25 . In segmentation and paging, why put extra bits in first level page table (segment table). Why cann't we do the same in two-level paging.

- everthing in the segment should have the same property. 
- In two-level page table, the first level table just devide the address space into equal block. It doest not have any meaning.

26 . Page tables for large address spaces may be ver large. One problem is that they must be in memory, and must be physically contiguous. What are two solutions to this problem.

- Using multilevel paging.
- Segmenting and paging.

27 . What steps must the OS take to handle a **page fault** exception?

- 1. issue a request to the dist to copy the missing page into memory,
- 2. block the faulting process
- 3. once the copy has completed, set P = 1 in the PTE and unblock the process ( or change the frame number in page table if we put the data into a new frame )

28 . What are the 4 **different page replacement policies** discussed on slide? Describe and compare them?

- **FIFO**(first in first out): provide fairness, but not a good solution 
- **Optimal Page Replacement**: replace the page that will not be refenced for the longest time. Requires knowledge of future, not real.
- **LRU** (Least Recently Used): replace the page taht has not been used for the longest time. LRU is difficult to implement in virtual memory systems. (WHY: everytime to read, need to scan the list and move it at end, it can be very expensive)
- **Clock Replacement Algorithm** (second chance): when scaned, when use bit = 1, set it to 0, if it is 0, this can be replaced.

29 . What are the two types of **locality** to consider when designing a page replacement policy?

- **Temploral locality** says that pages that have been used recently are likely to be used again.
- **Spatial locality** says pages "close" to those that have been used are likely to be used next.

30 . In practice, frequency base page replacement policies don't work very well. Why is this?

- OS is a real time program, we may not know the frequency of usage during runtime

31 . LRU page replacement is considered impractical in virtual memory systems. Why is this?

- Everytime to read, need to scan the list and move the item at end, it can be very expensive.

32 . Why are modified page more expensive to replace than a clean page?

- If the page is swapped to dist, we need to modify data on disk, which is expensive. Otherwise, we may loose recent modification.

33. What is **prefetching** and what is its goal? What are the hazards of prefetching? Which kind of locality does prefetching try and exploit?

- Idea: Often when we interested in reading page x, in the very near future, we will read page x+1, x+2 ... Thus we can read three of them at one time. It is specially good on array data.

34 . Give 3 advantages and 2 disatvantages of large page size.

- advantage
   - smaller page table
   - large TLB footprint
   - more efficient I/O
- disatvantages
   - greater internal fragmentation 
   - increased chance of paging in uncessary data or code

35 . Describe the **Working Set Model**, **working set** and resident set. Define a phase change.

- **Working Set Model**: some portions of the process's virtual address space are more likely to be referenced than others.
- **Working Set**: The heavily used portion of the address space at any any given time.
   -  working set decrease when you use the process touch the same memory over and over again
   -  working set increase when the process just call the function and not doing anything. 
- **Resident Set**: the set of pages that are located in memory.

36 . What is **trashing** and what are two solutions to it?

- **Trashing**: a system is spending too much time paging.
- Solution: 
   - Killing processes (not nice)
   - Suspending and swapping out processes (nicer)

37 . Why is it better to suspend and swap processes tha njust to have the all run at onece?

- Because killing process is not nice and expensive to recover, so in order to avoid trashing, suspend and swap out processes.

38 . Which process to suspend

- low priority processes (least important)
- blocked processes (not doing userful stuff)
- large processes (lots of space freed) or small process(easier to reload)