##Process and Kernel

1 . What information is contained within a **process**

- An address space (memory that holds the program's code and data, a thread of execution (possibly several threads), other resources (open files, sockets, other attributes...)

2 . Difference between a **sequential process** and a **concurrent process**

- A process with one thread is a **squential** process. A process with more than one thread is a **concurrent** process.

3 . Can threads from one process access memory from another process?

- No, iosolation.

- Yes,  interprocess communication.

4 . What can the kernel do in privledged execution mode that user programs can not directly accomplish?

- Control hardware, protect and isolate itself from prcess

5 . Describe what happens when system call is invoked.

- Switch to privledged mode,  save trap frame, call mips trap, determine if it is syscall or interupt, and perform syscall.

6 . In which registers does a system call expect the syscall code? Arugments?

- syscall code: V0, argument A0 A1 A2 A3

7 . In which registers will the system call place the return result? Retuen value?

- A3 contains 0 or 1, 0 means success, 1 means fail. V0 stores the return value.

8 . Why does OS161 have two stacks?

- One for user stack, another for kernel stack. Kernel stack stores trap frames, switch frames (avoid user programs change trap frames)...

9 . What are the only three ways for the CPU to enter **privileged mode**?

- Interrupts, Exceptions, Syscall.


10 . What is an **exception**? What is the difference between an exception and a syscall? And exception and a interrupt?

- Exceptions are another way that control is transfeered from a prcess to the kernel. Exceptions are conditions that occur during the execution of an instruction by a process. Exceptions are user caused and detected by the hardware. When an exception is detected, the hardware transfers control a specif address.

11 . The **mips_traps** function is called to handle system calls, exceptions, and interrupts. How does it differentiate between these three cases.

- Hardware sets a code to indicate the reason (syscall, exception or interrupt) that the exception handler has been invoked. The mips_trap function tests the reason code and calls the appropriate function.

12 . What does the OS161 exception handler **common_exception** code do?

- 1 Save trap frame. 2 calls the mips\_trap function to continue processing the exception. 3 When mips\_trap returns, restores teh application processor state from the trapframe. 4 return control to the application code.

13 . When returning from a system call, the program counter is not automatically adanced by the hardware. Why is this?

- When exception happens (such as TLB miss), we need to rerun the code again. Since both syscall and exception use the common exception handler, thus the hardware does not increment PC automatically.


14 . What might an OS want to keep track of in a **process table**

- Pid, state, exitcode, child process pid.

15 . Define **time sharing**. When can the CPU context switch to another thread?

- By switching from one process's thread to another process's thread, the kernel timeshares the process among multiple processes. CPU can context switch whenever it is in prevledged mode.

16 . What are three aspects of the process model that must be defined by the OS?