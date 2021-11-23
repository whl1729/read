# 《Code Complete》分析笔记

## Chapter 23 Debugging

### Q1：这一章的内容是什么？

### Q2：这一章的大纲是什么？

- Overview of Debugging Issues
  - Role of Debugging in Software Quality
    - Debugging is a last resort to build a quality product
  - Variations in Debugging Performance
    - 20-to-1 difference in the debugging time
  - Defects as Opportunities
  - An Ineffetive Approach
- Finding a Defect
  - The Scientific Method of Debugging
  - Methods for finding a defect
    - Stabilize the Error
    - LOcate the Source of the Error
  - Tips for Finding Defects
  - Brute-Force Debugging
  - Syntax Errors
- Fixing a Defect
- Psychological Considerations in Debugging
  - How "Psychological Set" Contributes to Debugging Blindness
  - How "Psychological Distance" Can Help
- Debugging Tools: Obvious and Not-So-Obvious
  - Source-Code Comparators
  - Compiler Warning Messages
  - Extended Syntax and Logic Checking
  - Execution Profilers
  - Test Frameworks/Scaffolding
  - Debuggers

### Q3：作者想要解决什么问题？

### Q4：这一章的关键词是什么？

- Psychological Distance
  - The ease with which two items can be differentiated. 

### Q5：这一章的关键句是什么？

#### 23.1 Overview of Debugging Issues

- Defects as Opportunities
  - Learn about the program you're working on
  - Learn about the kinds of mistakes you make
  - Learn about the quality of your code from the point of view of someone who has to read it
  - Learn about how you solve problems
  - Learn about how you fix defects

- An Ineffective Approach
  - The Devil's Guide to Debugging
    - Find the defect by guessing
    - Don't waste time trying to understand the problem
    - Fix the error with the most obvious fix
  - Debugging by Superstition

#### 23.2 Finding a Defect

- The Scientific Method of Debugging
  - Gather data through repeatable experiments
  - Form a hypothesis that accounts for the relevant data
  - Design an experiment to prove or disprove the hypothesis
  - Prove or disprove the hypothesis
  - Repeat as needed

- An effective approach for finding a defect
  - Stabilize the error
  - Locate the source of the error (the "fault")
    - Gather the data that produces the defect
    - Analyze the data that has been gathered, and form a hypothesis about the defect
    - Determine how to prove or disprove the hypothesis,
      either by testing the program or by examing the code.
  - Fix the defect
  - Test the fix
  - Look for similar errors

- Tips for Finding Defects
  - Use all the data available to make your hypothesis
  - Refine the test cases that produce the error
  - Exercise the code in your unit test suite
  - Use available tools
  - Reproduce the error several different ways
  - Generate more data to generate more hypotheses
  - Use the result of negative tests
  - Brainstorm for possible hypotheses
  - Keep a notepad by your desk, and make a list of things to try
  - Narrow the suspicious region of the code
  - Be suspicious of classes and routines that have had defects before
  - Check code that's changed recently
  - Expand the suspicious region of the code
  - Integrate incrementally
  - Check for common defects
  - Talk to someone else about the problem
  - Take a break from the problem
  - Set a maximum time for quick and dirty debugging
  - Make a list of brute-force techniques

- Brute-Force Debugging Techniques
  - Perform a full design and/or code review on the broken code.
  - Throw away the section of code and redesign/recode it from scratch.
  - Throw away the whole program and redesign/recode it from scratch.
  - Compile code with full debugging information.
  - Compile code at pickiest warning level and fix all the picky compiler warnings.
  - Strap on a unit test harness and test the new code in isolation.
  - Create an automated test suite and run it all night.
  - Step through a big loop in the debugger manually until you get to the error condition.
  - Instrument the code with print, display, or other logging statements.
  - Compile the code with a different compiler.
  - Compile and run the program in a different environment.
  - Link or run the code against special libraries or execution environments that produce warnings when code is used incorrectly.
  - Replicate the end-user’s full machine configuration.
  - Integrate new code in small pieces, fully testing each piece as it’s integrated

- Syntax Errors (Wu: Some suggestions are obsolete.)
  - Don't trust line numbers
  - Don't trust compiler messages
  - Don't trust the compiler's second message
  - Divide and Conquer
  - Find misplaced comments and quotation marks

#### 23.3 Fixing a Defect

- Guidelines for fixing a Defect
  - Understand the problem before you fix it
  - Understand the program, not just the problem
  - Confirm the defect diagnosis
  - Relax
  - Save the original source code
  - Fix the problem, not the symptom
  - Change the code only for good reason
  - Make one change at a time
  - Check your fix
  - Add a unit test that exposes the defect
  - Look for similar defects

#### 23.4 Psychological Considerations in Debugging

- Psychological set vs Debugging
  - First, it speaks to the importance of good programming practices.
    Good formatting, commenting, variable names, routine names, and other elements of programming style
    help structure the programming background so that likely defects appear as variations and stand out. 
  - The second impact of psychological set is in selecting parts of the program to examine when an error is found,
    you should be careful to overcome the "debugging blindness".

- How "Psychological Distance" Can Help
  - As you debug, be ready for the problems caused by insufficient psychological distance
    between similar variable names and between similar routine names.
  - As you construct code, choose names with large differences so that you avoid the problem.

#### 23.5 Debugging Tools: Obvious and Not-So-Obvious

- Compiler Warning Messages
  - Set your compiler's warning level to the highest, pickiest level pissible, and fix the errors it reports
  - Treat warnings as errors
  - Initiate projectwide standards for compile-time settings

#### 23.6 Checklists: Debugging Reminders

- General Approach to Debugging
  - [ ] Do you use debugging as an opportunity to learn more about your program, mistakes, code quality, and problem-solving approach?
  - [ ] Do you avoid the trial-and-error, superstitious approach to debugging?
  - [ ] Do you assume that errors are your fault?
  - [ ] Do you use the scientific method to stabilize intermittent errors?
  - [ ] Do you use the scientific method to find defects?
  - [ ] Rather than using the same approach every time, do you use several different techniques to find defects?
  - [ ] Do you verify that the fix is correct?
  - [ ] Do you use compiler warning messages, execution profiling, a test framework, scaffolding, and interactive debugging?

### Q6：作者是怎么论述的？

### Q7：作者解决了什么问题？

### Q8：我有哪些疑问？

### Q9：这一章说得有道理吗？为什么？

### Q10：如何拓展这一章？

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它？

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么？

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象？

### Q11：这一章和我有什么关系？

