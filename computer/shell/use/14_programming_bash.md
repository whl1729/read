# 《Unix Shells by Example》分析笔记

## Chapter 14: Programming the Bash Shell

### Q1：这一章的内容是什么？

### Q2：这一章的大纲是什么？

- Reading User Input
- Arithmetic
- Positional Parameters and Command-Line Arguments
- Conditional Constructs and Flow Control
- Looping Commands
- Functions
- Trapping Signals
- Debugging
- The Command Line
- bash Options
- Shell Built-In Commands

### Q3：作者想要解决什么问题？

### Q4：这一章的关键词是什么？

- word splitting

### Q5：这一章的关键句是什么？

#### 14.1 Introduction

- When the bash (Bourne Again) shell starts running noninteractively,
  it looks for the environment variable, BASH_ENV (ENV) and starts up the file (normally `.bashrc`) assigned as its value.
  After the BASH_ENV file has been read, the shell will start executing commands in the script.

> Wu: 子进程不是直接继承父进程的环境变量吗？为啥还要重新读入？

#### 14.2 Reading User Input

- The read command
  - `read answer` Reads a line from standard input and assigns it to the variable answer
  - `read first last` Reads a line from standard input to the first whitespace or newline,
    putting the first word typed into the variable first and the rest of the line into the variable last
  - `read` Reads a line from standard input and assigns it to the built-in variable REPLY (Bash and Korn shell)
  - `read -a arrayname` Reads a list of words into an array called arraynamea
  - `read -e` Used in interactive shells with command-line editing in effect;
    for example, if editor is vi, vi commands can be used on the input line.
  - `read -p prompt` Prints a prompt, waits for input, and stores input in REPLY variable
  - `read -r line` Allows the input to contain a backslash.

> Wu: Read `help read` for more details.

- You can also use the read command to cause a program to stop until the user hits Enter.

#### 14.3 Arithmetic

##### 14.3.1 Integers (declare and let Commands)

- The declare Command
  - If you attempt to assign any string value to integer, bash assigns 0 to the variable.
  - If you attempt to assign a floating-point number, bash reports a syntax error.
  - Numbers can also be represented in different bases such as binary, octal, and hex.
  - `declare -i` list all preset integers and their values.

- Representing and Using Different Bases.
  - Numbers can be represented in decimal (base 10, the default), octal (base 8), hexadecimal (base 16), and a range from base 2 to 36.
  - Format: `variable=base#number-in-that-base`. e.g., `n=2#101, x=16#ff`

> Wu: Numbers can be represented in a range from base 2 to 64 on my Ubuntu.

- Avoid using `set -e` and `i++` together!

  ```shell
  set -e
  i=0
  ((i++))    # Cause the shell to exit since the return value is 1
  ```

##### 14.3.2 Floating-Point Arithmetic

- Bash supports only integer arithmetic, but the bc, awk, and nawk utilities are useful if you need to perform floating-point calculations.

```shell
n=`echo "scale=10; 123.45 / 67.89" | bc`
product=`awk -v x=2.45 -v y=3.123 'BEGIN{printf "%.2f\n", x*y}'`
```

##### 14.4 Positional Parameters and Command-Line Arguments

- Positional Parameters
  - Positional parameters can be set or reset with the set command.
  - When the set command is used, any positional parameters previously set are cleared out.
  - To unset all of the positional parameters, use `set --`.

##### 14.5 Conditional Constructs and Flow Control

##### 14.5.1 Exit Status

- Bash allows you to test two types of conditions:
  the success or failure of commands or whether an expression is true or false.
  In either case, the exit status is always used.
  An exit status of 0 indicates success or true, and an exit status that is nonzero indicates failure or false.

##### 14.5.2 The Built-In test and let Commands

- `[]` vs `[[ ]]`
  - Shell metacharacter expansion is performed on expressions inside `[[ ]]`, but not `[]`.
  - Word splitting is performed on variables inside `[]`, but not `[[ ]]`.
  - `[]` use `-a` and `-o` for logical test, while `[[ ]]` use `&&` and `||`.
  - Neither `[]` nor `[[ ]]` can use `<` and `>` for integer comparison.
    - When used with `[[`, the `<` and `>` operators sort lexicographically using the current locale.

  ```shell
  # Shell wildcards expansion
  name="Tom"
  [ name == [Tt]om ]; echo $?    # Returns 1.
  [[ name == [Tt]om ]]; echo $?  # Returns 0.

  # Integer comparison
  [ 1 < 2 ]; echo $?    # Returns 0. Maybe Bourne shell recognize "<" as stream redirection here.
  [ 1 > 2 ]; echo $?    # Returns 0.
  [[ 12 < 2 ]]; echo $?    # Return 0. "12" is smaller than "2" lexicographically.
  ```

