# Java Multi-threading for Certification & Interviews

> **Instructor:** Durga (Java Trainer)
> **Target Audience:** Developers preparing for OCJA/OCJP certification exams, technical interviews, and day-to-day Java coding.

Multi-threading is one of the most powerful and frequently tested concepts in Java. This course provides a complete roadmap covering all major topics from fundamentals to advanced concurrency.

---

## 1. Course Syllabus & Roadmap

### 1.1 Ways to Define a Thread `[02:16]`
- Extending the `Thread` class
- Implementing the `Runnable` interface
- Comparison and when to use which approach

### 1.2 Thread Naming `[03:14]`
- Getting the name of a thread using `getName()`
- Setting the name of a thread using `setName()`

### 1.3 Thread Priorities `[03:14]`
- Setting and getting thread priorities
- Priority constants: `MIN_PRIORITY`, `NORM_PRIORITY`, `MAX_PRIORITY`

### 1.4 Methods to Prevent Thread Execution `[05:19]`
- `yield()` — voluntarily pausing the current thread
- `join()` — waiting for another thread to complete
- `sleep()` — pausing execution for a specified duration

### 1.5 Synchronization `[05:19]`
- The most critical concept in multi-threading
- Preventing data corruption in shared resources
- `synchronized` keyword — methods and blocks

### 1.6 Inter-Thread Communication `[07:09]`
- `wait()` — releasing the lock and waiting for notification
- `notify()` — waking up a single waiting thread
- `notifyAll()` — waking up all waiting threads

### 1.7 Deadlock `[07:09]`
- What is deadlock and how it occurs
- Strategies to detect and prevent deadlock

### 1.8 Daemon Threads `[07:09]`
- What are daemon threads
- Difference between user threads and daemon threads

### 1.9 Advanced Topics `[07:09]`
- `ReentrantLock` — advanced locking mechanism
- `ThreadLocal` — thread-confined variables
- **Executor Framework** — managed thread pools and task execution

---

> **Note:** Thorough knowledge of these topics will make a candidate highly confident in any Java interview.

---
---

# Topic 1: Introduction to Multi-threading

> 📺 **Video:** Java Multi-threading || Introduction to Multi-threading
> **By:** Durga Software Solutions

This topic builds the foundation for multi-threading by answering the key question: **Why do we need multi-threading?** It covers the concept of multitasking, its types, the advantages it brings, and real-world application areas.

---

## 1 What is Multitasking?

**Multitasking** is the ability to execute **multiple tasks simultaneously**. It is a fundamental concept that forms the basis of modern computing — from operating systems managing dozens of programs to web servers handling thousands of user requests.

> [!IMPORTANT]
> Multitasking is the broader concept. Multi-threading is a specific type of multitasking applied at the programmatic level.

### 1.1 Types of Multitasking

Multitasking is divided into **two categories** based on the nature of the tasks being executed:

| #   | Type                          | Scope                | Description                                                    |
|-----|-------------------------------|----------------------|----------------------------------------------------------------|
| 1   | **Process-Based Multitasking** | Operating System level | Multiple independent programs running simultaneously          |
| 2   | **Thread-Based Multitasking**  | Programmatic level    | Multiple independent parts of the **same program** running simultaneously |

---

## 2 Process-Based Multitasking `[11:38]`, `[23:36]`

In process-based multitasking, the operating system runs **several independent programs (processes)** at the same time. Each process has its own memory space, resources, and execution context.

### 2.1 Real-World Example

Consider what you do on your computer on a daily basis:

```
 ┌─────────────────────────────────────────────────────┐
 │                  Operating System                    │
 │                                                     │
 │   ┌──────────┐  ┌──────────┐  ┌──────────────────┐ │
 │   │  Text    │  │  Music   │  │   File Download  │ │
 │   │  Editor  │  │  Player  │  │   Manager        │ │
 │   │ (typing) │  │ (playing)│  │   (downloading)  │ │
 │   └──────────┘  └──────────┘  └──────────────────┘ │
 │                                                     │
 │   Process 1      Process 2       Process 3          │
 └─────────────────────────────────────────────────────┘
```

- **Process 1:** You are typing a document in a text editor.
- **Process 2:** Music is playing in the background via a media player.
- **Process 3:** A large file is downloading in the browser.

All three are **independent programs** running side by side. None of them is a part of the other — they are separate processes managed by the OS.

### 2.2 Key Characteristics

| Characteristic          | Description                                                   |
|-------------------------|---------------------------------------------------------------|
| **Independence**        | Each process is a completely separate program                 |
| **Memory**              | Each process has its own dedicated memory space               |
| **Communication**       | Inter-process communication (IPC) is complex and heavyweight  |
| **Context Switching**   | Expensive — the OS must save/restore entire process states    |
| **Best Suited For**     | Operating System level task management                        |

> [!NOTE]
> Process-based multitasking is primarily the responsibility of the **Operating System**, not the programmer. Java focuses on thread-based multitasking.

---

## 3 Thread-Based Multitasking `[11:51]`, `[30:29]`

In thread-based multitasking, a **single program** is divided into **multiple independent sub-tasks (threads)**, and each thread executes concurrently within the same process.

### 3.1 Real-World Example

Consider a media player application:

```
 ┌─────────────────────────────────────────────────────┐
 │              Media Player Application                │
 │                  (Single Process)                    │
 │                                                     │
 │   ┌──────────┐  ┌──────────┐  ┌──────────────────┐ │
 │   │ Thread 1 │  │ Thread 2 │  │    Thread 3      │ │
 │   │  Video   │  │  Audio   │  │   Subtitles      │ │
 │   │ Renderer │  │  Player  │  │   Display        │ │
 │   └──────────┘  └──────────┘  └──────────────────┘ │
 │                                                     │
 │   All threads share the SAME memory space           │
 └─────────────────────────────────────────────────────┘
```

- **Thread 1:** Renders the video frames on screen.
- **Thread 2:** Plays the audio track in sync.
- **Thread 3:** Displays subtitles at the correct timestamps.

All three are **parts of the same program** running concurrently. They share the same memory and can communicate with each other easily.

### 3.2 Key Characteristics

| Characteristic          | Description                                                   |
|-------------------------|---------------------------------------------------------------|
| **Independence**        | Each thread is an independent sub-task of the same program    |
| **Memory**              | All threads share the same memory space (heap)                |
| **Communication**       | Inter-thread communication is simple and lightweight          |
| **Context Switching**   | Cheap — only the thread's local state needs to be saved       |
| **Best Suited For**     | Programmatic level task optimization                          |

### 3.3 Process-Based vs. Thread-Based — Side-by-Side Comparison

| Aspect                   | Process-Based                     | Thread-Based                         |
|--------------------------|-----------------------------------|--------------------------------------|
| **Unit of Execution**    | Entire program (process)          | Sub-task within a program (thread)   |
| **Memory**               | Separate memory per process       | Shared memory among threads          |
| **Communication**        | Complex (IPC, sockets, pipes)     | Simple (shared variables, methods)   |
| **Context Switching**    | Heavyweight (expensive)           | Lightweight (cheap)                  |
| **Scope**                | OS level                          | Program level                        |
| **Example**              | Editor + Music Player + Browser   | Video + Audio + Subtitles in one app |
| **Java's Focus**         | ❌ Not the primary concern        | ✅ Core strength of Java              |

