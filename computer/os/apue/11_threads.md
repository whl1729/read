# 《Advanced Programming in the UNIX Environment》分析笔记

## 第11章 Threads

### Q1：这一章的内容属于哪一类别？

计算机/操作系统/Unix

### Q2：这一章的内容是什么？

介绍线程的基础知识。

### Q3：这一章的大纲是什么？

- Thread Concepts
- Thread Identification
- Thread Creation
- Thread Termination
- Thread Synchronization

### Q4：作者想要解决什么问题？

### Q5：这一章的关键词是什么？

### Q6：这一章的关键句是什么？

#### 11.2 Thread Concepts

- Benefits of multiple threads
  - Simplify code that deals with asynchronous events
    - By assigning a separate thread to handle each event type.
    - Each thread can then handle its event using a synchronous programming model.
    - A synchronous programming model is much simpler than an asynchronous one.
  - Easy to share memory and file descriptors
  - Improve the overall program throughput
  - Improve response time

- The benefits of a multithreaded programming model can be realized
  even if your program is running on a uniprocessor.

- The information that a thread contains
  - a thread ID that identifies the thread within a process,
  - a set of register values,
  - a stack,
  - a scheduling priority and policy,
  - a signal mask,
  - an errno variable,
  - thread-specific data

- Everything within a process is sharable among the threads in a process,
  - the text of the executable program,
  - the program’s global and heap memory,
  - the stacks,
  - and the file descriptors.

- Thread interfaces
  - The threads interfaces we’re about to see are from POSIX.1-2001.
  - The threads interfaces are also known as "pthreads" for "POSIX threads".
  - The feature test macro for POSIX threads is `_POSIX_THREADS`.

#### 11.3 Thread Identification

- The data type of a thread ID
  - A thread ID is represented by the `pthread_t` data type.
  - Implementations are allowed to use a structure to represent the `pthread_t` data type,
    so portable implementations can’t treat them as integers.
  - So that there is no portable way to print its value.

- Compare two thread IDs

  ```c
  #include <pthread.h>

  int pthread_equal(pthread_t tid1, pthread_t tid2);

  // Returns: nonzero if equal, 0 otherwise
  ```

- A thread can obtain its own thread ID

  ```c
  #include <pthread.h>

  pthread_t pthread_self(void);

  // Returns: the thread ID of the calling thread
  ```

- Usage of the `pthread_equal` and `pthread_self`
  - These functions can be used with pthread_equal when a thread needs to identify data structures that are tagged with its thread ID.
  - E.g., a master thread might place work assignments on a queue and use the thread ID to control which jobs go to each worker thread.

#### 11.4 Thread Creation

- `pthread_create` Function
  - The memory location pointed to by `tidp` is set to the thread ID of the newly created thread.
  - The `attr` argument is used to customize various thread attributes.
  - The newly created thread starts running at the address of the `start_rtn` function.
  - This function takes a single argument, `arg`, which is a typeless pointer.
  - If you need to pass more than one argument to the `start_rtn` function,
    then you need to store them in a structure and pass the address of the structure in `arg`.

  ```c
  #include <pthread.h>

  int pthread_create(pthread_t *restrict tidp,
                     const pthread_attr_t *restrict attr,
                     void *(*start_rtn)(void *), void *restrict arg);

  // Returns: 0 if OK, error number on failure
  ```

- Run order
  - When a thread is created, there is no guarantee which will run first:
    the newly created thread or the calling thread.

- Inheritance
  - The newly created thread has access to the process address space
    and inherits the calling thread’s floating-point environment and signal mask;
  - The set of pending signals for the thread is cleared.

- Error code
  - The pthread functions usually return an error code when they fail.
  - They don’t set `errno` like the other POSIX functions.

- Linux thread IDs
  - The Linux thread IDs look like pointers, even though they are represented as unsigned long integers.

#### 11.5 Thread Termination

- Thread Termination with terminating the entire process
  - Any thread within a process calls `exit`, `_Exit`, or `_exit`
  - A signal whose default action is to terminate the process sent to a thread

- Thread Termination without terminating the entire process
  - The thread can simply return from the start routine. The return value is the thread’s exit code.
  - The thread can be canceled by another thread in the same process.
  - The thread can call `pthread_exit`.

- `pthread_exit` Function
  - The `rval_ptr` pointer is available to other threads in the process by calling the `pthread_join` function.

  ```c
  #include <pthread.h>

  void pthread_exit(void *rval_ptr);
  ```

