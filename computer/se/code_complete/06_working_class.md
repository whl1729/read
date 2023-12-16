# 《Code Complete》分析笔记

## Chapter 6: Working Classes

### Q1：这一章的内容是什么

### Q2：这一章的大纲是什么

- Class Foundations: Abstract Data Types (ADTs)
- Good Class Interfaces
- Design and Implementation Issues
- Reasons to Create a Class
- Language-Specific Issues
- Beyond Classes: Packages
- Checklist: Class Quality

### Q3：作者想要解决什么问题

### Q4：这一章的关键词是什么

- ADT (Abstract Data Type)
- Law of Demeter
- mixin
- LSP (Liskov Substitution Principle)

### Q5：这一章的关键句是什么

- Class can reduce complexity
  - A key to being an effective programmer is maximizing the portion of a program that you can safely ignore while working on any one section of code.
  - Classes are the primary tool for accomplishing that objective.

#### 6.1 Class Foundations: Abstract Data Types (ADTs)

- Definition of ADT
  - An abstract data type is a collection of data and operations that work on that data.

- Benefits of Using ADTs
  - You can hide implementation details.
  - Changes don’t affect the whole program.
  - You can make the interface more informative.
  - It's easier to improve performance.
  - The program is more obviously correct.
  - The program becomes more self-documenting.
  - You don’t have to pass data all over your program.
  - You’re able to work with real-world entities rather than with low-level implementation structures.

- Guidelines of Using ADTs
  - Build or use typical low-level data types as ADTs, not as low-level data types.
    - If a stack represents a set of employees, treat the ADT as employees rather than as a stack.
  - Treat common objects such as files as ADTs.
  - Treat even simple items as ADTs.
    - You can define an ADT to model a light that supports only two operations—turning it on and turning it off.
  - Refer to an ADT independently of the medium it's stored on.
    - `RateTable.Read()` is better than `RateFile.Read()` because the latter exposes the storage medium.

- ADTs and Classes
  - One way of thinking of a class is as an abstract data type plus inheritance and polymorphism.

#### 6.2 Good Class Interfaces

- Good Abstraction
  - Present a consistent level of abstraction in the class interface.
    - Each class should implement one and only one ADT.
  - Be sure you understand what abstraction the class is implementing.
  - Provide services in pairs with their opposites.
  - Move unrelated information to another class.
  - Make interfaces programmatic rather than semantic when possible.
    - Each interface consists of a programmatic part and a semantic part.
    - The programmatic part consists of the data types and other attributes of the interface that can be enforced by the compiler.
    - The semantic part of the interface consists of the assumptions about how the interface will be used, which cannot be enforced by the compiler.
  - Beware of erosion of the interface’s abstraction under modification.
  - Don’t add public members that are inconsistent with the interface abstraction.
  - Consider abstraction and cohesion together.

- Good Encapsulation
  - Minimize accessibility of classes and members.
  - Don’t expose member data in public.
  - Avoid putting private implementation details into a class’s interface.
  - Don’t make assumptions about the class’s users.
  - Avoid friend classes.
  - Don’t put a routine into the public interface just because it uses only public routines.
  - Favor read-time convenience to write-time convenience.
    - Code is read far more times than it’s written, even during initial development.
  - Be very, very wary of semantic violations of encapsulation.
  - Watch for coupling that’s too tight.

#### 6.3 Design and Implementation Issues

- Containment ("has a" Relationships)
  - Implement "has a" through containment.
  - Implement "has a" through private inheritance as a last resort.
  - Be critical of classes that contain more than about seven data members.
    - If a class contains more than about seven data members,
      consider whether the class should be decomposed into multiple smaller classes.

- Inheritance ("is a" Relationships)
  - Implement “is a” through public inheritance
  - Design and document for inheritance or prohibit it
  - Adhere to the Liskov Substitution Principle (LSP)
  - Be sure to inherit only what you want to inherit
  - Don’t “override” a non-overridable member function
  - Move common interfaces, data, and behavior as high as possible in the inheritance tree
  - Be suspicious of classes of which there is only one instance
  - Be suspicious of base classes of which there is only one derived class
  - Be suspicious of classes that override a routine and do nothing inside the derived routine
  - Avoid deep inheritance trees
  - Prefer polymorphism to extensive type checking
  - Make all data private, not protected

- When you decide to use inheritance, you have to make several decisions:
  - For each member routine, will the routine be visible to derived classes?
    Will it have a default implementation? Will the default implementation be overridable?
  - For each data member (including variables, named constants, enumerations, and so on),
    will the data member be visible to derived classes?

- Multiple Inheritance
  - Multiple inheritance is useful primarily for defining "mixins".
  - For the sake of controlling complexity, you should maintain a heavy bias against inheritance.

- When to use inheritance and when to use containment
  - If multiple classes share common data but not behavior, create a common object that those classes can contain.
  - If multiple classes share common behavior but not data, derive them from a common base class that defines the common routines.
  - If multiple classes share common data and behavior, inherit from a common base class that defines the common data and routines.
  - Inherit when you want the base class to control your interface; contain when you want to control your interface.

- Member Functions and Data
  - Keep the number of routines in a class as small as possible.
  - Disallow implicitly generated member functions and operators you don’t want.
  - Minimize the number of different routines called by a class.
  - Minimize indirect routine calls to other classes.
  - In general, minimize the extent to which a class collaborates with other classes.
    - Number of kinds of objects instantiated
    - Number of different direct routine calls on instantiated objects
    - Number of routine calls on objects returned by other instantiated objects

