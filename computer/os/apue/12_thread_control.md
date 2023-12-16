# 《Advanced Programming in the UNIX Environment》分析笔记

## chapter 12: Thread Control

### Q1：这一章的内容属于哪一类别

计算机/操作系统。

### Q2：这一章的内容是什么

介绍配置与控制 Unix 线程的相关知识。

### Q3：这一章的大纲是什么

- Thread Limits
- Thread Attributes
- Synchronization Attributes
- Reentrancy
- Thread-Specific Data
- Cancel Options
- Threads and Signals
- Threads and fork
- Threads and I/O

### Q4：作者想要解决什么问题

### Q5：这一章的关键词是什么

### Q6：这一章的关键句是什么

#### 12.2 Thread Limits

| Name of limit | Description | name argument |
| ------------- | ----------- | ------------- |
| PTHREAD_DESTRUCTOR_ITERATIONS | maximum number of times an implementation will try to destroy the thread-specific data when a thread exits | `_SC_THREAD_DESTRUCTOR_ITERATIONS` |
| PTHREAD_KEYS_MAX | maximum number of keys that can be created by a process | `_SC_THREAD_KEYS_MAX`  |
| PTHREAD_STACK_MIN | minimum number of bytes that can be used for a thread’s stack | `_SC_THREAD_STACK_MIN`  |
| PTHREAD_THREADS_MAX | maximum number of threads that can be created in a process | `_SC_THREAD_THREADS_MAX` |

> 伍注：在 Ubuntu 20.04 系统下测试得到以下结果：
>
> PTHREAD_DESTRUCTOR_ITERATIONS=4
> PTHREAD_KEYS_MAX=1024
> PTHREAD_STACK_MIN=16384
> PTHREAD_THREADS_MAX=-1

#### 12.3 Thread Attributes

- The functions for managing thread attributes follow the same pattern
  - Each object is associated with its own type of attribute object
   (threads with thread attributes, mutexes with mutex attributes, and so on).
  - An initialization function exists to set the attributes to their default values.
  - Another function exists to destroy the attributes object.
    If the initialization function allocated any resources associated with the attributes object,
    the destroy function frees those resources.
  - Each attribute has a function to get the value of the attribute from the attribute object.
  - Each attribute has a function to set the value of the attribute.
    In this case, the value is passed as an argument, by value.

- Thread attributes
  - detachstate: detached thread attribute
  - guardsize: guard buffer size in bytes at end of thread stack
  - stackaddr: lowest address of thread stack
  - stacksize: minimum size in bytes of thread stack

- Attributes Initialization and Destroy

  ```c
  #include <pthread.h>

  int pthread_attr_init(pthread_attr_t *attr);
  int pthread_attr_destroy(pthread_attr_t *attr);

  // Both return: 0 if OK, error number on failure
  ```

- detachstate

  ```c
  #include <pthread.h>

  int pthread_attr_getdetachstate(const pthread_attr_t *restrict attr, int *detachstate);
  int pthread_attr_setdetachstate(pthread_attr_t *attr, int detachstate);

  // Both return: 0 if OK, error number on failure
  ```

- stackaddr and stacksize

  ```c
  #include <pthread.h>

  int pthread_attr_getstack(const pthread_attr_t *restrict attr,
                            void **restrict stackaddr,
                            size_t *restrict stacksize);

  int pthread_attr_setstack(pthread_attr_t *attr,
                            void *stackaddr, size_t stacksize);

  // Both return: 0 if OK, error number on failure
  ```

- stacksize

  ```c
  #include <pthread.h>

  int pthread_attr_getstacksize(const pthread_attr_t *restrict attr,
                                size_t *restrict stacksize);

  int pthread_attr_setstacksize(pthread_attr_t *attr, size_t stacksize);

  // Both return: 0 if OK, error number on failure
  ```

- guardsize
  - The guardsize thread attribute controls the size of the memory extent after the end of the thread’s stack
    to protect against stack overflow.
  - Its default value is implementation defined, but a commonly used value is the system page size.

  ```c
  #include <pthread.h>

  int pthread_attr_getguardsize(const pthread_attr_t *restrict attr,
                                size_t *restrict guardsize);

  int pthread_attr_setguardsize(pthread_attr_t *attr, size_t guardsize);

  // Both return: 0 if OK, error number on failure
  ```

#### 12.4 Synchronization Attributes

##### 12.4.1 Mutex Attributes