- The `rval_ptr` for `pthread_exit`
  - If we want to use `rval_ptr` to pass the address of a structure containing more complex information,
    we should either use a global structure or allocate the structure using malloc.

- `pthread_join` Function
  - The calling thread will block until the specified thread calls `pthread_exit`, returns from its start routine, or is canceled.

  ```c
  #include <pthread.h>

  int pthread_join(pthread_t thread, void **rval_ptr);

  // Returns: 0 if OK, error number on failure
  ```

- The `rval_ptr` for `pthread_join`
  - If the thread simply returned from its start routine, `rval_ptr` will contain the return code.
  - If the thread was canceled, the memory location specified by `rval_ptr` is set to `PTHREAD_CANCELED`.
  - If we’re not interested in a thread’s return value, we can set `rval_ptr` to NULL.

- Detached state
  - By calling `pthread_join`, we automatically place the thread with which we’re joining in the detached state
    so that its resources can be recovered.
  - If the thread was already in the detached state, `pthread_join` can fail, returning `EINVAL`,
    although this behavior is implementation-specific.

> 伍注：经过实测，在 Ubuntu 20.04 下，一个线程只能被 `pthread_join` 一次，第二次 `pthread_join` 会被 block。
> 因此，Linux 线程如果处于 detached 状态，`pthread_join` 会被 block？

- `pthread_cancel` Function
  - One thread can request that another in the same process be canceled with this function.
  - In the default circumstances, `pthread_cancel` will cause the thread specified by tid to behave
    as if it had called `pthread_exit` with an argument of `PTHREAD_CANCELED`.
  - A thread can elect to ignore or otherwise control how it is canceled.
  - `pthread_cancel` doesn’t wait for the thread to terminate; it merely makes the request.

  ```c
  #include <pthread.h>

  int pthread_cancel(pthread_t tid);

  // Returns: 0 if OK, error number on failure
  ```

- Thread cleanup handler
  - A thread can arrange for functions to be called when it exits.
  - The functions are known as thread cleanup handlers.
  - More than one cleanup handler can be established for a thread.
  - The handlers are recorded in a stack,
    which means that they are executed in the reverse order from that with which they were registered.

  ```c
  #include <pthread.h>

  void pthread_cleanup_push(void (*rtn)(void *), void *arg);

  void pthread_cleanup_pop(int execute);
  ```

- When is the `rtn` function to be called
  - The thread makes a call to `pthread_exit`
  - The thread responds to a cancellation request
  - The thread makes a call to `pthread_cleanup_pop` with a nonzero execute argument

- The `execute` argument
  - If the `execute` argument is set to zero, the cleanup function is not called.
  - In either case, `pthread_cleanup_pop` removes the cleanup handler established by the last call to `pthread_cleanup_push`.

- Similarities between the process functions and the thread functions

  | Process primitive | Thread primitive | Description |
  | ----------------- | ---------------- | ----------- |
  | fork | pthread_create | create a new flow of control |
  | exit | pthread_exit | exit from an existing flow of control |
  | waitpid | pthread_join | get exit status from flow of control |
  | atexit | pthread_cleanup_push | register function to be called at exit from flow of control |
  | getpid | pthread_self | get ID for flow of control |
  | abort  | pthread_cancel | request abnormal termination of flow of control |

- `pthread_detach` Function
  - After a thread is detached, we can’t use the `pthread_join` function to wait for its termination status,
    because calling `pthread_join` for a detached thread results in undefined behavior.
  - We can detach a thread by calling `pthread_detach`.

  ```c
  #include <pthread.h>

  int pthread_detach(pthread_t tid);

  // Returns: 0 if OK, error number on failure
  ```

#### 11.6 Thread Synchronization

##### 11.6.1 Mutexes

- Mutual-exclusion interfaces: One thread at a time
  - We can protect our data and ensure access by only one thread at a time by using the pthreads mutual-exclusion interfaces.
  - A mutex is basically a lock that we set (lock) before accessing a shared resource and release (unlock) when we’re done.
  - While it is set, any other thread that tries to set it will block until we release it.
  - If more than one thread is blocked when we unlock the mutex,
    then all threads blocked on the lock will be made runnable,
    and the first one to run will be able to set the lock.
    The others will see that the mutex is still locked and go back to waiting for it to become available again.

- Prerequisite for mutex
  - This mutual-exclusion mechanism works only if we design our threads to follow the same data-access rules.

