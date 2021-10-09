# 《Code Complete》分析笔记

## Chapter 5: Design in Construction

### Q1：这一章的内容是什么？

### Q2：这一章的大纲是什么？

- Design Challenges
- Key Design Concepts
- Design Building Blocks: Heuristics
- Design Practices
- Comments on Popular Methodologies

### Q3：作者想要解决什么问题？

### Q4：这一章的关键词是什么？

- Heuristics 启发式方法
- Popular Methodologies
- Rule of thumb 
  - An approximate method for doing something, based on practical experience rather than theory.

### Q5：这一章的关键句是什么？

#### 5.1 Design Challenges

- What is Software Design
  - The phrase "software design" means the conception, invention, or contrivance of a scheme for turning a specification for computer software into operational software.
  - Design is the activity that links requirements to coding and debugging.

- What is Good Design
  - A good top-level design provides a structure that can safely contain multiple lower-level designs.

- Design Is a Wicked Problem
  - Horst Rittel and Melvin Webber defined a "wicked" problem as one that could be clearly defined only by solving it, or by solving part of it.
  - This paradox implies, essentially, that you have to "solve" the problem once in order to clearly define it and then solve it again to create a solution that works. 

- Design Is a Sloppy Process (Even If it Produces a Tidy Result)
  - You take many false steps and go down many blind alleys— you make a lot of mistakes.
  - A good solution is often only subtly different from a poor one.
  - It's hard to know when your design is "good enough."

- Design Is About Tradeoffs and Priorities
  - A key part of the designer's job is to weigh competing design characteristics and strike a balance among those characteristics.

- Design Involves Restrictions
  - The point of design is partly to create possibilities and partly to restrict possibilities.

- Design Is Nondeterministic

- Design Is a Heuristic Process
  - Because design is nondeterministic, design techniques tend to be heuristics rather than repeatable processes that are guaranteed to produce predictable results.
  - Design involves trial and error.
  - No design tool is right for everything.

- Design Is Emergent
  - Designs evolve and improve through design reviews, informal discussions, experience writing the code itself, and experience revising the code.
  - Virtually all systems undergo some degree of design changes during their initial development,
    and then they typically change to a greater extent as they're extended into later versions. 

#### 5.2 Key Design Concepts

- Good design depends on understanding a handful of key concepts.
  - The role of complexity
  - Desirable characteristics of designs
  - Levels of design

##### 5.2.1 Software's Primary Technical Imperative: Managing Complexity

- Essential Properties vs Accidental Properties
  - The essential properties are the properties that a thing must have in order to be that thing.
  - The accidental properties are the properties a thing just happens to have, properties that don't really bear on whether the thing is what it is.

- Brooks argues that software development is made difficult because of two different classes of problems
  - The essential difficulties
  - The accidental difficulties

- The Accidental Difficulties
  - Accidental difficulties related to clumsy language syntaxes were largely eliminated in the evolution from assembly language to third-generation languages and have declined in significance incrementally since then.
  - Accidental difficulties related to noninteractive computers were resolved when time-share operating systems replaced batch-mode systems.
  - Integrated programming environments further eliminated inefficiencies in programming work arising from tools that worked poorly together.

- The Essential Difficulties
  - Progress on software’s remaining essential difficulties is bound to be slower.
  - The reason is that, at its essence, software development consists of working out all the details of a highly intricate, interlocking set of concepts.
  - The essential difficulties arise from the necessity of 
    - interfacing with the complex, disorderly real world;
    - accurately and completely identifying the dependencies and exception cases;
    - designing solutions that can’t be just approximately correct but that must be exactly correct;
    - and so on.

- Importance of Managing Complexity
  - Managing complexity is the most important technical topic in software development.
  - In my view, it’s so important that Software’s Primary Technical Imperative has to be managing complexity.

- Software Complexity vs Human Limitations
  - No one's skull is really big enough to contain a modern computer program.
  - We should try to organize our programs in such a way that we can safely focus on one part of it at a time.
  - The goal is to **minimize the amount of a program you have to think about at any one time.**