- Mutex Attributes Initialization and Destroy

  ```c
  #include <pthread.h>

  int pthread_mutexattr_init(pthread_mutexattr_t *attr);
  int pthread_mutexattr_destroy(pthread_mutexattr_t *attr);

  // Both return: 0 if OK, error number on failure
  ```

- process-shared Attributes
  - Allows the pthread library to provide more efficient mutex implementations when the attribute is set to `PTHREAD_PROCESS_PRIVATE`

  ```c
  #include <pthread.h>

  int pthread_mutexattr_getpshared(const pthread_mutexattr_t * restrict attr,
                                   int *restrict pshared);
  int pthread_mutexattr_setpshared(pthread_mutexattr_t *attr, int pshared);

  // Both return: 0 if OK, error number on failure
  ```

- robust mutex attribute
  - The default is `PTHREAD_MUTEX_STALLED`,
    which means that no special action is taken when a process terminates while holding a mutex.
  - The other value is `PTHREAD_MUTEX_ROBUST`.
    This value will cause a thread blocked in a call to `pthread_mutex_lock` to acquire the lock when another process holding the lock terminates without first unlocking it,
    but the return value from `pthread_mutex_lock` is `EOWNERDEAD` instead of 0.

  ```c
  #include <pthread.h>

  int pthread_mutexattr_getrobust(const pthread_mutexattr_t * restrict attr,
                                  int *restrict robust);
  int pthread_mutexattr_setrobust(pthread_mutexattr_t *attr, int robust);

  // Both return: 0 if OK, error number on failure
  ```

- The type mutex attribute
  - PTHREAD_MUTEX_NORMAL
    - A standard mutex type that doesn’t do any special error checking or deadlock detection.
  - PTHREAD_MUTEX_ERRORCHECK
    - A mutex type that provides error checking.
  - PTHREAD_MUTEX_RECURSIVE
    - A mutex type that allows the same thread to lock it multiple times without first unlocking it.
    - A recursive mutex maintains a lock count and isn’t released until it is unlocked the same number of times it is locked.
    - Thus, if you lock a recursive mutex twice and then unlock it, the mutex remains locked until it is unlocked a second time.
  - PTHREAD_MUTEX_DEFAULT
    - A mutex type providing default characteristics and behavior.
    - Implementations are free to map it to one of the other mutex types.
    - For example, Linux 3.2.0 maps this type to the normal mutex type.

  ```c
  #include <pthread.h>

  int pthread_mutexattr_gettype(const pthread_mutexattr_t * restrict attr,
                                int *restrict type);

  int pthread_mutexattr_settype(pthread_mutexattr_t *attr, int type);

  // Both return: 0 if OK, error number on failure
  ```

##### 12.4.2 Reader-Writer Lock Attributes

- Reader-Writer Lock Attributes Initialization and Destroy

  ```c
  #include <pthread.h>

  int pthread_rwlockattr_init(pthread_rwlockattr_t *attr);
  int pthread_rwlockattr_destroy(pthread_rwlockattr_t *attr);

  // Both return: 0 if OK, error number on failure
  ```

- process-shared attribute
  - The only attribute supported for reader-writer locks is the process-shared attribute.

  ```c
  #include <pthread.h>

  int pthread_rwlockattr_getpshared(const pthread_rwlockattr_t * restrict attr,
                                    int *restrict pshared);

  int pthread_rwlockattr_setpshared(pthread_rwlockattr_t *attr, int pshared);

  // Both return: 0 if OK, error number on failure
  ```

##### 12.4.3 Condition Variable Attributes

- Two attributes for condition variables:
  - the process-shared attribute
  - the clock attribute

- Condition Variabe Attributes Initialization and Destroy

  ```c
  #include <pthread.h>

  int pthread_condattr_init(pthread_condattr_t *attr);
  int pthread_condattr_destroy(pthread_condattr_t *attr);

  // Both return: 0 if OK, error number on failure
  ```

- process-shared attribute

  ```c
  #include <pthread.h>

  int pthread_condattr_getpshared(const pthread_condattr_t * restrict attr,
                                  int *restrict pshared);

  int pthread_condattr_setpshared(pthread_condattr_t *attr, int pshared);

  // Both return: 0 if OK, error number on failure
  ```

