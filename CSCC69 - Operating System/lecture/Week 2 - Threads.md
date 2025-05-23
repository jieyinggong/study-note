---
tags:
  - lec-note
  - temp
---

[[CSCC69-Multithreading.pdf]]

---

- clock interrupt → use to stop cpu and then switch threads

  ---
  
# Interrupts

## two kinds：
![[Screenshot_2025-05-09_at_11.45.57_AM.png]]

IRQs ← managed by two programmable interrupt controllers (PIC) (master - slave)

**INTR vector**

- external interrupt → hardware
- 
- **Interrupt Request lines (IRQ)**

- ! internal interrupts: caused by executing instructions (**synchronous**)

---

## Handling an interrupt

 INTR vector
save the program state: save it and then it can do something else
we can program the interrupting

example 多研究一下

---

# Context Switching

  
- give a cpu → program yield cpu


![[Screenshot_2025-05-09_at_12.00.58_PM.png]]
  

- keep waiting → waste time

- if one is waiting, cpu change to run the program is ready

- IO response → change the process from waiting to ready


**busy wait**: keep switching threads because multiple threads are waiting and not ready at the same time ← context switch is actually cpu is do something but with a small cost. it’s actually a waste
 

- election can have different way (different strategies, run robin?): priority in pintos

→ can give different priorities to different programs

for each threads, the os need to know its state and its execution context → TCB

  ---
  
## TCB: Thread Control Block

Data structure to record all the thread information that the OS needs to keep track of

### State Queues

The OS maintains a collection of queues with TCBs of all threads  

- one for ready state

- multiple queues for waiting state (each type of I/O requests)

---

# Synchronization

- Difficult to catch

- Instructions may appear in the unexpected order

→ non-deterministic for the outcome of x → different possible outcomes
 

**race-condition problems: The system behaviours depends on the sequence or timing of events that is non-deterministic.**
  
---

## Mutual Exclusion 排斥锁(MUTEX)

use mutual exclusion to synchronize access to shared recources ← **critical section**

  
**critical section:**

1. only one can execute in the critical section

2. all other threads are forced to wait on entry

3. when a thread leaves a critical section, another can enter


**Producer Consumer**

![[Screenshot_2025-05-09_at_12.49.29_PM.png]]

ensures safety property

  ---
  
## Lock

- `init()`

- `acquire()`

- `release()`
  
buffer and lock

  

## Condition variable

  
---

# thinking & questions:
#question 

1. how PIC connect IRQ, structure of two IRQs

2. how the interrupts change states (switch)? different stats? (waiting, ready, running, terminated)

3. yield()

4. buffer and lock. check buffer to avoid waste?