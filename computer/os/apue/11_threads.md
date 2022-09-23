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

### Q7：作者是怎么论述的？

### Q8：作者解决了什么问题？

### Q9：我有哪些疑问？

### Q10：这一章说得有道理吗？为什么？

### Q11: 这一章讨论的知识的本质是什么？

### Q12: 这一章讨论的知识的第一原则是什么？

### Q13：这一章讨论的知识的结构是怎样的？

### Q14：这一章讨论的知识为什么是这样的？为什么发展成这样？为什么需要它？

### Q15：有哪些相似的知识？它们之间的联系是什么？

### Q16：其他领域/学科有没有相关的知识？日常生活中有没有类似的现象？

### Q17: 这一章对我有哪些用处/帮助/启示？

### Q18: 我如何应用这一章的知识去解决问题？