> [!TIP]
> In interviews, always clarify that Java primarily deals with **thread-based multitasking**. Process-based multitasking is the OS's responsibility.

---

## 4 Why Multi-threading? — The Core Objective `[33:27]`, `[35:12]`

The primary objective of multitasking (and by extension, multi-threading) is to **maximize CPU utilization** by minimizing idle time and improving overall system performance.

### 4.1 The Problem — CPU Idle Time

In a single-threaded program, the CPU often sits idle while waiting for slow operations to complete:

```
 Single-Threaded Execution:

 CPU:  ████░░░░░░░░████░░░░░░████░░░░░░████
       work  idle      work  idle  work  idle  work

       ████ = CPU is busy (processing)
       ░░░░ = CPU is idle (waiting for I/O, network, disk, etc.)
```

### 4.2 The Solution — Multi-threading

With multi-threading, while one thread is waiting for a slow resource (I/O, network, database), another thread can **immediately use the CPU**:

```
 Multi-Threaded Execution:

 Thread 1:  ████░░░░████░░░░████
 Thread 2:  ░░░░████░░░░████░░░░
 Thread 3:  ██░░░░████░░░░████░░

 CPU:       ████████████████████
            CPU is almost NEVER idle!
```

### 4.3 Key Benefits

| #   | Benefit                           | Description                                                      |
|-----|-----------------------------------|------------------------------------------------------------------|
| 1   | **Reduced CPU Idle Time**         | Threads fill the gaps when other threads are waiting             |
| 2   | **Improved Response Time**        | Users get faster responses because tasks run in parallel         |
| 3   | **Better Resource Utilization**   | Maximum use of CPU, memory, and I/O channels                     |
| 4   | **Enhanced User Experience**      | Applications remain responsive even during heavy processing      |
| 5   | **Scalability**                   | Systems can handle more concurrent users/requests                |

> [!IMPORTANT]
> The main advantage of multi-threading is not about doing more work — it is about **doing work smarter** by keeping the processor busy at all times.

---

## 5 Application Areas of Multi-threading

Multi-threading is essential in scenarios where multiple independent tasks need to happen simultaneously to ensure efficiency and responsiveness.

### 5.1 Multimedia, Graphics, and Animation `[46:17]`

Rendering complex visuals requires simultaneous processing of multiple elements:

```
 ┌──────────────────────────────────────────────┐
 │            Animation Application              │
 │                                              │
 │   Thread 1: Render frames (30/60 FPS)        │
 │   Thread 2: Handle user input (mouse/keys)   │
 │   Thread 3: Play background music            │
 │   Thread 4: Load assets from disk            │
 │   Thread 5: Run physics engine               │
 │                                              │
 │   Without threads → Application FREEZES      │
 │   With threads    → Smooth experience        │
 └──────────────────────────────────────────────┘
```

- If animation rendering, user input, and audio were on a **single thread**, the application would **freeze** every time a frame is being rendered.
- Multi-threading ensures the UI remains responsive while heavy work happens in the background.

### 5.2 Web and Application Servers `[48:34]`

Servers like **Apache Tomcat** use multi-threading to handle thousands of concurrent user requests:

```
                    ┌─────────────┐
  User 1 ────────►  │             │ ──► Thread 1 ──► Process Request 1
  User 2 ────────►  │   Tomcat    │ ──► Thread 2 ──► Process Request 2
  User 3 ────────►  │   Server    │ ──► Thread 3 ──► Process Request 3
     ...             │             │
  User N ────────►  │  (Thread    │ ──► Thread N ──► Process Request N
                    │   Pool)     │
                    └─────────────┘
```

| Scenario            | Without Multi-threading                  | With Multi-threading                     |
|---------------------|------------------------------------------|------------------------------------------|
| **User Capacity**   | Only 1 user at a time                    | Thousands of users concurrently          |
| **Response Time**   | Each user waits for all previous users   | Each user gets an independent thread     |
| **Server Behavior** | Sequential, blocking                     | Parallel, non-blocking                   |

> [!NOTE]
> This is exactly how real web servers like Tomcat, Jetty, and Undertow work. Every incoming HTTP request is assigned to a thread from a **thread pool**, allowing a single server to support thousands of simultaneous users.

### 5.3 Task Parallelization — Divide and Conquer `[53:55]`

For data-heavy operations, multi-threading can dramatically improve performance by splitting one large task into multiple smaller parallel tasks.

#### 5.3.1 Example — Searching a Large File System

Suppose you need to search for a specific file across a drive with **10,000 folders**.

**Single-Threaded Approach:**
```
 Thread 1: Search Folder 1 → Folder 2 → ... → Folder 10,000
 
 Total time: ~10,000 units
```

**Multi-Threaded Approach (10 threads):**
```
 Thread 1:  Search Folders     1 – 1,000
 Thread 2:  Search Folders 1,001 – 2,000
 Thread 3:  Search Folders 2,001 – 3,000
 ...
 Thread 10: Search Folders 9,001 – 10,000

 Total time: ~1,000 units (10× faster!)
```

| Approach          | Threads | Time per Thread | Total Time | Speedup  |
|-------------------|---------|-----------------|------------|----------|
| Single-Threaded   | 1       | 10,000 units    | 10,000     | 1×       |
| Multi-Threaded    | 10      | 1,000 units     | ~1,000     | ~10×     |

> [!TIP]
> This is the principle behind frameworks like **Fork/Join** in Java and **MapReduce** in distributed computing — break a huge problem into smaller pieces, solve them in parallel, and combine the results.

---

## 6 Java's Advantage in Multi-threading `[57:12]`, `[58:16]`

Developing multi-threaded applications in Java is significantly easier compared to older languages like **C** or **C++**, because Java provides **built-in, rich API support** for threading out of the box.

### 6.1 What Java Provides

| Component               | Description                                                       |
|--------------------------|-------------------------------------------------------------------|
| `Thread` class           | Concrete class to create and manage threads                       |
| `Runnable` interface     | Functional interface to define the task a thread will execute     |
| `ThreadGroup` class      | Group multiple threads for collective management                  |
| `synchronized` keyword   | Built-in mechanism for thread safety and mutual exclusion         |
| `wait()` / `notify()`   | Built-in inter-thread communication                               |
| `java.util.concurrent`  | Advanced concurrency package (Executors, Locks, Atomic classes)   |

### 6.2 Java vs. Older Languages

| Aspect                          | C / C++                                           | Java                                               |
|---------------------------------|---------------------------------------------------|-----------------------------------------------------|
| **Threading API**               | External libraries (pthreads, Win32 API)          | Built-in (`java.lang.Thread`, `java.util.concurrent`) |
| **Thread Safety**               | Manual mutex/semaphore management                 | `synchronized` keyword — one line                   |
| **Memory Management**           | Manual allocation/deallocation (error-prone)      | Automatic garbage collection                        |
| **Platform Independence**       | Platform-specific threading code                  | Write once, run anywhere                            |
| **Complexity for Programmer**   | Must implement low-level mechanisms               | 90% handled by the Java API                         |

### 6.3 The 90/10 Rule

> [!IMPORTANT]
> In Java, **90%** of the complex underlying threading mechanisms — such as context switching, thread scheduling, stack management, and the `start()` method internals — are already implemented by the Java API. The programmer only needs to focus on **10%** — defining the task logic and managing synchronization.