> 伍注：互斥量能够奏效的前提是所有线程都遵循基于锁的数据访问规则。
> 好比厕所装了锁，但如果有人不管有没有锁就强行闯入，那这把锁也起不了保护的作用。

- `pthread_mutex_t` type
  - A mutex variable is represented by the `pthread_mutex_t` data type.

- `pthread_mutex_init` and `pthread_mutex_destroy` Functions
  - Before we can use a mutex variable, we must first initialize it by calling `pthread_mutex_init`.
  - If we allocate the mutex dynamically (by calling `malloc`, for example),
    then we need to call `pthread_mutex_destroy` before freeing the memory.

  ```c
  #include <pthread.h>

  int pthread_mutex_init(pthread_mutex_t *restrict mutex,
                         const pthread_mutexattr_t *restrict attr);

  int pthread_mutex_destroy(pthread_mutex_t *mutex);

  // Both return: 0 if OK, error number on failure
  ```

- `pthread_mutex_lock` series Functions

  ```c
  #include <pthread.h>

  int pthread_mutex_lock(pthread_mutex_t *mutex);
  int pthread_mutex_trylock(pthread_mutex_t *mutex);
  int pthread_mutex_unlock(pthread_mutex_t *mutex);

  // All return: 0 if OK, error number on failure
  ```

> 伍注：如果 pthread_mutex lock 两次会怎么样？
> 无论是否同一个线程，第二次 lock 会导致该进程被 block。
> 伍注：如果 pthread_mutex_unlock 两次会怎么样？
> 在 Ubuntu 20.04 的测试结果是：第二次 unlock 也能立即返回 0

- `pthread_mutex_trylock` Function
  - If a thread can’t afford to block, it can use `pthread_mutex_trylock` to lock the mutex conditionally.
  - If the mutex is unlocked at the time `pthread_mutex_trylock` is called,
    then pthread_mutex_trylock will lock the mutex without blocking and return 0.
  - Otherwise, `pthread_mutex_trylock` will fail, returning `EBUSY` without locking the mutex.

##### 11.6.2 Deadlock Avoidance

- A thread will deadlock itself if it tries to lock the same mutex twice.

- Example of deadlock
  - When we use more than one mutex in our programs,
    a deadlock can occur if we allow one thread to hold a mutex and block while trying to lock a second mutex
    at the same time that another thread holding the second mutex tries to lock the first mutex.

- Avoid deadlock
  - Carefully controll the order in which mutexes are locked.
  - Release your locks and try again at a later time.
    You can use the `pthread_mutex_trylock` interface to avoid deadlocking in this case.

- Locking granularity
  - If your locking granularity is too coarse,
    you end up with too many threads blocking behind the same locks, with little improvement possible from concurrency.
  - If your locking granularity is too fine,
    then you suffer bad performance from excess locking overhead, and you end up with complex code.
  - As a programmer, you need to find the correct balance between code complexity and performance,
    while still satisfying your locking requirements.

##### 11.6.3 `pthread_mutex_timedlock` Function

- `pthread_mutex_timedlock` Declaration
  - The `pthread_mutex_timedlock` function is equivalent to `pthread_mutex_lock`,
    but if the timeout value is reached,
    `pthread_mutex_timedlock` will return the error code `ETIMEDOUT` without locking the mutex.
  - `tsptr` specifies how long we are willing to wait in terms of **absolute time**.

  ```c
  #include <pthread.h>
  #include <time.h>

  int pthread_mutex_timedlock(pthread_mutex_t *restrict mutex,
                              const struct timespec *restrict tsptr);

  // Returns: 0 if OK, error number on failure
  ```

- Note that the time blocked can vary for several reasons:
  - the start time could have been in the middle of a second,
  - the resolution of the system’s clock might not be fine enough to support the resolution of our timeout,
  - or scheduling delays could prolong the amount of time until the program continues execution.

##### 11.6.4 Reader-Writer Locks

- Reader-Writer Locks vs Mutexes
  - Reader-writer locks are similar to mutexes, except that they allow for higher degrees of parallelism.
  - With a mutex, the state is either locked or unlocked, and only one thread can lock it at a time.
  - Only one thread at a time can hold a reader–writer lock in write mode,
    but multiple threads can hold a reader–writer lock in read mode at the same time.

