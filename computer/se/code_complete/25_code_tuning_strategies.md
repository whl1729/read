# 《Code Complete》分析笔记

## Chapter 25: Code-Tuning Strategies

### Q1：这一章的内容是什么

### Q2：这一章的大纲是什么

- Performance Overview
  - Quality Characteristic and Performance
  - Performance and Code Tuning
- Introduction to Code Tuning
  - The Pareto Principle
  - Old Wives' Tales
  - When to tune
- Kinds of Fat and Molasses
  - Common Sources of Inefficiency
  - Relative Performance Costs of Common Operations
- Measurement
  - Measurements Need to Be Precise
- Iteration
- Summary of the Approach to Code Tuning
- Checklist: Code-Tuning Strategies

### Q3：作者想要解决什么问题

### Q4：这一章的关键词是什么

- molasses: 糖蜜，糖浆
- tuning
  - Refers to small-scale changes that affect a single class, a single routine, or, more commonly, a few lines of code.
  - Not refer to large-scale design changes or other higher-level means of improving performance.
- The Pareto Principle (80/20 rule)
  - You can get 80 percent of the result with 20 percent of the effort.
- Old wives' tale
  - A supposed truth which is actually spurious or a superstition.

### Q5：这一章的关键句是什么

#### 25.1 Performance Overview

- Quality Characteristic and Performance
  - Users are more interested in tangible program characteristics than they are in code quality.
  - Users tend to be more interested in program throughput than raw performance.
    Delivering software on time, providing a clean user interface, and avoiding downtime are often more significant.
  - Be wary of sacrificing other characteristics to make your code faster.
    Your work on speed might hurt overall performance rather than help it.

- Performance and Code Tuning
  - Program requirements
    - Before you invest time solving a performance problem,
      make sure that you're solving a problem that needs to be solved.
  - Program design
    - Design a performance-oriented architecture,
      and then set resource goals for individual subsystems, features, and classes.
  - Class and routine design
    - Choice of data types and algorithms
  - Operating-system interactions
    - If performance isn't good, it might be because the operating-system routines are slow or fat.
  - Code compilation
    - Compiler optimizations that produce more efficient code than manual code tuning does.
  - Hardware
    - Buy new hardware
  - Code tuning

#### 25.2 Introduction to Code Tuning

- The Pareto Principle
  - Barry Boehm reports that 20 percent of a program's routines consume 80 percent of its execution time.

- Old Wives' Tales
  - Reducing the lines of code in a high-level language improves the speed or size of the resulting machine code — false!
  - Certain operations are probably faster or smaller than others — false!
  - You should optimize as you go — false!
  - A fast program is just as important as a correct one — false!

- When to tune
  - Use a high-quality design.
    Make the program right.
    Make it modular and easily modifiable so that it's easy to work on later.
    When it's complete and correct, check the performance.
    If the program lumbers, make it fast and small.
  - Don't optimize until you know you need to.

#### 25.3 Kinds of Fat and Molasses

- Relative Performance Costs of Common Operations
  - Input/output operations
    - One of the most significant sources of inefficiency is unnecessary input/output (I/O)
  - Paging
    - An operation that causes the operating system to swap pages of memory is much slower than
      an operation that works on only one page of memory.
  - System calls
    - Calls to system routines are often expensive.
  - Interpreted languages
  - Errors
    - Leaving debugging code turned on (such as logging trace information to a file)
    - Forgetting to deallocate memory
    - Improperly designing database tables
    - Polling nonexistent devices until they time out

#### 25.4 Measurement

- The only result of optimization you can usually be sure of without measuring performance is that
  you've made your code harder to read.

- Measurements Need to Be Precise
  - Make sure that you're measuring only the execution time of the code you're tuning

#### 25.6 Summary of the Approach to Code Tuning

1. Develop the software by using well-designed code that's easy to understand and modify.

2. If performance is poor,
  - a. Save a working version of the code so that you can get back to the "last known good state".
  - b. Measure the system to find hot spots.
  - c. Determine whether the weak performance comes from inadequate design, data types, or algorithms and whether code tuning is appropriate.
       If code tuning isn't appropriate, go back to step 1.
  - d. Tune the bottleneck identified in step (c).
  - e. Measure each improvement one at a time.
  - f. If an improvement doesn't improve the code, revert to the code saved in step (a).

3. Repeat from step 2.

#### 25.7 Checklist: Code-Tuning Strategies

- Overall Program Performance
  - [ ] Have you considered improving performance by changing the program requirements?
  - [ ] Have you considered improving performance by modifying the program's design?
  - [ ] Have you considered improving performance by modifying the class design?
  - [ ] Have you considered improving performance by avoiding operating system interactions?
  - [ ] Have you considered improving performance by avoiding I/O?
  - [ ] Have you considered improving performance by using a compiled language instead of an interpreted language?
  - [ ] Have you considered improving performance by using compiler optimizations?
  - [ ] Have you considered improving performance by switching to different hardware?
  - [ ] Have you considered code tuning only as a last resort?

- Code-Tuning Approach
  - [ ] Is your program fully correct before you begin code tuning?
  - [ ] Have you measured performance bottlenecks before beginning code tuning?
  - [ ] Have you measured the effect of each code-tuning change?
  - [ ] Have you backed out the code-tuning changes that didn't produce the intended improvement?
  - [ ] Have you tried more than one change to improve performance of each bottleneck—that is, iterated?

### Q6：作者是怎么论述的

### Q7：作者解决了什么问题

### Q8：我有哪些疑问

### Q9：这一章说得有道理吗？为什么

### Q10：如何拓展这一章

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象

### Q11：这一章和我有什么关系