- How to Reduce Complexity
  - Divide and Conquer
    - At the software-architecture level, the complexity of a problem is reduced by dividing the system into subsystems. 
    - The goal of all software-design techniques is to **break a complicated problem into simple pieces.**
  - Reduce you mental workload
    - Keeping routines short 
    - Writing programs in terms of the problem domain, rather than in terms of low-level implementation details
    - working at the highest level of abstraction
  - Readability
    - The bottom line is that programmers who compensate for inherent human limitations
      write code that’s easier for themselves and others to understand and that has fewer errors.

- A two-prong(双管齐下) approach to managing complexity
  - **Minimize the amount of essential complexity that anyone’s brain has to deal with at any one time.**
  - **Keep accidental complexity from needlessly proliferating.**

##### 5.2.2 Desirable Characteristics of a Design

- A high-quality design has several general characteristics.
  - Minimal complexity
    - Make "simple" and "easy-to-understand" designs.
    - If your design doesn't let you safely ignore most other parts of the program when you're immersed in one specific part, the design isn’t doing its job.
  - Ease of maintenance
    - Think of the maintenance programmer as your audience, and then design the system to be self-explanatory.
  - Loose coupling
    - Hold connections among different parts of a program to a minimum.
  - Extensibility
    - You can change a piece of a system without affecting other pieces.
  - Reusability
  - High fan-in
    - High fan-in implies that a system has been designed to make good use of utility classes at the lower levels in the system.
  - Low-to-medium fan-out
    - High fan-out (more than about seven) indicates that a class uses a large number of other classes and may therefore be overly complex. 
  - Portability
  - Leanness (精简)
    - Designing the system so that it has no extra parts.
  - Stratification (分层)
    - keep the levels of decomposition stratified so that you can view the system at any single level and get a consistent view.
  - Standard techniques
    - Try to give the whole system a familiar feeling by using standardized, common approaches.

- Some goals contradict other goals, but that’s the challenge of design—creating a good set of tradeoffs from competing objectives.

##### 5.2.3 Levels of Design

- Design is needed at several different levels of detail in a software system.
  - Level 1: Software system
  - Level 2: Division into subsystems/packages
    - Of particular importance at this level are the rules about how the various subsystems can **communicate**.
  - Level 3: Division into classes within packages
  - Level 4: Division into data and routines within classes
  - Level 5: Internal routine design

- Some design techniques apply at all levels, and some apply at only one or two.

- Common Subsystem
  - Business rules
  - User interface
  - Database access
  - System dependencies

#### 5.3 Design Building Blocks: Heuristics

##### 5.3.1 Find Real-World Objects

- The steps in designing with objects are
  - Identify the objects and their attributes (methods and data).
  - Determine what can be done to each object.
  - Determine what each object is allowed to do to other objects.
  - Determine the parts of each object that will be visible to other objects—which
  - parts will be public and which will be private.
  - Define each object's public interface.

##### 5.3.2 Form Consistent Abstractions

- Abstraction is the ability to engage with a concept while safely ignoring some of its details—
  handling different details at different levels. 

- A good class interface is an abstraction that allows you to focus on the interface 
  without needing to worry about the internal workings of the class.

- From a complexity point of view, the principal benefit of abstraction is that it allows you to ignore irrelevant details.

##### 5.3.3 Encapsulate Implementation Details

- Abstractions vs Encapsulate
  - Abstraction says, "You're allowed to look at an object at a high level of detail."
  - Encapsulation says, "Furthermore, you aren't allowed to look at an object at any other level of detail."

##### 5.3.4 Inherit — When Inheritance Simplifies the Design

- Inheritance can provide great benefits when used well, and it can do great damage when used naively.

##### 5.3.5 Hide Secrets (Information Hiding)

- Information hiding is part of the foundation of both structured design and object-oriented design.
  - In structured design, the notion of “black boxes” comes from information hiding.
  - In object-oriented design, it gives rise to the concepts of encapsulation and modularity and it is associated with the concept of abstraction. 

