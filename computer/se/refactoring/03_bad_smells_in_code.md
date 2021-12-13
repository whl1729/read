# 《Refactoring: Improve the Design of Existing Code》分析笔记

## Chapter 3: Bad Smells in Code

### Q1：这一章的内容属于哪一类别？

### Q2：这一章的内容是什么？

### Q3：这一章的大纲是什么？

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

### Q4：作者想要解决什么问题？

### Q5：这一章的关键词是什么？

- Shotgun surgery
  - An antipattern in software development and occurs
    where a developer adds features to an application codebase
    which span a multiplicity of implementors or implementations in a single change.

- Feature Envy
  - A classic case of Feature Envy occurs when a function in one module
    spends more time communicating with functions or data inside another module
    than it does within its own module.

### Q6：这一章的关键句是什么？

#### Mysterious Name

- When you can't think of a good name for something, it's often a sign of a deeper design malaise.

> 伍注：当你发现很难起一个好的名字时，这通常暗示着设计上的不合理。

- Refactoring Skills
  - Change Function Declaration
  - Rename Variable
  - Rename Field

#### Duplicated Code

- Refactoring Skills
  - Extract Function
  - Pull Up Method
  - Slide Statement (为抽取函数做准备)

#### Long Function

- The longer a function is, the more difficult it is to understand.

- Use function to comment
  - A heuristic we follow is that whenever we feel the need to comment something, we write a function instead.

- Decompose functions if the **semantic distance** is long
  - We may do this on a group of lines or even on a single line of code.
  - We do this even if the method call is longer than the code it replaces—
    provided the method name explains the purpose of the code.
  - The key here is not function length but the semantic distance between what the method does and how it does it.

- Refactoring Skills
  - Extract Function
  - Replace Temp with Query （消除临时变量）
  - Introduce Parameter Object （解决参数过多的问题）
  - Preserver Whole Object （同上）
  - Replace Function with Command （解决临时变量或参数过多的问题）
  - Decompose Conditional
  - Replace Conditional with Polymorphism

#### Long Parameter List

- Refactoring Skills
  - Replace Parameter with Query
  - Preserve Whole Object
  - Introduce Parameter Object
  - Remove Flag Argument
  - Combine Functions into Class

#### Global Data

- Refactoring Skills
  - Encapsulate Variable

#### Mutable Data

- Refactoring Skills
  - Encapsulate Variable (便于检视变量的访问情况及后续修改)
  - Split Variable (当变量有多个用途时，将其拆分，避免误修改)
  - Slide Variable (将无副作用的代码与有副作用的代码分开)
  - Extract Function （同上）
  - Separate Query from Modifier （避免调用者调用了有副作用的代码）
  - Remove Setting Method （避免修改）
  - Replace Derived Variable with Query （避免临时变量，自然也无从修改）
  - Combine Functions into Class （缩写修改范围）
  - Combine Functions into Transform （将修改的逻辑集中在一起）
  - Change Reference to Value （避免修改）

#### Divergent Change

- Refactoring Skills
  - Split Phase （将复杂的处理逻辑分阶段处理，使逻辑更清晰、日后修改更容易）
  - Move Function （将函数封装在模块内部，便于梳理处理逻辑，为拆分阶段做准备）
  - Extract Function （为搬移函数做准备）
  - Extract Class （为模块封装做准备）

> 伍注：解决发散式修改的问题的方法是：对需要修改数据的代码进行封装，缩小修改范围。

#### Shotgun Surgery

- Refactoring Skills
  - Move Function
  - Move Field
  - Combine Functions into Class
  - Combine Functions into Transform
  - Inline Function
  - Inline Class

> 伍注：Shotgun Surgery 和 Divergent Change 相反，
> 前者的问题是需要修改多个模块或类，解决方法是将多个模块合并；
> 后者的问题是同一个模块常常因不同原因被修改，解决方法是拆分成多个模块。

#### Feature Envy

- When we modularize a program, we are trying to separate the code into zones to maximize the interaction inside a zone and minimize interaction between zones.

- Refactoring Skills
  - Move Function
  - Extract Function (根据需要/不需要移到其他模块来拆分函数，为搬移函数做准备)

- The fundamental rule of thumb is to **put things together that change together**.

#### Data Clumps

- When to turn data clumps into one object
  - A good test is to consider deleting one of the data values.
  - If you did this, would the others make any sense?
  - If they don’t, it’s a sure sign that you have an object that’s dying to be born.

- Refactoring Skills
  - Extract Class
  - Introduce Parameter Object
  - Presere Whole Object

#### Primitive Obsession

- Create your own fundamental types which are useful for your domain if necessary。

- Refactoring Skills
  - Replace Primitive with Object
  - Replace Type Code With Subclasses
  - Replace Conditional with Polymorphism

#### Repeated Switches

- The problem with such duplicate switches
  - whenever you add a clause, you have to find all the switches and update them.

> 伍注：使用多态来代替重复的switch语句的好处是：将要修改的地方集中在一起，避免遗漏修改。

- Refactoring Skills
  - Replace Conditional with Polymorphism

#### Loops

- Refactoring Skills
  - Replace Loop with Pipeline

#### Lazy Element

#### Speculative Generality

#### Temporary Field

#### Message Chains

#### Middle Man

#### Insider Trading

#### Large Class

#### Alternative Classes with Different Interfaces

#### Data Class

### Q7：作者是怎么论述的？

### Q8：作者解决了什么问题？

### Q9：我有哪些疑问？

#### Q9.1: 如何理解Combine Functions into Transform这个重构技巧？

### Q10：这一章说得有道理吗？为什么？

### Q11: 这一章讨论的知识的本质是什么？

### Q12: 这一章讨论的知识的第一原则是什么？

### Q13：这一章讨论的知识的结构是怎样的？

### Q14：这一章讨论的知识为什么是这样的？为什么发展成这样？为什么需要它？

### Q15：有哪些相似的知识？它们之间的联系是什么？

### Q16：其他领域/学科有没有相关的知识？日常生活中有没有类似的现象？

### Q17: 这一章对我有哪些用处/帮助/启示？

### Q18: 我如何应用这一章的知识去解决问题？

