# 《xxx》分析笔记

## Chapter 14: Advanced I/O

### Q1：这一章的内容属于哪一类别

计算机/操作系统/Unix

### Q2：这一章的内容是什么

介绍各种高级 I/O 的概念和函数。

### Q3：这一章的大纲是什么

- Nonblocking I/O
- Record Locking
- I/O Multiplexing
  - `select` and `pselect` Functions
  - `poll` Function
- Asynchronous I/O
  - System V Asynchronous I/O
  - BSD Asynchronous I/O
  - POSIX Asynchronous I/O
- `readv` and `writev` Functions
- `readn` and `writen` Functions
- Memory-Mapped I/O

### Q4：作者想要解决什么问题

### Q5：这一章的关键词是什么

### Q6：这一章的关键句是什么

#### 14.2 Nonblocking I/O

- Definition of Nonblocking I/O
  - Nonblocking I/O lets us issue an I/O operation, such as an `open`, `read`, or `write`, and not have it block forever.
  - If the operation cannot be completed, the call returns immediately with an error noting that the operation would have blocked.

- Two ways to specify nonblocking I/O
  - If we call `open` to get the descriptor, we can specify the `O_NONBLOCK` flag.
  - For a descriptor that is already open, we call `fcntl` to turn on the `O_NONBLOCK` file status flag

- `errno` command
  - Description: look up errno names and descriptions
  - Installation: `sudo apt install moreutils`
  - Usage: `errno {name-or-code}`

- 在 ubuntu 20.04 系统下，如果以 nonblocking 的方式往 terminal 写大量数据，`errno` 可能会被设置为 `EAGAIN`。
  意为 `EAGAIN 11 Resource temporarily unavailable`。

#### 14.3 Record Locking

> 伍注：为避免写竞争，所有进程都需要遵循先获取锁再进行I/O操作的规则。
> 只要有一个进程不遵守规则，比如说无视锁的存在直接读写，那也无法避免写竞争。

- Record locking
  - Describe the ability of a process to prevent other processes from modifying a region of a file
    while the first process is reading or modifying that portion of the file.

- `fcntl` Record Locking

  ```c
  #include <fcntl.h>

  // Returns: depends on cmd if OK (see following), −1 on error
  int fcntl(int fd, int cmd, ... /* struct flock *flockptr */ );
  ```

> 伍注：Ubuntu 系统下，`man fcntl` 可以查看 fcntl 函数的具体用法。

- `flock` structure

  ```c
  struct flock {
    short l_type;   /* F_RDLCK, F_WRLCK, or F_UNLCK */
    short l_whence; /* SEEK_SET, SEEK_CUR, or SEEK_END */
    off_t l_start;  /* offset in bytes, relative to l_whence */
    off_t l_len;    /* length, in bytes; 0 means lock to EOF */
    pid_t l_pid;    /* returned with F_GETLK */
  };
  ```

- Three rules govern the automatic inheritance and release of record locks
  - Locks are associated with a process and a file.
    - When a process terminates, all its locks are released.
    - Whenever a descriptor is closed, any locks on the file referenced by that descriptor for that process are released.
  - Locks are never inherited by the child across a fork.
  - Locks are inherited by a new program across an `exec`.

#### 14.4 I/O Multiplexing

- `select` Function

  ```c
  #include <sys/select.h>

  // maxfdp1: maximum file descriptor plus 1.
  // readfds, writefds, exceptfds: any of these can be NULL if we're not interested in that condition.
  // tvptr: NULL means wait forever, and 0 means don't wait at all.
  // returns: -1 means error, 0 means no descriptors are ready, positive value means the number of descriptors that are ready.
  int select(int maxfdp1,
             fd_set *restrict readfds,
             fd_set *restrict writefds,
             fd_set *restrict exceptfds,
             struct timeval *restrict tvptr);

  // Returns: count of ready descriptors, 0 on timeout, −1 on error
  ```

> 伍注：`man select` 可以查看 Linux 系统下 `select` 和 `pselect` 的帮助文档。

- `pselect` Function

  ```c
  #include <sys/select.h>

  // Returns: count of ready descriptors, 0 on timeout, −1 on error
  int pselect(int maxfdp1,
              fd_set *restrict readfds,
              fd_set *restrict writefds,
              fd_set *restrict exceptfds,
              const struct timespec *restrict tsptr,
              const sigset_t *restrict sigmask);
  ```

- `select` vs `pselect`
  - The timeout value for `select` is specified by a `timeval` structure,
    but for `pselect`, a `timespec` structure is used.
  - The timeout value for `pselect` is declared `const`
  - An optional signal mask argument is available with `pselect`.
    If `sigmask` is `NULL`, `pselect` behaves as `select` does with respect to signals.

- `poll` Function

  ```c
  #include <poll.h>

  // Returns: count of ready descriptors, 0 on timeout, −1 on error
  int poll(struct pollfd fdarray[], nfds_t nfds, int timeout);
  ```