- Prevent starving writers
  - Although implementations vary,
    reader-writer locks usually block additional readers
    if a lock is already held in read mode and a thread is blocked trying to acquire the lock in write mode.
  - This prevents a constant stream of readers from starving waiting writers.

- Suitable situations
  - Reader-writer locks are well suited for situations in which data structures are read more often than they are modified.

- Shared-exclusive locks
  - Reader-writer locks are also called shared-exclusive locks.
  - When a reader-writer lock is read locked, it is said to be locked in **shared mode**.
  - When it is write locked, it is said to be locked in **exclusive mode**.

- Initialization and Clear

  ```c
  #include <pthread.h>

  int pthread_rwlock_init(pthread_rwlock_t *restrict rwlock,
                          const pthread_rwlockattr_t *restrict attr);

  int pthread_rwlock_destroy(pthread_rwlock_t *rwlock);

  // Both return: 0 if OK, error number on failure
  ```

- Lock and unlock
  - We can unlock both the rdlock and wrlock by calling `pthread_rwlock_unlock`.

  ```c
  #include <pthread.h>

  int pthread_rwlock_rdlock(pthread_rwlock_t *rwlock);
  int pthread_rwlock_wrlock(pthread_rwlock_t *rwlock);
  int pthread_rwlock_unlock(pthread_rwlock_t *rwlock);

  // All return: 0 if OK, error number on failure
  ```

- Whether to check the return value
  - Implementations might place a limit on the number of times a reader–writer lock can be locked in shared mode,
    so we need to check the return value of `pthread_rwlock_rdlock`.
  - We don’t need to check the return value of `pthread_rwlock_wrlock` and `pthread_rwlock_unlock`
    if we design our locking properly.

- Try lock

  ```c
  #include <pthread.h>

  int pthread_rwlock_tryrdlock(pthread_rwlock_t *rwlock);
  int pthread_rwlock_trywrlock(pthread_rwlock_t *rwlock);

  // Both return: 0 if OK, error number on failure
  ```

##### 11.6.5 Reader-Writer Locking with Timeouts

- Reader-Writer Locking with Timeouts
  - If they can’t acquire the lock, these functions return the `ETIMEDOUT` error when the timeout expires.
  - Like the `pthread_mutex_timedlock` function, the timeout specifies an **absolute time**, not a relative one.

  ```c
  #include <pthread.h>
  #include <time.h>

  int pthread_rwlock_timedrdlock(pthread_rwlock_t *restrict rwlock,
                                 const struct timespec *restrict tsptr);

  int pthread_rwlock_timedwrlock(pthread_rwlock_t *restrict rwlock,
                                 const struct timespec *restrict tsptr);

  // Both return: 0 if OK, error number on failure
  ```

##### 11.6.6 Condition Variables

> 伍注：互斥量与条件变量的区别：前者保证对资源的互斥访问，后者保证同步，后者其实类似一种消息等待与通知机制。

- Function
  - When used with mutexes, condition variables allow threads to wait in a race-free way for arbitrary conditions to occur.

- Condition variables vs Mutexes
  - The condition itself is protected by a mutex.

- Initialization and Destroy
  - If the condition variable is allocated statically, we can assign the constant `PTHREAD_COND_INITIALIZER` to it.
  - If the condition variable is allocated dynamically, we can use the `pthread_cond_init` function to initialize it.

  ```c
  #include <pthread.h>

  // Set `attr` to NULL if you want to use default attributes.
  int pthread_cond_init(pthread_cond_t *restrict cond,
                        const pthread_condattr_t *restrict attr);

  int pthread_cond_destroy(pthread_cond_t *cond);

  // Both return: 0 if OK, error number on failure
  ```

- Wait for a condition to be true
  - When it returns from a successful call to `pthread_cond_wait` or `pthread_cond_timedwait`,
    a thread needs to reevaluate the condition,
    since another thread might have run and already changed the condition.

  ```c
  #include <pthread.h>

  // The `mutex` must be locked before passing to this function.
  int pthread_cond_wait(pthread_cond_t *restrict cond,
                        pthread_mutex_t *restrict mutex);

  // The `tsptr` is an absolute time.
  // If the timeout expires without the condition occurring,
  // it will reacquire the mutex and return the error ETIMEDOUT.
  int pthread_cond_timedwait(pthread_cond_t *restrict cond,
                             pthread_mutex_t *restrict mutex,
                             const struct timespec *restrict tsptr);

  // Both return: 0 if OK, error number on failure
  ```