- Constructors
  - Initialize all member data in all constructors, if possible.
  - Enforce the singleton property by using a private constructor.
  - Prefer deep copies to shallow copies until proven otherwise.

#### 6.4 Reasons to Create a Class

- Good reasons to create a class
  - Model real-world objects.
  - Model abstract objects.
  - Reduce complexity.
    - Create a class to hide information so that you won't need to think about it.
  - Isolate complexity.
  - Hide implementation details.
  - Limit effects of changes.
    - Isolate areas that are likely to change so that the effects of changes are limited to the scope of a single class or a few classes.
  - Hide global data.
  - Streamline parameter passing.
    - passing lots of data around suggests that a different class organization might work better.
  - Make central points of control.
    - Control each task in one place.
  - Facilitate reusable code.
  - Plan for a family of programs.
    - Think about what the whole family of programs might look like is a powerful heuristic for anticipating entire categories of changes.
  - Package related operations.
  - Accomplish a specific refactoring.

- Classes to Avoid
  - Avoid creating god classes.
  - Eliminate irrelevant classes.
    - If a class consists only of data but no behavior, ask yourself whether it’s really a class and
      consider demoting it so that its member data just becomes attributes of one or more other classes.
  - Avoid classes named after verbs.
    - A class that has only behavior but no data is generally not really a class.

#### 6.5 Language-Specific Issues

- Here are some of the class-related areas that vary significantly depending on the language:
  - Behavior of overridden constructors and destructors in an inheritance tree
  - Behavior of constructors and destructors under exception-handling conditions
  - Importance of default constructors (constructors with no arguments)
  - Time at which a destructor or finalizer is called
  - Wisdom of overriding the language’s built-in operators, including assignment and equality
  - How memory is handled as objects are created and destroyed or as they are declared and go out of scope

#### 6.6 Beyond Classes: Packages

- If you’re programming in a language that doesn’t support packages directly,
  you can create your own poor-programmer’s version of a package and enforce it through programming standards that include the following:
  - Naming conventions that differentiate which classes are public and which are for the package’s private use
  - Naming conventions, code-organization conventions (project structure),
    or both that identify which package each class belongs to
  - Rules that define which packages are allowed to use which other packages,
    including whether the usage can be inheritance, containment, or both

#### 6.7 Checklist: Class Quality

- Abstract Data Types
  - [ ] Have you thought of the classes in your program as abstract data types and evaluated their interfaces from that point of view?
- Abstraction
  - [ ] Does the class have a central purpose?
  - [ ] Is the class well named, and does its name describe its central purpose?
  - [ ] Does the class's interface present a consistent abstraction?
  - [ ] Does the class's interface make obvious how you should use the class?
  - [ ] Is the class's interface abstract enough that you don't have to think about how its services are implemented? Can you treat the class as a black box?
  - [ ] Are the class's services complete enough that other classes don't have to meddle with its internal data?
  - [ ] Has unrelated information been moved out of the class?
  - [ ] Have you thought about subdividing the class into component classes, and have you subdivided it as much as you can?
  - [ ] Are you preserving the integrity of the class's interface as you modify the class?
- Encapsulation
  - [ ] Does the class minimize accessibility to its members?
  - [ ] Does the class avoid exposing member data?
  - [ ] Does the class hide its implementation details from other classes as much as the programming language permits?
  - [ ] Does the class avoid making assumptions about its users, including its derived classes?
  - [ ] Is the class independent of other classes? Is it loosely coupled?
- Inheritance
  - [ ] Is inheritance used only to model "is a" relationships—that is, do derived classes adhere to the Liskov Substitution Principle?
  - [ ] Does the class documentation describe the inheritance strategy?
  - [ ] Do derived classes avoid "overriding" non-overridable routines?
  - [ ] Are common interfaces, data, and behavior as high as possible in the inheritance tree?
  - [ ] Are inheritance trees fairly shallow?
  - [ ] Are all data members in the base class private rather than protected?
- Other Implementation Issues
  - [ ] Does the class contain about seven data members or fewer?
  - [ ] Does the class minimize direct and indirect routine calls to other classes?
  - [ ] Does the class collaborate with other classes only to the extent absolutely necessary?
  - [ ] Is all member data initialized in the constructor?
  - [ ] Is the class designed to be used as deep copies rather than shallow copies unless there's a measured reason to create shallow copies?
- Language-Specific Issues
  - [ ] Have you investigated the language-specific issues for classes in your specific programming language?

#### 6.8 Additional Resources

- Glasses in General
  - Object-Oriented Software Construction
  - Object-Oriented Design Heuristics

- C++
  - Effective C++: 50 Specific Ways to Improve Your Programs and Designs
  - More Effective C++: 35 New Ways to Improve Your Programs and Designs

- Java
  - Effective Java Programming Language Guide

### Q6：作者是怎么论述的

### Q7：作者解决了什么问题

### Q8：我有哪些疑问

#### Q8.1: What are good class interfaces

#### Q8.2: How to design a class

#### Q8.3: How to implement a class

#### Q8.4: When should we create a class, and when shouldn't

### Q9：这一章说得有道理吗？为什么

### Q10：如何拓展这一章

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象

### Q11：这一章和我有什么关系
