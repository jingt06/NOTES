1 . What are the three properties of a good implementation of sysnchronization?

- Enforce **mutualy exclusion** (only one thread at a time uses a shared object)
- Efficient (not wasting CPU cycles)
- Fairness and no starvation

2 . Can the OS know when a program is in a critical section?

- Generally NO, but may be some exception under some implementation

3 . When is it appropriate to **disable interrupts**? What happens when you disable interrupts on a multiprocessor? Give pros and cons fo disabbling interrupts.

- It is appropriate to disable interrupts when critical section are very small.
- It would not enforce mutual exclusion by disabling interrupts on a multiprocessor
- Pros:
   - enforcing mutual exclusion on uniprocessor
   - no need for hardware support
   - easy to implement
- Cons:
   - no way to preempt running thread
   - need to perform privileged operation (turning on/off interrupts)
   - easy to cheat
   - may cause interrupt becoming lost
   - kernel unaware of passage of time
   - not working on multpressor

4 . How does **Test and Set** work? How would you use it in a program? What is a potential problem with Test and Set.

- test-and-set(addr, value) is a instruction **atomically** sets the value of a specifed memory locations and either places that memory locations's old value into a register. It can be used to implement a **spinlock**. Spinlock may cause starvation and CPU is busy while waiting for lock.

5 . What is a **semaphore**? Which two operations does it support? Are they atomic?

- **Semaphore** is a synchronization primitive that can be used to enforce mutual exclusion requirements. It can also be used to solve other kinds of synchronization problems (controlling access). It have P() and V() operations. They are regarded as atomic.

6 . Describe how you would synchronize producer and consumer threads using a sempahore

- Call V() when adding item to the list, and call P() when removing item from the list

7 . What is the primary difference between a **lock** and a **binary semaphore**.

- Both enforce mutual exclusion. Lock make sure that the thread calls lock\_release is the thread called lock\_require while binary semaphore will not check who calls P() and V().

8 . Is the implementation of binary semaphores given in the notes starvation free? Why?

- No, it depends on the policy used in choosing a thread when multiple thread are waiting at wchan. 
- Yes, first come first serve will make semaphore starvation free.

9 . What is a **conditional variable**? How are they used in conjunction with **locks**?

- **Condition variable** is basically a container of  threads that are waiting for a certain condition. Each condition variable is intended to work together with a lock. It is only used from within the critical section that is protected by the lock.

10 . Define **deadlock**. How does the system recover from a deadlock?

- **Deadlock**: neither thread can make progress. The threads are permanently stuck.
- **Deadlock recovery** is usually accomplished by terminating one or more of the threads invlolved in the deadlock.

11 . Give the deadlock detection algorithm and describe the three deadlock prevention methods.

- the system maintains the resource allocation graph and tests it to determine whether there is a deadlock
- Three **deadlock prevention**
   - **No Hold and Wait**: may cause livelock
   - **Preemption**:  hard to implement and usually not possible
   - **Resource Ordering**: may be not effecient