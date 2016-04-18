1 . Describe how OS161 uses memory mapping for devices

- There is a uncached memory in Kernel seg2, which have some bits mapped to devices register.

2 . What is the difference between **program controlled I/O** and **Direct Memory Access**? What are their respective advantege?

- **program controlled I/O**: the device driver moves the data iteratively, one word at a time. It is simple, but the CPU is busy while the data is being transferred
- **direct memory access (DMA)**: CPU is not busy during transfer, and is free to do something else.

3 . OS's often buffer data that is moving between devices and application programs' address spaces. What are the benefits/drawbacks of this?
The 

- The process will block until device generates completion interrupt. The CPU is free to run other threads.

4 . What is the only way for a suer application to talk to a device?

- through kernel

5 . What does the statement "disks are non-volatile" mean?

- data persists even when the devices is without power.

6 . Using **simplified cost model** for disk block transfer, what are the three components that make up "requst service time"?

- **service time** = seek time + rotational latency + transfer time
- **seek time**: move the read/write heads to the appropriate cylinder
- **rotational latency**: wait until the desired sectors spin to the read/write heads
- **transfer time**: wait while the desired sectors spin past the read/write heads

7 . If a disk spins at x rotations per second, what is the **expected rotational latency** in terms of x?

- 1/2x

8 . If there are k sectors to be transferred and there  are T sectors per track, what is the transfer time in temrs of k, T, and n?

- transfer time = k/Tx

9 . If k is the required seek distance, what is the seek time?

- seek time: k*t/C
- C is the total number of cylinders,t is the seek time from innermost cylinder to the outermost cylinder.

10 . Why is sequential I/O more efficent than non-sequential I/O?

- **sequential IO**: put data of same file on closer block(track)
- sequential I/O operations eliminate the need for (most) seeks
- disks use other techniques, like track buffering, to reduce the cost of sequential I/O even more

11 . Define **tracking buffering**

- when fetching data from disk, prefetch the next severl blocks of data.

12 **disk scheduling algorithms** 

- **FCFS** (first come first serve): fair and simple, but no optimization of seek time
- **SSTF(shortest seek time first)**: choose closest request, seek times are reduced, but requests may starve
- **Elevator algorithms(SCAN)**: the disk head moves in one direction until there are no more requests in fornt of it, then reverses direction. It reduces seek times, while avoiding starvation.