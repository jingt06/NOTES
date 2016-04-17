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

- see answer above..\