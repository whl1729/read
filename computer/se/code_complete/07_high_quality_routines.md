# 《Code Complete》分析笔记

## Chapter 7: High-Quality Routines

### Q1：这一章的内容是什么？

### Q2：这一章的大纲是什么？

- Valid Reasons to Create a Routine
- Design at the Routine Level
- Good Routine Names
- How Long Can a Routine Be?
- How to Use Routine Paramters
- Special Considerations in the Use of Functions
- Macro Routines and Inline Routines

### Q3：作者想要解决什么问题？

### Q4：这一章的关键词是什么？

- Cohesion
  - Sequential Cohesion
  - Communicational Cohesion
  - Temporal Cohesion
  - Procedural Cohesion
  - Logical Cohesion
  - Coincidental Cohesion

### Q5：这一章的关键句是什么？

#### 7.1 Valid Reasons to Create a Routine

- Valid Reasons to Create a Routine
  - Reduce complexity
    - Create a routine to hide information so that you won't need to think about it.
  - Introduce an intermediate, understandable abstraction
    - The routine name makes the code more readable and easier to understand.
  - Avoid duplicate code
  - Support subclassing
  - Hide sequences
    - It's a good idea to hide the order in which events happen to be processed.
  - Hide pointer operations
  - Improve portability
    - Use of routines isolates nonportable capabilities, explicitly identifying and isolating future portability work.
  - Simplify complicated boolean tests
    - It can reduce complexity and increase readability.
  - Improve performance
    - Having code in one place will make it easier to profile to find inefficiencies, refactor or recode.

- In addition, many of the reasons to create a class are also good reasons to create a routine:
  - Isolate complexity
  - Hide implementation details
  - Limit effects of changes
  - Hide global data
  - Make central points of control
  - Facilitate reusable code
  - Accomplish a specific refactoring

- Operations That Seem Too Simple to Put Into Routines
  - Constructing a whole routine to contain two or three lines of code might seem like overkill,
    but experience shows how helpful a good small routine can be.

> 伍注：不要因为代码行数少而放弃封装成函数。

#### 7.2 Design at the Routine Level

- For routines, cohesion refers to how closely the operations in a routine are related.

- The best Cohesion
  - Functional cohesion is the strongest and best kind of cohesion, occurring when a routine performs one and only one operation.

- Notideal Cohesion
  - Sequential cohesion
    - A routine contains operations that must be performed in a specific order, that share data from step to step,
      and that don't make up a complete function when done together.
  - Communicational cohesion
    - Operations in a routine make use of the same data and aren't related in any other way.
  - Temporal cohesion
    - Operations are combined into a routine because they are all done at the same time.

- Unacceptable Cohesion
  - Procedural cohesion
    - Operations in a routine are done in a specified order. 
  - Logical cohesion
    - Several operations are stuffed into the same routine and one of the operations is selected by a control flag that's passed in.
  - Coincidental cohesion
    - operations in a routine have no discernible relationship to each other.

#### 7.3 Good Routine Names

#### 7.4 How Long Can a Routine Be?

#### 7.5 How to Use Routine Paramters

#### 7.6 Special Considerations in the Use of Functions

#### 7.7 Macro Routines and Inline Routines


### Q6：作者是怎么论述的？

### Q7：作者解决了什么问题？

### Q8：我有哪些疑问？

#### Q8.1 Why are sequential cohesion, communicational cohesion and temporal cohesion less than ideal?

#### Q8.2 Why are procedural cohesion, logical cohesion and coincidental cohesion unacceptable?

### Q9：这一章说得有道理吗？为什么？

### Q10：如何拓展这一章？

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它？

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么？

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象？

### Q11：这一章和我有什么关系？

