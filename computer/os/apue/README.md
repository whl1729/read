# 《Advanced Programming in the UNIX Environment》分析笔记

## Q1：这本书属于哪一类别的书

计算机/操作系统。

## Q2：这本书的内容是什么

介绍UNIX操作系统的基础知识。

## Q3：这本书的大纲是什么

### 一级大纲

- UNIX System Overview
- UNIX Standardization and Implementations
- File I/O
- Files and Directories
- Standard I/O Library
- System Data Files and Information
- Process Environment
- Process Control
- Process Relationships
- Signals
- Threads
- Thread Control
- Daemon Processes
- Advanced I/O
- Interprocess Communication
- Network IPC: Sockets
- Advanced IPC
- Terminal I/O
- Pseudo Terminals
- A Database Library
- Communicating with a Network Printer

### 二级大纲

- UNIX System Overview
  - UNIX Architecture
  - Logging In
  - Files and Directories
  - Input and Output
  - Programs and Processes
  - Error Handling
  - User Identification
  - Signals
  - Time Values
  - System Calls and Library Functions
- UNIX Standardization and Implementations
  - UNIX Standardization
  - UNIX System Implementations
  - Relationship of Standards and Implementations
  - Limits
  - Options
  - Feature Test Macros
  - Primitive System Data Types
  - Differences Between Standards
- File I/O
  - File Descriptors
  - `open` and `openat` Functions
  - `create` Function
  - `close` Function
  - `lseek` Function
  - `read` Function
  - `write` Function
  - I/O Efficiency
  - File Sharing
  - Atomic Operations
  - `dup` and `dup2` Functions
  - `sync`, `fsync`, and `fdatasync` Functions
  - `fcntl` Function
  - `ioctl` Function
  - `/dev/fd`
- Files and Directories
  - `stat`, `fstat`, `fstatat`, and `lstat` Functions
  - File Types
  - Set-User-ID and Set-Group-ID
  - File Access Permissions
  - Ownership of New Files and Directories
  - `access` and `faccessat` Functions
  - `umask` Function
  - `chmod`, `fchmod`, and `fchmodat` Function
  - Sticky Bit
  - `chown`, `fchown`, `fchownat` and `lchown` Functions
  - File Size
  - File Truncation
  - File Systems
  - `link`, `linkat`, `unlink`, `unlinkat`, and `remove` Functions
  - `rename` and `renameat` Functions
  - Symbolic Links
  - Creating and Reading Symbolic Links
  - File Times
  - `futimens`, `utimensat`, and `utimes` Functions
  - `mkdir`, `mkdirat`, and `rmdir` Functions
  - Reading Directories
  - `chdir`, `fchdir`, and `getcwd` Functions
  - Device Special Files
  - Summary of File Access Permission Bits
- Standard I/O Library
  - Streams and `FILE` Objects
  - Standard Input, Standard Output, and Standard Error
  - Buffering
  - Opening a Stream
  - Reading and Writing a Stream
  - Line-at-a-Time I/O
  - Standard I/O Efficiency
  - Binary I/O
  - Positioning a Stream
  - Formatted I/O
  - Implementation Details
  - Temporary Files
  - Memory Streams
  - Alternatives to Standard I/O
- System Data Files and Information
  - Password File
  - Shadow Passwords
  - Group File
  - Supplementary Group IDs
  - Implementation Differences
  - Other Data Files
  - Login Accounting
  - System Identification
  - Time and Date Routines
- Process Environment
  - `main` Function
  - Process Termination
  - Command-Line Arguments
  - Environment List
  - Memory Layout of a C Program
  - Shared Libraries
  - Memory Allocation
  - Environment Variables
  - `setjmp` and `longjmp` Functions
  - `getrlimit` and `setrlimit` Functions
- Process Control
  - Process Identifiers
  - `fork` Function
  - `vfork` Function
  - `exit` Functions
  - `wait` and `waitpid` Functions
  - `waitid` Function
  - `wait3` and `wait4` Functions
  - Race Conditions
  - `exec` Functions
  - Changing User IDs and Group IDs
  - Interpreter Files
  - `system` Function
  - Process Accounting
  - User Identification
  - Process Scheduling
  - Process Times
- Process Relationships
  - Terminal Logins
  - Network Logins
  - Process Groups
  - Sessions
  - Controlling Terminal
  - `tcgetpgrp`, `tcsetpgrp`, and `tcgetsid` Functions
  - Job Control
  - Shell Execution of Programs
  - Orphaned Process Groups
  - FreeBSD Implementation
- Signals
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
- Threads
  - Thread Concepts
  - Thread Identification
  - Thread Creation
  - Thread Termination
  - Thread Synchronization
- Thread Control
  - Thread Limits
  - Thread Attributes
  - Synchronization Attributes
  - Reentrancy
  - Thread-Specific Data
  - Cancel Options
  - Threads and Signals
  - Threads and fork
  - Threads and I/O
- Daemon Processes
  - Daemon Characteristics
  - Coding Rules
  - Error Logging
  - Single-Instance Daemons
  - Daemon Conventions
  - Client-Server Model
- Advanced I/O
  - Nonblocking I/O
  - Record Locking
  - I/O Multiplexing
  - Asynchronous I/O
  - `readv` and `writev` Functions
  - `readn` and `writen` Functions
  - Memory-Mapped I/O
- Interprocess Communication
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
- Network IPC: Sockets
  - Socket Descriptors
  - Addressing
  - Connection Establishment
  - Data Transfer
  - Socket Options
  - Out-of-Band Data
  - Nonblocking and Asynchronous I.O
- Advanced IPC
  - UNIX Domain Sockets
  - Unique Connections
  - Passing File Descriptors
  - An Open Server, Version 1
  - An Open Server, Version 2
- Terminal I/O
  - Special Input Characters
  - Getting and Setting Terminal Attributes
  - Terminal Option Flags
  - `stty` Command
  - Baud Rate Functions
  - Line Control Functions
  - Terminal Identification
  - Canonical Mode
  - Noncanonical Mode
  - Terminal Window Size
  - `termcap`, `terminfo`, and `curses`
- Pseudo Terminals
  - Opening Pseudo-Terminal Devices
  - `pty_fork` Function
  - `pty` Program
  - Using the `pty` Program
  - Advanced Features
- A Database Library
  - History
  - The Library
  - Implementation Overview
  - Centralized or Decentralized
  - Concurrency
  - Building the Library
  - Performance
- Communicating with a Network Printer
  - The Internet Printing Protocol
  - The Hypertext Transfer Protocol
  - Printer Spooling
- Appendix
  - Function Prototypes

## Q4：作者想要解决什么问题

## Q5：这本书的关键词是什么

## Q6：这本书的关键句是什么

## Q7：作者是怎么论述的

## Q8：作者解决了什么问题

## Q9：我有哪些疑问

## Q10：这本书说得有道理吗？为什么

## Q11：如何拓展这本书

### Q11.1：为什么是这样的？为什么发展成这样？为什么需要它

### Q11.2：有哪些相似的知识点？它们之间的联系是什么

### Q11.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象

## Q12：这本书和我有什么关系