- The clock attribute
  - controls which clock is used when evaluating the timeout argument (tsptr) of the pthread_cond_timedwait function.

  ```c
  #include <pthread.h>
  int pthread_condattr_getclock(const pthread_condattr_t * restrict attr,
                                clockid_t *restrict clock_id);

  int pthread_condattr_setclock(pthread_condattr_t *attr, clockid_t clock_id);

  // Both return: 0 if OK, error number on failure
  ```

##### 12.4.4 Barrier Attributes

- Barrier Attributes Initialization and Destroy

  ```c
  #include <pthread.h>

  int pthread_barrierattr_init(pthread_barrierattr_t *attr);
  int pthread_barrierattr_destroy(pthread_barrierattr_t *attr);

  // Both return: 0 if OK, error number on failure
  ```

- process-shared attribute
  - The only barrier attribute currently defined is the process-shared attribute

  ```c
  #include <pthread.h>

  int pthread_barrierattr_getpshared(const pthread_barrierattr_t * restrict attr,
                                     int *restrict pshared);

  int pthread_barrierattr_setpshared(pthread_barrierattr_t *attr, int pshared);

  // Both return: 0 if OK, error number on failure
  ```

#### 12.5 Reentrancy

- thread-safe
  - If a function can be safely called by multiple threads at the same time,
    we say that the function is thread-safe.

- Check whether support thread-safe
  - Implementations that support thread-safe functions will define the `_POSIX_THREAD_SAFE_FUNCTIONS` symbol in `<unistd.h>`.
  - Applications can also use the `_SC_THREAD_SAFE_FUNCTIONS` argument with `sysconf` to check for support of thread-safe functions at runtime.

- The thread-safe functions of some of the POSIX.1 functions that aren't thread-safe
  - Same names as their non-thread-safe relatives, but with an `_r` appended at the end of the name,
    signifying that these versions are reentrant.

- Why many functions are not thread-safe
  - because they return data stored in a static memory buffer.

- async-signal safe
  - A function that is safe to be reentered from an asynchronous signal handler is async-signal safe.
  - Thread-safe doesn't means async-signal safe

- Manage FILE objects in a thread-safe way
  - You can use `flockfile` and `ftrylockfile` to obtain a lock associated with a given FILE object.

  ```c
  #include <stdio.h>

  int ftrylockfile(FILE *fp);
  // Returns: 0 if OK, nonzero if lock can’t be acquired

  void flockfile(FILE *fp);
  void funlockfile(FILE *fp);
  ```

- Unlocked versions of the character-based standard I/O routines
  - These four functions should not be called unless they are surrounded by calls to `flockfile` (or `ftrylockfile`) and `funlockfile`.

  ```c
  #include <stdio.h>

  int getchar_unlocked(void);
  int getc_unlocked(FILE *fp);
  // Both return: the next character if OK, EOF on end of file or error

  int putchar_unlocked(int c);
  int putc_unlocked(int c, FILE *fp);
  // Both return: c if OK, EOF on error
  ```

#### 12.6 Thread-Specific Data

- Thread-specific data
  - also known as thread-private data, is a mechanism for storing and finding data associated with a particular thread.

- Why we need thread-specific data
  - Provide a mechanism for adapting process-based interfaces to a multithreaded environment.
  - To make it possible for threads to use the same system calls and library routines, `errno` is redefined as thread-private data.

- key
  - Before allocating thread-specific data, we need to create a key to associate with the data.
  - The key will be used to gain access to the thread-specific data.

  ```c
  #include <pthread.h>

  int pthread_key_create(pthread_key_t *keyp, void (*destructor)(void *));
  int pthread_key_delete(pthread_key_t key);
  // Buth Return: 0 if OK, error number on failure
  ```

- `pthread_once`
  - If each thread calls `pthread_once`,
    the system guarantees that the initialization routine, `initfn`, will be called only once, on the first call to `pthread_once`.

  ```c
  #include <pthread.h>

  pthread_once_t initflag = PTHREAD_ONCE_INIT;
  int pthread_once(pthread_once_t *initflag, void (*initfn)(void));
  // Returns: 0 if OK, error number on failure
  ```

- get / set thread-specific data

  ```c
  #include <pthread.h>

  void *pthread_getspecific(pthread_key_t key);
  // Returns: thread-specific data value or NULL if no value has been associated with the key

  int pthread_setspecific(pthread_key_t key, const void *value);
  // Returns: 0 if OK, error number on failure
  ```

#### 12.7 Cancel Options

