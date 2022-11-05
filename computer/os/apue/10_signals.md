# 《Advanced Programming in the UNIX Environment》分析笔记

## 第10章 Signals

### Q1：这一章的内容属于哪一类别？

计算机/操作系统/Unix。

### Q2：这一章的内容是什么？

### Q3：这一章的大纲是什么？

- Introduction
- Signal Concepts
- `signal` Function
- Unreliable Signals
- Interrupted System Calls
- Reentrant Functions
- `SIGCLD` Semantics
- Reliable-Signal Terminology and Semantics
- `kill` and `raise` Functions
- `alarm` and `pause` Functions
- Signal Sets
- `sigprocmask` Function
- `sigpending` Function
- `sigaction` Function
- `sigsetjmp` and `siglongjmp` Functions
- `sigsuspend` Function
- `abort` Function
- `system` Function
- `sleep`, `nanosleep`, and `clock_nanosleep` Functions
- `sigqueue` Function
- Job-Control Signals
- Signal Names and Numbers

### Q4：作者想要解决什么问题？

### Q5：这一章的关键词是什么？

### Q6：这一章的关键句是什么？

#### 10.1 Introduction

- Signals are software interrupts.

- Signals provide a way of handling asynchronous events.

#### 10.2 Signal Concepts

- Signal name
  - First, every signal has a name.
  - These names all begin with the three characters `SIG`.
  - Signal names are all defined by positive integer constants (the signal number) in the header `<signal.h>`.

- Signal number
  - Mac OS X 10.6.8 and Linux 3.2.0 each support 31 different signals.
  - No signal has a signal number of 0.
  - The `kill` function uses the signal number of 0 for a special case.
  - POSIX.1 calls this value the null signal.

