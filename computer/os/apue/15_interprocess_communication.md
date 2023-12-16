# 《Advanced Programming in the UNIX Environment》分析笔记

## Chapter 15: Interprocess Communication

### Q1：这一章的内容属于哪一类别

计算机/操作系统/Unix。

### Q2：这一章的内容是什么

介绍 Unix 系统下进程间通信的方式。

### Q3：这一章的大纲是什么

- Pipes
- `popen` and `pclose` Functions
- Coprocesses
- FIFOs
- XSI IPC
- Message Queues
- Semaphores
- Shared Memory
- POSIX Semaphores
- Client-Server Properties

### Q4：作者想要解决什么问题

### Q5：这一章的关键词是什么

### Q6：这一章的关键句是什么

#### 15.2 Pipes

- Limitations of pipes
  - Historically, they have been half duplex (i.e., data flows in only one direction).
  - Pipes can be used only between processes that have a common ancestor.
    - Normally, a pipe is created by a process, that process calls `fork`, and the pipe is used between the parent and the child.

- `pipe` function
  - `fd[0]` is open for reading, and `fd[1]` is open for writing.
  - The output of `fd[1]` is the input for `fd[0]`.

  ```c
  #include <unistd.h>

  // Returns: 0 if OK, −1 on error
  int pipe(int fd[2]);
  ```

#### 15.3 `popen` and `pclose` Functions

- `popen` function
  - The returned file pointer is readable if type is "r" or writable if type is "w".

  ```c
  #include <stdio.h>

  // Returns: file pointer if OK, NULL on error.
  FILE *popen(const char *cmdstring, const char *type);
  ```

- `pclose` function
  - Closes the standard I/O stream, waits for the command to terminate, and returns the termination status of the shell.

  ```c
  #include <stdio.h>

  // Returns: termination status of cmdstring, or −1 on error.
  int pclose(FILE *fp);
  ```

#### 15.4 Coprocesses

- A coprocess normally runs in the background from a shell,
  and its standard input and standard output are connected to another program using a pipe.

> 伍注：不太懂这一节。

#### 15.5 FIFOs

- FIFOs are sometimes called named pipes.
  - With FIFOs, unrelated processes can exchange data.

- `mkfifo` function

  ```c
  #include <sys/stat.h>

  // Both return: 0 if OK, −1 on error
  int mkfifo(const char *path, mode_t mode);
  int mkfifoat(int fd, const char *path, mode_t mode);
  ```

#### 15.6 XSI IPC

- 3 types of IPC that we call XSI IPC
  - message queues
  - semaphores
  - shared memory

- Identifiers and Keys
  - The identifier is an internal name for an IPC object.
  - Cooperating processes need an external naming scheme to be able to rendezvous using the same IPC object.
  - An IPC object is associated with a **key** that acts as an external name.

- Ways for a client and a server to rendezvous at the same IPC structure
  - Specifying a key of `IPC_PRIVATE`.
  - Defining the key in a common header.
  - Agree on a pathname and project ID and call the function `ftok` to convert these two values into a key.

  ```c
  #include <sys/ipc.h>

  // Returns: key if OK, (key_t)−1 on error
  key_t ftok(const char *path, int id);
  ```

- Reference an existing queue
  - Never specify `IPC_PRIVATE` to reference an existing queue, since this special key value always creates a new queue.
  - To reference an existing queue that was created with a key of `IPC_PRIVATE`,
    we must know the associated identifier and then use that identifier in the other IPC calls, bypassing the get function.

- Permission Structure
  - XSI IPC associates an `ipc_perm` structure with each IPC structure.
  - This structure defines the permissions and owner and others.

  ```c
  struct ipc_perm {
    key_t          __key;       /* Key supplied to msgget(2) */
    uid_t          uid;         /* Effective UID of owner */
    gid_t          gid;         /* Effective GID of owner */
    uid_t          cuid;        /* Effective UID of creator */
    gid_t          cgid;        /* Effective GID of creator */
    unsigned short mode;        /* Permissions */
    unsigned short __seq;       /* Sequence number */
  };
  ```

- Configuration Limits
  - All three forms of XSI IPC have built-in limits that we may encounter.
  - Most of these limits can be changed by reconfiguring the kernel.

- Problems of XSI IPC
  - The IPC structures are systemwide and do not have a reference count.
  - These IPC structures are not known by names in the file system.
  - Since these forms of IPC don’t use file descriptors, we can’t use the multiplexed I/O functions with them.

- Advantages of XSI IPC
  - Reliable, flow controlled, and record oriented,
  - They can be processed in other than first-in, first-out order.

#### 15.7 Message Queues

> 伍注：Ubuntu 系统下可以使用 man 命令查看以下函数。

- `msgget` function
  - Either open an existing queue or create a new queue.

  ```c
  #include <sys/msg.h>

  // Returns: message queue ID if OK, −1 on error
  int msgget(key_t key, int flag);
  ```

- `msgctl` function
  - Performs various operations on a queue:
    - `IPC_STAT`
    - `IPC_SET`
    - `IPC_RMID`

  ```c
  #include <sys/msg.h>

  // Returns: 0 if OK, −1 on error
  int msgctl(int msqid, int cmd, struct msqid_ds *buf );
  ```