- How the `mutex` changes
  - Before calling `pthread_cond_wait`, the `mutex` has been locked.
  - During executing `pthread_cond_wait`, the os atomically places the calling thread on the list of threads waiting for the condition
    and **unlocks** the mutex.
  - After `pthread_cond_wait` returns, the `mutex` has been locked again.

- Create a future time

  ```c
  #include <sys/time.h>
  #include <stdlib.h>

  void
  maketimeout(struct timespec *tsp, long minutes)
  {
    struct timeval now;

    /* get the current time */
    gettimeofday(&now, NULL);
    tsp->tv_sec = now.tv_sec;
    tsp->tv_nsec = now.tv_usec * 1000; /* usec to nsec */

    /* add the offset to get timeout value */
    tsp->tv_sec += minutes * 60;
  }
  ```

- Notify threads that a condition has been satisfied
  - Be careful to signal the threads only after changing the state of the condition.

  ```c
  #include <pthread.h>

  // Wake up at least one thread waiting on a condition
  int pthread_cond_signal(pthread_cond_t *cond);

  // Wake up all threads waiting on a condition.
  int pthread_cond_broadcast(pthread_cond_t *cond);

  Both return: 0 if OK, error number on failure
  ```

##### 11.6.7 Spin Locks

- Spin Lock vs mutex
  - When the process cannot acquire the mutex, it is blocked by sleeping.
  - When the process cannot acquire the spin lock, it is blocked by busy-waiting (spinning) until the lock can be acquired.

- When spin lock can be used
  - A spin lock could be used in situations where locks are held for short periods of times
    and threads don't want to incur the cost of being descheduled.
  - Spin locks are often used as low-level primitives to implement other types of locks.

- How spin lock can be implemented
  - They can be implemented efficiently using test-and-set instructions.

- The disadvantage of Spin lock
  - Although efficient, they can lead to wasting CPU resources:
  - while a thread is spinning and waiting for a lock to become available, the CPU can't do anything else.
  - This is why spin locks should be held only for short periods of time.

- The spin lock is less useful
  - Many mutex implementations are so efficient that the performance of applications using mutex locks is equivalent to their performance if they had used spin locks.
  - In fact, some mutex implementations will spin for a limited amount of time trying to acquire the mutex, and only sleep when the spin count threshold is reached.
  - These factors, combined with advances in modern processors that allow them to context switch at faster and faster rates, make spin locks useful only in limited circumstances.

- Initialization and Destroy

  ```c
  #include <pthread.h>

  int pthread_spin_init(pthread_spinlock_t *lock, int pshared);
  int pthread_spin_destroy(pthread_spinlock_t *lock);

  // Both return: 0 if OK, error number on failure
  ```

- The `pshared` argument
  - The `pshared` argument represents the process-shared attribute, which indicates how the spin lock will be acquired.
  - If it is set to `PTHREAD_PROCESS_SHARED`, then the spin lock can be acquired by threads that have access to the lock's underlying memory,
    even if those threads are from different processes.
  - Otherwise, the pshared argument is set to `PTHREAD_PROCESS_PRIVATE` and the spin lock can be accessed only from threads within the process that initialized it.

- Lock and Unlock

  ```c
  #include <pthread.h>

  // If the thread already has it locked, the results are undefined.
  int pthread_spin_lock(pthread_spinlock_t *lock);

  // It will return the EBUSY error if the lock can't be acquired immediately.
  int pthread_spin_trylock(pthread_spinlock_t *lock);

  // If we try to unlock a spin lock that is not locked, the results are also undefined.
  int pthread_spin_unlock(pthread_spinlock_t *lock);

  // All return: 0 if OK, error number on failure
  ```

> 伍注：经过实测，在 Ubuntu 20.04 下，
> 1. 同一个线程在已经获取到自旋锁的时候再次获取自旋锁，会导致线程被 blocked。
> 2. 同一个线程在已经获取到自旋锁的时候调用 pthread_spin_trylock 尝试获取自旋锁，会立即返回错误码 16.
> 3. 同一个线程在已经释放自旋锁的时候再次调用 pthread_spin_unlock 来释放自旋锁，会立即返回成功。

- Don't sleep
  - We need to be careful not to call any functions that might sleep while holding the spin lock.
  - If we do, then we'll waste CPU resources by extending the time other threads will spin if they try to acquire it.

##### 11.6.8 Barriers