- Conditions of generating a signal
  - The terminal-generated signals occur when users press certain terminal keys.
    - `Ctrl-C` -> `SIGINT (2)`
    - `Ctrl-\` => `SIGQUIT (3)`
    - `Ctrl-Z` -> `SIGTSTP (20)`
  - Hardware exceptions generate signals:
    - divide by 0,
    - invalid memory reference, and the like.
  - The `kill(2)` function allows a process to send any signal to another process or process group.
    - Limitations: we have to be the owner of the process that we’re sending the signal to,
      or we have to be the superuser.
  - The `kill(1)` command allows us to send signals to other processes.
    - This program is just an interface to the kill function.
    - This command is often used to terminate a runaway background process.
  - Software conditions can generate signals when a process should be notified of various events.
    - `SIGURG` (generated when out-of-band data arrives over a network connection)
    - `SIGPIPE` (generated when a process writes to a pipe that has no reader)
    - `SIGALRM` (generated when an alarm clock set by the process expires).

- Disposition of the signal
  - Ignore the signal.
    - This works for most signals, but two signals can never be ignored: `SIGKILL` and `SIGSTOP`.
    - The reason these two signals can’t be ignored is
      to provide the kernel and the superuser with a surefire way of either killing or stopping any process.
  - Catch the signal.
    - To do this, we tell the kernel to call a function of ours whenever the signal occurs.
    - In our function, we can do whatever we want to handle the condition.
  - Let the default action apply.
    - Every signal has a default action. (伍注：可以通过命令 `man 7 signal` 来查看)
    - Note that the default action for most signals is to terminate the process.

> 伍注：在 Linux 系统下，`SIGKILL` 和 `SIGSTOP` 这两个信号既不能忽略也不能捕捉。
> 如果你调用 `signal` 函数为这两个信号注册处理函数，`signal` 函数会返回错误。

- The core file for Ubuntu
  - [Ubuntu 系统默认关闭 core dumps 日志功能][1]，打开方法：`sudo service apport start`
  - Ubuntu 系统下，[core file 的存放目录][2]：`/var/lib/apport/coredump/`

- `abort()`
  - If the `SIGABRT` signal is ignored, or caught by a handler that returns,
    the abort() function will still terminate the process.
  - It does this by restoring the default disposition for `SIGABRT` and then raising the signal for a second time.

#### 10.3 signal Function

- `signal` function

  ```c
  #include <signal.h>

  void (*signal(int signo, void (*func)(int)))(int);

  // Returns: previous disposition of signal (see following) if OK, SIG_ERR on error
  ```

> 伍注：signal 返回上一个调用 signal 注册 signo 信号的处理函数，若尚未注册则返回默认的处理函数。

- The value of func `signal` is:
  - the constant `SIG_IGN`
  - the constant `SIG_DFL`
  - the address of a function to be called when the signal occurs.

- 3 constant handlers

  ```c
  #define SIG_ERR  (void (*)())-1
  #define SIG_DFL  (void (*)())0
  #define SIG_IGN  (void (*)())1
  ```

- A limitation of the `signal` function
  - We are not able to determine the current disposition of a signal without changing the disposition.

- Process Creation
  - When a process calls fork, the child inherits the parent’s signal dispositions.
  - Since the child starts off with a copy of the parent’s memory image,
    the address of a signal-catching function has meaning in the child.

#### 10.4 Unreliable Signals

- In earlier versions of the UNIX System (such as Version 7), signals were unreliable.
  - Signals could get lost: a signal could occur and the process would never know about it.
  - A process had little control over a signal: a process could catch the signal or ignore it.

> 伍注：这一节简单了解即可。

#### 10.5 Interrupted System Calls

- A characteristic of earlier UNIX systems was that
  - If a process caught a signal while the process was blocked in a "slow" system call, the system call was interrupted.
  - The system call returned an error and errno was set to EINTR.

- Categories of system calls
  - The system calls are divided into two categories: the "slow" system calls and all the others.
  - The slow system calls are those that can block forever.

- The slow system calls
  - Reads that can block the caller forever if data isn’t present with certain file types (pipes, terminal devices, and network devices)
  - Writes that can block the caller forever if the data can’t be accepted immediately by these same file types
  - Opens on certain file types that block the caller until some condition occurs
    (such as a terminal device open waiting until an attached modem answers the phone)
  - The `pause` function (which by definition puts the calling process to sleep until a signal is caught) and the wait function
  - Certain `ioctl` operations
  - Some of the interprocess communication functions

- Auto restart
  - To prevent applications from having to handle interrupted system calls,
    4.2BSD introduced the automatic restarting of certain interrupted system calls.
  - The system calls that were automatically restarted are `ioctl`, `read`, `readv`, `write`, `writev`, `wait`, and `waitpid`.

#### 10.6 Reentrant Functions

- Reentrant Functions
  - The Single UNIX Specification specifies the functions that are guaranteed to be safe to call from within a signal handler.
  - These functions are reentrant and are called **async-signal safe** by the Single UNIX Specification.
  - Besides being reentrant, they block any signals during operation if delivery of a signal might cause inconsistencies.

- Why some functions are nonreentrant
  - (a) they are known to use static data structures,
  - (b) they call malloc or free,
  - (c) they are part of the standard I/O library.
    Most implementations of the standard I/O library use global data structures in a nonreentrant way.

#### 10.7 SIGCLD Semantics

- `SIGCLD` vs `SIGCHLD`
  - Two signals that continually generate confusion are `SIGCLD` and `SIGCHLD`.
  - The name `SIGCLD` is from System V, and this signal has different semantics from the BSD signal, named `SIGCHLD`.
  - The POSIX.1 signal is also named `SIGCHLD`.

> 伍注：目前知道两者有差异即可，以后有需要再详细研究。

#### 10.8 Reliable-Signal Terminology and Semantics

- Generated
  - First, a signal is generated for a process (or sent to a process) when the event that causes the signal occurs.
  - The event could be
    - a hardware exception (e.g., divide by 0),
    - a software condition (e.g., an alarm timer expiring),
    - a terminal-generated signal,
    - or a call to the kill function.
  - When the signal is generated, the kernel usually sets a flag of some form in the process table.

- Delivered
  - A signal is delivered to a process when the action for a signal is taken.

- Pending
  - During the time between the generation of a signal and its delivery, the signal is said to be pending.

- Blocking
  - A process has the option of blocking the delivery of a signal.
  - If a signal that is blocked is generated for a process,
    and if the action for that signal is either the default action or to catch the signal,
    then the signal remains pending for the process
    until the process either (a) unblocks the signal or (b) changes the action to ignore the signal.
  - The `sigpending` function can be called by a process to determine which signals are blocked and pending.

- What happens if a blocked signal is generated more than once before the process unblocks the signal?
  - POSIX.1 allows the system to deliver the signal either once or more than once.
  - If the system delivers the signal more than once, we say that the signals are queued.
  - Most UNIX systems do not queue signals unless they support the real-time extensions to POSIX.1.
  - Instead, the UNIX kernel simply delivers the signal once.

- What happens if more than one signal is ready to be delivered to a process?
  - POSIX.1 does not specify the order in which the signals are delivered to the process.
  - The Rationale for POSIX.1 does suggest that signals related to the current state of the process be delivered before other signals.
    (SIGSEGV is one such signal.)

- Signal mask
  - Each process has a signal mask that defines the set of signals currently blocked from delivery to that process.
  - We can think of this mask as having one bit for each possible signal.
  - If the bit is on for a given signal, that signal is currently blocked.
  - A process can examine and change its current signal mask by calling `sigprocmask`.

- Signal set
  - Since it is possible for the number of signals to exceed the number of bits in an integer,
    POSIX.1 defines a data type, called `sigset_t`, that holds a signal set.
  - The signal mask is stored in one of these signal sets.

#### 10.9 `kill` and `raise` Functions

- `kill` vs `raise`
  - The `kill` function sends a signal to a process or a group of processes.
  - The `raise` function allows a process to send a signal to itself.
  - The call `raise(signo);` is equivalent to the call `kill(getpid(), signo);`.

  ```c
  #include <signal.h>
  int kill(pid_t pid, int signo);
  int raise(int signo);

  // Both return: 0 if OK, −1 on error
  ```

- `pid` argument
  - `pid > 0` The signal is sent to the process whose process ID is pid.
  - `pid == 0` The signal is sent to all processes whose process group ID equals the process group ID of the sender
    and for which the sender has permission to send the signal.
    Note that the term all processes excludes an implementation-defined set of system processes.
    For most UNIX systems, this set of system processes includes the kernel processes and init (pid 1).
  - `pid < 0` The signal is sent to all processes whose process group ID equals the absolute value of pid
    and for which the sender has permission to send the signal.
    Again, the set of all processes excludes certain system processes, as described earlier.
  - `pid == −1` The signal is sent to all processes on the system for which the sender has permission to send the signal.
    As before, the set of processes excludes certain system processes.

- Permission
  - A process needs permission to send a signal to another process.
  - The superuser can send a signal to any process.
  - For other users, the basic rule is that
    the real or effective user ID of the sender has to equal the real or effective user ID of the receiver.

- Null signal
  - If the signo argument is 0, then the normal error checking is performed by kill, but no signal is sent.
  - This technique is often used to determine if a specific process still exists.
  - If we send the process the null signal and it doesn’t exist, kill returns −1 and errno is set to ESRCH.
  - Be aware that UNIX systems recycle process IDs after some amount of time,
    so the existence of a process with a given process ID does not necessarily mean that it’s the process that you think it is.
  - Also understand that the test for process existence is not atomic.
    By the time that kill returns the answer to the caller, the process in question might have exited,
    so the answer is of limited value.

> 伍注：目测现在很少这样用，简单了解即可。

#### 10.10 `alarm` and `pause` Functions

- `alarm` Function
  - Allows us to set a timer that will expire at a specified time in the future.
  - When the timer expires, the SIGALRM signal is generated.
  - If we ignore or don’t catch this signal, its default action is to terminate the process.
  - There is only one of these alarm clocks per process.
  - If a previously registered alarm clock for the process has not yet expired and if the seconds value is 0,
    the previous alarm clock is canceled.

  ```c
  #include <unistd.h>
  unsigned int alarm(unsigned int seconds);

  // Returns: 0 or number of seconds until previously set alarm.
  ```

- `pause` Function
  - The only time pause returns is if a signal handler is executed and that handler returns.

  ```c
  #include <unistd.h>
  int pause(void);

  // Returns: −1 with errno set to EINTR
  ```

- Two ways to set a time limit on an I/O operation
  - Use `longjmp`, while recognizing its possible interaction with other signal handlers.
  - Use the `select` or `poll` functions.

#### 10.11 Signal Sets

- Signal Set
  - A Data Type to represent multiple signals
  - Use this data type with such functions as `sigprocmask`
    to tell the kernel not to allow any of the signals in the set to occur.

- Signal Set Functions
  - All applications have to call either `sigemptyset` or `sigfillset` once for each signal set.

  ```c
  #include <signal.h>

  // Initializes the signal set pointed to by set so that all signals are excluded.
  int sigemptyset(sigset_t *set);

  // Initializes the signal set so that all signals are included.
  int sigfillset(sigset_t *set);

  // Adds a single signal to an existing set.
  int sigaddset(sigset_t *set, int signo);

  // Removes a single signal from a set.
  int sigdelset(sigset_t *set, int signo);

  // All four return: 0 if OK, −1 on error.

  int sigismember(const sigset_t *set, int signo);

  // Returns: 1 if true, 0 if false, −1 on error.
  ```

#### 10.12 `sigprocmask` Function

- Signal Mask
  - The signal mask of a process is the set of signals currently blocked from delivery to that process.
  - A process can examine its signal mask, change its signal mask, or perform both operations in one step by calling `sigprocmask`.

- `sigprocmask` Function
  - First, if `oset` is a non-null pointer, the current signal mask for the process is returned through `oset`.
  - Second, if `set` is a non-null pointer, the `how` argument indicates how the current signal mask is modified.
  - If `set` is a null pointer, the signal mask of the process is not changed, and `how` is ignored.

  ```c
  #include <signal.h>

  int sigprocmask(int how, const sigset_t *restrict set, sigset_t *restrict oset);

  // Returns: 0 if OK, −1 on error
  ```

- `how` Parameter
  - `SIG_BLOCK` The new signal mask for the process is the **union** of
    its current signal mask and the signal set pointed to by `set`.
    That is, set contains the additional signals that we want to block.
  - `SIG_UNBLOCK` The new signal mask for the process is the **intersection** of
    its current signal mask and the complement of the signal set pointed to by `set`.
    That is, set contains the signals that we want to unblock.
  - `SIG_SETMASK` The new signal mask for the process is replaced by the value of the signal set pointed to by `set`.

- After calling `sigprocmask`, if any unblocked signals are pending,
  at least one of these signals is delivered to the process before `sigprocmask` returns.

#### 10.13 `sigpending` Function

- `sigpending` Function
  - Returns the set of signals that are blocked from delivery and currently pending for the calling process.
  - The set of signals is returned through the `set` argument.

  ```c
  #include <signal.h>

  int sigpending(sigset_t *set);

  // Returns: 0 if OK, −1 on error
  ```

- Be careful to unblock a signal
  - If we write a function that can be called by others and if we need to block a signal in our function,
    we can’t use `SIG_UNBLOCK` to unblock the signal.
  - In this case, we have to use `SIG_SETMASK` and restore the signal mask to its prior value,
    because it’s possible that the caller had specifically blocked this signal before calling our function.

- Additional occurrences of the same signal are usually not queued.

#### 10.14 `sigaction` Function

- `sigaction` Function
  - Examine or modify (or both) the action associated with a particular signal.
  - If the `act` pointer is non-null, we are modifying the action.
  - If the `oact` pointer is non-null, the system returns the previous action for the signal through the `oact` pointer.

  ```c
  #include <signal.h>

  int sigaction(int signo, const struct sigaction *restrict act, struct sigaction *restrict oact);

  // Returns: 0 if OK, −1 on error
  ```

- `sigaction` struct

  ```c
  struct sigaction {
    void (*sa_handler)(int); /* addr of signal handler, */
                             /* or SIG_IGN, or SIG_DFL */
    sigset_t sa_mask;  /* additional signals to block */
    int sa_flags;  /* signal options */

    /* alternate handler */
    void (*sa_sigaction)(int, siginfo_t *, void *);
  };
  ```

- `SA_SIGINFO` flag

  ```c
  // Normally, the signal handler is called as
  void handler(int signo);

  // But if the SA_SIGINFO flag is set, the signal handler is called as
  void handler(int signo, siginfo_t *info, void *context);
  ```

- `siginfo` struct

  ```c
  struct siginfo {
    int si_signo; /* signal number */
    int si_errno; /* if nonzero, errno value from errno.h */
    int si_code; /* additional info (depends on signal) */
    pid_t si_pid; /* sending process ID */
    uid_t si_uid; /* sending process real user ID */
    void *si_addr; /* address that caused the fault */
    int si_status; /* exit value or signal number */
    union sigval si_value; /* application-specific value */
    /* possibly other fields also */
  };
  ```

- `ucontext_t` struct
  - The `context` argument is a typeless pointer that can be cast to a `ucontext_t` structure
    identifying the process context at the time of signal delivery.

  ```c
  struct ucontext_t {
    ucontext_t *uc_link;    /* pointer to context resumed when */
                            /* this context returns */
    sigset_t uc_sigmask;    /* signals blocked when this context */
                            /* is active */
    stack_t uc_stack;       /* stack used by this context */
    mcontext_t uc_mcontext; /* machine-specific representation of */
                            /* saved context */
    /* possibly other fields also */
  }
  ```

#### 10.15 `sigsetjmp` and `siglongjmp` Functions

- `setjmp & longjmp` vs `sigsetjmp & siglongjmp`
  - POSIX.1 does not specify the effect of `setjmp` and `longjmp` on signal masks.
  - `sigsetjmp` and `siglongjmp` should always be used when branching from a signal handler.

- `sigsetjmp & siglongjmp` Functions

  ```c
  #include <setjmp.h>

  // If savemask is nonzero, then sigsetjmp also saves the current signal mask of the process in env.
  // Returns: 0 if called directly, nonzero if returning from a call to siglongjmp
  int sigsetjmp(sigjmp_buf env, int savemask);

  // When siglongjmp is called, if the env argument was saved by a call to sigsetjmp with a nonzero savemask,
  // then siglongjmp restores the saved signal mask.
  void siglongjmp(sigjmp_buf env, int val);
  ```

#### 10.16 `sigsuspend` Function

- Why we need `sigsuspend` Function
  - we need a way to both restore the signal mask and put the process to sleep in a single **atomic** operation.
  - 伍注：`sigsuspend` 有点像先后调用了 `sigprocmask` 和 `pause`，但又保证了这两个调用是一个原子操作。

- `sigsuspend` Function
  - The signal mask of the process is set to the value pointed to by `sigmask`.
  - Then the process is suspended until a signal is caught or until a signal occurs that terminates the process.

  ```c
  #include <signal.h>

  int sigsuspend(const sigset_t *sigmask);

  // Returns: −1 with errno set to EINTR
  ```

- Use of `sigsuspend` Function
  - To protect a critical region of code from a specific signal.
  - To wait for a signal handler to set a global variable

#### 10.17 `abort` Function

- `abort` Declaration

  ```c
  #include <stdlib.h>

  void abort(void);

  // This function never returns
  ```

- What `abort` does
  - This function sends the `SIGABRT` signal to the caller.
  - ISO C states that calling `abort` will deliver an unsuccessful termination notification
    to the host environment by calling `raise(SIGABRT)`.

- When the `SIGABRT` is caught
  - ISO C requires that if the signal is caught and the signal handler returns, `abort` still doesn’t return to its caller.
  - If this signal is caught, the only way the signal handler can’t return is
    if it calls exit, `_exit`, `_Exit`, `longjmp`, or `siglongjmp`.
  - POSIX.1 also specifies that abort overrides the blocking or ignoring of the signal by the process.

- Why catches the `SIGABRT`
  - To allow the process to perform any cleanup that it wants to do before the process terminates.
  - If the process doesn’t terminate itself from this signal handler,
    POSIX.1 states that, when the signal handler returns, `abort` terminates the process.

- Whether to flush the output stream
  - POSIX.1 allows an implementation to call `fclose` on open standard I/O streams before terminating
    if the call to `abort` terminates the process.

#### 10.18 `system` Function

- Ignored signal
  - POSIX.1 requires that system ignore `SIGINT` and `SIGQUIT` and block `SIGCHLD`.

- Return value
  - When writing programs that use the `system` function, be sure to interpret the return value correctly.
  - If you call fork, exec, and wait yourself, the termination status is not the same as if you call system.

#### 10.19 `sleep`, `nanosleep` and `clock_nanosleep` Functions

- `sleep` Declaration

  ```c
  #include <unistd.h>

  unsigned int sleep(unsigned int seconds);

  // Returns: 0 or number of unslept seconds
  ```

- `nanosleep` Declaration

  ```c
  #include <time.h>

  int nanosleep(const struct timespec *reqtp, struct timespec *remtp);

  // Returns: 0 if slept for requested time or −1 on error
  ```

- `clock_nanosleep` Declaration

  ```c
  #include <time.h>

  int clock_nanosleep(clockid_t clock_id, int flags, const struct timespec *reqtp, struct timespec *remtp);

  // Returns: 0 if slept for requested time or error number on failure
  ```

#### 10.20 `sigqueue` Function

- `sigqueue` Declaration

  ```c
  #include <signal.h>

  int sigqueue(pid_t pid, int signo, const union sigval value)

  // Returns: 0 if OK, −1 on error
  ```

#### 10.21 Job-Control Signals

- POSIX.1 considers six to be job-control signals:
  - `SIGCHLD` Child process has stopped or terminated.
  - `SIGCONT` Continue process, if stopped.
  - `SIGSTOP` Stop signal (can’t be caught or ignored).
  - `SIGTSTP` Interactive stop signal.
  - `SIGTTIN` Read from controlling terminal by background process group member.
  - `SIGTTOU` Write to controlling terminal by a background process group member.

- Interactions between the job-control signals
  - When any of the four stop signals (`SIGTSTP`, `SIGSTOP`, `SIGTTIN`, or `SIGTTOU`) is generated for a process,
    any pending `SIGCONT` signal for that process is discarded.
  - When the `SIGCONT` signal is generated for a process, any pending stop signals for that same process are discarded.

#### 10.22 Signal Names and Numbers

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

  [1]: https://askubuntu.com/a/1109747
  [2]: https://askubuntu.com/a/1374285
