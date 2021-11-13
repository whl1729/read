# 《Professional JavaScript for Web Developers》分析笔记

## Chapter 7: Iterators and Generators

### Q1：这一章的内容是什么？

### Q2：这一章的大纲是什么？

- Introduction to Iteration
- The Iterator Pattern
  - The Iterable Protocol
  - The Iterator Protocol
  - Custom Iterator Definition
  - Early Termination of Iterators
- Generators
  - Generator Basics
  - Interrupting Execution with "yield"
  - Using a Generator as the Default Iterator
  - Early Termination of Generators

### Q3：作者想要解决什么问题？

### Q4：这一章的关键词是什么？

- iterable
- iterator
- generator
- yield

### Q5：这一章的关键句是什么？

#### 7.1 Introduction to Iteration

- Perfoming iteration using the common loop is not ideal
  - Iterating through the data structure requires a specific knowledge of how to use the data structure.
  - The order of traversal is not inherent to the data structure.

#### 7.2 The Iterator Pattern

- Iterable vs Iterator
  - Anything that implements the Iterable interface
    can be "consumed" by an object that implements the Iterator interface.
  - An iterator is a separate object created on demand and intended for a single use.
  - Each iterator is associated with an iterable,
    and the iterator exposes an API to iterate through the associated iterable a single time.
  - The iterator doesn’t need to understand the structure of the iterable it is associated with;
    it only must know how to retrieve sequential values.

- The Iterable Protocol
  - Default iterator: `Symbol.iterator`
    - Iterator factory function

- The Iterator Protocol
  - `next()` returns `{done, value}`

- Garbage Collection
  - An iterator maintains a reference to the iterable object,
    so be aware that the iterator’s existence will prevent garbage collection of the iterable object.

- Early Termination of Iterators
  - The optional `return()` method allows for specifying behavior that will execute only if the iterator is closed prematurely.
  - Scenarios where this might happen include the following:
    - A for...of loop exits early via break, continue, return, or throw.
    - A destructuring operation does not consume all values.
  - Because the return() method is optional, not all iterators are closable.
    - Array Iterators are not closable.

#### 7.3 Generators

- Generator Basics
  - `function* generatorFn() {}`
  - Arrow functions cannot be used as generator functions.
  - Generator function execution will only begin upon the initial next() invocation.
  - Generator objects implement the Iterable interface.

- Interrupting Execution with "yield"
  - The yield keyword allows generators to stop and start execution.
  - A generator function exiting via the yield keyword will have a done value of false;
    a generator function exiting via the return keyword will have a done value of true.

- Using a Generator Object as an Iterable

- Using "yield" for Input and Output

- Early Termination of Generators
  - `return()`
  - `throw()`
  - If the generator object has not yet begun execution,
    calling throw() cannot be caught inside the function
    because the error is thrown from outside the function block.

### Q6：作者是怎么论述的？

### Q7：作者解决了什么问题？

### Q8：我有哪些疑问？

#### Q8.1: what is the differences between "iterator is closeable" and "iterator has return function"?

### Q9：这一章说得有道理吗？为什么？

### Q10：如何拓展这一章？

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它？

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么？

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象？

### Q11：这一章和我有什么关系？

