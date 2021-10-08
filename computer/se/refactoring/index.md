# 《Refactoring: Improving the Design of Existing Code》分析笔记

## Q1：这本书属于哪一类别的书？

计算机/软件工程。

## Q2：这本书的内容是什么？

## Q3：这本书的大纲是什么？

### 一级大纲

- Refactoring: A First Example
- Principles in Refactoring
- Bad Smells in Code
- Building Tests
- Introducing the Catalog
- A First Set of Refactorings
- Encapsulation
- Moving Features
- Organizing Data
- Simplifying Conditional Logic
- Refactoring APIs
- Dealing with Inheritance

### 二级大纲

- Refactoring: A First Example
- Principles in Refactoring
  - Defining Refactoring
  - The Two Hats
  - Why Should We Refactor?
  - When Should We Refactor?
  - Problems with Refactoring
  - Refactoring, Architecture, and YAGNI
  - Refactoring and the Wider Software Development Process
  - Refactoring and Performance
  - Where did Refactoring Come From?
  - Automated Refactorings
  - Going Further
- Bad Smells in Code
  - Mysterious Name
  - Duplicated Code
  - Long Function
  - Long Parameter List
  - Global Data
  - Mutable Data
  - Divergent Change
  - Shotgun Surgery
  - Feature Envy
  - Data Clumps
  - Primitive Obsession
  - Repeated Switches
  - Loops
  - Lazy Element
  - Speculative Generality
  - Temporary Field
  - Message Chains
  - Middle Man
  - Insider Trading
  - Large Class
  - Alternative Classes with Different Interfaces
  - Data Class
  - Refused Bequest
- Building Tests
  - The Value of Self-Testing Code
  - Sample Code to Test
  - A First Test
  - Add Another Test
  - Modifying the Fixture
  - Probing the Boundaries
  - Much More Than This
- Introducing the Catalog
  - Format of the Refactorings
  - The Choice of Refactorings
- A First Set of Refactorings
  - Extract Function
  - Inline Function
  - Extract Variable
  - Inline Variable
  - Change Function Declaration
  - Encapsulate Variable
  - Rename Variable
  - Introduce Parameter Object
  - Combine Functions into Class
  - Combine Functions into Transform
  - Split Phase
- Encapsulation
  - Encapsulate Record
  - Encapsulate Collection
  - Replace Primitive with Object
  - Replace Temp with Query
  - Extract Class
  - Inline Class
  - Hide Delegate
  - Remove Middle Man
  - Substitute Algorithm
- Moving Features
  - Move Function
  - Move Field
  - Move Statements into Function
  - Move Statements to Callers
  - Replace Inline Code with Function Call
  - Slide Statements
  - Split Loop
  - Replace Loop with Pipeline
  - Remove Dead Code
- Organizing Data
  - Split Variable
  - Rename Field
  - Replace Derived Variable with Query
  - Change Reference to Value
  - Change Value to Reference
  - Replace Magic Literal
- Simplifying Conditional Logic
  - Decompose Conditional
  - Consolidate Conditional Expression
  - Replace Nested Conditional with Guard Clauses
  - Replace Conditional with Polymorphism
  - Introduce Special Case
  - Introduce Assertion
  - Replace Control Flag with Break
- Refactoring APIs
  - Separate Query from Modifier
  - Parameterize Function
  - Remove Flag Argument
  - Preserve Whole Object
  - Replace Parameter with Query
  - Replace Query with Parameter
  - Remove Setting Method
  - Replace Constructor with Factory Function
  - Replace Function with Command
  - Replace Command with Function
  - Return Modified Value
  - Replace Error Code with Exception
  - Replace Exception with Precheck
- Dealing with Inheritance
  - Pull Up Method
  - Pull Up Field
  - Pull Up Constructor Body
  - Push Down Method
  - Push Down Field
  - Replace Type Code with Subclasses
  - Remove Subclass
  - Extract Superclass
  - Collapse Hierarchy
  - Replace Subclass with Delegate
  - Replace Superclass with Delegate

## Q4：作者想要解决什么问题？

## Q5：这本书的关键词是什么？

- Catalog 关于本书介绍的所有重构技巧的目录
- The Two Hats 将增加功能与重构活动分离
  - When I use refactoring to develop software, I divide my time between two distinct activities: adding functionality and refactoring.
  - When I add functionality, I shouldn’t be changing existing code; I'm just adding new capabilities.
    I measure my progress by adding tests and getting the tests to work.
  - When I refactor, I make a point of not adding functionality; I only restructure the code.
    I don’t add any tests (unless I find a case I missed earlier); I only change tests when I have to accommodate a change in an interface.
- The Rule of Three 重复三次以上就应该重构
  - Here’s a guideline Don Roberts gave me:
    The first time you do something, you just do it.
    The second time you do something similar, you wince at the duplication, but you do the duplicate thing anyway.
    The third time you do something similar, you refactor.
  - Or for those who like baseball: **Three strikes, then you refactor.**
- Bad Smells in Code
  - Shotgun Surgery 霰弹式修改
    - Shotgun surgery is an antipattern in software development and occurs 
      where a developer adds features to an application codebase which span a multiplicity of implementors or implementations in a single change.
  - Feature Envy
  - Data Clumps
  - Primitive Obsession
  - Lazy Element
  - Speculative Generality
  - Temporary Field
  - Message Chains
  - Insider Trading
  - Alternative Classes with Different Interfaces
  - Data Class
  - Refused Bequest

## Q6：这本书的关键句是什么？


## Q7：作者是怎么论述的？

## Q8：作者解决了什么问题？

## Q9：我有哪些疑问？

## Q10：这本书说得有道理吗？为什么？

## Q11：如何拓展这本书？

### Q11.1：为什么是这样的？为什么发展成这样？为什么需要它？

### Q11.2：有哪些相似的知识点？它们之间的联系是什么？

#### 相关网站

- [refactoring.com][1]
- [refactoring.guru][2]
- 「左耳听风」专栏提到的软件设计方面的网站

  [1]: https://refactoring.com/
  [2]: https://refactoring.guru/

### Q11.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象？

## Q12：这本书和我有什么关系？

