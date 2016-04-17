1 . What are the three views of an **operating system**? Describe them.

- **Application View**: provides an execution environment for running programs
   -  The execution environment provides a program with the processor time and memory space that it needs to run.
   -  The execution environment provids interfaces to use hardware.
   -  The execution environment isolates running programs from one another and prevents undesirable interactions among them.
- **System View**: The OS manages the hardware resources of a computer system.
   - Resources include processors, memory, disks, and other storage devices, network interfaces, I/O devices and so on,
   - The OS allocates resources among running programs. It controls the sharing of resources among programs.
   - The OS itself also uses resources, which it must share with appication programs.  
- **Implementation View**: The OS is a concurrent, real-time program.
   - Concurrency arises naturally in an OS when it supports concurrent applicationsm and because it must interact directl with the hardware.
   - Hardware iteractions also impose timing constraints.

2 . Define the **kernel** of the OS. What things are considered part of the OS but not the kernel?

- **Kernel**: The operations system kernel is the part of the perating system that responds to system calls, interrupts and execptions.
- Things are part of OS but not kernel: utility programs, command interpreters, programming libraries.

3 . What are some advantages of allowing more than one thread to exists simultaneously

- Allows programs run more effeciently

4 . What is contained in a **thread context**? What is **thread control bock**?

- **Thread context** consists of 
   - The processor's CPU state, including PC, the stack pointer, other registers, and the execution mode (privileged/non-privileged)
   - A stack, which is located in the address space of the thread's process
- **Thread control block** is the dta structure used by the thread library to store a thread context.

5 . Describe what happens during a **context switch**? What is **dispatching**?

- (thread) context switch 
  1. decide which thread will run next
  2. save the contest of currently running thread
  3. restore the context of the thread that is to run next
- **Dispatching**: the act of saving the context of the current thread and installing the context of the next thread to run is called dispatching

6 . What is diefferent between thread_yield() and wchan_sleep()

- yield: go to ready queue
- sleep: go to blocking queue.

7 . How is an involuntary context switch accomplished? Define **quantum**

- **quantum**: the ammount of tiem that a thread is allocated is called scheduling quantum
- When interrupt occurs, the timer-specif part of the interrupt handler can increment running\_time and then test its value
   - If running\_time is less than q(quantum), the interrupt handler simply returns and the running thread resumes its execuion
   - If running\_time is euqal to q, then the interrupt handler invoks thread\_yield to cause a context switch
   
8 . Describe what happends when an **interrupt** occurs. Where do **interrupt** come from.

- When interrupt occurs, the hardware automatically transfers control to a fixed location in memory. At the memory location, the thread library places a procedure called an **interrupt handler**. **Interrupt handler** saves the current thread context(trap frame), determines whihc devices caused the interrupt and performs device-specific processing. THen restores the saved thread context and resumes execution in that context.
- Interrupt are caused by system devices(hardeware), e.g., a timer, a disk, a network interface.