```
 ┌────────────────────────────────────────────────────┐
 │               Multi-threading in Java               │
 │                                                    │
 │   ┌──────────────────────────────────────────────┐ │
 │   │            Java API Handles (90%)            │ │
 │   │                                              │ │
 │   │  • Thread lifecycle management               │ │
 │   │  • Context switching                         │ │
 │   │  • Thread scheduling                         │ │
 │   │  • Stack frame management                    │ │
 │   │  • Native OS thread mapping                  │ │
 │   │  • start() method internals                  │ │
 │   └──────────────────────────────────────────────┘ │
 │                                                    │
 │   ┌──────────────────────────────────────────────┐ │
 │   │         Programmer Handles (10%)             │ │
 │   │                                              │ │
 │   │  • Define the task (run() method)            │ │
 │   │  • Manage synchronization                    │ │
 │   │  • Handle inter-thread communication         │ │
 │   └──────────────────────────────────────────────┘ │
 └────────────────────────────────────────────────────┘
```

---

## 7 Summary — Introduction to Multi-threading

| #   | Concept                        | Key Point                                                                              |
|-----|--------------------------------|----------------------------------------------------------------------------------------|
| 1   | **Multitasking**               | Executing multiple tasks simultaneously to improve efficiency                          |
| 2   | **Process-Based**              | Multiple independent programs running at OS level (heavyweight)                        |
| 3   | **Thread-Based**               | Multiple parts of the same program running concurrently (lightweight)                  |
| 4   | **Why Multi-threading?**       | To reduce CPU idle time and improve response time / system performance                 |
| 5   | **Application Areas**          | Multimedia, Servers (Tomcat), Task Parallelization (Divide & Conquer)                  |
| 6   | **Java's Advantage**           | Rich built-in API — 90% of threading complexity handled by Java, only 10% by the programmer |

---

> **Coming Up Next:** Topic 2 — Defining a Thread by Implementing `Runnable`, Thread Constructors, and Thread Names

---
---

# Topic 2: Implementing Runnable, Thread Constructors & Thread Names

> 📺 **Video:** Core Java with OCJP/SCJP — Defining Threads by Implementing Runnable, Thread Names & currentThread()
> **By:** Durga Software Solutions

This topic covers the **second (and recommended)** approach to defining a thread — implementing the `Runnable` interface. It also explains the various `Thread` constructors, how thread names work, and how to identify the currently executing thread.

---

## 1 Defining a Thread by Implementing `Runnable` `[05:23]`

While extending the `Thread` class is one way to create a thread, the **recommended approach** is to implement the `Runnable` interface. This approach offers greater flexibility and better object-oriented design.

### 1.1 The Step-by-Step Approach

| Step | Action                                                              | Code                                        |
|------|---------------------------------------------------------------------|---------------------------------------------|
| 1    | Create a class that **implements** `Runnable`                       | `class MyTask implements Runnable { ... }`  |
| 2    | **Override** the `run()` method with the task logic                 | `public void run() { ... }`                |
| 3    | Create an object of this class (the **Runnable target**)            | `MyTask task = new MyTask();`              |
| 4    | Pass the target into the `Thread` constructor `[08:48]`             | `Thread t = new Thread(task);`             |
| 5    | Call `start()` on the `Thread` object `[09:09]`                     | `t.start();`                               |

### 1.2 Complete Example

```java
// Step 1: Implement the Runnable interface
class MyTask implements Runnable {

    // Step 2: Override the run() method — define the job
    @Override
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println("Child Thread: " + i);
        }
    }
}

public class RunnableDemo {
    public static void main(String[] args) {

        // Step 3: Create the Runnable target object
        MyTask task = new MyTask();

        // Step 4: Pass the target to the Thread constructor
        Thread t = new Thread(task);

        // Step 5: Start the thread
        t.start();

        // Main thread continues its own work
        for (int i = 0; i < 5; i++) {
            System.out.println("Main Thread: " + i);
        }
    }
}
```

### 1.3 Visual Flow

```
 ┌─────────────────────────────────────────────────────┐
 │                   main() method                      │
 │                                                     │
 │   MyTask task = new MyTask();     ─── Runnable obj  │
 │         │                                           │
 │         ▼                                           │
 │   Thread t = new Thread(task);    ─── Thread obj    │
 │         │                                           │
 │         ▼                                           │
 │   t.start();                                        │
 │         │                                           │
 │    ┌────┴────────────────────┐                      │
 │    │                         │                      │
 │    ▼                         ▼                      │
 │  Main Thread              Child Thread              │
 │  (continues in main)     (executes task.run())      │
 │                                                     │
 └─────────────────────────────────────────────────────┘
```

> [!IMPORTANT]
> You must call `t.start()`, **not** `task.run()`. Calling `run()` directly will execute the code in the **current thread** — no new thread is created.

### 1.4 Internal Mechanism — What Happens When `start()` is Called?

When `t.start()` is invoked, the following happens internally:

```
 t.start()
     │
     ▼
 1. JVM registers the thread with the Thread Scheduler
     │
     ▼
 2. JVM performs all low-level setup (stack allocation, native thread creation)
     │
     ▼
 3. Thread Scheduler allocates CPU time to the new thread
     │
     ▼
 4. JVM automatically calls the run() method of the Runnable target
     │
     ▼
 5. run() executes in the NEW child thread (not in main)
```

---

## 2 Why Implementing `Runnable` is Recommended `[32:14]`, `[36:51]`

### 2.1 The Inheritance Problem

In Java, a class can **only extend one class** (single inheritance). If your thread class extends `Thread`, it **cannot** extend any other class:

```java
// ❌ PROBLEM: Cannot extend both Thread and another class
class MyTask extends Thread {       // Already used the one allowed "extends"
    // Cannot extend MyApplication, HttpServlet, etc.
}
```

```java
// ✅ SOLUTION: Implement Runnable, keep "extends" free
class MyTask extends MyApplication implements Runnable {
    // Can extend MyApplication AND define thread logic
    @Override
    public void run() {
        // Task logic here
    }
}
```

### 2.2 Extending `Thread` vs. Implementing `Runnable`

| Aspect                     | Extending `Thread`                        | Implementing `Runnable`                    |
|----------------------------|-------------------------------------------|--------------------------------------------|
| **Inheritance**            | ❌ Cannot extend any other class          | ✅ Free to extend one other class          |
| **Design**                 | Your class **IS-A** Thread                | Your class **HAS-A** task (better OOP)     |
| **Flexibility**            | Tightly coupled to Thread                 | Loosely coupled — task is separate         |
| **Reusability**            | Task logic is locked inside Thread        | Same Runnable can be shared across threads |
| **Separation of Concerns** | Mixes "what to do" with "how to run"     | Cleanly separates task from thread         |
| **Recommendation**         | Use only for simple, standalone threads   | ✅ **Preferred approach in production**    |

> [!TIP]
> **Interview Tip:** Always state that implementing `Runnable` is the preferred approach because it preserves the single inheritance slot and provides better separation of concerns. This is a very common interview question.

### 2.3 Reusability Advantage — One Task, Multiple Threads

With `Runnable`, you can assign the **same task** to multiple threads:

```java
MyTask task = new MyTask();         // One task object

Thread t1 = new Thread(task);       // Thread 1 runs the same task
Thread t2 = new Thread(task);       // Thread 2 runs the same task
Thread t3 = new Thread(task);       // Thread 3 runs the same task

t1.start();
t2.start();
t3.start();
```

This is not possible when extending `Thread` — each `Thread` subclass object can only be started once.

---

