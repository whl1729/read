# 《Refactoring: Improving the Design of Existing Code》分析笔记

## Chapter 2: Principles in Refactoring

### Q1：这一章的内容属于哪一类别？

计算机/软件工程。

### Q2：这一章的内容是什么？

介绍重构的基本原则。

### Q3：这一章的大纲是什么？

#### 一级大纲

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

#### 二级大纲

- Defining Refactoring
- The Two Hats
- Why Should We Refactor?
  - Refactoring Improves the Design of Software
  - Refactoring Makes Software Easier to Understand
  - Refactoring Helps Me Find Bugs
  - Refactoring Helps Me Program Faster
- When Should We Refactor?
  - The Rule of Three
  - Preparatory Refactoring: Making It Easier to Add a Feature
  - Comprehension Refactoring: Making Code Easier to Understand
  - Litter-Pickup Refactoring
  - Planned and Opportunistic Refactoring
  - Long-Term Refactoring
  - Refactoring in a Code Review
    - pair programming
  - What Do I Tell My Manager?
    - Don't tell!
  - When Should I Not Refactor?
- Problems with Refactoring
  - Slowing Down New Features
  - Code Ownership
  - Branches
  - Testing
  - Legacy Code
  - Databases
- Refactoring, Architecture, and YAGNI
- Refactoring and the Wider Software Development Process
- Refactoring and Performance
- Where did Refactoring Come From?
- Automated Refactorings
- Going Further

### Q4：作者想要解决什么问题？

### Q5：这一章的关键词是什么？

- The Two Hats: 将增加功能与重构活动分离
- YAGNI: You Aren't Gonna Need It
- Legacy Code
- Merging vs Integration
  - Mergeing: merge mainline into my code, this is a one-way movement—
    my branch changes but the mainline doesn't.
  - Integration: A two-way process that pulls changes from mainline into my branch and 
    then pushes the result back into mainline, changing both.
- CI: Continuous Integration
- Legacy Code: 历史代码
- Design Stamina Hypothesis: 努力维持良好的内部设计，可以让代码持久健康。

### Q6：这一章的关键句是什么？

#### Defining Refactoring

- The noun's definition
  - A change made to the internal structure of software
    to make it easier to understand and cheaper to modify
    without changing its observable behavior.

- The verb's definition
  - To restructure software by applying a series of refactorings
    without changing its observable behavior.

#### The Two Hats

- Adding Functionality vs Refactoring
  - When I use refactoring to develop software, I divide my time between two distinct activities:
    adding functionality and refactoring.
  - When I add functionality, I shouldn't be changing existing code; I'm just adding new capabilities.
    I measure my progress by adding tests and getting the tests to work.
  - When I refactor, I make a point of not adding functionality; I only restructure the code.
    I don’t add any tests (unless I find a case I missed earlier);
    I only change tests when I have to accommodate a change in an interface.

#### Why Should We Refactor?

- Refactoring Improves the Design of Software
  - Without refactoring, the internal design—the architecture—of software tends to decay.
  - As people change code to achieve short-term goals, often without a full comprehension of the architecture,
    the code loses its structure.
  - Cumulative Effect: 越难看出代码的设计，越难保留其设计，软件腐烂得越快。
  - An important aspect of improving design is to eliminate duplicated code.

  > The essence of good design:
  >     The code says everything once and only once.

- Refactoring Makes Software Easier to Understand
  - Programming is all about **saying exactly what I want**.
  - I make a point of trying to put everything I should remember into the code so I don't have to remember it.

- Refactoring Helps Me Find Bugs
  - Help in understanding the code also means help in spotting bugs.

  > Kent Beck:
  >     I'm not a great programmer; I'm just a good programmer with great habits.

- Refactoring Helps Me Program Faster
  - Software with a good internal design allows me to easily find how and where I need to make changes to add a new feature.
  - Good modularity allows me to only have to understand a small subset of the code base to make a change.
  - If the code is clear, I'm less likely to introduce a bug, and if I do, the debugging effort is much easier.

