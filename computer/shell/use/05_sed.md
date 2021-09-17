# 《Unix Shells by Example》分析笔记

## Chapter 5: sed, the Streamlined Editor

### Q1：这一章的内容是什么？

介绍sed工具的基础知识。

### Q2：这一章的大纲是什么？

- What is sed
- Versions of sed
- How Does sed work
- Regular Expressions
- Addressing
- Commands and Options
- Error Messages and Exit Status
- Metacharacters
- sed Scripting

### Q3：作者想要解决什么问题？

### Q4：这一章的关键词是什么？

- streamlined editor

### Q5：这一章的关键句是什么？

#### 5.1 What is sed?

- Sed is a streamlined, noninteractive editor. 

- The sed editor is nondestructive.
  - It does not change your file unless you save the output with shell redirection.
  - All lines are printed to the screen by default.

#### 5.3 How does sed work?

- The sed editor processes a file (or input) **one line at a time** and sends its output to the screen.

- Pattern space or temporary buffer
  - Store: Sed stores the line it is currently processing in a temporary buffer called a pattern space or temporary buffer.
  - Process: Once sed is finished processing the line in the pattern space (i.e., executing sed commands on that line),
    the line in the pattern space is sent to the screen (unless the command was to delete the line or suppress its printing).
  - Remove: After the line has been processed, it is removed from the pattern space and the next line is then read into the pattern space, processed, and displayed.
  - Stop: Sed ends when the last line of the input file has been processed.
  - By storing each line in a temporary buffer and performing edits on that line, the original file is never altered or destroyed.

#### 5.4 Regular Expressions

- To change the regular expression delimeter,
  some character, say x, is preceded by a backslash, followed by the regular expression, and that character.

  ```shell
  $ sed -n '/12\/10\/04/p' datafile
  $ sed -n '\x12/10/04xp' datafile
  ```

- Exit status
  - The exit status of the sed command, however, will be zero, whether or not the pattern being searched for is found.
  - The only time the exit status will be nonzero is when the command contains a syntax error.

#### 5.5 Addressing

- You can use addressing to decide which lines you want to edit.

- Without specifying an address, sed processes all lines of the input file.

- The addresses can be in the form of decimal numbers or regular expressions (also called context addresses), or a combination of both.
  - When an address consists of a number, the number represents a line number.
  - A dollar sign can be used to represent the last line of the input file.
  - If a comma separates two line numbers, the addresses that will be processed are within that range of lines, including the first and last line in the range.
  - The range may be numbers, regular expressions, or a combination of numbers and regular expressions.

### Q6：作者是怎么论述的？

### Q7：作者解决了什么问题？

### Q8：我有哪些疑问？

### Q9：这一章说得有道理吗？为什么？

### Q10：如何拓展这一章？

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它？

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么？

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象？

### Q11：这一章和我有什么关系？