- `[[ ]]`
  - Word splitting and pathname expansion are not performed on the words between the [[ and ]];
  - Tilde expansion, parameter and variable expansion, arithmetic expansion, command substitution,
    process substitution, and quote removal are performed.

- The test Command Operators
  - `[ string1 = string2 ]` String1 is equal to String2 (space surrounding = required).
  - `[ string1==string2 ]` Can be used instead of the single = sign on bash versions 2.x.

> Wu: we can use `==` to test equality in bash. That's great!

- The `let` Command and `(( ))`
  - They are equivalent, both can be used to Evaluate arithmetic expressions.
  - If the value of the expression is non-zero, the return status is 0 (indicating success);
    otherwise the return status is 1 (indicating failure).

    ```shell
    (( 1 < 2 )); echo $?    # Returns 0
    (( 1 > 2 )); echo $?    # Returns 1
    ```

> Wu: We'd better use let command to evaluate arithmetic expressions.

##### 14.5.3 The if Command

- The if Command Format

  ```shell
  if command1; then command2; fi
  if test expression; then command; fi
  if [ string/numeric expression ]; then command; fi
  if [[ string expression ]]; then command; fi
  if (( numeric expression )); then command; fi
  ```

- The if/elif/else Command Format

  ```shell
  if command; then
    command(s)
  elif command; then
    command(s);
  else
    command(s)
  fi
  ```

##### 14.5.7 The null Command

- The null command
  - Represented by a colon, is a built-in, do-nothing command that returns an exit status of 0.
  - It is used as a placeholder after an if command when you have nothing to say,
    but need a command or the program will produce an error message because a command is required after the then statement.
  - Often the null command is used as an argument to a loop command to make the loop a forever loop.

  ```shell
  if expr "$number" + 0 >& /dev/null; then
    :    # null command
  else
    echo "You did not enter an integer value."
    exit 1
  fi
  ```

> Wu: I think using null command is ugly, I would try to avoid it.

##### 14.5.8 The case Command

- The case Command Format

  ```shell
  case variable in
  value1)
    command(s)
    ;;
  value2)
    command(s)
    ;;
  *)
    command(s)
    ;;
  esac
  ```

#### 14.6 Looping Commands

- If the for loop is not provided with a wordlist, it iterates through the positional parameters.

  ```shell
  for file; do    # This is the same as "for file in $*"
    echo ${file}
  done
  ```

> Wu: I think this is a terrible practice. Never do it!

- The until command
  - Like the while command, but executes the loop statements only if the command after until fails.

  ```shell
  until command; do
    command(s)
  done
  ```

- The select Command
  - A menu of numerically listed items is displayed to standard error.
  - The PS3 prompt is used to prompt the user for input; by default, PS3 is #?.
  - The input is stored in the special shell REPLY variable.
  - The LINES and COLUMNS variables can be used to determine the layout of the menu items displayed on the terminal.
  - Because the select command is a **looping** command,
    it is important to remember to use either the break command to get out of the loop, or the exit command to exit the script.

  ```shell
  select var in wordlist; do
    command(s)
  done
  ```

- Looping Control Commands
  - The shift Command
  - The break Command
  - The continue Command

- I/O Rediction and Subshells
  - Output from a bash loop can be sent to a file rather than to the screen.
  - Output can be either piped to another command(s) or redirected to a file.

- Loops can be executed to run in the background.

#### 14.7  Functions

- `unset -f function_name`
  - Remove a function from memory

- `export -f function_name`
  - Export a function

- `local name=val`
  - Create local variables that are private to the function and will disappear after the function exits.

- `return` or `return ${num}`
  - The return value of a function is really just the value of the exit status of the last command in the script,
    unless you give a specific argument to the return command.

### Q6：作者是怎么论述的？

### Q7：作者解决了什么问题？

### Q8：我有哪些疑问？

#### Q8.1 What is Word Splitting

- The shell scans the results of parameter expansion, command substitution, and arithmetic expansion
  that did  not  occur  within  double quotes for word splitting.

> Wu: So if the expansions is quoted, no word splitting occurs.

- Word splitting is performed on the results of almost all unquoted expansions.
  The result of the expansion is broken into separate words based on the characters of the IFS variable.

  ```shell
  var="This is a variable"
  ./run.sh $var    # Word splitting occurs: For run.sh, $# = 4
  ./run.sh "$var"  # No word splitting: For run.sh, $# = 1
  ```

> Wu: Read [Word Splitting][split] for more details.

  [split]: https://mywiki.wooledge.org/WordSplitting

### Q9：这一章说得有道理吗？为什么？

### Q10：如何拓展这一章？

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它？

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么？

- 对比zsh与bash的异同点？

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象？

### Q11：这一章和我有什么关系？