- Design Stamina Hypothesis
  - By putting our effort into a good internal design,
    we increase the stamina of the software effort, allowing us to go faster for longer.

#### When Should We Refactor?

- The Rule of Three
  - The first time you do something, you just do it.
  - The second time you do something similar, you wince at the duplication, but you do the duplicate thing anyway.
  - The third time you do something similar, you refactor.

- Time to refactor
  - When you add a new feature
  - When you fix a bug
  - When you gain some understanding in your head
  - When you realize the code is doing something badly

- Preparatory Refactoring
  - The best time to refactor is just before I need to add a new feature to the code base.

- Comprehension Refactoring
  - Whenever I have to think to understand what the code is doing,
    I ask myself if I can refactor the code to make that understanding more immediately apparent.
  - By refactoring I move the understanding from my head into the code itself.

- Litter-Pickup Refactoring
  - If I make it a little better each time I pass through the code, over time it will get fixed.

- You have to refactor when you run into ugly code—
  but excellent code needs plenty of refactoring too.

- The fastest way to add a new feature is to change the code to make it easy to add.

  > Kent Beck:
  >   For each desired change, make the change easy (warning: this may be hard), then make the easy change

- Long-Term Refactoring
  - A useful strategy is to agree to gradually work on the problem over the course of the next few weeks.

- Refactoring in a code review
  - Pair programming
  - The common pull request model, where a reviewer looks at code without the original author, doesn't work too well.
  - It's better to have the original author of the code present
    because the author can provide context on the code and fully appreciate the reviewers' intentions for their changes.

- When Should I Not Rerfactor?
  - If I run across code that is a mess, but I don't need to modify it, then I don't need to refactor it.
  - It's only when I need to understand how it works that refactoring gives me any benefit.
  - Another case is when it's easier to rewrite it than to refactor it.

#### Problems with Refactoring

- Slowing Down New Features
  - Although many people see time spent refactoring as slowing down the development of new features,
    the whole purpose of refactoring is to speed things up.
  - I do run into situations where I see a (large-scale) refactoring that really needs to be done,
    but the new feature I want to add is so small that I prefer to add it and leave the larger refactoring alone.

> 伍注：从长远的眼光来看，重构可以帮助我们提高开发效率。但也要注意「过犹不及」——过度重构也会降低开发新特性的效率。

- The Purpose of Refactoring
  - The whole purpose of refactoring is to make us program faster, producing more value with less effort.
  - We refactor because it makes us faster—faster to add features, faster to fix bugs.
  - The economic benefits of refactoring should always be the driving factor.

- Code Ownership
  - It's hard to change a published interface
  - Code ownership boundaries impose limitations:
     I cannot make the kinds of changes I want without breaking my clients.

- Branches
  - The cost that feature branches impose on refactoring is excessive.
  - You should keeping feature branches short and use CI.

- CI doesn't come for free:
  - It means you use practices to ensure the mainline is healthy,
  - learn to break large features into smaller chunks,
  - and use feature toggles (aka feature flags) to switch off any in-process features that can't be broken down.

- Testing
  - In most cases, if I want to refactor, I need to have self-testing code.
  - Another way to deal with the testing problem:
    - If I use an environment that has good automated refactorings,
      I can trust those refactorings even without running tests.

- Legacy Code
  - Follow the guideance from the book named Working Effectively with Legacy Code.
  - It advises you to get the system under test by finding seams in the program where you can insert tests.

- Databases
  - Pramod Sadalage developed an approach to evolutionary database design and database refactoring that is now widely used.
  - The essence of the technique is to combine the structural changes to a database's schema and
    access code with data migration scripts that can easily compose to handle large changes.

#### Refactoring, Architecture, and YAGNI