- Barriers
  - A synchronization mechanism that can be used to coordinate multiple threads working in parallel.
  - A barrier allows each thread to wait until all cooperating threads have reached the same point, and then continue executing from there.

- Initialization and Destroy

  ```c
  #include <pthread.h>

  // `count` specifies the number of threads that must reach the barrier before all of the threads will be allowed to continue.
  int pthread_barrier_init(pthread_barrier_t *restrict barrier,
                           const pthread_barrierattr_t *restrict attr,
                           unsigned int count);

  int pthread_barrier_destroy(pthread_barrier_t *barrier);

  // Both return: 0 if OK, error number on failure
  ```

- Wait
  - The thread calling `pthread_barrier_wait` is put to sleep if the barrier count is not yet satisfied.
  - If the thread is the last one to call `pthread_barrier_wait`, thereby satisfying the barrier count, all of the threads are awakened.

  ```c
  #include <pthread.h>

  int pthread_barrier_wait(pthread_barrier_t *barrier);

  // Returns: 0 or PTHREAD_BARRIER_SERIAL_THREAD if OK, error number on failure
  ```

> 伍注：经过实测，在 Ubuntu 20.04 下，PTHREAD_BARRIER_SERIAL_THREAD 的取值为 -1.

- PTHREAD_BARRIER_SERIAL_THREAD
  - To one arbitrary thread, it will appear as if the `pthread_barrier_wait` function returned a value of `PTHREAD_BARRIER_SERIAL_THREAD`.
  - The remaining threads see a return value of 0.
  - This allows one thread to continue as the **master** to act on the results of the work done by all of the other threads.

### Q7：作者是怎么论述的？

### Q8：作者解决了什么问题？

### Q9：我有哪些疑问？

#### Q9.1 互斥量与条件变量有什么区别？

我在上面提到，互斥量主要用于对资源的互斥访问，而条件变量主要用于同步，是一种信号通知与等待机制。
为什么需要条件变量呢？如果没有条件变量，我们能利用互斥量实现同步吗？
答案是可以，但是会低效——浪费 CPU 时间。
实现思路类似自旋锁，不断轮询某个条件是否满足。当然，为了保证互斥访问这个条件，可以使用互斥量。

综上所述，互斥量与条件变量在功能上确实存在较大差异：前者用于互斥，后者用于同步。
前者最常用的场景是保证对某个全局变量的互斥访问，后者的常用场景是「生产者-消费者」问题。

#### Q9.2 条件变量与信号量有什么区别？

#### Q9.3 互斥量与自旋锁有什么区别？

根据第 11.6.7 节开头的描述，两者的一个区别是在无法获得资源（互斥量或锁）时的处理方法：
使用互斥量的线程会睡眠（sleeping），使用自旋锁的线程会一直忙等待（busy-waiting），
这有什么区别呢？区别在于前者不会消耗 CPU 时间，后者会不断消耗 CPU 时间。
那为什么前者不会消耗 CPU 时间呢？因为前者由于 sleep 而处于阻塞态（blocked），
处于阻塞态的线程不会被调度——只有处于就绪态的线程才会被调度。

使用生活中的例子来进行不太精确的类比，大概就是：
A （类比互斥量）和 B （类比自旋锁）都想上厕所，但是厕所暂时被其他人使用。
A 的策略是先去睡觉，等厕所管理员（虚构人物，类比 os）来通知厕所没人了再去上厕所；
B 的策略是不断地在厕所门口等待。

#### Q9.4 互斥量、读写锁、条件变量、自旋锁与信号量分别是怎样实现的？

#### Q9.5 互斥量、读写锁、条件变量、自旋锁与信号量有什么区别与联系？

#### Q9.6 `pthread_cond_wait` 是如何实现的？

由睡眠态切换到就绪态，与重新获取到锁之间，存在时间窗口？这个时间窗口可能会有其他线程执行其他任务？

### Q10：这一章说得有道理吗？为什么？

### Q11: 这一章讨论的知识的本质是什么？

### Q12: 这一章讨论的知识的第一原则是什么？

### Q13：这一章讨论的知识的结构是怎样的？

### Q14：这一章讨论的知识为什么是这样的？为什么发展成这样？为什么需要它？

### Q15：有哪些相似的知识？它们之间的联系是什么？

### Q16：其他领域/学科有没有相关的知识？日常生活中有没有类似的现象？

### Q17: 这一章对我有哪些用处/帮助/启示？

### Q18: 我如何应用这一章的知识去解决问题？
