# 《Code Complete》分析笔记

## Chapter 10: General Issues in Using Variables

### Q1：这一章的内容是什么？

### Q2：这一章的大纲是什么？

- Data Literacy
- Making Variable Declarations Easy
- Guidelines for Initializing Variables
- Scope
- Persistence
- Binding Time
- Relationship Between Data Types and Control Structures
- Using Each Variable for Exactly One Purpose

### Q3：作者想要解决什么问题？

### Q4：这一章的关键词是什么？

- Persistence

### Q5：这一章的关键句是什么？

#### 10.2 Making Variable Declarations Easy

- Suggestions for variable declarations
  - Turn off implicit declarations
  - Declare all variables
  - Use naming conventions
  - Check variable names

#### 10.3 Guidelines for Initializing Variables

- Guidelines for Initializing Variables
  - Initialize each variable as it's declared
  - Initialize each variable close to where it's first used
  - Ideally, declare and define each variable close to where it's first used
  - Use final or const when possible
  - Pay special attention to counters and accumulators
    - A common error is forgetting to reset a counter or an accumulator before the next time it's used.
  - Initialize a class's member data in its constructor
  - Check the need for reinitialization
  - Initialize named constants once; initialize variables with executable code
    - Initialize them in a Startup() routine
  - Use the compiler setting that automatically initializes all variable
  - Take advantage of your compiler's warning messages
  - Check input parameters for validity
  - Use a memory-access checker to check for bad pointers
  - Initialize working memory at the beginning of your program

#### 10.4 Scope

- Guidelines for scope
  - Localize References to Variables
  - Keep Variables "Live" for as Short a Time as Possible

- General Guidelines for Minimizing Scope
  - Initialize variables used in a loop immediately before the loop
    rather than back at the beginning of the routine containing the loop
  - Don't assign a value to a variable until just before the value is used
  - Break groups of related statements into separate routines
  - Begin with most restricted visibility, and expand the variable's scope only if necessary

- Global scope vs local scope

  | &nbsp; | global scope | local scope |
  | ------ | ------------ | ----------- |
  | convenience |  good   |   not good  |
  | intellectual manageability | bad | good |
  | readability |  bad    |  good |

#### 10.5 Persistence

- Some variables persist
  - for the life of a particular block of code or routine.
    Variables declared inside a for loop in C++ or Java are examples of this kind of persistence.
  - as long as you allow them to.
    In C++, variables created with new persist until you delete them.
  - for the life of a program.
    Global variables in most languages fit this description, as do static variables in C++ and Java.
  - forever.
    These variables might include values that you store in a database between executions of a program.

- Suggestions for persistence
  - Use debug code or assertions in your program to check critical variables for reasonable values.
    If the values aren't reasonable, display a warning that tells you to look for improper initialization.
  - Set variables to "unreasonable values" when you're through with them.
    For example, you could set a pointer to null after you delete it.
  - Write code that assumes data isn't persistent.
    For example, if a variable has a certain value when you exit a routine, don't assume it has the same value the next time you enter the routine.
  - Develop the habit of declaring and initializing all data right before it's used.
    If you see data that's used without a nearby initialization, be suspicious!

#### 10.6 Binding Time

- Possible time that a variable can be bound to a value
  - Coding time (use of magic numbers)
  - Compile time (use of a named constant)
  - Load time (reading a value from an external source such as the Windows registry file or a Java properties file)
  - Object instantiation time (such as reading the value each time a window is created)
  - Just in time (such as reading the value each time the window is drawn)

- Keep a balance between flexibility and complexity
  - The earlier the binding time, the lower the flexibility and the lower the complexity.
  - The greater the flexibility desired, the higher the complexity of the code needed to support that flexibility and the more error-prone the code will be.
  - Because successful programming depends on minimizing complexity,
    a skilled programmer will build in as much flexibility as needed to meet the software's requirements
    but will not add flexibility—and related complexity—beyond what's required.

#### 10.7 Relationship Between Data Types and Control Structures

- Three types of data and corresponding control structures
  - Sequential data translates to sequential statements in a program
  - Selective data translates to if and case statements in a program
  - Iterative data translates to for, repeat, and while looping structures in a program

> Wu: I don't know why should we care about the relationship between data types and control structures?

#### 10.8 Using Each Variable for Exactly One Purpose

- Use each variable for one purpose only.
  - Using the same variable in both instances makes it seem as though they’re related when they’re not.
  - Creating unique variables for each purpose makes your code more readable.

- Avoid variables with hidden meanings.
  - Avoid “hybrid coupling”

- Make sure that all declared variables are used.

#### 10.9 Checklist: General Considerations In Using Data

- Initializing Variables
  - [ ] Does each routine check input parameters for validity?
  - [ ] Does the code declare variables close to where they’re first used?
  - [ ] Does the code initialize variables as they’re declared, if possible?
  - [ ] Does the code initialize variables close to where they’re first used,
        if it isn’t possible to declare and initialize them at the same time?
  - [ ] Are counters and accumulators initialized properly and, if necessary, reinitialized each time they are used?
  - [ ] Are variables reinitialized properly in code that’s executed repeatedly?
  - [ ] Does the code compile with no warnings from the compiler? (And have you turned on all the available warnings?)
  - [ ] If your language uses implicit declarations, have you compensated for the problems they cause?
- Other General Issues in Using Data
  - [ ] Do all variables have the smallest scope possible?
  - [ ] Are references to variables as close together as possible,
        both from each reference to a variable to the next reference and in total live time?
  - [ ] Do control structures correspond to the data types?
  - [ ] Are all the declared variables being used?
  - [ ] Are all variables bound at appropriate times—that is,
        are you striking a conscious balance between the flexibility of late binding and the increased complexity associated with late binding?
  - [ ] Does each variable have one and only one purpose?
  - [ ] Is each variable’s meaning explicit, with no hidden meanings?

### Q6：作者是怎么论述的？

### Q7：作者解决了什么问题？

### Q8：我有哪些疑问？

### Q9：这一章说得有道理吗？为什么？

### Q10：如何拓展这一章？

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它？

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么？

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象？

### Q11：这一章和我有什么关系？
