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
[[CSCC69-Multithreading.pdf#page=37|CSCC69-Multithreading, p.37]]
Semaphores are **“integers”** that support two operation:
- `Semaphore::P()`-> decrement, **block until semaphore is open**
	- a.k.a `wait()`, or `sem_wait()`, or `sema_down()`
- `Semaphore::V()`-> increment, allow another thread to enter
	- a.k.a `signal()`, or `sem_post()`, or `sema_up()`

- Semaphore value **safe property: always ${\ge 0 }$**
	- if the semaphore value is always greater than 0 -> it will not be blocked （好像是的吧）
	- if the semaphore value is equal to 0 -> it might be **blocked**
- Producer and consumer can be in the critical section **at the same time**
	- so need to be careful here (for deadlock)

**Blocking mechanism**
Associated with each semaphore is a queue of waiting threads
- When **`P()`** is called by a **thread**: ***decrement***
	- If semaphore is open, thread continue 
	- If semaphore is closed, thread **blocks** on queue
- Then **V( )** opens the **semaphore**: ***increment***
	- If a thread is waiting on the queue, the thread is unblocked 
	- If no threads are waiting on the queue, the signal is remembered for the next thread

semaphore 和 lock的差别 ？好处？ 更灵活？
- ❓还是不太理解这里的semaphore value
-  semaphore 作为 mutex 是有特指semaphore value 为1的情况嘛？

#### Comparing good use and bad use
- why good use avoid deadlock here ❓
- ***Bad use 1:** [[CSCC69-Multithreading.pdf#search=(Bad) Producers Consumers using a semaphor|CSCC69-Multithreading, p.39]]
- ![[Screenshot 2025-05-24 at 8.50.12 PM.png]]
	- 这里producer和consumer会同时在critical section --> race condition
			- 是因为`not_full`是n 如果大于 1 的话...not_full 不会在consumer 跑的时候block？ 
	- 需要再单独加一个mutex来控制只有一个thread在critical section中
		- `sem_init(mutex, 1)`

- **Bad use 2:**[[CSCC69-Multithreading.pdf#search=(Bad) Producers Consumers using a semaphor|CSCC69-Multithreading, p.40]]
- ![[Screenshot 2025-05-24 at 8.47.40 PM.png]]
	- 这里- cpu may completely block and frozen -> **DEADLOCK**
		- 这里consumer可能会先运行`sem_wait(mutex)`导致`mutex` block --> producer needs to wait for consumer release `mutex`
		- 而producer 一直wait block 在`sem_wait(mutex)`这里，无法跑到下面 `sem_signal(not_empty)`release `not_empty` 导致 `not_empty` 是block的 --> consumer needs to wait for producer release `not_empty`
- 啊哈这里问过某人所以看懂了呢ww

- **Good use:** [[CSCC69-Multithreading.pdf#search=(Good) Producers Consumers using semaphore|CSCC69-Multithreading, p.42]]
![[Screenshot 2025-05-24 at 8.45.34 PM.png]]
- 这里调换顺序之后可以让consumer先`sem_wait(not_empty)` block 在 `not_empty` 不会去动`mutex` --> producer 就不会block住可以自己release `mutex`然后正常跑
- 等producer跑完然后release `not_empty`之后consumer才可以跑下去，之后再`sem_wait(mutex)` 也不会让producer和consumer在同一个critical section中
- 但是这能完全解决嘛...？ 万一consumer接收到unblock 的signal慢了一点，让producer的`sem_wait(mutex)` 跑到了前面呢？consumer会一直waiting嘛？这是可能的嘛？


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
- ~~两周前学了什么已经快忘的差不多了hmmm...全部一起重新理一遍吧~~
- Semaphore P & V; good use and bad use how to avoid deadlock 
- 各个问题和fix 方法； 每个bad use导致的问题和good use how to fix it
- 核心还是资源竞争， 资源的调取和各个冲突什么的感觉
- preemptive? once it's running we can interrupt it
- time quantum 不能过大的原因
- Starvation of high priority thread for MLQ and why MLFQ solve this