- Cancelability state and Cancelability type
  - These attributes affect the behavior of a thread in response to a call to `pthread_cancel`

> 伍注：感觉这两个属性的应用场景很少，暂时不深入学习。

#### 12.8 Threads and Signals

- Each thread has its own signal mask, but the signal disposition is shared by all threads in the process.
  - When a thread modifies the action associated with a given signal, all threads share the action.

> 伍注：Ubuntu 20.04 系统下测试表明：
> 1. 各个线程可以分别设置对各个信号是否屏蔽。比如可以设置线程1屏蔽信号A、线程2接收信号A。
> 2. 各个线程均可以注册各个信号的处理函数，并且处理函数是共享的，这意味着：
> (1) 假如线程1注册了信号A的处理函数F，即使线程1屏蔽了信号A，其他没有屏蔽信号A的线程会使用到函数F。
> (2) 如果多个线程都注册了信号A的处理函数，那么最终生效的是最后一次注册时的函数。这与一个线程重复注册的情况是类似的。
> 3. 简而言之，信号掩码是线程私有的，信号处理函数是线程之间共享的。

- pthread_sigmask

  ```c
  #include <signal.h>

  // how: SIG_BLOCK, SIG_SETMASK or SIG_UNBLOCK
  // Returns: 0 if OK, error number on failure
  int pthread_sigmask(int how, const sigset_t *restrict set, sigset_t *restrict oset);
  ```

- sigwait

  ```c
  #include <signal.h>

  // signop points to the number of the signal that was delivered.
  // Returns: 0 if OK, error number on failure
  int sigwait(const sigset_t *restrict set, int *restrict signop);

  ```

- pthread_kill

  ```c
  #include <signal.h>

  // Returns: 0 if OK, error number on failure
  int pthread_kill(pthread_t thread, int signo);
  ```

#### 12.9 Threads and fork

- What would child inherits after a fork
  - By inheriting a copy of the address space,
    the child also inherits the state of every mutex, reader–writer lock, and condition variable from the parent process.
  - The child doesn't inherits any other threads created by the parent.

> 伍注：在多线程环境下使用 fork 容易出问题。参考阅读：[Why threads can't fork][1]

- pthread_atfork
  - `prepare` is called in the parent before `fork` creates the child process.
    Its job is to acquire all locks defined by the parent.
  - `parent` is called in the context of the parent after `fork` has created the child process, but before `fork` has returned.
    Its job is to unlock all the locks acquired by the `prepare` fork handler.
  - The `child` fork handler is called in the context of the child process before returning from `fork`.
    Its job is to unlock all the locks acquired by the `prepare` fork handler, too.

  ```c
  #include <pthread.h>

  // Returns: 0 if OK, error number on failure
  int pthread_atfork(void (*prepare)(void), void (*parent)(void), void (*child)(void));
  ```

#### 12.10 Threads and I/O

- `pread` vs `pwrite`
  - Calling pread is equivalent to calling lseek followed by a call to read, with the following exceptions.
    - There is no way to interrupt the two operations that occur when we call pread.
    - The current file offset is not updated.
  - Calling pwrite is equivalent to calling lseek followed by a call to write, with similar exceptions.

  ```c
  #include <unistd.h>

  // Returns: number of bytes read, 0 if end of file, −1 on error
  ssize_t pread(int fd, void *buf, size_t nbytes, off_t offset);

  // Returns: number of bytes written if OK, −1 on error
  ssize_t pwrite(int fd, const void *buf, size_t nbytes, off_t offset);
  ```

### Q7：作者是怎么论述的

### Q8：作者解决了什么问题

### Q9：我有哪些疑问

#### Q9.1: 为什么 fork 得到的子进程不会继承父进程的线程

### Q10：这一章说得有道理吗？为什么

### Q11: 这一章讨论的知识的本质是什么

### Q12: 这一章讨论的知识的第一原则是什么

### Q13：这一章讨论的知识的结构是怎样的

### Q14：这一章讨论的知识为什么是这样的？为什么发展成这样？为什么需要它

### Q15：有哪些相似的知识？它们之间的联系是什么

### Q16：其他领域/学科有没有相关的知识？日常生活中有没有类似的现象

### Q17: 这一章对我有哪些用处/帮助/启示

### Q18: 我如何应用这一章的知识去解决问题

  [1]: https://thorstenball.com/blog/2014/10/13/why-threads-cant-fork/
