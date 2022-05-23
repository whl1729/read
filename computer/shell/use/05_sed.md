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

#### 5.1 What is sed

- Sed is a streamlined, noninteractive editor.

- The sed editor is nondestructive.
  - It does not change your file unless you save the output with shell redirection.
  - All lines are printed to the screen by default.

#### 5.3 How does sed work

- The sed editor processes a file (or input) **one line at a time** and sends its output to the screen.

- Pattern space or temporary buffer
  - Store: Sed stores the line it is currently processing in a temporary buffer called a pattern space or temporary buffer.
  - Process: Once sed is finished processing the line in the pattern space (i.e., executing sed commands on that line),
    the line in the pattern space is sent to the screen (unless the command was to delete the line or suppress its printing).
  - Remove: After the line has been processed, it is removed from the pattern space and the next line is then read into the pattern space, processed, and displayed.
  - Stop: Sed ends when the last line of the input file has been processed.
  - By storing each line in a temporary buffer and performing edits on that line, the original file is never altered or destroyed.

#### 5.4 Regular Expressions

- Regular expressions are patterns of characters **enclosed in forward slashes** for searches and substitutions.

> 伍注：正则表达式是用斜杠包围起来的字符串。

- To change the regular expression delimeter,
  some character, say x, is preceded by a backslash, followed by the regular expression, and that character.

  ```shell
  sed -n '/12\/10\/04/p' datafile
  sed -n '\x12/10/04xp' datafile
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

#### 5.6 Commands and Options

##### 5.6.1 sed Commands

- `a\` Appends one or more lines of text to the current line. (伍注：在下一行输入追加内容时才需要使用反斜杠)
- `c\` Changes (replaces) text in the current line with new text
- `d`  Deletes lines
- `i\` Inserts text above the current line
- `h` Copies the contents of the pattern space to a holding buffer
- `H` Appends the contents of the pattern space to a holding buffer
- `g` Gets what is in the holding buffer and copies it into the pattern buffer, overwriting what was there
- `G` Gets what is in the holding buffer and copies it into the pattern buffer, appending to what was there
- `l` Lists nonprinting characters
- `p` Prints lines
- `n` Reads the next input line and starts processing the newline with the next command rather than the first command
- `N` Appends the next input line and starts processing the newline with the next command rather than the first command
- `q` Quits or exits sed
- `r` Reads lines from a file
- `!` Applies the command to all lines except the selected ones
- `s` Substitutes one string for another

##### 5.6.2 sed Substitution Flags

- `g` Globally substitutes on a line
- `p` Prints lines
- `r` Append text read from file
- `w` Writes lines out to a file
- `x` Exchanges contents of the holding buffer with the pattern space
- `y` Translates one character to another (cannot use regular expression metacharacters with y)

##### 5.6.2 sed Options

- `-e` Allows multiple edits
- `-f` Precedes a sed script filename
- `-n` Suppresses default output

#### 5.8 Metacharacters

- `^` Beginning-of-line anchor
- `$` End-of-line anchor
- `.` Matches one character, **but not the newline character**
- `*` Matches zero or more characters
- `[]` Matches one character in the set
- `[^]` Matches one character not in the set
- `\<` Beginning-of-word anchor
- `\>` End-of-word anchor
- `\(..\)` Saves matched characters.
  - Tags marked portion in a register to be remembered later as number 1. To reference later, use `\1` to repeat the pattern.
- `&` Saves search string so it can be remembered in the replacement string. eg: `s/love/**&**/`
- `x\{m\}` Repetition of character x m times
- `x\{m,\}` Repetition of character x at least m times
- `x\{m,n\}` Repetition of character x between m and n times

#### 5.10 sed Scripting

- Sed is very particular about the way you type lines into the script.
  - There cannot be any **trailing whitespace or text** at the end of the command.
  - If commands are not placed on a line by themselves, they must be terminated with a **semicolon**.

### Q6：作者是怎么论述的？

### Q7：作者解决了什么问题？

### Q8：我有哪些疑问？

### Q9：这一章说得有道理吗？为什么？

### Q10：如何拓展这一章？

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它？

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么？

##### [SED 简明教程][sed_tutorial]

- sed 可以指定替换第几个匹配项

  ```shell
  sed 's/s/S/1' my.txt   # 只替换每一行的第1个s
  sed 's/s/S/3g' my.txt  # 只替换每一行的第3个以后的s
  ```

- 一次替换多个模式的两种方法
  - 使用分号来隔开
  - 使用多个`-e`

  ```shell
  sed '1,3s/my/your/g; 3,$s/This/That/g' my.txt   # 使用分号来隔开
  sed -e '1,3s/my/your/g' -e '3,$s/This/That/g' my.txt  # 使用多个`-e`
  ```

  [sed_tutorial]: https://coolshell.cn/articles/9104.html

##### [How do I use variables in a sed command?][sed_variable]

- Use **double quotes** to make the shell expand variables while preserving whitespace.
  - e.g. `sed -i "s/$var1/ZZ/g" "$file"`

  [sed_variable]: https://askubuntu.com/questions/76808/how-do-i-use-variables-in-a-sed-command

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象？

### Q11：这一章和我有什么关系？