## 3 Thread Constructors `[43:09]`

The `Thread` class provides **eight constructors** that allow you to create threads with different configurations.

### 3.1 All Eight Constructors

| #   | Constructor                                                      | Description                                         |
|-----|------------------------------------------------------------------|-----------------------------------------------------|
| 1   | `Thread()`                                                       | Creates a thread with a default name                |
| 2   | `Thread(Runnable target)`                                        | Creates a thread with the specified Runnable task   |
| 3   | `Thread(String name)`                                            | Creates a thread with a custom name                 |
| 4   | `Thread(Runnable target, String name)`                           | Creates a thread with a task and a custom name      |
| 5   | `Thread(ThreadGroup group, String name)`                         | Creates a thread in a specific group with a name    |
| 6   | `Thread(ThreadGroup group, Runnable target)`                     | Creates a thread in a specific group with a task    |
| 7   | `Thread(ThreadGroup group, Runnable target, String name)`        | Group + task + name                                 |
| 8   | `Thread(ThreadGroup group, Runnable target, String name, long stackSize)` | Group + task + name + custom stack size   |

### 3.2 Most Commonly Used Constructors

In practice, the following four constructors cover the vast majority of use cases:

```java
// 1. Default — no task, default name
Thread t1 = new Thread();

// 2. With Runnable target — most common
Thread t2 = new Thread(task);

// 3. With custom name — useful for debugging
Thread t3 = new Thread("WorkerThread");

// 4. With target and name — best practice
Thread t4 = new Thread(task, "DataProcessor");
```

> [!NOTE]
> The `ThreadGroup` and `stackSize` parameters are advanced features. For most applications, constructors 1–4 are sufficient.

---

## 4 Managing Thread Names `[52:15]`, `[56:26]`

Every thread in Java has a **name**. This name is critical for debugging, logging, and monitoring multi-threaded applications.

### 4.1 Default Thread Naming

If the programmer does not assign a name, the JVM automatically generates one using the pattern `Thread-N`, where `N` starts from `0`:

```java
Thread t1 = new Thread();    // Name: "Thread-0"
Thread t2 = new Thread();    // Name: "Thread-1"
Thread t3 = new Thread();    // Name: "Thread-2"
```

The **main thread** always has the name `"main"`.

```
 ┌──────────────────────────────────────────────┐
 │           JVM Default Thread Names            │
 │                                              │
 │   Main Thread  →  "main"                     │
 │   Thread 1     →  "Thread-0"                  │
 │   Thread 2     →  "Thread-1"                  │
 │   Thread 3     →  "Thread-2"                  │
 │   ...                                        │
 └──────────────────────────────────────────────┘
```

### 4.2 Getting and Setting Thread Names `[01:04:42]`, `[01:05:08]`

| Method                    | Return Type | Description                           |
|---------------------------|-------------|---------------------------------------|
| `getName()`               | `String`    | Returns the name of the thread        |
| `setName(String name)`    | `void`      | Changes the name of the thread        |

#### 4.2.1 Example — Get and Set Names

```java
class NameDemo {
    public static void main(String[] args) {

        // Get the main thread's name
        System.out.println("Current thread: " + Thread.currentThread().getName());
        // Output: Current thread: main

        Thread t = new Thread();
        System.out.println("Default name: " + t.getName());
        // Output: Default name: Thread-0

        // Change the thread's name
        t.setName("WorkerThread");
        System.out.println("Custom name: " + t.getName());
        // Output: Custom name: WorkerThread
    }
}
```

### 4.3 Changing the Main Thread's Name `[57:04]`

Even the **main thread's** name can be changed at runtime:

```java
public class MainThreadName {
    public static void main(String[] args) {

        Thread mainThread = Thread.currentThread();

        System.out.println("Before: " + mainThread.getName());
        // Output: Before: main

        mainThread.setName("PrimaryThread");

        System.out.println("After: " + mainThread.getName());
        // Output: After: PrimaryThread
    }
}
```

> [!NOTE]
> Changing the main thread's name is allowed and can be useful in logging frameworks where you want more descriptive thread identifiers.

---

## 5 Identifying the Currently Executing Thread `[54:14]`

### 5.1 `Thread.currentThread()` Method

`Thread.currentThread()` is a **static method** that returns a reference to the `Thread` object representing the thread that is **currently executing** the code.

| Method                         | Return Type | Description                                         |
|--------------------------------|-------------|-----------------------------------------------------|
| `Thread.currentThread()`       | `Thread`    | Returns the thread object currently executing code  |

### 5.2 Why is This Important? `[01:12:08]`

In a multi-threaded application, the **same `run()` method** can be executed by different threads. `Thread.currentThread()` allows you to determine **which thread** is actually running a specific block of code — essential for debugging and understanding execution flow.

### 5.3 Practical Example

```java
class SharedTask implements Runnable {
    @Override
    public void run() {
        // Which thread is running this code right now?
        System.out.println("Executing thread: " + Thread.currentThread().getName());
    }
}

public class CurrentThreadDemo {
    public static void main(String[] args) {

        SharedTask task = new SharedTask();

        Thread t1 = new Thread(task, "Alpha");
        Thread t2 = new Thread(task, "Beta");
        Thread t3 = new Thread(task, "Gamma");

        t1.start();
        t2.start();
        t3.start();

        // Main thread also calls currentThread()
        System.out.println("Main thread: " + Thread.currentThread().getName());
    }
}
```

**Possible Output (order may vary due to thread scheduling):**
```
Main thread: main
Executing thread: Alpha
Executing thread: Gamma
Executing thread: Beta
```

### 5.4 `this` vs. `Thread.currentThread()`

This distinction is subtle but **critical** for interviews:

| Context                              | `this`                                   | `Thread.currentThread()`                   |
|--------------------------------------|------------------------------------------|--------------------------------------------|
| **Inside a class extending `Thread`** | Refers to the Thread object itself       | Refers to the currently executing thread   |
| **Inside a `Runnable` implementation** | Refers to the Runnable object (NOT a Thread) | Refers to the Thread executing the Runnable |
| **Best Practice**                    | Avoid using `this` for thread identity   | ✅ Always use `Thread.currentThread()`     |

#### 5.4.1 Example — The Difference

```java
class MyRunnable implements Runnable {
    @Override
    public void run() {
        // 'this' refers to the MyRunnable object — NOT a Thread
        System.out.println("this: " + this);

        // Thread.currentThread() refers to the actual Thread executing this code
        System.out.println("Current thread: " + Thread.currentThread().getName());
    }
}

public class ThisVsCurrentThread {
    public static void main(String[] args) {
        MyRunnable task = new MyRunnable();
        Thread t = new Thread(task, "Worker");
        t.start();
    }
}
```

**Output:**
```
this: MyRunnable@<hashcode>          ← This is the Runnable object, NOT a Thread
Current thread: Worker               ← This is the actual thread name
```

> [!CAUTION]
> In a `Runnable` implementation, `this` does **NOT** refer to the thread. It refers to the Runnable object. Always use `Thread.currentThread()` to get the executing thread's reference.

---

## 6 Summary — Implementing Runnable, Constructors & Thread Names

