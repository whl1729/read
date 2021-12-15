# 《Refactoring: Improve the Design of Existing Code》分析笔记

## Chapter 3: Bad Smells in Code

### Q1：这一章的内容属于哪一类别？

### Q2：这一章的内容是什么？

### Q3：这一章的大纲是什么？

- Mysterious Name （神秘命名）
- Duplicated Code （重复代码）
- Long Function （过长函数）
- Long Parameter List （过长参数列表）
- Global Data （全局数据）
- Mutable Data （可变数据）
- Divergent Change （发散式变化）
- Shotgun Surgery （霰弹式修改）
- Feature Envy （依恋情结）
- Data Clumps （数据泥团）
- Primitive Obsession （基本类型偏执）
- Repeated Switches （重复的switch）
- Loops （循环语句）
- Lazy Element （冗余的元素）
- Speculative Generality （夸夸其谈通用性）
- Temporary Field （临时字段）
- Message Chains （过长的消息链）
- Middle Man （中间人）
- Insider Trading （黑幕交易）
- Large Class （过大的类）
- Alternative Classes with Different Interfaces （异曲同工的类）
- Data Class （纯数据类）
- Refused Bequest （被拒绝的遗赠）
- Comments （注释）

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

- Definition
  - Sometimes the structure isn't needed.

> 伍注：有时会出现定义了一个不必要的函数或类，这时应该去除它。

- Refactoring Skills
  - Inline Function
  - Inline Class
  - Collapse Hierarchy

#### Speculative Generality

- Definition
  - You get it when people say,
    "Oh, I think we'll need the ability to do this kind of thing someday"
    and thus add all sorts of hooks and special cases to handle things that aren’t required.

- Refactoring Skills
  - Collapse Hierarchy
  - Inline Function
  - Inline Class
  - Change Function Declaration
  - Remove Dead Code

#### Temporary Field

- Definition
  - Sometimes you see a class in which a field is set only in certain circumstances.

- Refactoring Skills
  - Extract Class
  - Move Function
  - Introduce Special Case

#### Message Chains

> 伍注：过长的消息链会导致耦合度高，进而导致难以修改。

- Refactoring Skills
  - Hide Delegate
  - Extract Function
  - Move Function

#### Middle Man

- Refactoring Skills
  - Remove Middle Man
  - Inline Function
  - Replace Superclass with Delegate
  - Replace Subclass with Delegate

#### Insider Trading

- Refactoring Skills
  - Move Function
  - Move Field
  - Hide Delegate
  - Replace Subclass with Delegate
  - Replace Superclass with Delegate

#### Large Class

- Bad Smells
  - Large class often has too many fields, which means duplicated code cannot be far behind.
  - A class with too much code is a prime breeding ground for duplicated code, chaos, and death.

- Refactoring Skills
  - Extract Class
  - Extract Superclass
  - Replace Type Code with Subclass

#### Alternative Classes with Different Interfaces

- Refactoring Skills
  - Change Function Declaration
  - Move Function
  - Extract Superclass

#### Data Class

- Bad Smells
  - Such classes are dumb data holders and are often being manipulated in far too much detail by other classes.
  - You can make big progress by moving it from the client into the data class itself.

> 伍注：如果一个类只提供getter/setter方法，可能意味着它的封装性不够好。

- Refactoring Skills
  - Encapsulate Record
  - Remove Setting Method
  - Move Function
  - Extract Function

#### Refused Bequest

- Bad Smells
  - The subclass is reusing behavior but does not want to support the interface of the superclass

- Refactoring Skills
  - Push Down Method
  - Push Down Field
  - Replace Subclass with Delegate
  - Replace Superclass with Delegate

#### Comments

- Bad Smells
  - Comments are often used as a deodorant.
  - Usually comments are there because the code is bad.

- Refactoring Skills
  - Extract Function
  - Change Function Declaration
  - Introduce Assertion

- When you feel the need to write a comment,
  first try to refactor the code so that any comment becomes superfluous.

- When to comment
  - A good time to use a comment is when you don't know what to do.
  - In addition to describing what is going on, comments can indicate areas in which you aren't sure.
  - A comment can also explain why you did something.
  - This kind of information helps future modifiers, especially forgetful ones.

### Q7：作者是怎么论述的？

### Q8：作者解决了什么问题？

### Q9：我有哪些疑问？

#### Q9.1: 如何理解Combine Functions into Transform这个重构技巧？

#### Q9.2: 如何理解Replace Superclass with Delegate 和 Replace Subclass with Delegate 这两个技巧？

#### Q9.3: 如何理解Alternative Classes with Different Interfaces这个技巧？

### Q10：这一章说得有道理吗？为什么？

### Q11: 这一章讨论的知识的本质是什么？

### Q12: 这一章讨论的知识的第一原则是什么？

### Q13：这一章讨论的知识的结构是怎样的？

### Q14：这一章讨论的知识为什么是这样的？为什么发展成这样？为什么需要它？

### Q15：有哪些相似的知识？它们之间的联系是什么？

### Q16：其他领域/学科有没有相关的知识？日常生活中有没有类似的现象？

### Q17: 这一章对我有哪些用处/帮助/启示？

### Q18: 我如何应用这一章的知识去解决问题？

