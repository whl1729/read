# 《Advanced Programming in the UNIX Environment》分析笔记

## Chapter 16: Network IPC: Sockets

### Q1：这一章的内容属于哪一类别？

计算机/操作系统/Unix

### Q2：这一章的内容是什么？

介绍网络中进程间通信方式——套接字。

### Q3：这一章的大纲是什么？

- Socket Descriptors
- Addressing
- Connection Establishment
- Data Transfer
- Socket Options
- Out-of-Band Data
- Nonblocking and Asynchronous I/O

### Q4：作者想要解决什么问题？

### Q5：这一章的关键词是什么？

### Q6：这一章的关键句是什么？

#### 16.2 Socket Descriptors

- Socket
  - An abstraction of a communication endpoint.

- Socket descriptors
  - Are implemented as file descriptors in the UNIX System.

- `socket` function

  ```c
  #include <sys/socket.h>

  // Returns: file (socket) descriptor if OK, −1 on error
  int socket(int domain, int type, int protocol);
  ```

> 备注1：`man socket`。
> 备注2：domain 选定一个协议族，type 选定数据报文类型。
> 目前最常用的用法是，domain 选择 ip 或 ipv6，type 选择 tcp 或 udp，
> 这么看来，domain 确定了网络层协议，type 确定了运输层协议。

- `shutdown` function
  - Allows us to deactivate a socket independently of the number of active file descriptors referencing it.
  - It is sometimes convenient to shut a socket down in one direction only.

  ```c
  #include <sys/socket.h>

  // Returns: 0 if OK, −1 on error
  int shutdown(int sockfd, int how);
  ```

#### 16.3 Addressing

##### 16.3.3 Address Lookup

- The network configuration information
  - This information can be kept in static files (e.g., /etc/hosts, /etc/services),
  - or it can be managed by a name service, such as DNS (Domain Name System) or NIS (Network Information Service).
  - Regardless of where the information is kept, the same functions can be used to access it.

> 伍注：以上告诉我们：获取网络配置方式至少有两种方法：查看系统文件、调用函数。

- Get host information
  - `gethostent` 的返回结果跟 `/etc/hosts` 文件相对应。

  ```c
  #include <netdb.h>

  // Returns: pointer if OK, NULL on error
  struct hostent *gethostent(void);

  void sethostent(int stayopen);
  void endhostent(void);
  ```

  ```bash
  along:~/exercise/apue/16$ ./gethostent
  h_name: localhost
  h_addrtype: 2
  h_length: 4
  h_aliases:
  addr:

  h_name: along
  h_addrtype: 2
  h_length: 4
  h_aliases:
  addr:

  h_name: ip6-localhost
  h_addrtype: 2
  h_length: 4
  h_aliases: ip6-loopback
  addr:

  along:~/exercise/apue/16$ cat /etc/hosts
  127.0.0.1 localhost
  127.0.1.1 along

  # The following lines are desirable for IPv6 capable hosts
  ::1     ip6-localhost ip6-loopback
  fe00::0 ip6-localnet
  ff00::0 ip6-mcastprefix
  ff02::1 ip6-allnodes
  ff02::2 ip6-allrouters
  ```

- Get network names and numbers
  - `getnetbyaddr` 的返回结果跟 `/etc/networks` 文件相对应。

  ```c
  #include <netdb.h>

  // All return: pointer if OK, NULL on error
  struct netent *getnetbyaddr(uint32_t net, int type);
  struct netent *getnetbyname(const char *name);
  struct netent *getnetent(void);

  void setnetent(int stayopen);
  void endnetent(void);
  ```

  ```bash
  # Ubuntu 20.04 下，`getnetbyaddr` 的 `net` 参数需要按网络序填写。
  # 目前只有 `169.254.0.0` 这个地址能够返回成功（结果如下），`127.0.0.1` 等地址均会返回 NULL。
  # 这个地址恰好是 `/etc/networks` 文件里配置的地址。
  along:~/exercise/apue/16$ ./getnetbyaddr $(printf "%d" 0xa9fe0000)
  n_name: link-local
  n_addrtype: 2
  n_net: 2851995648
  n_aliases:

  along:~/exercise/apue/16$ cat /etc/networks
  # symbolic names for networks, see networks(5) for more information
  link-local 169.254.0.0
  ```

  ```bash
  # Ubuntu 20.04 下，`getnetbyname` 的 `name` 参数需要为 `/etc/networks` 文件里的网络名字。
  along:~/exercise/apue/16$ ./getnetbyname link-local
  n_name: link-local
  n_addrtype: 2
  n_net: 2851995648
  n_aliases:
  ```

- Get protocol information
  - 以下接口对应 `/etc/protocols` 文件的内容。

  ```c
  #include <netdb.h>

  // All return: pointer if OK, NULL on error
  struct protoent *getprotobyname(const char *name);
  struct protoent *getprotobynumber(int proto);
  struct protoent *getprotoent(void);

  void setprotoent(int stayopen);
  void endprotoent(void);
  ```

- Get server information
  - 以下接口返回的服务名字与 `/etc/services` 相对应，但是端口号对应不上。

  ```c
  #include <netdb.h>

  // All return: pointer if OK, NULL on error
  // getservbyname: echo: 1792; datetime: 3328; ftp: 5376
  struct servent *getservbyname(const char *name, const char *proto);
  struct servent *getservbyport(int port, const char *proto);
  struct servent *getservent(void);

  void setservent(int stayopen);
  void endservent(void);
  ```

#### 16.4 Connection Establishment

#### 16.5 Data Transfer

#### 16.6 Socket Options

#### 16.7 Out-of-Band Data

#### 16.8 Nonblocking and Asynchronous I/O

### Q7：作者是怎么论述的？

### Q8：作者解决了什么问题？

### Q9：我有哪些疑问？

#### Q9.1: 操作系统是如何管理进程端口的？

### Q10：这一章说得有道理吗？为什么？

### Q11: 这一章讨论的知识的本质是什么？

### Q12: 这一章讨论的知识的第一原则是什么？

### Q13：这一章讨论的知识的结构是怎样的？

### Q14：这一章讨论的知识为什么是这样的？为什么发展成这样？为什么需要它？

### Q15：有哪些相似的知识？它们之间的联系是什么？

### Q16：其他领域/学科有没有相关的知识？日常生活中有没有类似的现象？

### Q17: 这一章对我有哪些用处/帮助/启示？

### Q18: 我如何应用这一章的知识去解决问题？
