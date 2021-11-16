# 《Professional JavaScript for Web Developers》分析笔记

## Chapter 8: Objects, Classes, and Object-Oriented Programming

### Q1：这一章的内容是什么？

### Q2：这一章的大纲是什么？

- Understanding Objects
- Object creation
- Inheritance
- Classes

### Q3：作者想要解决什么问题？

### Q4：这一章的关键词是什么？

### Q5：这一章的关键句是什么？

- What is an object
  - An unordered collection of properties
  - An array of values in no particular order
  - Hash tables:
    nothing more than a grouping of name-value pairs
    where the value may be data or a function

#### 8.1 Understanding Objects

- Types of Properties
  - Data Properties
    - `[[Configurable]]`
    - `[[Enumerable]]`
    - `[[Writable]]`
    - `[[Value]]`
  - Accessor Properties
    - `[[Configurable]]`
    - `[[Enumerable]]`
    - `[[Get]]`
    - `[[Set]]`

- Defining Multiple Properties
  - `Object.defineProperties()`

- Reading Property Attributes
  - `Object.getOwnPropertyDescriptor()`
  - `Object.getOwnPropertyDescriptors()`

- Merging Objects: `Object.assign()`
  - for each source object copies the enumerable and own  properties onto the destination object.
  - shallow copy

- Object Identity and Equality
  - `===`
  - `Object.is()`

- Enhanced Object Syntax
  - Property Value Shorthand
  - Computed Property Keys
  - Concise Method Syntax

- Object Destructuring
  - Nested Destructuring
  - Partial Destructing Completion
  - Parameter Context Matching

#### 8.2 Object creation

#### 8.3 Inheritance

#### 8.4 Classes

### Q6：作者是怎么论述的？

### Q7：作者解决了什么问题？

### Q8：我有哪些疑问？

#### Q8.1: P255 "Defining Multiple Properties"一节的例子中，为什么修改year失败？

### Q9：这一章说得有道理吗？为什么？

### Q10：如何拓展这一章？

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它？

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么？

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象？

### Q11：这一章和我有什么关系？

