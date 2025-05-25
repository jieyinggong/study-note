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
### External Interrupts
- hardware interrupts
- caused by an I/O device that needs some attention ( **asynchronous**)
#### the naive implementation:
 I/O devices are wired to Interrupt Request lines (IRQs)
 **Problems**:
 - Not flexible (hardwired) 
 - CPU might get interrupted all the time 
 - How to handle interrupt priority
### Internal Interrupts
-  system calls, exceptions and faults 
- caused by executing instructions ( (synchronous)

### The real implementation for internal & external interrupt

[[CSCC69-Multithreading.pdf#search=Internal Interrupt and External Interrupt - the real implementatio|CSCC69-Multithreading, p.11]]
![[Screenshot_2025-05-09_at_11.45.57_AM.png]]

IRQs ← managed by two programmable interrupt controllers (PIC) (master - slave)
❓*这个master and slave 结构的意义是什么？ 处理priority？为什么要两个？*
不太理解这里的irq和pic结构

**Programmable Interrupt Controllers (PIC):** Responsible to tell CPU when and which devices wishes to interrupt through the **INTR vector**
- -> **INTR vector**:
	- external interrupt → hardware
	- **Interrupt Request lines (IRQ)**
	- ! internal interrupts: caused by executing instructions (**synchronous**)

- Advantage:
	- 16 lines of interrupt (IRQ0 - IRQ15) 
	- interrupts have different priority
	- Interrupts can be masked


---

## Handling an interrupt
[[Hardware.pdf#page=3|Hardware, p.3]]  (B58: The interrupt handler)
1. the **cpu** receives an interrupt on the **INTR vector**
2. the **cpu** stops the running program and transfer the corresponding handler in the Interrupt Descriptor Table(IDT)----> *B58 content*
❓*这里的handler是handler function吗*
3. the **handler** save the current program state
	- save it and then it can do something else
	- 想一下assemble 里的`jal` [[Assembly.pdf#search=Functions|Assembly, p.4]] (b58)
we can program the interrupting
4. the **handler** executes the functionality
	 - we can program the interrupting handler
5. The **handler** restores (or halt) the running program
	- 这里应该是jump回存储的current program state了，可以想一下assemble里的`jr & ra`

[[CSCC69-Multithreading.pdf#search=Example|CSCC69-Multithreading, p.15]]
![[Screenshot 2025-05-24 at 5.42.11 PM.png]]

---

# Context Switching

- give a cpu → program **yield** cpu
[[CSCC69-Multithreading.pdf#search=The different states of a threa|CSCC69-Multithreading, p.18]]
![[Screenshot_2025-05-09_at_12.00.58_PM.png]]
  

- keep waiting → waste time
- if one is waiting, cpu change to run the program is ready
- IO response → change the process from waiting to ready
 
**OS Context Switching when**:
1. receives a fault
2.  receives a System Clock Interrupt or a System Call Trap (I/O request)
	- election can have different way (different strategies, round robin): priority in pintos -->  [[Week 3 - Threads & Scheduling#Scheduling]]
		- → can give different priorities to different programs
3.  receives any other I/O interrupt

**busy wait**: 
- keep switching threads because multiple threads are waiting and not ready at the same time 
	- context switch is actually cpu is do something but with a small cost. it’s actually a waste

for each threads, the os need to know its **state and its execution context** → **TCB**

  ---
  
## TCB: Thread Control Block

Data structure to record all the thread information that the OS needs to keep track of:
-  Tid (thread id) 
-  State (as either running, ready, waiting) 
- Registers (including eip and esp) 
-  Pointer to a Process Control Block (coming next week) 
-  User (forthcoming lecture on user space)

### State Queues
The OS maintains a collection of queues with TCBs of all threads  
- one for ready state
- multiple queues for waiting state (each type of I/O requests)

---

# Synchronization

- Difficult to catch
- Instructions may appear in the unexpected order

→ non-deterministic for the outcome of x → different possible outcomes
 
**race-condition problems:**
- **The system behaviours depends on the sequence or timing of events that is non-deterministic.**
  
---

## Mutual Exclusion 排斥锁(MUTEX)

use mutual exclusion to synchronize access to shared recources ← **critical section**
#### **critical section:**
1. only one can execute in the critical section
2. all other threads are forced to wait on entry
3. when a thread leaves a critical section, another can enter


**Producer Consumer**
[[CSCC69-Multithreading.pdf#search=A classical example - Producer Consum|CSCC69-Multithreading, p.30]]
![[Screenshot_2025-05-09_at_12.49.29_PM.png]]

**ensures safety property！**

  ---
  
## Lock

- `init()`
- `acquire()`: **waits until the mutex is unlocked**, then **locks** it to enter the C.S
- `release()`: **unlocks** the mutex to leave the C.S, waking up anyone waiting for it
  
**buffer and lock:**
- Avoid writing into a full buffer 
- Avoid reading from an empty buffer
[[CSCC69-Multithreading.pdf#search=(Good) Producer consumer using a lock|CSCC69-Multithreading, p.34]]
![[Screenshot 2025-05-24 at 7.03.32 PM.png]]

不加上 `while(full(buffer))` 和 `while(emtpy(buffer))` 的话 
- 会是bad use of lock: 会让producer write into a fuller buffer & consumer read from an empty buffer (于是会block --> [[w7 pcrs.pdf#search=Handle Synchronization :|w7 pcrs, p.5]] (b09: handle synchronization)
- 所以需要check buffer to avoid waste


  
---

# thinking & questions:
#question 

1. how PIC connect IRQ, structure of two IRQs

2. ~~how the interrupts change states (switch)? different stats? (waiting, ready, running, terminated)~~

3. yield()

4. ~~buffer and lock. check buffer to avoid waste?~~