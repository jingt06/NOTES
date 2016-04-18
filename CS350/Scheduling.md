1 . What are the 4 into scheduling algorithms disscussed in lecture

- **FCFS** (first come first serve)
  -  simple, avoids starvation
- **SJF** (shortest job first)
  - minimizes average **turnaround** time   
  - long jobs may starve
- **Round Robin**: the pre-emptive variant of FCFS
- **SRTF** (shortest remaining time first): the pre-emptive variant of SJF

2 . Describe **multilevel feedback queue** works.

- If a thread blocks before its quantum is used up ,**raise** its priority
- If a thread uses its entire quantum, **lower** its priority
- Interactive process is higher priority and it is frequently blockd
- This may **starve** thread in lowe queues. Various enhance can avoid this. (eg. periodically migrate all threads into higher priority queue.)

3 . In a prioritized scheduling environment, low-priority threads risk starvation. How can this be solved?

- periodically migrate all threads into higher priority queue.

4 . Describe **Linux Completely Fair Scheduler (CFS)**: a weighted fair sharing approach

- all process runs the same number of virtual time
- process have a priority, ( priority / sum of priority of all process ) * vitural time = actual time

5 . compare **per-core ready queue** and **shared ready queue**

- **per-core ready queue**
   - advantage: same thread run on he same core. no critical setion need since queue are not shared among cores.  It can scales to a larger number of cores. CPU cache support (no need to reaload caches).
   - disadvantage: load balance 
- **shared ready queue**
   - advantage: no problem of load balance
   - disadvantage: as core grows, contention for ready queue becomes a problem. Critical section is required for accessing shared ready queue. 