| #   | Concept                          | Key Point                                                                                |
|-----|----------------------------------|------------------------------------------------------------------------------------------|
| 1   | **Implementing `Runnable`**      | Create a `Runnable` target → pass it to `Thread` constructor → call `start()`            |
| 2   | **Why Recommended**              | Preserves single inheritance slot; better separation of concerns and reusability          |
| 3   | **Thread Constructors**          | 8 constructors available; most common: `Thread(Runnable)` and `Thread(Runnable, String)` |
| 4   | **Default Thread Names**         | JVM auto-generates names: `Thread-0`, `Thread-1`, ...; main thread is named `"main"`    |
| 5   | **`getName()` / `setName()`**    | Get or change any thread's name, including the main thread                                |
| 6   | **`Thread.currentThread()`**     | Static method returning the currently executing thread; essential for debugging           |
| 7   | **`this` vs `currentThread()`**  | In `Runnable`, `this` is the Runnable object, NOT the thread — always use `currentThread()` |

---

> **Coming Up Next:** Topic 3 — Defining a Thread by Extending the `Thread` Class

---
---

# Topic 3: Defining a Thread by Extending the `Thread` Class

> 📺 **Video:** Core Java with OCJP/SCJP — Defining a Thread by Extending Thread Class
> **By:** Durga Software Solutions

This topic covers the **first approach** to defining a thread in Java — extending the `Thread` class. It dives deep into the mechanics of `start()` vs `run()`, the thread scheduler, the basic thread life cycle, and common pitfalls.

---

## 1 Defining a Thread by Extending `Thread` `[06:23]`, `[10:04]`

The simplest way to define a thread is to create a class that extends the `Thread` class and overrides the `run()` method.

### 1.1 The Step-by-Step Approach

| Step | Action                                                              | Code                                        |
|------|---------------------------------------------------------------------|---------------------------------------------|
| 1    | Create a class that **extends** `Thread`                            | `class MyThread extends Thread { ... }`     |
| 2    | **Override** the `run()` method — this is the thread's "job"        | `public void run() { ... }`                |
| 3    | Create an object of this class                                      | `MyThread t = new MyThread();`             |
| 4    | Call `start()` on the thread object                                 | `t.start();`                               |

### 1.2 Complete Example

```java
// Step 1: Extend the Thread class
class MyThread extends Thread {

    // Step 2: Override the run() method — define the job
    @Override
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println("Child Thread: " + i);
        }
    }
}

public class ThreadDemo {
    public static void main(String[] args) {

        // Step 3: Create the thread object
        MyThread t = new MyThread();

        // Step 4: Start the thread
        t.start();

        // Main thread continues its own work
        for (int i = 0; i < 5; i++) {
            System.out.println("Main Thread: " + i);
        }
    }
}
```

### 1.3 Visual Flow

```
 ┌─────────────────────────────────────────────────────┐
 │                   main() method                      │
 │                                                     │
 │   MyThread t = new MyThread();    ─── Thread obj    │
 │         │                                           │
 │         ▼                                           │
 │   t.start();                                        │
 │         │                                           │
 │    ┌────┴────────────────────┐                      │
 │    │                         │                      │
 │    ▼                         ▼                      │
 │  Main Thread              Child Thread              │
 │  (continues in main)     (executes t.run())         │
 │                                                     │
 └─────────────────────────────────────────────────────┘
```

---

## 2 The Thread Scheduler `[19:51]`, `[20:43]`, `[26:34]`

The **Thread Scheduler** is a component of the JVM responsible for deciding which thread gets CPU time and in what order.

### 2.1 Key Characteristics