- Value of Information Hiding
  - Thinking about information hiding inspires and promotes design decisions that thinking about objects does not.
  - Get into the habit of asking "What should I hide?" You'll be surprised at how many difficult design issues dissolve before your eyes.

- Secrets and the Right to Privacy
  - The class's job is to keep this information hidden and to protect its own right to privacy.
  - The interface to a class should reveal as little as possible about its inner workings.
  - Two Categories of Secrets:
    - Hiding complexity so that your brain doesn't have to deal with it unless you're specifically concerned with it
    - Hiding sources of change so that when change occurs, the effects are localized

- Barriers to Information Hiding
  - Excessive distribution of information
  - Circular dependencies
  - Class data mistaken for global data
  - Perceived performance penalties

##### 5.3.6 Identify Areas Likely to Change

- Design vs Changes
  - One common attributes of great designers was their ability to anticipate change.
  - Accommodating changes is one of the most challenging aspects of good program design.
  - The goal is to isolate unstable areas so that the effect of a change will be limited to one routine, class, or package.

- Steps for Accommodating changes 
  - Identify items that seem likely to change.
  - Separate items that are likely to change.
  - Isolate items that seem likely to change.
    - Design the interclass interfaces to be insensitive to the potential changes.
    - Design the interfaces so that changes are limited to the inside of the class and the outside remains unaffected.

- Areas that are likely to change
  - Business rules
  - Hardware dependencies
    - Isolate hardware dependencies in their own subsystem or class.
  - Input and Output
    - The application data file format will probably change as your application becomes more sophisticated.
    - User-level input and output formats will also change.
  - Nonstandard language features
    - Hide nonstandard extensions in a class of their own so that you can replace them with your own code when you move to a different environment.
    - If you use library routines that aren't available in all environments,
      hide the actual library routines behind an interface that works just as well in another environment.
  - Difficult design and construction areas
  - Status variables
    - Don't use a boolean variable as a status variable.
    - Use access routines rather than checking the variable directly.
  - Data-size constraints

- When you're developing a program for volatile hardware,
  - You can write software that simulates interaction with specific hardware,
  - have the hardware-interface subsystem use the simulator as long as the hardware is unstable or unavailable, and
  - then unplug the hardware-interface subsystem from the simulator and plug the subsystem into the hardware when it's ready to use.

##### 5.3.7 Anticipating Different Degrees of Change

- When thinking about potential changes to a system,
  design the system so that the effect or scope of the change is proportional to the chance that the change will occur.

- A good technique for identifying areas likely to change is
  - First to identify the minimal subset of the program that might be of use to the user.
    The subset makes up the core of the system and is unlikely to change.
  - Next, define minimal increments to the system. They can be so small that they seem trivial. 

##### 5.3.8 Keep Coupling Loose

- Loose Coupling
  - The goal is to create classes and routines with small, direct, visible, and flexible relations to other classes and routines.
  - In software, make the connections among modules as simple as possible.
  - Try to create modules that depend little on other modules. 

### Q6：作者是怎么论述的？

### Q7：作者解决了什么问题？

### Q8：我有哪些疑问？

#### Q8.1: What are the design challenges?

根据第5.1节的内容，软件设计的挑战来自于其本身的特点——
软件设计充满不确定性，需要满足各种约束条件，需要平衡各方面资源，需要不断试错、不断改进。

#### Q8.2: What are the key design concepts?

根据第5.2节的内容，软件设计的关键概念包括：

- 管理复杂性
- 好设计的特点
- 设计的层次

#### Q8.3: What is the design heuristics?

#### Q8.4: What is the best design practices?

#### Q8.5: What are the popular methodologies?

#### Q8.6: What are the differences between Encapsulation and Information Hiding?

根据我目前的理解，封装一般是面向对象中的概念，信息隐藏的适用范围更广泛。

### Q9：这一章说得有道理吗？为什么？

### Q10：如何拓展这一章？

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它？

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么？

- 常见设计原则
  - 「左耳听风」提到的设计原则
- 相关书籍
  - 设计模式
  - 敏捷软件开发

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象？

### Q11：这一章和我有什么关系？

