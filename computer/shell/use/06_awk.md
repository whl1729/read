# 《Unix Shells by Example》分析笔记

## Chapter 6: The awk Utility

### Q1：这一章的内容是什么

介绍awk的基础知识。

### Q2：这一章的大纲是什么

- What's awk
- awk's Format
- How awk Works
- Formatting Output
- awk Commands from Within a File
- Records and Fields
- Patterns and Actions
- Regular Expressions
- Comparison Expressions
- Variables
- Arrays
- Redirection and Pipes
- Conditional Statements
- Loops
- Program Control Statements
- awk Built-In Functions
- User-Defined Function

### Q3：作者想要解决什么问题

### Q4：这一章的关键词是什么

### Q5：这一章的关键句是什么

#### 6.1 What's awk?

- Awk is a UNIX programming language used for manipulating data and generating reports.

- Nawk is a newer version of awk, and gawk is the GNU version used on Linux.

- Awk stands for the first initials in the last names of each of the authors of the language:
  Alfred Aho, Brian Kernighan, and Peter Weinberger.

#### 6.2 Format

- An awk program consists of the awk command, the program instructions enclosed in quotes (or in a file), and the name of the input file.
  - If an input file is not specified, input comes from standard input (stdin), the keyboard.

- Awk instructions consist of **patterns**, **actions**, or a combination of patterns and actions.
  - A pattern is a statement consisting of an expression of some type.
  - Actions consist of one or more statements separated by semicolons or newlines and enclosed in curly braces.

#### 6.3 How awk Works

- Take a line
  - Awk takes a line of input (from a file or pipe) and puts the line into an internal variable called `$0`.
  - Each line is also called a **record** and is terminated by a newline, by default.
- Split the line
  - The line is broken into fields (words) separated by whitespace.
  - Each field is stored in a numbered variable, starting with $1.
  - There can be as many as 100 fields.
  - The internal variable `FS` designates the field separator. Initially, FS is assigned whitespace—tabs and spaces.
- Print the fields
  - Awk uses the print function to print the fields.
  - The comma in `{print $1,$3}`generates whatever character has been assigned to the OFS variable.
  - The internal variable `OFS (output field separator)` is assigned a space as its default.

#### 6.4 Formatting Output

- The print Function
  - The print function accepts arguments as variables, computed values, or string constants.
  - Strings must be enclosed in double quotes.
  - Commas are used to separate the arguments; if commas are not provided, the arguments are concatenated together.
  - The comma evaluates to the value of the OFS, which is by default a space.

- print Escape Sequences
  - `\b` Backspace
  - `\f` Form feed
  - `\n` Newline
  - `\r` Carriage return
  - `\t` Tab
  - `\047` Octal value 47, a single quote
  - `\c` c represents any other character, e.g., \

- OFMT
  - The special awk variable, OFMT, can be set to control the printing of numbers when using the print function.
  - It is set by default to `%.6g`—six significant digits to the right of the decimal are printed.

- The printf Function
  - The printf function returns a formatted string to standard output, like the printf statement in C.
  - The printf statement consists of a quoted control string that may be embedded with format specifications and modifiers.

- printf Conversion Characters
  - `e` Floating-point number in scientific notation (e-notation)
  - `f` Floating-point number
  - `g` Floating-point number using either e or f conversion, whichever takes the least space

- printf Modifiers
  - `-` Left-justification modifier
  - `#` Integers in octal format are displayed with a leading 0; integers in hexadecimal form are displayed with a leading 0x
  - `+` For conversions using d, e, f, and g, integers are displayed with a numeric sign + or -
  - `0` The displayed value is padded with zeros instead of whitespace

#### 6.5 awk Commands from Within a File

- How awk run the commands in the file
  - A record is read into awk’s buffer and each of the commands in the awk file is tested and executed for that record.
  - After awk has finished with the first record, it is discarded and the next record is read into the buffer, and so on.

> 伍注：执行awk脚本时是依次对输入文本的每一行执行所有命令，而不是依次对每一条命令执行输入文本的所有行。

#### 6.6 Records and Fields

- The Record Separator
  - By default, the output and input record separator (line separator) is a carriage return (newline),
    stored in the built-in awk variables ORS and RS, respectively.
  - The ORS and RS values can be changed, but only in a limited fashion.

- The $0 Variable
  - An entire record is referenced as $0 by awk.
    (When $0 is changed by substitution or assignment, the value of NF, the number of fields, may be changed.)
  - The newline value is stored in awk’s built-in variable RS, a carriage return by default.

- The NR Variable
  - The number of each record is stored in awk’s built-in variable, NR.
  - After a record has been processed, the value of NR is incremented by one.

