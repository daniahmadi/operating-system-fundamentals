# Operating Systems, Processes, Threads, and Concurrency

## 1. Operating System

An operating system (OS) manages computer hardware and provides an environment for applications to execute.

Examples include Windows, Linux, macOS, Android, and iOS.

## 2. CPU and CPU Cores

The Central Processing Unit (CPU) executes program instructions.

A CPU may contain multiple physical cores. Each core can execute instructions independently. Modern processors may also support simultaneous multithreading (SMT).

The operating system schedules runnable threads on available logical CPUs.

## 3. Processes

A process is an instance of a program in execution.

A process typically has:
- A process identifier (PID)
- Its own virtual address space
- Resources managed by the operating system
- One or more threads

Processes are isolated by default but can communicate through mechanisms such as pipes, sockets, and shared memory.

## 4. Threads

A thread is an execution unit within a process.

A process can contain multiple threads. Threads in the same process typically share memory and many resources, while each thread maintains its own stack and execution state.

### Example: Download Manager

A download manager can divide a file into multiple segments and download them concurrently.

Each worker thread may download a different segment. The threads coordinate their progress so that the segments can be combined into the completed file.

## 5. Concurrency vs. Parallelism

**Concurrency** means multiple tasks can make progress during overlapping periods. On a single CPU core, the operating system can switch between tasks.

**Parallelism** means multiple tasks execute at the same time, for example on separate CPU cores.

Concurrency does not necessarily require multiple cores. Threads can execute in parallel when suitable hardware and scheduling resources are available.

## 6. Worked Example

Assume two independent CPU-bound tasks:

- Task A requires 4 ms of CPU time.
- Task B requires 3 ms of CPU time.

### Scenario A: One CPU Core

| Time | Running task |
|---|---|
| 0–2 ms | A |
| 2–4 ms | B |
| 4–6 ms | A |
| 6–7 ms | B |

Task A completes at 6 ms, and Task B completes at 7 ms.

Total completion time: **7 ms**, excluding scheduling overhead.

### Scenario B: Two CPU Cores

| Core | Task | Execution interval |
|---|---|---|
| Core 1 | A | 0–4 ms |
| Core 2 | B | 0–3 ms |

Both tasks execute in parallel.

Total completion time: **4 ms**, excluding scheduling overhead.

These are simplified scheduling examples, not guarantees about a particular operating system.

## 7. Key Takeaways

- The OS manages hardware resources and provides services to applications.
- A process is an instance of a program in execution.
- A thread is an execution unit within a process.
- Threads within a process commonly share memory and resources.
- Concurrency allows tasks to make progress over overlapping periods.
- Parallelism involves simultaneous execution on multiple processing resources.
- The OS scheduler determines which runnable threads execute on available logical CPUs.

## 8. Reference

- [Operating System Fundamentals — CodeBaz](https://codebaz.dev/operating-system-fundamentals/)

---

*Educational notes prepared as part of studying Operating System Fundamentals.*

# Exercises: Processes, Threads, and Concurrency

## Exercise 1: Identify the Concepts

A user opens a web browser and a music player.

1. How many application processes might be created?
2. Can each process contain multiple threads?
3. Does running both applications mean they are always executing in parallel?

## Exercise 2: Concurrency or Parallelism?

For each scenario, identify whether it demonstrates concurrency, parallelism, or potentially both.

1. A single CPU core switches between two runnable tasks.
2. Two independent CPU-bound threads execute on two different CPU cores.
3. Two threads alternate between computation and waiting for network responses.

## Exercise 3: Calculate Completion Time

Two independent CPU-bound tasks require 6 ms and 4 ms of CPU time, respectively.

Assume no scheduling overhead.

1. What is the total completion time when both tasks run sequentially on one core?
2. What is the total completion time when they start simultaneously on two separate cores?
3. Why can the second scenario finish sooner?

## Exercise 4: Explain Shared Resources

Explain two differences between processes and threads, focusing on memory and resource sharing.

## Exercise 5: Practical Investigation

Open Task Manager on Windows or an equivalent system monitor on your operating system.

1. Find a running application.
2. Observe its process information.
3. Investigate whether the application uses multiple threads.

Write down your observations and explain what they demonstrate about processes and threads.
