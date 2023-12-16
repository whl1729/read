# Fluent Python 分析笔记

## 21 Asynchronous Programming

### 第21章讨论哪些话题

- 四种异步结构：async def, await, async with, async for
- 支持异步结构的对象：原生协程、异步版本的上下文管理器、迭代器、生成器和列表推导式
- 异步库：asyncio

### 目前为止我知道什么

- 我不了解 Python 的异步编程，但对 JavaScript 的异步编程有所了解
- JavaScript 使用 async 定义异步函数，async 函数里面可以使用 await
- JavaScript 可以定义 Future 对象，Future 对象可以被 await

### 目前为止我不知道什么

- 四种异步编程结构的用法：async def, await, async with, async for
- 支持异步结构的对象的用法：原生协程、异步版本的上下文管理器、迭代器、生成器和列表推导式
- 异步库的使用：asyncio

### 第21章的主要内容是什么

- 原生协程：使用 `async def` 定义的函数
- 古典协程：使用 `my_coro.send(data)` 来发送数据或 `yield` 来接收数据的函数
- 基于生成器的协程：使用 `@types.coroutine` 装饰的生成器函数
- 异步生成器：使用 `async def` 定义或函数中使用 `yield` 的生成器

### 关于第21章我有哪些疑问

#### Q1: Example 21-1 的处理流程是怎样的

- 第8步创建了多个 coroutine 后，await 的操作会自动运行吗？还是要等到 asyncio.as_completed 时才会运行？

#### Q1: Example 21-1 执行 await loop.getaddrinfo 后究竟会发生什么

- 首先分析 getaddrinfo 的内部实现
  - getaddrinfo 需要进行网络 IO，比如请求 DNS 服务器。
  - getaddrinfo 向 DNS 服务器发送请求后，需要等待响应。
  - 为了避免因等待响应而浪费时间，应该让 CPU 先去做其他事情。
  - 等到网卡受到 DNS 服务器的响应后，再通知 CPU 去处理响应结果。
  - 那么执行 await loop.getaddrinfo 函数后，是否会先发送完网络请求后才返回？
  - 估计需要看到 C 源码才能弄懂这个流程，等看完全书再回头研究吧。

- 然后分析 Python coroutine 的创建与执行顺序
  - 测试发现，第8步创建 coroutine 的时候不会执行 coroutine 的任何语句。
  - 遇到一个困难：我发现执行完第9步，也就是找到一个 completed 的 coro 的时候，coro 里面的语句却还没有被执行
  - 异步编程太难分析执行流程了！

- 浅析 `asyncio.as_completed`
  - 看了此函数的源码，它是一个迭代器，返回一个个 coroutine，因此不会 block
  - 刚使用时我产生了误解，以为它返回的 coroutine 是已经完成执行的
  - 事实上并非如此，你需要 await 它返回的 coroutine，对应的 coroutine 才会被执行
  - 此函数实际更像是一个 coroutine 调度器，感觉跟 JavaScript 的 `Promise.all` 差不多

### 如何拓展第21章的内容

- asyncio.as_completed 跟操作系统的 select 是否类似？异步I/O？
- asyncio.as_completed 与 Node.js 的 Promise.all 是否类似？
- "What Color Is Your Function?" by Bob Nystrom
- Caleb Hattingh's book: Using Asyncio in Python

### 第21章如何指导实践

- Example 21-11: pathlib.Path 重载 `/` 来拼接路径：`Path(__file__).parent.absolute() / 'static'`
- Example 21-12: 使用 `functools.partial` 来适配接口