- The Input Field Separator
  - Awk’s built-in variable, FS, holds the value of the input field separator.
  - When the default value of FS is used, awk separates fields by spaces and/or tabs, stripping leading blanks and tabs.
  - The value of FS can be changed by assigning a new value to it, either in a BEGIN statement or at the command line.
  - You may specify more than one input separator.
    - If more than one character is used for FS, then the string is a regular expression and is enclosed in square brackets.
    - e.g. `awk -F'[ :\t]'`

- The Output Field Separator.
  - The default output field separator is a single space and is stored in awk’s internal variable, OFS.
  - The fields are jammed together if a comma is not used to separate the fields.
  - The OFS will not be evaluated unless the comma separates the fields.
  - The OFS can be changed.

#### 6.7 Patterns and Actions

- Patterns
  - When reading a pattern expression, there is an implied if statement.
  - The default action is to print each line where the expression results in a true condition.
  - When an if is implied, there can be no curly braces surrounding it.
  - When the if is explicit, it becomes an action statement and the syntax is different. (Question: Not understand?)
  - e.g. `awk '$3 < 4000' /tmp/employees`

- Actions
  - Actions are statements enclosed within curly braces and separated by semicolons.
  - Actions can be simple statements or complex groups of statements.
  - Statements are separated by semicolons, or by a newline if placed on their own line.

#### 6.8 Regular Expressions

- `^` Matches at the beginning of string
- `$` Matches at the end of string
- `.` Matches for a single character
- `*` Matches for zero or more of the preceding characters
- `+` Matches for one or more of the preceding characters
- `?` Matches for zero or one of the preceding characters
- `[ABC]` Matches for any one character in the set of characters A, B, or C
- `[^ABC]` Matches any one character not in the set of characters A, B, or C
- `[A–Z]` Matches for any one character in the range from A to Z
- `A|B` Matches either A or B
- `(AB)+` Matches one or more sets of AB; e.g., AB, ABAB, ABABAB
- `\*` Matches for a literal asterisk
- `&` Used in the replacement string to represent what was found in the search string

- Metacharacters NOT supported
  - `\< >/` Word anchors
  - `\( \)` Backreferencing
  - `\{ \}` Repetition

- The match operator
  - The tilde (~), is used to match an expression within a record or field.

#### 6.9 awk Commands in a Script File

