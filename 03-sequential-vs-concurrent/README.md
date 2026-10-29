# Sequential vs. Concurrent Programming

## 1. Introduction

Programming tasks can be organized in different ways depending on how they execute and how their progress overlaps.

Two important approaches are:

- **Sequential Programming:** Tasks execute in a defined order, usually one after another.
- **Concurrent Programming:** Multiple tasks can make progress during overlapping periods.

Concurrency is closely related to the operating system's management of processes, threads, and system resources.

**Important:** Concurrency and parallelism are related but different concepts. Concurrent tasks do not necessarily execute at the exact same time.

## 2. Sequential Programming

Sequential programming organizes operations so that one step normally finishes before the next step begins.

A typical sequential program follows a predictable flow of execution.

### Example: Sequential Python Code

```python
import time

def say_hi(name):
    time.sleep(1)
    print("Hi", name)

say_hi("Ali")
say_hi("Fatima")
say_hi("Mahboobeh")
```

Each function call waits for approximately one second before printing its message.

The calls execute one after another, so the total execution time is approximately three seconds, excluding additional overhead.

### Characteristics

- Execution follows a defined sequence.
- The flow of control is generally easier to understand.
- Debugging is often simpler.
- A slow operation can delay subsequent operations.
- An unhandled exception can prevent later statements in the same execution flow from running.

### Example: Finding the Largest Number

Suppose a program must:

1. Read three numbers.
2. Find the largest number.
3. Display the result.
4. Print a thank-you message.

These operations can be performed sequentially.

If the program attempts to convert invalid input into a number without handling the resulting exception, execution may stop before the result and thank-you message are displayed.

Input validation and exception handling can make sequential programs more robust.

## 3. Concurrent Programming

Concurrent programming allows multiple tasks to make progress during overlapping periods.

A program can use techniques such as threads, asynchronous programming, or multiple processes to manage multiple tasks.

The best technique depends on the type of work being performed.

### Example: Concurrent Python Code Using Threads

```python
import time
import threading

def say_hi(name):
    time.sleep(1)
    print("Hi", name)

threads = []

for name in ["Ali", "Fatima", "Mahboobeh"]:
    thread = threading.Thread(target=say_hi, args=(name,))
    threads.append(thread)
    thread.start()

for thread in threads:
    thread.join()
```

In this example:

- Each thread runs the `say_hi` function.
- The calls to `start()` allow the threads to begin execution.
- The `join()` calls make the main thread wait until the worker threads finish.
- The three one-second waits overlap, so the total runtime is typically close to one second plus overhead, rather than three seconds.

The order in which the messages appear is not guaranteed.

This example demonstrates concurrency. It does not prove that all three functions execute simultaneously on different CPU cores.

## 4. Concurrency vs. Parallelism

**Concurrency** is about managing multiple tasks whose progress overlaps.

**Parallelism** means multiple tasks actually execute at the same time, typically on different CPU cores or processing units.

For example:

- A single CPU core can switch between multiple tasks, enabling concurrency.
- Two CPU cores can execute two suitable tasks simultaneously, enabling parallelism.

A concurrent program may be parallel, but concurrency does not require parallel execution.

## 5. Analogy: Cars Behind a Truck

Imagine twenty cars stuck behind a slow truck on a narrow, single-lane road.

If every car must follow the truck, the cars cannot move ahead until the truck moves or the road conditions change.

Now imagine a two-lane road that allows cars to pass safely.

More cars can make progress without waiting for the truck.

This analogy helps explain the difference between a restrictive execution path and allowing tasks to make progress independently.

However, a road lane is only an analogy for an execution resource; it is not a precise equivalent of a process or thread.

## 6. Practical Example: Downloading and Processing Images

Imagine a program that downloads images from the internet and checks whether each image contains a cat.

The program has two main kinds of work:

1. Download images from a remote server.
2. Process the downloaded images.

A purely sequential implementation might download and process each image before moving to the next one.

A concurrent implementation could start downloading several images while processing images that have already arrived.

This can improve overall throughput, particularly when network operations spend time waiting for responses.

For CPU-intensive image processing, multiple processes or another suitable parallel execution strategy may improve performance, depending on the language runtime, hardware, and workload.

## 7. Advantages and Disadvantages

### Sequential Programming

**Advantages**
- Easier to understand and debug in many cases.
- Straightforward control flow.
- Often suitable for small tasks and operations with strict dependencies.

