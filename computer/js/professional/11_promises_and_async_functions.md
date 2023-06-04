# Professional JavaScript for Web Developers 分析笔记

## 11 Promises and Async Functions

- Controlling Promise State with the Executor
  - Executor 内部的同步代码会被立即执行，resolve 或 reject 语句需要等事件循环来执行

- Promise.resolve()

  ```javascript
  // The following two are effectively equivalent
  let p1 = new Promise((resolve, reject) => resolve());
  let p2 = Promise.resolve();
  ```

- Promise.reject()

  ```javascript
  // The following two are effectively equivalent
  let p1 = new Promise((resolve, reject) => reject())
  let p2 = Promise.reject()
  ```

- Synchronous/Asynchronous Execution Duality

> 伍注：同步代码和异步代码可以理解为两套不同的执行机制，所以同步代码无法捕获异步代码抛出的异常。
> 这里跟那篇 What Color is Your Function 可以相互印证。
>
> The error from the rejected promise is not being thrown inside the synchronous execution thread,
> but instead from the browser’s asynchronous message queue execution.
> Therefore, the encapsulating try/catch block will not suffice to catch this error.
>
> Once code starts to execute in this asynchronous mode,
> the only way to interact with it is to use asynchronous mode constructs—more specifically, promise methods.