- Refactoring vs Architecture
  - Refactoring allows you to significantly alter the architecture of software that's been running in production for years.
  - Refactoring can improve the design of existing code.
  - Refactoring can be used to form a well-designed code base that can respond gracefully to changing needs.

- Refactoring vs YAGNI
  - I build software that solves only the currently understood needs,
    but I make this software excellently designed for those needs.
  - As my understanding of the users' needs changes, I use refactoring to adapt the architecture to those new demands.
  - Only if I can see that it would be substantially harder to refactor later
    do I consider adding a flexibility mechanism now.

#### Refactoring and the Wider Software Development Process

- Refactoring's early adoption was as part of Extreme Programming (XP)

- There is a strong synergy between the three practices of
  self-testing code, continuous integration, and refactoring.

#### Refactoring and Performance

- Fast and Slow
  - Refactoring can certainly make software go more slowly—but it also makes the software more amenable to performance tuning.

- The secret to fast software
  - To write tunable software first and then tune it for sufficient speed.

- 3 approaches to writing fast software
  - Time Budgeting 
    - Often used in hard real-time systems
    - As you decompose the design, you give each component a budget for resources—time and footprint.
  - Constant Attention Approach
    - Every programmer, all the time, does whatever she can to keep performance high.
  - Write tunable software first and then tune it

> 伍注：第二种方法是持续、每时每刻关注性能，第三种方法是先不关注性能，写出结构良好的代码后，再考虑性能。

- 90-percent statistic
  - In most programs, most of their time is spent in a small fraction of the code.
  - If I optimize all the code equally,
    I'll end up with 90 percent of my work wasted because it's optimizing code that isn't run much.

#### Where did Refactoring Come From?

- Ward Cunningham and Kent Beck
  - Two of the first people to recognize the importance of refactoring
  - They realized that refactoring was important in improving their productivity and
    have been applying it to serious software projects and refining it.
  - Their work developed into Extreme Programming.

- Ralph Johnson (One of the authors of the "Gang of Four" book)
  - Explored how refactoring can help develop an efficient and flexible framework.

- Bill Opdyke
  - Bill was interested in refactorings that would be useful for C++ framework development
  - He researched the necessary semantics-preserving refactorings and 
    showed how to prove they were semantics-preserving and
    how a tool could implement these ideas.
  - Bill's doctoral thesis was the first substantial work on refactoring.

- John Brant and Don Roberts
  - Took the refactoring tool ideas much further to produce the Refactoring Browser,
    the first refactoring tool, appropriately for the Smalltalk environment.

- Martin Fowler
  - Write this book

#### Automated Refactorings

- Text manipulation
  - Including
    - search/replace to change a name
    - simple reorganizing of code
  - This is a very crude approach that certainly can't be trusted without rerunning tests.

- Many refactorings are made much safer when applied in a language with static typing.

#### Going Further

- Books Recommended
  - Refactoring Workbook, Bill Wake
  - Refactoring to Patterns, Josh Kerievsky
  - Refactoring Databases, Scott Ambler and Pramod Sadalage
  - Refactoring HTML, Elliotte Rusty Harold
  - Working Effectively with Legacy Code, Michael Feathers

### Q7：作者是怎么论述的？

### Q8：作者解决了什么问题？

### Q9：我有哪些疑问？

### Q10：这一章说得有道理吗？为什么？

### Q11: 这一章讨论的知识的本质是什么？

### Q12: 这一章讨论的知识的第一原则是什么？

### Q13：这一章讨论的知识的结构是怎样的？

### Q14：这一章讨论的知识为什么是这样的？为什么发展成这样？为什么需要它？

### Q15：有哪些相似的知识？它们之间的联系是什么？

#### 相关网站

#### 相关书籍

见「Going Further」一节。

### Q16：其他领域/学科有没有相关的知识？日常生活中有没有类似的现象？

### Q17: 这一章对我有哪些用处/帮助/启示？

### Q18: 我如何应用这一章的知识去解决问题？

