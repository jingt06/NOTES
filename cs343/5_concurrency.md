# 5 Concurrency

**thread**: an independent sequential execution path through a program.

**process**: a program coponent that has its own thread.

**task**: similar to a process while tasks usually share a common memory. A task is sometimes called a light-weight process (LWP).

**Parallel execution**: when 2 or more operations occurs simultaneously. (only occur when multiple processors / multi-core CPUs are present.)

**Concurrent execution**: execution of multiple threads *appears* to be performed in parallel.

## 5.1 Why Write Concurrent Programs

- Dividing a problem into multiple executing threads is an important programming technique
- Expressing a problem with multiple executing threas may be the natural (best) way of describing it
- Enhance execution-time efficiency

## 5.2 Why Concurrency is Defficult

- to understand
   -  difficult to manage and coordinate them
   -  things interact with one another
- to specify
   - How should/can a problem be broken up so that parts of it can be solved at the same time
   - How and why are these parts interact or be independent
   - What infomation to be shared between tasks
- to debug
   - hard to reproduce
   - much more complex than for single thread

## 5.3 Concurrent Hardware

Unlike coroutines, task switching may occur at non-deterministic program locations

**distributed system**: Concurrent/parallel execution of threads with single/multiple CPUs on different computers with separate memories.

## 5.4 Execution States

- new -> ready
- ready <-> running
- running -> blocked
- blocked -> ready
- running -> halted