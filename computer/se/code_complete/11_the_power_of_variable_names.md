# 《Code Complete》分析笔记

## Chapter 11: The Power of Variable Names

### Q1：这一章的内容是什么

### Q2：这一章的大纲是什么

- Considerations in Choosing Good Names
- Naming Specific Types of Data
- The Power of Naming Conventions (Wu: Not impormtant)
- Informal Naming Conventions
- Standardized Prefixes (Wu: Not important)
- Creating Short Names That Are Readable
- Kinds of Names to Avoid
- Checklist (Wu: Important!)

### Q3：作者想要解决什么问题

### Q4：这一章的关键词是什么

### Q5：这一章的关键句是什么

#### 11.1 Considerations in Choosing Good Names

- The most important naming consideration
  - An effective technique for coming up with a good name is to state in words **what the variable represents**.
  - Names should be as specific as possible.
    - Names like x, temp, and i that are general enough to be used for more than one purpose
      are not as informative as they could be and are usually bad names.

- Problem Orientation
  - A good mnemonic name generally speaks to the **problem** rather than the solution.
  - A good name tends to express the **what** more than the how.

- The Effect of Scope on Variable Name
  - Longer names are better for rarely used variables or global variables.
  - Shorter names are better for local variables or loop variables.
  - Use qualifiers on names that are in the global namespace.
    (e.g., use the namespace keyword to partition the global namespace)

- Put the computed-value qualifier at the end of the name
  - So the most significant part of the variable name is at the front.
  - e.g., revenueTotal, expenseTotal, revenueAverage, expenseAverage

- Use opposites precisely.

#### 11.2 Naming Specific Types of Data

- Naming Loop Indexes
  - Carefully chosen names for loop-index variables avoid the common problem of index cross-talk.
  - If you have to use i, j, and k, don’t use them for anything other than loop indexes for simple loops.

- Naming Status Variables
  - Think of a better name than flag for status variables.

- Naming Temporary Variables
  - Be leery of "temporary" variables. Give them a descriptive name rather than "temp".

- Naming Boolean Variables
  - Keep typical boolean names in mind. `done, error, found, success, or ok`
  - Give boolean variables names that imply true or false.
  - Use positive boolean variable names.

#### 11.4 Informal Naming Conventions

- Guidelines for a Language-Independent Convention
  - Differentiate between variable names and routine names
  - Differentiate between classes and objects
  - Identify global variables
  - Identify member variables
  - Identify type definitions
  - Identify named constants
  - Identify elements of enumerated types
  - Identify input-only parameters in languages that don't enforce them
  - Format names to enhance readability

#### 11.6 Creating Short Names That Are Readable

- General Abbreviation Guidelines
  - Use standard abbreviations (the ones in common use, which are listed in a dictionary).
  - Remove all nonleading vowels. (computer becomes cmptr, and screen becomes scrn.)
  - Remove articles: and, or, the, and so on.
  - Use the first letter or first few letters of each word.
  - Truncate consistently after the first, second, or third (whichever is appropriate) letter of each word.
  - Keep the first and last letters of each word.
  - Use every significant word in the name, up to a maximum of three words.
  - Remove useless suffixes—ing, ed, and so on.
  - Keep the most noticeable sound in each syllable.
  - Be sure not to change the meaning of the variable.
  - Iterate through these techniques until you abbreviate each variable name to between 8 to 20 characters or
    the number of characters to which your language limits variable names.

- Comments on Abbreviations
  - Don’t abbreviate by removing one character from a word.
  - Abbreviate consistently.
  - Create names that you can pronounce.
  - Avoid combinations that result in misreading or mispronunciation.
  - Use a thesaurus(辞典) to resolve naming collisions.
  - Document extremely short names with translation tables in the code.
  - Document all abbreviations in a project-level "Standard Abbreviations" document.
  - Remember that names matter more to the reader of the code than to the writer.

#### 11.7 Kinds of Names to Avoid

- Guidelines regarding variable names to avoid
  - Avoid misleading names or abbreviations.
  - Avoid names with similar meanings.
  - Avoid variables with different meanings but similar names.
  - Avoid names that sound similar, such as wrap and rap.
  - Avoid numerals in names. e.g. "file1" and "file2".
  - Avoid misspelled words in names.
  - Avoid words that are commonly misspelled in English.
  - Don't differentiate variable names solely by capitalization.
  - Avoid multiple natural languages.
  - Avoid the names of standard types, variables, and routines.
  - Don't use names that are totally unrelated to what the variables represent.
  - Avoid names containing hard-to-read characters.

#### Checklist: Naming Variables

- General Naming Considerations
  - [ ] Does the name fully and accurately describe what the variable represents?
  - [ ] Does the name refer to the real-world problem rather than to the programming-language solution?
  - [ ] Is the name long enough that you don’t have to puzzle it out?
  - [ ] Are computed-value qualifiers, if any, at the end of the name?
  - [ ] Does the name use Count or Index instead of Num?
- Naming Specific Kinds of Data
  - [ ] Are loop index names meaningful (something other than i, j, or k if the loop is more than one or two lines long or is nested)?
  - [ ] Have all “temporary” variables been renamed to something more meaningful?
  - [ ] Are boolean variables named so that their meanings when they’re true are clear?
  - [ ] Do enumerated-type names include a prefix or suffix that indicates the category—for example, Color_ for Color_Red, Color_Green, Color_Blue, and so on?
  - [ ] Are named constants named for the abstract entities they represent rather than the numbers they refer to?
- Naming Conventions
  - [ ] Does the convention distinguish among local, class, and global data?
  - [ ] Does the convention distinguish among type names, named constants, enumerated types, and variables?
  - [ ] Does the convention identify input-only parameters to routines in languages that don’t enforce them?
  - [ ] Is the convention as compatible as possible with standard conventions for the language?
  - [ ] Are names formatted for readability?
- Short Names
  - [ ] Does the code use long names (unless it’s necessary to use short ones)?
  - [ ] Does the code avoid abbreviations that save only one character?
  - [ ] Are all words abbreviated consistently?
  - [ ] Are the names pronounceable?
  - [ ] Are names that could be misread or mispronounced avoided?
  - [ ] Are short names documented in translation tables?
- Common Naming Problems: Have You Avoided...
  - [ ] ...names that are misleading?
  - [ ] ...names with similar meanings?
  - [ ] ...names that are different by only one or two characters?
  - [ ] ...names that sound similar?
  - [ ] ...names that use numerals?
  - [ ] ...names intentionally misspelled to make them shorter?
  - [ ] ...names that are commonly misspelled in English?
  - [ ] ...names that conflict with standard library routine names or with predefined variable names?
  - [ ] ...totally arbitrary names?
  - [ ] ...hard-to-read characters?

### Q6：作者是怎么论述的

### Q7：作者解决了什么问题

### Q8：我有哪些疑问

### Q9：这一章说得有道理吗？为什么

### Q10：如何拓展这一章

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象

### Q11：这一章和我有什么关系