| Property                    | Description                                                        |
|-----------------------------|--------------------------------------------------------------------|
| **Part of**                 | The JVM (not the programmer's control)                             |
| **Algorithm**               | Not guaranteed — varies from JVM to JVM                            |
| **Determinism**             | ❌ You **cannot** predict the exact order of thread execution      |
| **Output**                  | Only consider "possible outputs", never expect a specific one      |

### 2.2 Why Output is Unpredictable

```java
public class SchedulerDemo {
    public static void main(String[] args) {
        MyThread t = new MyThread();
        t.start();

        for (int i = 0; i < 3; i++) {
            System.out.println("Main: " + i);
        }
    }
}
```

**Possible Output 1:**
```
Main: 0
Child Thread: 0
Main: 1
Child Thread: 1
Main: 2
Child Thread: 2
```

**Possible Output 2:**
```
Child Thread: 0
Child Thread: 1
Child Thread: 2
Main: 0
Main: 1
Main: 2
```

**Possible Output 3:**
```
Main: 0
Main: 1
Main: 2
Child Thread: 0
Child Thread: 1
Child Thread: 2
```

> [!CAUTION]
> In multi-threading, **never write code that depends on a specific execution order** of threads. If you need ordering, use synchronization mechanisms like `join()`, `wait()/notify()`, or other concurrency tools.

---

## 3 `start()` vs `run()` — The Most Critical Distinction `[33:50]`, `[34:18]`, `[38:28]`

This is one of the **most frequently asked interview questions** in Java.

### 3.1 What `start()` Does

When you call `t.start()`:

```
 t.start()
     │
     ▼
 1. A NEW, SEPARATE call stack is created
     │
     ▼
 2. A new thread is BORN (registered with the scheduler)
     │
     ▼
 3. JVM automatically calls run() in this NEW thread
     │
     ▼
 4. run() executes CONCURRENTLY with the calling thread
```

### 3.2 What `run()` Does (When Called Directly)

When you call `t.run()` directly:

```
 t.run()
     │
     ▼
 1. NO new thread is created
     │
     ▼
 2. NO new call stack is created
     │
     ▼
 3. run() executes like a NORMAL METHOD in the CURRENT thread
     │
     ▼
 4. Execution is SEQUENTIAL, not concurrent
```

### 3.3 Side-by-Side Comparison

| Aspect                   | `t.start()`                                | `t.run()`                                  |
|--------------------------|--------------------------------------------|--------------------------------------------|
| **New Thread?**          | ✅ Yes — a new thread is created           | ❌ No — runs in the current thread         |
| **New Call Stack?**      | ✅ Yes — separate stack for the new thread | ❌ No — uses the existing stack            |
| **Execution**            | Concurrent / Parallel                      | Sequential / Same thread                   |
| **Who calls `run()`?**   | The JVM (internally, in the new thread)    | The programmer (like any normal method)    |
| **Multi-threading?**     | ✅ Achieved                                | ❌ NOT achieved                            |

### 3.4 Example — The Difference in Action

```java
class MyThread extends Thread {
    @Override
    public void run() {
        System.out.println("run() executed by: " + Thread.currentThread().getName());
    }
}

public class StartVsRun {
    public static void main(String[] args) {
        MyThread t = new MyThread();

        // Case 1: Using start()
        t.start();
        // Output: run() executed by: Thread-0   ← NEW thread

        // Case 2: Using run() directly
        MyThread t2 = new MyThread();
        t2.run();
        // Output: run() executed by: main        ← SAME thread (no multi-threading!)
    }
}
```

> [!IMPORTANT]
> ⭐ **Interview Answer:** `start()` creates a new thread and internally calls `run()` in that new thread. Calling `run()` directly does NOT create a new thread — it simply executes as a normal method in the caller's thread. **Always use `start()` for multi-threading.**

---

## 4 Importance of `start()` — The Heart of Multi-threading `[46:02]`, `[50:19]`

The `Thread.start()` method is the **heart** of multi-threading. Without it, no new thread can be initiated.

### 4.1 What `start()` Does Internally

```
 t.start()
     │
     ├──► 1. Register the thread with the Thread Scheduler
     │
     ├──► 2. Allocate a new call stack for the thread
     │
     ├──► 3. Perform all mandatory JVM-level setup
     │        (native thread creation, memory allocation)
     │
     └──► 4. Invoke the run() method in the new thread
```

### 4.2 Why You Cannot Skip `start()`

| Without `start()`                                | With `start()`                                    |
|--------------------------------------------------|---------------------------------------------------|
| Thread is NOT registered with the scheduler      | Thread IS registered with the scheduler           |
| No new call stack is created                     | A new, independent call stack is created          |
| `run()` runs as a normal method in current thread | `run()` runs in its own separate thread           |
| No multi-threading occurs                        | True multi-threading is achieved                  |

---

## 5 Overloading the `run()` Method `[53:30]`, `[54:24]`, `[58:14]`

### 5.1 Is Overloading Allowed?

**Yes**, overloading `run()` is perfectly legal in Java. You can define multiple `run()` methods with different parameter lists.

### 5.2 The Catch — `start()` Always Calls the No-Arg `run()`

The `Thread.start()` method will **always** invoke the **no-argument** `run()` method. Any overloaded versions must be called manually.

```java
class MyThread extends Thread {

    // This is the run() that start() will call
    @Override
    public void run() {
        System.out.println("No-arg run() — called by start()");
    }

    // Overloaded run() — start() will NEVER call this
    public void run(int count) {
        System.out.println("Overloaded run(" + count + ") — must be called manually");
    }
}

public class OverloadRunDemo {
    public static void main(String[] args) {
        MyThread t = new MyThread();

        t.start();          // Calls: run()         ← no-arg version
        t.run(10);          // Calls: run(int)      ← manual call, no new thread
    }
}
```

**Output:**
```
No-arg run() — called by start()
Overloaded run(10) — must be called manually
```

> [!NOTE]
> Overloading `run()` is legal but rarely useful. The overloaded versions are just regular methods — they have no special thread behavior.

---

## 6 Not Overriding `run()` `[01:02:16]`

### 6.1 What Happens?

If you extend `Thread` but **do not override** `run()`, the code will still **compile and run without errors**. However, nothing useful will happen because the default `Thread.run()` method has an **empty implementation**.

```java
class MyThread extends Thread {
    // No run() method overridden!
}

public class NoRunDemo {
    public static void main(String[] args) {
        MyThread t = new MyThread();
        t.start();

        // A new thread IS created and started,
        // but it immediately terminates because
        // the default run() does NOTHING.

        System.out.println("Main thread completes.");
    }
}
```

**Output:**
```
Main thread completes.
```

### 6.2 The Default `run()` in the `Thread` Class

```java
// Inside java.lang.Thread (simplified)
public class Thread implements Runnable {
    private Runnable target;

    @Override
    public void run() {
        if (target != null) {
            target.run();
        }
        // If target is null and run() is not overridden → does nothing
    }
}
```

| Scenario                          | Behavior                                           |
|-----------------------------------|-----------------------------------------------------|
| `run()` is overridden             | ✅ Your custom code executes in the new thread      |
| `run()` is NOT overridden         | The default empty `run()` executes — thread does nothing |
| `Runnable` target is provided     | Default `run()` delegates to `target.run()`         |

> [!TIP]
> Not overriding `run()` is not a compile-time error, but it defeats the purpose of creating a thread. Always override it with your task logic.

---

## 7 Overriding `start()` — Not Recommended `[01:14:44]`, `[01:16:01]`

### 7.1 Can You Override `start()`?

**Yes**, you can override `start()`. But you **should not** — unless you have a very specific reason, and even then, you **must** call `super.start()`.

### 7.2 What Happens Without `super.start()`

If you override `start()` without calling `super.start()`, the JVM will execute your overridden method like a **normal method call**. No new thread will be created.

```java
class MyThread extends Thread {
    @Override
    public void start() {
        // ❌ No super.start() — no new thread is created!
        System.out.println("start() overridden — runs in: " + Thread.currentThread().getName());
    }

    @Override
    public void run() {
        System.out.println("run() — runs in: " + Thread.currentThread().getName());
    }
}

public class OverrideStartBad {
    public static void main(String[] args) {
        MyThread t = new MyThread();
        t.start();
    }
}
```

**Output:**
```
start() overridden — runs in: main       ← No new thread! Runs in main thread.
```

> `run()` is **never called** because `super.start()` was never invoked.

### 7.3 The Correct Way — With `super.start()`

```java
class MyThread extends Thread {
    @Override
    public void start() {
        System.out.println("Custom setup before starting thread...");
        super.start();      // ✅ This ensures a new thread is created
    }

    @Override
    public void run() {
        System.out.println("run() — runs in: " + Thread.currentThread().getName());
    }
}

public class OverrideStartGood {
    public static void main(String[] args) {
        MyThread t = new MyThread();
        t.start();
    }
}
```

**Output:**
```
Custom setup before starting thread...    ← Runs in main thread
run() — runs in: Thread-0                 ← Runs in NEW thread ✅
```

> [!CAUTION]
> Overriding `start()` without calling `super.start()` is a **silent bug** — the code compiles and runs, but no new thread is ever created. This is very hard to debug.

---

## 8 Thread Life Cycle (Basic States) `[01:26:11]`

Every thread in Java passes through a defined set of **states** during its lifetime.

### 8.1 The Four Basic States

```
 ┌─────────────────────────────────────────────────────────────┐
 │                   Thread Life Cycle (Basic)                  │
 │                                                             │
 │   new MyThread()          t.start()          Scheduler       │
 │        │                     │               allocates CPU   │
 │        ▼                     ▼                    │          │
 │   ┌─────────┐          ┌──────────┐          ┌─────────┐   │
 │   │  NEW /  │ ──────►  │ RUNNABLE │ ──────►  │ RUNNING │   │
 │   │  BORN   │  start() │ (Ready)  │ Scheduler│         │   │
 │   └─────────┘          └──────────┘          └────┬────┘   │
 │                                                    │        │
 │                                             run() completes │
 │                                                    │        │
 │                                               ┌────▼────┐   │
 │                                               │  DEAD   │   │
 │                                               │         │   │
 │                                               └─────────┘   │
 └─────────────────────────────────────────────────────────────┘
```

### 8.2 State Details

| #   | State                     | Trigger                                  | Description                                       |
|-----|---------------------------|------------------------------------------|---------------------------------------------------|
| 1   | **New / Born** `[01:26:11]` | `new MyThread()`                         | Thread object is created but not yet started      |
| 2   | **Runnable** `[01:26:32]`   | `t.start()`                              | Thread is ready and waiting for the scheduler     |
| 3   | **Running** `[01:27:11]`    | Scheduler allocates CPU                  | Thread is actively executing its `run()` method   |
| 4   | **Dead** `[01:27:32]`       | `run()` completes (or exception thrown)  | Thread has finished execution — cannot be restarted |

### 8.3 State Transitions

```
 NEW ──start()──► RUNNABLE ──scheduler──► RUNNING ──run() ends──► DEAD
                      ▲                      │
                      │                      │
                      └──── scheduler ───────┘
                       (thread can move back
                        to Runnable if the
                        scheduler preempts it)
```

> [!NOTE]
> A thread can move back and forth between **Runnable** and **Running** states multiple times during its lifetime as the scheduler preempts and re-allocates CPU time. But once it reaches the **Dead** state, it **cannot** go back.

---

## 9 `IllegalThreadStateException` `[01:40:44]`

### 9.1 The Rule

Once a thread has been started, you **cannot restart it**. Calling `start()` on a thread that is already started (whether running or dead) throws a **runtime exception**.

### 9.2 Example

```java
class MyThread extends Thread {
    @Override
    public void run() {
        System.out.println("Thread is running...");
    }
}

public class RestartDemo {
    public static void main(String[] args) {
        MyThread t = new MyThread();

        t.start();          // ✅ First call — thread starts normally

        // t.start();       // ❌ Second call — throws IllegalThreadStateException!
    }
}
```

### 9.3 What Happens with Each Call

| Call         | Thread State     | Result                                    |
|--------------|------------------|-------------------------------------------|
| `t.start()` (1st) | New → Runnable   | ✅ Thread starts normally                 |
| `t.start()` (2nd) | Runnable/Dead    | ❌ `IllegalThreadStateException` thrown   |
| `t.start()` (3rd) | Dead             | ❌ `IllegalThreadStateException` thrown   |

### 9.4 The Exception Output

```
Exception in thread "main" java.lang.IllegalThreadStateException
    at java.lang.Thread.start(Thread.java:708)
    at RestartDemo.main(RestartDemo.java:12)
```

> [!IMPORTANT]
> A thread's lifecycle is **one-way**: `New → Runnable → Running → Dead`. Once dead, a thread **cannot be resurrected**. If you need to repeat a task, create a **new** thread object.

---

## 10 Summary — Extending the `Thread` Class

| #   | Concept                          | Key Point                                                                                |
|-----|----------------------------------|------------------------------------------------------------------------------------------| 
| 1   | **Defining a Thread**            | Extend `Thread` → override `run()` → call `start()`                                     |
| 2   | **Thread Scheduler**             | JVM component; execution order is unpredictable — only consider "possible outputs"       |
| 3   | **`start()` vs `run()`**         | `start()` creates a new thread; `run()` runs as a normal method in the current thread    |
| 4   | **Importance of `start()`**      | Heart of multi-threading — handles registration, stack creation, then invokes `run()`    |
| 5   | **Overloading `run()`**          | Legal, but `start()` always calls the no-arg `run()`; overloaded versions need manual calls |
| 6   | **Not Overriding `run()`**       | Compiles fine, but the thread does nothing (default `run()` is empty)                    |
| 7   | **Overriding `start()`**         | Not recommended; must call `super.start()` or no new thread is created                   |
| 8   | **Thread Life Cycle**            | New → Runnable → Running → Dead (one-way lifecycle)                                      |
| 9   | **`IllegalThreadStateException`**| Thrown if you call `start()` on an already-started thread — threads cannot be restarted   |

---

> **Coming Up Next:** Topic 4 — Thread Priorities

---
---

# Topic 4: Thread Priorities

> 📺 **Video:** Core Java with OCJP/SCJP — Thread Priorities
> **By:** Durga Software Solutions

This topic explains the thread priority mechanism in Java — how the Thread Scheduler uses priorities to influence execution order, the valid range, default values, inheritance behavior, and important platform-level caveats.

---

## 1 What are Thread Priorities? `[00:36]`, `[17:06]`

Every thread in Java has a **priority** — an integer value that serves as a **hint to the Thread Scheduler**. When multiple threads are in the **Runnable** state and competing for CPU time, the scheduler uses these priorities to decide which thread gets to run next.

```
 ┌─────────────────────────────────────────────────────┐
 │              Thread Scheduler                        │
 │                                                     │
 │   Runnable Threads (waiting for CPU):               │
 │                                                     │
 │   ┌──────────┐  ┌──────────┐  ┌──────────────────┐ │
 │   │ Thread A │  │ Thread B │  │    Thread C      │ │
 │   │ Priority │  │ Priority │  │   Priority       │ │
 │   │    10    │  │    5     │  │      1           │ │
 │   └──────────┘  └──────────┘  └──────────────────┘ │
 │                                                     │
 │   Scheduler PREFERS Thread A (highest priority)     │
 │   But behavior is NOT guaranteed — it's a hint      │
 └─────────────────────────────────────────────────────┘
```

> [!IMPORTANT]
> Priorities are **suggestions**, not commands. The Thread Scheduler is free to ignore them. The actual behavior depends on the underlying operating system's scheduling algorithm.

---

## 2 Priority Range & Constants `[01:49]`, `[07:33]`

Thread priorities in Java are represented as integers within a fixed range, with three named constants provided by the `Thread` class for convenience.

| Constant                  | Value | Description                  |
|---------------------------|-------|------------------------------|
| `Thread.MIN_PRIORITY`     | `1`   | Lowest possible priority     |
| `Thread.NORM_PRIORITY`    | `5`   | Default priority for threads |
| `Thread.MAX_PRIORITY`     | `10`  | Highest possible priority    |

```
  Priority Scale:

  1 ─── 2 ─── 3 ─── 4 ─── 5 ─── 6 ─── 7 ─── 8 ─── 9 ─── 10
  │                         │                               │
  MIN_PRIORITY         NORM_PRIORITY                  MAX_PRIORITY
  (lowest)             (default)                      (highest)
```

> [!NOTE]
> These are not "ranks" in the sense that a higher number implies more "important" in a human sense. They are numerical instructions to the scheduler, indicating relative preference for CPU allocation.

---

## 3 Methods for Thread Priority `[22:28]`

The `Thread` class provides two methods for inspecting and modifying a thread's priority:

| Method                   | Return Type | Description                                |
|--------------------------|-------------|--------------------------------------------|
| `getPriority()`          | `int`       | Returns the current priority of the thread |
| `setPriority(int p)`     | `void`      | Sets the priority of the thread            |

### 3.1 Basic Example

```java
class PriorityDemo {
    public static void main(String[] args) {

        Thread t = new Thread();

        // Get the default priority
        System.out.println("Default priority: " + t.getPriority());
        // Output: Default priority: 5

        // Set a custom priority
        t.setPriority(8);
        System.out.println("Updated priority: " + t.getPriority());
        // Output: Updated priority: 8

        // Using named constants
        t.setPriority(Thread.MAX_PRIORITY);
        System.out.println("Max priority: " + t.getPriority());
        // Output: Max priority: 10
    }
}
```

### 3.2 Error Handling — `IllegalArgumentException` `[22:28]`, `[26:03]`

If you attempt to set a priority **outside the valid range** (1–10), the JVM throws an `IllegalArgumentException` at runtime:

```java
Thread t = new Thread();

t.setPriority(0);    // ❌ IllegalArgumentException (below 1)
t.setPriority(11);   // ❌ IllegalArgumentException (above 10)
t.setPriority(-1);   // ❌ IllegalArgumentException (negative)
t.setPriority(100);  // ❌ IllegalArgumentException (way out of range)
```

```
 ┌──────────────────────────────────────────────────────┐
 │           setPriority(int p) Validation               │
 │                                                      │
 │   if (p < 1 || p > 10)                               │
 │       throw new IllegalArgumentException();           │
 │                                                      │
 │   Valid Range:   1 ≤ p ≤ 10                           │
 │   Invalid:       p < 1  OR  p > 10                    │
 └──────────────────────────────────────────────────────┘
```

> [!CAUTION]
> This is a **runtime exception**, not a compile-time error. The code will compile without any issues — the exception only surfaces when the invalid `setPriority()` call is executed.

---

## 4 Default Priorities & Inheritance `[27:19]`, `[28:47]`

### 4.1 Main Thread Default Priority

The **main thread** always starts with a priority of **5** (`Thread.NORM_PRIORITY`):

```java
public class MainPriority {
    public static void main(String[] args) {
        System.out.println("Main thread priority: "
            + Thread.currentThread().getPriority());
        // Output: Main thread priority: 5
    }
}
```

### 4.2 Priority Inheritance

When a new thread is created, it **inherits its priority from the parent thread** (the thread that created it). It does **not** default to `5` unconditionally — it copies whatever priority the parent has at the time of creation.

```java
class InheritanceDemo {
    public static void main(String[] args) {

        // Main thread priority is 5 by default
        System.out.println("Main priority: "
            + Thread.currentThread().getPriority());
        // Output: Main priority: 5

        Thread child1 = new Thread(() -> {});
        System.out.println("Child1 priority: " + child1.getPriority());
        // Output: Child1 priority: 5  (inherits from main)

        // Change main thread's priority to 9
        Thread.currentThread().setPriority(9);

        Thread child2 = new Thread(() -> {});
        System.out.println("Child2 priority: " + child2.getPriority());
        // Output: Child2 priority: 9  (inherits the updated parent priority)
    }
}
```

```
 ┌──────────────────────────────────────────────────────┐
 │            Priority Inheritance Chain                  │
 │                                                      │
 │   Main Thread (priority = 5)                         │
 │       │                                              │
 │       ├── Child Thread A  →  inherits priority 5     │
 │       │                                              │
 │   Main Thread priority changed to 9                  │
 │       │                                              │
 │       ├── Child Thread B  →  inherits priority 9     │
 │       │                                              │
 │       └── Child Thread C  →  inherits priority 9     │
 └──────────────────────────────────────────────────────┘
```

> [!IMPORTANT]
> The inherited priority is a **snapshot at creation time**. If the parent's priority changes *after* the child is created, the child's priority is **not** retroactively updated.

---

## 5 Thread Scheduler Behavior `[18:40]`, `[19:38]`

### 5.1 Higher Priority Preference

The Thread Scheduler **generally prefers** threads with higher priority values. A thread with priority `10` is more likely to get CPU time than a thread with priority `1`.

```
 ┌──────────────────────────────────────────────────────┐
 │          Scheduler Priority Preference                │
 │                                                      │
 │   Priority 10:  ████████████████████  (most CPU)     │
 │   Priority  7:  ████████████                         │
 │   Priority  5:  ████████                             │
 │   Priority  3:  ████                                 │
 │   Priority  1:  ██                    (least CPU)    │
 │                                                      │
 │   This is the EXPECTED behavior, but NOT guaranteed  │
 └──────────────────────────────────────────────────────┘
```

### 5.2 Equal Priority — No Guaranteed Order

If two or more threads have the **same priority**, the execution order is **not guaranteed**. The actual order depends on the specific algorithm used by the underlying Thread Scheduler.

| Scheduling Algorithm      | Behavior                                                     |
|---------------------------|--------------------------------------------------------------|
| **Round Robin**           | Each thread gets equal time slices in rotation               |
| **First-Come-First-Served** | Threads are scheduled in the order they entered the queue  |
| **Preemptive**            | Higher-priority threads interrupt lower-priority ones        |
| **Platform-Specific**     | Varies by OS — the JVM maps to the native scheduler         |

> [!NOTE]
> The exact scheduling algorithm is platform-dependent and **not specified** by the Java Language Specification. You should never write code that relies on a specific scheduling order.

---

## 6 Practical Example — Priority in Action

```java
class PriorityTask extends Thread {

    public PriorityTask(String name) {
        super(name);
    }

    @Override
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println(getName() + " [Priority "
                + getPriority() + "] — iteration " + i);
        }
    }
}

public class PriorityExample {
    public static void main(String[] args) {

        PriorityTask low    = new PriorityTask("LowThread");
        PriorityTask normal = new PriorityTask("NormalThread");
        PriorityTask high   = new PriorityTask("HighThread");

        low.setPriority(Thread.MIN_PRIORITY);       // 1
        normal.setPriority(Thread.NORM_PRIORITY);    // 5
        high.setPriority(Thread.MAX_PRIORITY);       // 10

        low.start();
        normal.start();
        high.start();
    }
}
```

**Expected Behavior:**
- `HighThread` (priority 10) is **most likely** to finish first.
- `LowThread` (priority 1) is **most likely** to finish last.
- However, the actual order is **not guaranteed** — it depends on the OS and JVM implementation.

---

## 7 Platform Limitations `[56:07]`, `[58:08]`

### 7.1 The Platform-Dependence Problem

Some operating systems do **not fully support** Java's 10-level priority system. The JVM maps Java's 10 priority levels to the **native OS priority levels**, and different OSes have different numbers of priority levels.

| Operating System | Native Priority Levels | Java Mapping                                   |
|------------------|------------------------|-------------------------------------------------|
| **Linux**        | ~2 (normal, real-time) | Multiple Java levels may map to the same OS level |
| **Windows**      | 7 levels               | Some Java levels collapse into the same OS level  |
| **Solaris**      | ~128 levels            | Good granularity — close to 1:1 mapping          |

### 7.2 Practical Impact

```
 ┌──────────────────────────────────────────────────────┐
 │        Platform Priority Mapping (Simplified)         │
 │                                                      │
 │   Java Priority:   1  2  3  4  5  6  7  8  9  10    │
 │                    │  │  │  │  │  │  │  │  │  │     │
 │   Some OS Levels:  ▼  ▼  ▼  ▼  ▼  ▼  ▼  ▼  ▼  ▼   │
 │                    1  1  1  2  3  4  5  5  6  7     │
 │                                                      │
 │   Java priorities 1, 2, 3 → ALL map to OS level 1   │
 │   Setting priority 1 vs 3 has NO practical effect!   │
 └──────────────────────────────────────────────────────┘
```

> [!WARNING]
> Even if you explicitly set thread priorities, the expected execution order may **not** be observed on all platforms. This is a **platform-dependent issue**, not a problem with the Java code itself. Do not write code that depends on thread priorities for correctness — use them only as performance hints.

---

## 8 Summary — Thread Priorities

| #   | Concept                          | Key Point                                                                                 |
|-----|----------------------------------|-------------------------------------------------------------------------------------------|
| 1   | **Priority Range**               | Valid range is `1` to `10`; constants: `MIN_PRIORITY (1)`, `NORM_PRIORITY (5)`, `MAX_PRIORITY (10)` |
| 2   | **`getPriority()` / `setPriority()`** | Get or set a thread's priority; invalid values throw `IllegalArgumentException`          |
| 3   | **Main Thread Default**          | Main thread starts with priority `5` (`NORM_PRIORITY`)                                   |
| 4   | **Priority Inheritance**         | Child threads inherit priority from the parent thread at the time of creation             |
| 5   | **Scheduler Behavior**           | Higher-priority threads are generally preferred, but order is never guaranteed             |
| 6   | **Equal Priority**               | Execution order depends on the OS-specific scheduling algorithm (Round Robin, FCFS, etc.) |
| 7   | **Platform Limitations**         | Some OSes don't fully support 10 priority levels — multiple Java levels may map to one OS level |

---

> **Coming Up Next:** Topic 5 — Methods to Prevent Thread Execution (`yield()`, `join()`, `sleep()`)

---
