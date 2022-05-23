# 《Code Complete》分析笔记

## Chapter 8: Defensive Programming

### Q1：这一章的内容是什么？

### Q2：这一章的大纲是什么？

- Protecting Your Program from Invalid Input
- Assertions
- Error-Handling Techniques
- Exceptions
- Barricade Your Program to Contain the Damage Caused by Errors
- Debugging Aids
- Determining How Much Defensive Programming to Leave in Production Code
- Being Defensive About Defensive Programming

### Q3：作者想要解决什么问题？

### Q4：这一章的关键词是什么？

### Q5：这一章的关键句是什么？

- Defensive Programming
  - The main idea is that if a routine is passed bad data,
    it won’t be hurt, even if the bad data is another routine’s fault.

#### 8.1 Protecting Your Program from Invalid Input

- 3 general ways to handle garbage in
  - Check the values of all data from external sources
  - Check the values of all routine input parameters
  - Decide how to handle bad inputs

#### 8.2 Assertions

- Why assertions
  - Assertions are especially useful in large, complicated programs and in high-reliability programs.
    They enable programmers to more quickly flush out mismatched interface assumptions, errors that creep in when code is modified, and so on.

- When to use assertions
  - Assertions are primarily for use during development and maintenance.
  - Assertions are normally compiled into the code at development time and compiled out of the code for production.
  - During development, assertions flush out contradictory assumptions, unexpected conditions, bad values passed to routines, and so on.
  - During production, they can be compiled out of the code so that the assertions don’t degrade system performance.

- Guidelines for Using Assertions
  - Use error-handling code for conditions you expect to occur;
    use assertions for conditions that should never occur.
  - Avoid putting executable code into assertions.
  - Use assertions to document and verify preconditions and postconditions.
  - For highly robust code, assert and then handle the error anyway.

#### 8.3 Error-Handling Techniques

- Error-Handling Techniques
  - Return a neutral value
  - Substitute the next piece of valid data
    - Processing a stream of data
  - Return the same answer as the previous time
    - Thermometer-reading software
  - Substitute the closest legal value
    - Reading veolcity
  - Log a warning message to a file
  - Return an error code
  - Call an error-processing routine/object
  - Display an error message wherever the error is encountered
  - Handle the error in whatever way works best locally
  - Shut down
    - Safety-critical applications

- Robustness vs Correctness
  - The two terms are at opposite ends of the scale from each other.
    - Correctness means never returning an inaccurate result; returning no result is better than returning an inaccurate result.
    - Robustness means always trying to do something that will allow the software to keep operating,
      even if that leads to results that are inaccurate sometimes.
  - Which is more important
    - Safety-critical applications tend to favor correctness to robustness.
    - Consumer applications tend to favor robustness to correctness.

#### 8.4 Exceptions

- Suggestions for Using exceptions
  - Use exceptions to notify other parts of the program about errors that should not be ignored
  - Throw an exception only for conditions that are truly exceptional
  - Don't use an exception to pass the buck (推卸责任)
  - Avoid throwing exceptions in constructors and destructors unless you catch them in the same place
  - Throw exceptions at the right level of abstraction
  - Include in the exception message all information that led to the exception
  - Avoid empty catch blocks
  - Know the exceptions your library code throws
  - Consider building a centralized exception reporter
  - Standardize your project's use of exceptions
  - Consider alternatives to exceptions

#### 8.5 Barricade Your Program to Contain the Damage Caused by Errors

- How to barricade your program
  - Designate certain interfaces as boundaries to "safe" areas.
    Check data crossing the boundaries of a safe area for validity, and respond sensibly if the data isn't valid.
  - As an operating-room technique.
    Sanitizing external data as it arrives.
  - Convert input data to the proper type at input time.

- Barricades vs Assertions
  - Routines that are outside the barricade should use error handling
    because it isn't safe to make any assumptions about the data.
  - Routines inside the barricade should use assertions,
    because the data passed to them is supposed to be sanitized before it's passed across the barricade.

#### 8.6 Debugging Aids

- Don't Automatically Apply Production Constraints to the Development Version.
- Introduce Debugging Aids Early.
- Use Offensive Programming
- Plan to Remove Debugging Aids
  - Use version-control tools and build tools like ant and make
  - Use a built-in preprocessor
  - Write your own preprocessor
  - Use debugging stubs

#### 8.7 Determining How Much Defensive Programming to Leave in Production Code

- Guidelines for deciding how much defensive programming tools to leave in your production code
  - Leave in code that checks for important errors
  - Remove code that checks for trivial errors
  - Remove code that results in hard crashes
  - Leave in code that helps the program crash gracefully
  - Log errors for your technical support personnel
  - Make sure that the error messages you leave in are friendly

#### 8.8 Being Defensive About Defensive Programming

- Too much defensive programming creates problems of its own.
  - If you check data passed as parameters in every conceivable way in every conceivable place,
    your program will be fat and slow.
  - What's worse, the additional code needed for defensive programming adds complexity to the software.

#### 8.9 Checklist: Defensive Programming

- General
  - [ ] Does the routine protect itself from bad input data?
  - [ ] Have you used assertions to document assumptions, including preconditions and postconditions?
  - [ ] Have assertions been used only to document conditions that should never occur?
  - [ ] Does the architecture or high-level design specify a specific set of errorhandling techniques?
  - [ ] Does the architecture or high-level design specify whether error handling should favor robustness or correctness?
  - [ ] Have barricades been created to contain the damaging effect of errors and reduce the amount of code that has to be concerned about error processing?
  - [ ] Have debugging aids been used in the code?
  - [ ] Have debugging aids been installed in such a way that they can be activated or deactivated without a great deal of fuss?
  - [ ] Is the amount of defensive programming code appropriate—neither too much nor too little?
  - [ ] Have you used offensive-programming techniques to make errors difficult to overlook during development?

- Exceptions
  - [ ] Has your project defined a standardized approach to exception handling?
  - [ ] Have you considered alternatives to using an exception?
  - [ ] Is the error handled locally rather than throwing a nonlocal exception, if possible?
  - [ ] Does the code avoid throwing exceptions in constructors and destructors?
  - [ ] Are all exceptions at the appropriate levels of abstraction for the routines that throw them?
  - [ ] Does each exception include all relevant exception background information?
  - [ ] Is the code free of empty catch blocks? (Or if an empty catch block truly is appropriate, is it documented?)

- Security Issues
  - [ ] Does the code that checks for bad input data check for
        attempted buffer overflows, SQL injection, HTML injection, integer overflows, and other malicious inputs?
  - [ ] Are all error-return codes checked?
  - [ ] Are all exceptions caught?
  - [ ] Do error messages avoid providing information that would help an attacker break into the system?

#### 8.10 Additional Resources

- Security
  - Howard, Michael, and David LeBlanc. Writing Secure Code, 2d ed.
- Assertions
  - Maguire, Steve. Writing Solid Code.
  - Meyer, Bertrand. Object-Oriented Software Construction.

### Q6：作者是怎么论述的？

### Q7：作者解决了什么问题？

### Q8：我有哪些疑问？

#### Q8.1: How to barricde your program to contain the damage caused by errors?

#### Q8.2: How much defensive programming should be left in production code?

#### Q8.3: What does it that being defensive about defensive programming?

### Q9：这一章说得有道理吗？为什么？

### Q10：如何拓展这一章？

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它？

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么？

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象？

### Q11：这一章和我有什么关系？