- `pollfd` structure

  ```c
  struct pollfd {
    int fd;        /* file descriptor to check, or <0 to ignore */
    short events;  /* events of interest on fd */
    short revents; /* events that occurred on fd */
  };
  ```

- [`select` vs `poll` vs `epoll`][1]
  - [The C10K Problem][2]

#### 14.5 Asynchronous I/O

- Complexity of using the POSIX asynchronous I/O
  - We have to worry about three sources of errors for every asynchronous operation:
    - one associated with the submission of the operation,
    - one associated with the result of the operation itself,
    - one associated with the functions used to determine the status of the asynchronous operations.
  - The interfaces themselves involve a lot of extra setup and processing rules compared to their conventional counterparts
  - Recovering from errors can be difficult.

- `aiocb` structure

  ```c
  struct aiocb {
    /* The order of these fields is implementation-dependent */
    int             aio_fildes;     /* File descriptor */
    off_t           aio_offset;     /* File offset */
    volatile void  *aio_buf;        /* Location of buffer */
    size_t          aio_nbytes;     /* Length of transfer */
    int             aio_reqprio;    /* Request priority */
    struct sigevent aio_sigevent;   /* Notification method */
    int             aio_lio_opcode; /* Operation to be performed;
                                      lio_listio() only */

    /* Various implementation-internal fields not shown */
  };
  ```

- `aio` functions

  ```c
  #include <aio.h>

  // Return: 0 if OK, −1 on error
  int aio_read(struct aiocb *aiocb);
  int aio_write(struct aiocb *aiocb);
  int aio_fsync(int op, struct aiocb *aiocb);

  // Return: 0 if OK, -1 if failed, EINPROGRESS if pending, anything else if the result of the asynchronous operation.
  int aio_error(const struct aiocb *aiocb);

  // Return: -1 if failed, anything else is the result of the asynchronous operation.
  ssize_t aio_return(const struct aiocb *aiocb);
  ```

> 伍注：`man aio` 可以查看 aio 函数的具体用法。

#### 14.6 `readv` and `writev` Functions

- `readv` and `writev` Functions
  - Let us read into and write from multiple noncontiguous buffers in a single function call.

  ```c
  #include <sys/uio.h>

  // Both return: number of bytes read or written, −1 on error
  ssize_t readv(int fd, const struct iovec *iov, int iovcnt);
  ssize_t writev(int fd, const struct iovec *iov, int iovcnt);
  ```

- `iovec` structure

  ```c
  struct iovec {
    void  *iov_base; /* Starting address */
    size_t iov_len;  /* Number of bytes to transfer */
  };
  ```

#### 14.7 `readn` and `writen` Functions

> 伍注：这两个函数是作者定义的，不具通用性，因此不做笔记。

#### 14.8 Memory-Mapped I/O

- `mmap` function
  - Lets us map a file on disk into a buffer in memory

  ```c
  #include <sys/mman.h>

  // Returns: starting address of mapped region if OK, MAP_FAILED on error
  void *mmap(void *addr, size_t len, int prot, int flag, int fd, off_t off );
  ```

> 伍注：`man mmap` 可以查看 mmap 函数的具体用法。

- `mprotect` function
  - Change the permissions on an existing mapping.

  ```c
  #include <sys/mman.h>

  // Returns: 0 if OK, −1 on error
  int mprotect(void *addr, size_t len, int prot);
  ```

- `msync` function
  - Flush the changes to the file that backs the mapping.

  ```c
  #include <sys/mman.h>

  // Returns: 0 if OK, −1 on error
  int msync(void *addr, size_t len, int flags);
  ```

- `munmap` function

  ```c
  #include <sys/mman.h>

  // Returns: 0 if OK, −1 on error
  int munmap(void *addr, size_t len);
  ```

### Q7：作者是怎么论述的

### Q8：作者解决了什么问题

### Q9：我有哪些疑问

#### Q9.1: v-node 和 i-node 的内部实现是怎样的

#### Q9.2: `poll` 和 `epoll` 有什么区别

#### Q9.3: 什么场景下需要使用 `mmap`

### Q10：这一章说得有道理吗？为什么

### Q11: 这一章讨论的知识的本质是什么

### Q12: 这一章讨论的知识的第一原则是什么

### Q13：这一章讨论的知识的结构是怎样的

### Q14：这一章讨论的知识为什么是这样的？为什么发展成这样？为什么需要它

### Q15：有哪些相似的知识？它们之间的联系是什么

### Q16：其他领域/学科有没有相关的知识？日常生活中有没有类似的现象

### Q17: 这一章对我有哪些用处/帮助/启示

### Q18: 我如何应用这一章的知识去解决问题

  [1]: https://stackoverflow.com/questions/8858328/poll-vs-epoll-insight
  [2]: https://stackoverflow.com/questions/4039832/select-vs-poll-vs-epoll
