---
tags:
  - lec-note
  - temp
---

[[CSCC69-Multithreading.pdf]]
[[CSCC69-Scheduling.pdf]]

---

# Continuing week 2

## mutex
- lock
- condition variable
- semaphore
#### Lock

#### Condition variable
exactly equv to lock, nothing actually change


#### Semaphore
- Semaphore value is a safe property: always ${\ge 0 }$ ❓
	- if the semaphore value is always greater than 0 -> it will not be blocked
	- if the semaphore value is equal to 0 -> it might be blocked
- Producer and consumer can be in the critical section **at the same time**
	- so need to be careful here (for deadlock)
#### Comparing good use and bad use
- why good use avoid deadlock here ❓


**BAD USE OF SEMAPHORE:**
- cpu may completely block and frozen -> **DEADLOCK**



---
## Deadlock

### two ways to solve


### spin lock
problem is that it can be interrupted 
so  it handle the interrupt and let it not be interrupted ?


![[Screenshot 2025-05-23 at 11.50.05 AM.png]]

bad reason: 什么不要把选择权交给user， 可能会让cpu frozen or 出各种问题


![[Screenshot 2025-05-23 at 11.53.10 AM.png]]

this is a better solution
avoid busy waiting？

in project 1, have to write disable interrupt in one case that can't use mutex
do not use it if not necessary, use mutex as possible

- 要知道这里的两种不同方式！

## Other synchronization prob

### Readers Writers
#### **Writers starvation:**
一直都有新的reader进来，不结束
Writer never get in, keep waiting -> never get resource
##### how to fix? 
- add a mutex 
- 加上限制？类似让writer 插队嘛？❓


### Dining Philosophers
 this is a **deadlock**: take the first fork at the same time and other can't get fork?
 - live lock?
```c
if ((i+1) == n){ 
	sem_wait(fork[(i + 1)% n]) 
	sem_wait(fork[i]) 
}else{ 
	sem_wait(fork[i]) 
	sem_wait(fork[(i + 1)% n])
}

```



### problem summary
 synchronization problem?
- busy waiting
- race condition
- deadlock
- starvation


---
# Scheduling
[[CSCC69-Scheduling.pdf]]
## Important to know
- round robin (RR)
- MLQ (fixed priority)
- MLFQ (fixed priority)

### Starvation: non goal
side effect of scheduling algo and synchronization

### Scheduling Criteria
- Throughput
- Turnaround time
- Response time（waiting time）
	why computer and mobile phone 处理会不一样
	因为电脑会需要click 键盘然后再见到页面变化， 会有一些轻微延迟
	但是mobile phone 会需要更快的反应,更加及时的变化

在不同的systems上会有不同的需求for balance criteria
- Batch systems - non-preemptive
- Interactive systems - preemptive
Depends on different systems

##  Scheduling algorithm
### FCFS - First Come First Serve (non-preemptive)
Run jobs **in order** that they arrive (no interrupt) 
- Problem : convoy effect

### SJF - Shortest-Job-First (non-preemptive)
Choose the thread with the shortest processing time
turnaround and waiting time is way better
- Problem: need to know processing time in advance

### SRTF - Shortest-Remaining-Time-First (preemptive)
if a new thread arrives with CPU burst length less than remaining time of current executing thread, preempt current thread
- good: optimize waiting time
- problem: can lead to **starvation**
	- 可能一个big thread 永远不会结束嘛因为remaining time过长？

### RR - Round Robin (preemptive)
Each job is **given a time slice** called a **quantum**, preempt job after duration of quantum, move to back of **FIFO queue**
- good: fair allocation of CPU, low waiting time (interactive)
- Problem : no **priority** between threads
	- all threads are equal: not good because we want to give some tasks higher priority

#### Time quantum
**How to choose?**
- Want much larger than context switch cost: 不能过小，context switch cost 会占比过大
- Majority of bursts should be less than quantum - But not so large system reverts to FCFS： 不能过大
**Typical values**: 1–100 ms

#### Why Priority?
- Optimize job turnaround time for “batch” jobs 
- Minimize response time for “interactive” job

### MLQ - Multilevel Queue Scheduling (preemptive)
Associate a priority with each thread and execute highest priority thread first. 
If same priority, do round-robin.

![[Screenshot 2025-05-23 at 12.50.16 PM.png]]
- Problem 1 : **starvation** of low priority thread
-  Problem 2 : (possibly) **starvation** of high priority thread 
	- what we need to fix in pintos
-  Problem 3 : how to decide on the priority?

#### Starvation of high priority thread
可能会被low priority thread grab mutex first，就算有higher priority也 cannot run, because it would be blocked by mutex
但是因为priority不同，所以higher priority 的thread 无法release 这个lower priority thread 加上的mutex嘛
- **Solution:** priority donation
	- give its high priority to lower priority and release the lock


### MLFQ - Multilevel Feedback Queue Scheduling (preemptive)
Same as MLQ but change the priority of the process based on observations

![[Screenshot 2025-05-23 at 12.59.28 PM.png]]

- Good: Turing-award winner algorithm
- there is hard thing to do on sth (calculating on integers? 好像是系统的什么东西很难处理)


linux care more about services 
different os and difference choices depend on their usage




---

# 需要好好再多看看的
#question
- 两周前学了什么已经快忘的差不多了hmmm...全部一起重新理一遍吧
- Semaphore P & V; good use and bad use how to avoid deadlock 
- 各个问题和fix 方法； 每个bad use导致的问题和good use how to fix it
- 核心还是资源竞争， 资源的调取和各个冲突什么的感觉
- preemptive? once it's running we can interrupt it
- time quantum 不能过大的原因
- Starvation of high priority thread for MLQ and why MLFQ solve this