**Disadvantages**
- A slow operation can delay subsequent operations.
- Independent tasks may remain idle while another task waits.
- It may not make full use of available processing resources.

### Concurrent Programming

**Advantages**
- Can overlap waiting periods with useful work.
- Can improve responsiveness and throughput.
- Can take advantage of parallel hardware when the implementation and workload allow it.
- Can organize independent tasks more effectively.

**Disadvantages**
- More complicated control flow.
- Harder debugging and testing in some cases.
- Shared mutable data can cause race conditions.
- Synchronization introduces additional complexity and overhead.

Concurrency does not automatically make a program faster. For small tasks, the overhead of creating and coordinating threads or processes can outweigh the benefits.

## 8. Comparison Table

| Feature | Sequential Programming | Concurrent Programming |
|---|---|---|
| Execution | Tasks follow a defined sequence | Task progress can overlap |
| Threads | Often uses one thread for the main flow | May use multiple threads, processes, or asynchronous tasks |
| Parallel execution | Not required | Possible, but not guaranteed |
| Complexity | Usually simpler | Often more complex |
| Debugging | Often easier | May require more careful testing |
| Waiting operations | Can block later steps | May allow other tasks to progress |
| Common examples | Simple calculations and ordered workflows | Network requests, servers, and concurrent downloads |

## 9. Key Takeaways

- Sequential programming usually executes operations one after another.
- Concurrent programming allows multiple tasks to make progress during overlapping periods.
- Parallelism means executing multiple tasks at the same time.
- Threads, processes, and asynchronous programming are different tools for implementing concurrency.
- Concurrent programming can improve responsiveness and throughput, but it introduces complexity.
- The appropriate approach depends on the workload, dependencies, programming language, and available hardware.

## 10. Review Questions

1. What is the difference between sequential and concurrent programming?
2. Does concurrency always mean parallel execution? Explain.
3. What are two advantages and two disadvantages of sequential programming?
4. What are two advantages and two disadvantages of concurrent programming?
5. Why can concurrent downloads improve performance?
6. Why does the order of printed messages in the threaded example vary?
7. Why might concurrency make debugging more difficult?

## Reference

- [Concurrent vs. Sequential Programming — CodeBaz](https://codebaz.dev/concurrent-vs-sequential-programming/)

---

*Educational notes prepared as part of studying Operating System Fundamentals.*

# Exercises: Sequential vs. Concurrent Programming

## Exercise 1: Basic Concepts

Answer the following questions.

1. What is sequential programming?
2. What is concurrent programming?
3. What is the difference between concurrency and parallelism?

## Exercise 2: Advantages and Disadvantages

List two advantages and two disadvantages of each approach:

- Sequential programming
- Concurrent programming

## Exercise 3: Calculate Execution Time

Three independent tasks each spend approximately 2 seconds waiting.

Assume there is no significant overhead.

1. Approximately how long will the tasks take if executed sequentially?
2. Approximately how long might they take if their waiting periods overlap through concurrency?
3. Why are these estimates not guaranteed for every real program?

## Exercise 4: Analyze the Code

Consider the following Python code:

```python
import time
import threading

def work(number):
    time.sleep(2)
    print("Task", number, "completed")

threads = []

for number in range(3):
    thread = threading.Thread(target=work, args=(number,))
    threads.append(thread)
    thread.start()

for thread in threads:
    thread.join()

print("All tasks completed")
```

Answer the questions:

1. How many worker threads are created?
2. Why is `join()` used?
3. Is the order of the three task-completion messages guaranteed?
4. Does this code prove that all tasks execute simultaneously on separate CPU cores?

## Exercise 5: Choose an Approach

For each scenario, explain whether sequential or concurrent execution may be more suitable.

1. Performing three simple calculations where each calculation depends on the previous result.
2. Downloading ten independent files over a network.
3. Processing a large number of images using CPU-intensive operations.
4. Executing a set of database operations that must follow a strict order.

Explain that the best choice may depend on implementation details and task dependencies.

## Exercise 6: Practical Experiment

Run both the sequential and threaded examples from the lesson.

1. Measure the execution time of each version.
2. Record the results.
3. Explain why the threaded version may finish sooner.
4. Repeat the experiment and observe whether the exact execution time changes.

## Exercise 7: Short Written Answer

In your own words, explain why concurrent programming can improve responsiveness but can also make debugging more difficult.
