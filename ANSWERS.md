# Assignment Questions

## Instructions
Answer all 4 questions with detailed explanations. Each answer should be **3-5 sentences minimum** and demonstrate your understanding of the concepts.

---

## Question 1: Thread vs Process

**Question**: Explain the difference between a **thread** and a **process**. Why did we use threads in this assignment instead of creating separate processes?

**Your Answer:**

[a process is like a program that is running with its memory. on the hand a thread is a smaller unit that shares memory with other threads. this means threads are easier to create and they can talk to each other faster.

we used threads in this assignment of separate processes because threads can do many things at the same time and they can easily share things, like the process queue within a single application.

this is shown in the schedulersimulation.java file where we make threads using thread thread = thread(process) and start them. these threads share the memory space.

by using these threads instead of big processes our simulation does not have to deal with the high time and resource overhead that comes with the operating system switching between full processes. we used threads to avoid this problem. threads are what made our simulation work better
]

---

## Question 2: Ready Queue Behavior

**Question**: In Round-Robin scheduling, what happens when a process doesn't finish within its time quantum? Explain using an example from your program output.

**Your Answer:**

[in round-robin scheduling when a process doesn't finish within its allocated time quantum it is preempted. the process pauses its execution yields the cpu and is sent to the very back of the ready queue. it must then wait in the queue and will only run again after all the other processes ahead of it have received their respective time slice]

Example from my output:
```
? P1 executing quantum [4000ms]
  ? Quantum progress: [???????????????] 100%
  ? P1 completed quantum 4000ms ? Overall progress: [????????????????????] 46%
     Remaining time: 4574ms
  ? P1 yields CPU for context switch

  ? P1 ( Priority: 3) enters the ready queue... ? Burst time: 8574ms
?? Ready Queue ?????????????????????????????????????????????????????????????????
? [P3 ? P4 ? P5 ? P6 ? P7 ? P8 ? P9 ? P10 ? P11 ? P12 ? P13 ? P14 ? P1]
????????????????????????????????????????????????????????????????????????????????


[Paste a relevant snippet from your program output here showing a process being re-queued]
```

**Explanation of example:**
[in this snippet process p1 started running.

its total burst time is 8574 milliseconds.

this is more, than the time limit set, which's 4000 milliseconds.

so it used its 4000 milliseconds time slice.

now it has 4574 milliseconds left.

since its not finished yet it gave up the cpu.

it was then moved to the end of the queue.

you can see this in the queue list where p1 is placed after p14.

it will not get the cpu again until processes p3 through p14 all have their turns.

]

---

## Question 3: Thread States

**Question**: A thread can be in different states: **New**, **Runnable**, **Running**, **Waiting**, **Terminated**. Walk through these states for one process (P1) from your simulation.

**Your Answer:**

[in our simulation, the lifecycle of process p1 is managed by the schedulersimulation class. throughout its execution, p1 transitions through different thread states based on how it is created, queued, and processed by the round-robin algorithm. below is a detailed trace of when p1 enters each specific state during the simulation.]

1. **New**: [p1 is in the new state exactly when its thread object is instantiated but not yet active. in the simulation, this happens inside the addprocesstoqueue method when the code calls thread thread = new thread(process);]

2. **Runnable**: [p1 becomes runnable when it is dequeued from the processqueue and the main scheduler loop calls currentthread.start();. this signals to the jvm that p1 is ready to run, transitioning it from new to runnable, waiting for cpu allocation.]

3. **Running**: [p1 is running when the operating system grants it cpu time and it actively begins executing the instructions inside the run() or runtocompletion() methods, actively printing its progress bar to the terminal.]

4. **Waiting**: [p1 enters a waiting state during its execution when the code calls thread.sleep(steptime) inside the run() method. this is used to simulate the actual physical time the cpu would spend processing its time quantum.]

5. **Terminated**: [p1 is terminated when its run() method finishes executing all its statements and returns. if p1 has finished its entire burst time (remaining time reaches 0), it prints "finished execution!" and the thread terminates permanently.]

---

## Question 4: Real-World Applications

**Question**: Give **TWO** real-world examples where Round-Robin scheduling with threads would be useful. Explain why this scheduling algorithm works well for those scenarios.

**Your Answer:**

### Example 1: [Web Server Handling User Requests]

**Description**: 
[A web server (like Apache ) receives multiple requests from different users at the same time, such as requesting a web page, downloading a video, or fetching database information. The server assigns each incoming user request to a separate thread so they can be processed concurrently.]

**Why Round-Robin works well here**: 
[Round-Robin scheduling is really good, in this situation because it makes sure everything is fair and works well. If one user is getting a big file, Round-Robin scheduling will only let their task run for a little while before it gives the computers brain to the next task in line. This stops the download from taking over the whole system so other users who just want a small text file will get what they need quickly without having to wait for the big download to finish. Round-Robin scheduling helps with this because it keeps everything moving and makes sure Round-Robin scheduling is doing its job.]

### Example 2: [Video Game Engine]

**Description**: 
[Modern video games must perform many complex tasks simultaneously, such as rendering 3D graphics, calculating object physics, processing non-player character artificial intelligence,and playing background audio. The game engine utilizes separate threads to handle each of these major subsystems independently.]

**Why Round-Robin works well here**: 
[Round-Robin works well in this situation because it makes things happen in a predictable way, which is very important for the game to run smoothly. The scheduling algorithm gives each part of the game a set amount of time to do its thing. This means that if the game is doing something that takes a lot of work like figuring out a path it cannot take over the entire processor. Each part of the game like the graphics and the audio gets a turn to update. This stops the graphics from freezing and the audio from stuttering. The result is that the game is very responsive and it feels seamless, to the player. Round-Robin makes sure that the game runs well and that Round-Robin helps to keep everything working together.]

---

## Summary

**Key concepts I understood through these questions:**
1. threads share memory and are faster than processes.
2. round-robin scheduling uses time slices for fairness
3. threads transition through states from new to terminated.

**Concepts I need to study more:**
1. thread synchronization and how to prevent race conditions when sharing memory.
2. other cpu scheduling algorithms beyond the round-robin method.