- The script is a file containing awk comments and statements.
- If statements and actions are on the same line, they are separated by semicolons.
- If statements are on separate lines, semicolons are not necessary.
- If an action follows a pattern, the opening curly brace must be on the same line as the pattern.
- Comments are preceded by a pound (#) sign.

#### 6.11 Comparison Expressions

- Relational and Equality Operators
  - `<, <=, >, >=, ==, !=, ~, !~`
  - `~` Matched by regular expression
  - `!~` Not matched by regular expression

- Conditional Expressions
  - `conditional expression1 ? expression2 : expression3`

- Computation
  - Computation can be performed within patterns.
  - Awk (all versions) performs all arithmetic in floating point.
  - Arithmetic Operators: `+, -, *, /, %, ^`

- Logical Operators
  - `&&, ||, !`

- Range Patterns
  - Range patterns match from the first occurrence of one pattern to the first occurrence of the second pattern,
    then match for the next occurrence of the first pattern to the next occurrence of the second pattern, and so on.
  - If the first pattern is matched and the second pattern is not found, awk will display all lines to the end of the file.

#### 6.13 Variables

- Initialization and Type Coercion
  - Just mentioning a variable in your awk program causes it to exist.
  - Uninitialized variables have the value zero or the value " ", depending on the context in which they are used.

- Built-in Variable
  - `ARGC` Number of command-line argument
  - `ARGIND` Index in ARGV of the current file being processed from the command line (gawk only)
  - `ARGV` Array of command-line arguments
  - `CONVFMT` Conversion format for numbers, %.6g, by default (gawk only)
  - `ENVIRON` An array containing the values of the current environment variables passed in from the shell
  - `ERRNO` Contains a string describing a system error occurring from redirection
    when reading from the getline function or when using the close function (gawk only)
  - `FIELDWIDTHS` A whitespace-separated list of fieldwidths used instead of FS when splitting records of fixed fieldwidth (gawk only)
  - `FILENAME` Name of current input file
  - `FNR` Record number in current file
  - `FS` The input field separator, by default a space
  - `IGNORECASE` Turns off case sensitivity in regular expressions and string operations (gawk only)
  - `NF` Number of fields in current record. (Wu: `$NF` represents the last field)
  - `NR` Number of records so far
  - `OFMT` Output format for numbers
  - `OFS` Output field separator
  - `ORS` Output record separator
  - `RLENGTH` Length of string matched by match function
  - `RS` Input record separator
  - `RSTART` Offset of string matched by match function
  - `RT` The record terminator; gawk sets it to the input text that matched the character or regex specified by RS
  - `SUBSEP` Subscript separator

- BEGIN Patterns
  - The BEGIN pattern is followed by an action block that is executed before awk processes any lines from the input file.
  - The BEGIN action is often used to change the value of the built-in variables, OFS, RS, FS, and so forth,
    to assign initial values to user-defined variables and to print headers or titles as part of the output.
  - 伍注: The shell commands in BEGIN action must be enclosed in **double quotes**.

- END Patterns
  - END patterns do not match any input lines, but execute any actions that are associated with the END pattern.
  - END patterns are handled after all lines of input have been processed.

- How to reference a variable in awk
  - Neither double quotes or dollar sign are needed, just the variable name.

  ```shell
  awk -v name="$some_name" '$1 ~ name {print $2}' file
  awk -F: -v value="$some_value" '$3 == value {print NR}' file
  ```

#### 6.14 Redirection and Pipes

- Output Redirection
  - When redirecting output from within awk to a UNIX/Linux file, the shell redirection operators are used.
  - The filename must be enclosed in **double quotes**.

- Input Redirection (The getline Function)
  - The getline function is used to read input from the standard input, a pipe, or a file other than the current file being processed.
  - It gets the next line of input and sets the NF, NR, and the FNR built-in variables.
  - The getline function returns 1 if a record is found and 0 if EOF (end of file) is reached.
    If there is an error, such as failure to open a file, the getline function returns a value of -1.

- Closing Files and Pipes
  - If you plan to use a file or pipe in an awk program again for reading or writing, you may want to close it first,
    because it remains open until the script ends.
  - Once opened, the pipe remains open until awk exits. Therefore, statements in the END block will also be affected by the pipe.

- The system Function.
  - The built-in system function takes a UNIX/Linux system command as its argument, executes the command,
    and returns the exit status to the awk program.
  - It is similar to the C standard library function, also called system(). The UNIX/Linux command must be enclosed in double quotes.

#### 6.18 Loops

- while Loop

- for Loop
  - In awk, the first statement within the parentheses of the for loop can perform only one initialization.
    (In C, you can have multiple initializations separated by commas.)

- break and continuse Statements

#### 6.19 Program Control Statements

- next Statement
  - The next statement gets the next line of input from the input file, restarting execution at the top of the awk script.

- exit Statement
  - The exit statement is used to terminate the awk program.
  - It stops processing records, but does not skip over an END statement.

#### 6.20 Arrays

- Arrays in awk are called **associative arrays** because the subscripts can be either numbers or strings.

- hashing
  - Due to the techniques used for hashing, the array elements are not stored in a sequential order.
  - When the contents of the array are displayed, they may not be in the order you expected.

- The Special-for Loop: `for (index_value in array) statement`

- The split Function
  - Awk's built-in split function allows you to split a string into words and store them in an array.
  - `split(string, array, field separator)`
  - `split(string, array)`

- The delete Statement
  - `delete array[expr]` removes an array element.

#### 6.21 awk Built-in Functions

- String Function
  - `sub(regular expression, substitution string, target string)`
    - If a target string is specified, the regular expression is matched for the largest and leftmost substring in the target string,
      and the substring is replaced with the substitution string.
    - If a target string is not specified, the entire record is used.
  - `gsub(regular expression, substitution string, target string)`
    - global substitution
  - `index(string, substring)`
    - **Offset starts at position 1.**
  - `length(string)`
    - Without an argument, the length function returns the number of characters in a record.
  - `substr(string, starting position, length of string)`
    - **first position is one****.
    - If the length of the substring is given, that part of the string is returned.
    - If the specified length exceeds the actual string, the string is returned.
  - `match(string, regular expression)`
    - The match function returns the index where the regular expression is found in the string, or zero if not found.
    - The match function sets the built-in variable RSTART to the starting position of the substring within the string,
      and RLENGTH to the number of characters to the end of the substring.
  - `split(string, array, field separator)`
    - The split function splits a string into an array using whatever field separator is designated as the third parameter.
    - If the third parameter is not provided, awk will use the current value of FS.
    - **The array subscript starts at 1.**
  - `sprintf`
  - `tolower`
  - `toupper`

- Arithmetic Function
  - `atan2(x,y)` Arctangent of y/x in the range
  - `cos(x)` Cosine of x (x in radians)
  - `exp(x)` Exponential function e to the power of x
  - `int(x)` Integer portion of x; truncated toward 0 when x > 0
  - `log(x)` Natural (base e) logarithm of x
  - `rand(` ) Random number r, where `0 < r < 1`
  - `sin(x)` Sine of x (with x in radians)
  - `sqrt(x)` Square root of x
  - `srand(x)` x is a new seed for rand( )

- Time Function
  - `systime`

- Reading Input
  - `getline`

### Q6：作者是怎么论述的

### Q7：作者解决了什么问题

### Q8：我有哪些疑问

### Q9：这一章说得有道理吗？为什么

### Q10：如何拓展这一章

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象

### Q11：这一章和我有什么关系
