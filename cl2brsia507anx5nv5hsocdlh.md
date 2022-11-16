# Threading & Fair Race w/ MutEx

We all know that threading changed the way of task execution entirely. Since every masterpiece has its consequences, threading is not counted as an exception. In this article, we'll discover the dependent threads and the way that threads manage their access to a shared resource meanwhile making changes to it.

### Threading
Imagine a single-threaded program. You're allowed to do only a single task at a time. *If your browser were a single-threaded program, you were not able to surf the web while you were downloading from somewhere*. When your program is made up of multiple threads, they are capable to serve multiple facilities for users whether concurrently or in parallelism.

### Cores
Each CPU core can run only one thread at a time. I have a 6-core CPU on my machine. Does that actually mean that I can run only 4 threads at a time? How's that even possible? My operating system reserves at least hundreds of threads at the time! That's actually the trick of concurrency, parallelism, and concurrent parallelism tasks.

Threads are sleepy. They fall asleep when they are about to do a heavy process that takes a little bit of time. So, should your system fall asleep too? Where are other threads? The tricky part is that CPUs are so smart like their cores are so fast at switching between hundreds of threads that you will never feel that substitution ever. By the way, did you know that the display screen you're looking at is actually blinking? You may catch it in slow-mo. We are dealing with that type of speed. The speed of electrons.

### Race Condition
What if threads need to access a specific point together like two threads responsible for adding some value to a global variable? What if there is a necessity of being a caching structure to cache the last updated value of the global variable then adding values and updating the global variable with the local one?

Well, threads have a poor unity and connection between themselves. They are not as smart as cores but they do what they've been told other than being smart stubborn like cores. Imagine the part you add the value to the cached variable as the critical zone. What if a thread updates its local cache variable and before adding a number to it, the other thread writes something to the global value? In that case, threads enter that zone without checking any flag or permission so their local cached variable might get updated in the wrong way and cause some conflicts that might change the final result.

### Here Comes MutEx
**Mut**ual **Ex**clusion allows threads to know the entrance time. Imagine some gates for threads that open at specified times so then threads are able to enter the critical zone whenever it's needed. Mutex also acts as a token. Threads will need a key to open the gate and enter the critical zone. Whenever a thread leaves the zone, it passes the token to another thread and provides the required access for the other thread to enter.

#### Signals
Threads can enter the critical zone based on the status of some flags as we discussed earlier. Another theory is to implement signals for our threads and force them to check the other thread's signal before it enters the gate. Each thread can enter the gate if the other thread's signal is off. So, what if our program faces some conflicts and in the end, we end up with both threads' signals turned on? In that case, our threads are stuck in a deadlock situation where none of them is able to enter the critical section.

#### Dekker's Algorithm
Basically, this algorithm is the combination of two Mutex and Signals algorithms. It has better stability than the other ones and the implementation is not that expensive and complex. The token passing structure now happens for changing the status of signals and threads will only look at the signals for the rest of the process.

### Conclusion
In this article, we talked about one of the common problems that most developers run into which is Race Condition, then discovered the different algorithms for solving the condition and their pros and cons. We saw how a 6-core CPU can handle hundreds of threads **barely** at the moment.