- `msgsnd` function

  ```c
  #include <sys/msg.h>

  // Returns: 0 if OK, −1 on error
  int msgsnd(int msqid, const void *ptr, size_t nbytes, int flag);
  ```

> 伍注：msgsnd 传入的数据会被拷贝到队列的缓冲区里。

- `msgrcv` function

  ```c
  #include <sys/msg.h>

  // Returns: size of data portion of message if OK, −1 on error
  ssize_t msgrcv(int msqid, void *ptr, size_t nbytes, long type, int flag);
  ```

- The removal of a message queue is ungraceful
  - The removal of a queue simply generates errors on the next queue operation by processes still using the queue.

#### 15.8 Semaphores

> 伍注：感觉 XSI Semaphores 的接口设计得有点像大杂烩，不太好用，暂时不深入了解。

- `semget` function

  ```c
  #include <sys/sem.h>

  // Returns: semaphore ID if OK, −1 on error
  int semget(key_t key, int nsems, int flag);
  ```

- `semctl` function

  ```c
  #include <sys/sem.h>

  int semctl(int semid, int semnum, int cmd, ... /* union semun arg */ );
  ```

- `semop` function

  ```c
  #include <sys/sem.h>

  // Returns: 0 if OK, −1 on error
  int semop(int semid, struct sembuf semoparray[], size_t nops);
  ```

#### 15.9 Shared Memory

- Shared Memory is the fastest form of IPC
  - because the data does not need to be copied between the client and the server.

- The only trick in using shared memory is
  - synchronizing access to a given region among multiple processes.

- `shmget` function

  ```c
  #include <sys/shm.h>

  // Returns: shared memory ID if OK, −1 on error
  int shmget(key_t key, size_t size, int flag);
  ```

- `shmctl` function

  ```c
  #include <sys/shm.h>

  // Returns: 0 if OK, −1 on error
  int shmctl(int shmid, int cmd, struct shmid_ds *buf );
  ```

- `shmat` function

  ```c
  #include <sys/shm.h>

  // Returns: pointer to shared memory segment if OK, −1 on error
  void *shmat(int shmid, const void *addr, int flag);
  ```

- `shmdt` function

  ```c
  #include <sys/shm.h>

  // Returns: 0 if OK, −1 on error
  int shmdt(const void *addr);
  ```

#### 15.10 POSIX Semaphores

- `sem_open` function

  ```c
  #include <semaphore.h>

  // Returns: Pointer to semaphore if OK, SEM_FAILED on error
  sem_t *sem_open(const char *name, int oflag, ... /* mode_t mode, unsigned int value */ );
  ```

- `sem_close` function

  ```c
  #include <semaphore.h>

  // Returns: 0 if OK, −1 on error
  int sem_close(sem_t *sem);
  ```

- `sem_unlink` function

  ```c
  #include <semaphore.h>

  // Returns: 0 if OK, −1 on error
  int sem_unlink(const char *name);
  ```

- `sem_wait` function

  ```c
  #include <semaphore.h>

  // Both return: 0 if OK, −1 on error
  int sem_trywait(sem_t *sem);
  int sem_wait(sem_t *sem);
  ```

- `sem_timedwait` function

  ```c
  #include <semaphore.h>
  #include <time.h>

  // Returns: 0 if OK, −1 on error
  int sem_timedwait(sem_t *restrict sem, const struct timespec *restrict tsptr);
  ```

- `sem_post` function

  ```c
  #include <semaphore.h>

  // Returns: 0 if OK, −1 on error
  int sem_post(sem_t *sem);
  ```

- `sem_init` function

  ```c
  #include <semaphore.h>

  // Returns: 0 if OK, −1 on error
  int sem_init(sem_t *sem, int pshared, unsigned int value);
  ```

- `sem_destroy` function

  ```c
  #include <semaphore.h>

  // Returns: 0 if OK, −1 on error
  int sem_destroy(sem_t *sem);
  ```

- `sem_getvalue` function

  ```c
  #include <semaphore.h>

  // Returns: 0 if OK, −1 on error
  int sem_getvalue(sem_t *restrict sem, int *restrict valp);
  ```

### Q7：作者是怎么论述的

### Q8：作者解决了什么问题

### Q9：我有哪些疑问

#### Q9.1: pipe 是怎么实现的

#### Q9.2: 共享内存是怎么实现的

### Q10：这一章说得有道理吗？为什么

### Q11: 这一章讨论的知识的本质是什么

### Q12: 这一章讨论的知识的第一原则是什么

### Q13：这一章讨论的知识的结构是怎样的

### Q14：这一章讨论的知识为什么是这样的？为什么发展成这样？为什么需要它

### Q15：有哪些相似的知识？它们之间的联系是什么

### Q16：其他领域/学科有没有相关的知识？日常生活中有没有类似的现象

### Q17: 这一章对我有哪些用处/帮助/启示

### Q18: 我如何应用这一章的知识去解决问题
