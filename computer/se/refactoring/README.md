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
- The Rule of Three 重复三次以上就应该重构
- Bad Smells in Code
  - Shotgun Surgery 霰弹式修改，一次修改太多地方或增加太多功能
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

## Q11: 这本书讨论的知识的本质是什么？

重构的本质（或者说重构的定义）：

在不改变软件可观察行为的前提下，
为提高其可理解性和降低其修改成本，
对软件内部结构进行的调整。

## Q12: 这本书讨论的知识的第一原则是什么？

## Q13：这本书讨论的知识的结构是怎样的？

这本书讨论了「重构」的基本知识，主要包括四个部分：

- 重构的原则
- 代码坏味道
- 测试方法
- 重构技巧

这四个部分之间是递进关系：

- 对于重构活动，我们首先需要知道重构的基本原则，用来指导我们的实践。
- 为什么需要重构？因为我们闻到了代码的坏味道。
- 重构的第一步应该做什么？写测试用例、搭建测试环境。
- 闻到代码坏味道，并且写好测试用例后，接下来便是运用各种重构技巧去对代码进行重构。

## Q14：这本书讨论的知识为什么是这样的？为什么发展成这样？为什么需要它？

## Q15：有哪些相似的知识？它们之间的联系是什么？

### 相关网站

- [refactoring.com][1]
- [refactoring.guru][2]
- 「左耳听风」专栏提到的软件设计方面的网站

  [1]: https://refactoring.com/
  [2]: https://refactoring.guru/

## Q16：其他领域/学科有没有相关的知识？日常生活中有没有类似的现象？

## Q17: 这本书对我有哪些用处/帮助/启示？

## Q18: 我如何应用这本书的知识去解决问题？
