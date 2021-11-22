# 《Professional JavaScript for Web Developers》分析笔记

## Chapter 8: Objects, Classes, and Object-Oriented Programming

### Q1：这一章的内容是什么？

### Q2：这一章的大纲是什么？

- Understanding Objects
  - Types of Properties
    - Data Properties
    - Accessor Properties
  - Defining Multiple Properties
    - `Object.defineProperties`
  - Reading Property Attributes
    - `Object.getOwnPropertyDescriptors`
  - Merging Objects
    - `Object.assign`
  - Object Identity and Equality
    - `Object.is` and `===`
  - Enhanced Object Syntax
    - Property Value Shorthand: `let person = { name }`
    - Computed Property Keys: `let person = { [nameKey]: 'Guo Jing' }`
    - Concise Method Syntax: omit the function keyword
  - Object Destructuring
    - Nested Destructuring
    - Partial Destructuring Completion
    - Parameter Context Matching
- Object creation
  - The Factory Pattern
    - `function createPerson(name, age, job) {}`
  - The Function Constructor Pattern
    - `let person = new Person('Guo Jing', 20, 'Soldier')`
    - Constructors as Functions
    - Problems with Constructors
  - The Prototype Pattern
    - How Prototypes Work
    - Understanding the Prototype Hierarchy
    - Prototypes and the "in" Operator
    - Property Enumeration Order
  - Object Iteration
    - Alternate Prototype Syntax
    - Dynamic Nature of Prototypes
    - Native Object Prototypes
    - Problems with Prototypes
- Inheritance
  - Prototype Chaining
    - Default Prototypes
    - Prototype and Instance Relationships
    - Working with Methods
    - Problems with Prototype Chaining
  - Constructor Stealing
    - Passing Arguments
    - Problems with Constructor Stealing
  - Combination Inheritance
  - Prototypal Inheritance
  - Parasitic Inheritance
  - Parasitic Combination Inheritance
- Classes
  - Class Definition Basics
    - Class Composition
  - The Class Constructor
    - Instantiation
    - Understanding Classes as Special Functions
  - Instance, Prototype and Class Members
    - Instance Members
    - Prototype Methods and Accessors
    - Static Class Methods and Accessors
    - Non-Function Prototype and Class Members
    - Iterator and Generator Methods
  - Inheritance
    - Inheritance Basics
    - Constructors, HomeObjects, and super()
    - Abstract Base Classes
    - Inheriting from Built-in Types
    - Class Maxins

### Q3：作者想要解决什么问题？

### Q4：这一章的关键词是什么？

- Prototype
- Prototype Chaining
- Constructor Stealing
- Combination Inheritance
- Prototypal Inheritance
- Parasitic Inheritance
- Parasitic Combination Inheritance

### Q5：这一章的关键句是什么？

- What is an object
  - An unordered collection of properties
  - An array of values in no particular order
  - Hash tables:
    nothing more than a grouping of name-value pairs
    where the value may be data or a function

#### 8.1 Understanding Objects

- Types of Properties
  - Data Properties: Contain a single location for a **data value**
    - `[[Configurable]]`
    - `[[Enumerable]]`
    - `[[Writable]]`
    - `[[Value]]`
  - Accessor Properties: contain a combination of a getter function and a setter function
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

