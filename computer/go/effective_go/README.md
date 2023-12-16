# 《Effective Go》分析笔记

## Q1：这本书属于哪一类别的书

计算机/编程语言/Go

## Q2：这本书的内容是什么

## Q3：这本书的大纲是什么

- Introduction
  - Examples
- Formatting
- Commentary
- Names
  - Package names
  - Getters
  - Interface names
  - MixedCaps
- Semicolons
- Control structures
  - If
  - Redeclaration and reassignment
  - For
  - Switch
  - Type switch
- Functions
  - Multiple return values
  - Named result parameters
  - Defer
- Data
  - Allocation with new
  - Constructors and composite literals
  - Allocation with make
  - Arrays
  - Slices
  - Two-dimensional slices
  - Maps
  - Printing
  - Append
- Initialization
  - Constants
  - Variables
  - The init function
- Methods
  - Pointers vs. Values
- Interfaces and other types
  - Interfaces
  - Conversions
  - Interface conversions and type assertions
  - Generality
  - Interfaces and methods
- The blank identifier
  - The blank identifier in multiple assignment
  - Unused imports and variables
  - Import for side effect
  - Interface checks
- Embedding
- Concurrency
  - Share by communicating
  - Goroutines
  - Channels
  - Channels of channels
  - Parallelization
  - A leaky buffer
- Errors
  - Panic
  - Recover
- A web server

## Q4：作者想要解决什么问题

## Q5：这本书的关键词是什么

## Q6：这本书的关键句是什么

### Introduction

- Examples
  - The [Go package sources][1] are intended to serve not only as the core library but also as examples of how to use the language.

### Formatting

- run `gofmt` to format your code

- Indentation
  - We use tabs for indentation and gofmt emits them by default. Use spaces only if you must.

- Line length
  - Go has no line length limit.
  - If a line feels too long, wrap it and indent with an extra tab.

- Parentheses
  - Go needs fewer parentheses than C and Java:
    control structures (if, for, switch) do not have parentheses in their syntax.
  - The operator precedence hierarchy is shorter and clearer
    eg: `x<<8 + y<<16` means what the spacing implies, unlike in the other languages.

### Commentary

- [Go Doc Comments][2]

### Names

- Package names
  - By convention, packages are given lower case, single-word names; there should be no need for underscores or mixedCaps.
  - Another convention is that the package name is the base name of its source directory.
  - The importer of a package will use the name to refer to its contents,
    so exported names in the package can use that fact to avoid repetition.

  ```go
  // Avoid repetition

  // Good:
  bufio.Reader()

  // Bad:
  bufio.BufReader()

  // Good:
  ring.New()

  // Bad:
  ring.NewRing()
  ```

- Getters
  - Go doesn't provide automatic support for getters and setters.
  - It's neither idiomatic nor necessary to put Get into the getter's name.

- Interface names
  - By convention, one-method interfaces are named by the method name plus an `-er` suffix or similar modification to construct an agent noun:
    Reader, Writer, Formatter, CloseNotifier etc.
  - If your type implements a method with the same meaning as a method on a well-known type,
    give it the same name and signature;
    call your string-converter method String not ToString.

- MixedCaps
  - The convention in Go is to use MixedCaps or mixedCaps rather than underscores to write multiword names.

### Semicolons

- The Go source code is mostly free of semicolons.

- Idiomatic Go programs have semicolons only in places such as for loop clauses, to separate the initializer, condition, and continuation elements.

- One consequence of the semicolon insertion rules
  - You cannot put the opening brace of a control structure (if, for, switch, or select) on the next line.
  - If you do, a semicolon will be inserted before the brace, which could cause unwanted effects. 

### Control structures

- The control structures of Go are related to those of C but differ in important ways.
  - There is no do or while loop, only a slightly generalized for;
  - switch is more flexible;
  - if and switch accept an optional initialization statement like that of for;
  - break and continue statements take an optional label to identify what to break or continue;
  - and there are new control structures including a type switch and a multiway communications multiplexer, select.

- The syntax is also slightly different: there are no parentheses and the bodies must always be brace-delimited.

- If
  - Since if and switch accept an initialization statement, it's common to see one used to set up a local variable.

- For
  - If you're looping over an array, slice, string, or map, or reading from a channel, a `range` clause can manage the loop.

- Switch
  - There is no automatic fall through, but cases can be presented in comma-separated lists.

- Type switch
  - If the switch declares a variable in the expression, the variable will have the corresponding type in each clause.
  - It's also idiomatic to reuse the name in such cases, in effect declaring a new variable with the same name but a different type in each case.

  ```go
  var t interface{}
  t = functionOfSomeType()
  switch t := t.(type) {
  default:
      fmt.Printf("unexpected type %T\n", t)     // %T prints whatever type t has
  case bool:
      fmt.Printf("boolean %t\n", t)             // t has type bool
  case int:
      fmt.Printf("integer %d\n", t)             // t has type int
  case *bool:
      fmt.Printf("pointer to boolean %t\n", *t) // t has type *bool
  case *int:
      fmt.Printf("pointer to integer %d\n", *t) // t has type *int
  }
  ```

### Functions

- Multiple return values
  - It can obviates the need to pass a pointer to a return value to simulate a reference parameter.

  ```go
  func nextInt(b []byte, i int) (int, int) {
      for ; i < len(b) && !isDigit(b[i]); i++ {
      }
      x := 0
      for ; i < len(b) && isDigit(b[i]); i++ {
          x = x*10 + int(b[i]) - '0'
      }
      return x, i
  }
  ```

- Named result parameters
  - The names are not mandatory but they can make code shorter and clearer: they're documentation.

- Defer
  - Release resources
  - Trace function execution

### Data

- Allocation with `new`
  - It does not initialize the memory, it only zeros it.

  ```go
  type SyncedBuffer struct {
      lock    sync.Mutex
      buffer  bytes.Buffer
  }

  p := new(SyncedBuffer)  // type *SyncedBuffer
  var v SyncedBuffer      // type  SyncedBuffer
  ```

- Constructors and composite literals
  - A composite literal is an expression that creates a new instance each time it is evaluated.
  - Composite literals can also be created for arrays, slices, and maps, with the field labels being indices or map keys as appropriate. 

  ```go
  // snippet from some function
  f := File{fd, name, nil, 0}
  return &f

  // refactor 1
  return &File{fd, name, nil, 0}

  // refactor 2
  return &File{fd: fd, name: name}
  ```

  ```go
  // Enone, Eio and Einval are integral constants
  a := [...]string   {Enone: "no error", Eio: "Eio", Einval: "invalid argument"}
  s := []string      {Enone: "no error", Eio: "Eio", Einval: "invalid argument"}
  m := map[int]string{Enone: "no error", Eio: "Eio", Einval: "invalid argument"}
  ```

- Allocation with `make`
  - The built-in function `make(T, args)` serves a purpose different from `new(T)`.
  - It creates slices, maps, and channels only, and it returns an initialized (not zeroed) value of type T (not *T).
  - The reason for the distinction is that these three types represent references to data structures that must be initialized before use. 
  - Remember that make applies only to maps, slices and channels and does not return a pointer.
  - To obtain an explicit pointer allocate with new or take the address of a variable explicitly.

  ```go
  var p *[]int = new([]int)       // allocates slice structure; *p == nil; rarely useful
  var v  []int = make([]int, 100) // the slice v now refers to a new array of 100 ints

  // Unnecessarily complex:
  var p *[]int = new([]int)
  *p = make([]int, 100, 100)

  // Idiomatic:
  v := make([]int, 100)
  ```

- Arrays
  - There are major differences between the ways arrays work in Go and C. In Go,
    - Arrays are values. Assigning one array to another copies all the elements.
    - In particular, if you pass an array to a function, it will receive a copy of the array, not a pointer to it.
    - The size of an array is part of its type. The types [10]int and [20]int are distinct.
  - If you want C-like behavior and efficiency, you can pass a pointer to the array.
    - But even this style isn't idiomatic Go. Use slices instead.

- Slices
  - The `append` must return the slice afterwards because,
    - although `append` can modify the elements of slice,
      the slice itself (the run-time data structure holding the pointer, length, and capacity) is passed by value.
  - Two-dimennsional slices
    - Because slices are variable-length, it is possible to have each inner slice be a different length.

- Maps
  - A set can be implemented as a map with value type bool.
    Set the map entry to true to put the value in the set, and then test it by simple indexing.
  - Use the "comma ok" idiom to distinguish a missing entry from a zero value.
  - Use the blank identifier (`_`) to test for presence in the map without worrying about the actual value.
  - It's safe to use the `delete` built-in function even if the key is already absent from the map.

- Printing
  - `Printf` vs `Print`
  - The numeric formats such as `%d` do not take flags for signedness or size;
    instead, the printing routines use the type of the argument to decide these properties.
  - Use the catchall format `%v` (for "value") for the default conversion
  - `%+v` annotates the fields of the structure with their names
  - `%#v` prints the value in full Go syntax.
  - `%q` uses the quoted string format.
  - `%#q` uses backquotes for the string.
  - `%x` works on strings, byte arrays and byte slices as well as on integers, generating a long hexadecimal string,
  - With a space in the format (`% x`) it puts spaces between the bytes.
  - Custom control: Define a method with the signature `String()` string on the type.
  - **Don't construct a String method by calling Sprintf in a way that will recur into your String method indefinitely.**
  - Another printing technique is to pass a print routine's arguments directly to another such routine.

- Append
  - The result needs to be returned because the underlying array may change.
  - That's why append is built in: it needs support from the compiler.

### Initialization

- Constants
  - They are created at compile time, even when defined as locals in functions.
    So `math.Sin(math.Pi/4)` is not because the function call to `math.Sin` needs to happen at run time.
  - They can only be numbers, characters (runes), strings or booleans.
  - `iota`
    - Its value is the index of the respective ConstSpec in that constant declaration, starting at zero.
    - Within a parenthesized const declaration list the expression list may be omitted from any but the first ConstSpec.


  ```go
  // 仅需第一行的 const 语句提供 iota 表达式，后面的 const 语句可以省略 iota 表达式。
  const (
      bit0, mask0 = 1 << iota, 1<<iota - 1  // bit0 == 1, mask0 == 0  (iota == 0)
      bit1, mask1                           // bit1 == 2, mask1 == 1  (iota == 1)
      _, _                                  //                        (iota == 2, unused)
      bit3, mask3                           // bit3 == 8, mask3 == 7  (iota == 3)
  )
  ```

- Variables
  - Variables can be initialized just like constants but the initializer can be a general expression computed at run time.

- The init function
  - `init` is called after all the variable declarations in the package have evaluated their initializers,
  - and those are evaluated only after all the imported packages have been initialized.
  - A common use of init functions is to verify or repair correctness of the program state before real execution begins.

### Methods

- Pointers vs. Values
  - value methods can be invoked on pointers and values, but pointer methods can only be invoked on pointers.
  - There is a handy exception, though.
    When the value is addressable,
    the language takes care of the common case of invoking a pointer method on a value by inserting the address operator automatically. 

> 伍注：不是所有的 value 都可以调用 pointer method，比如函数返回值就不可以。参考[stack overflow][3]。

### Interfaces and other types

- Conversions
  - It's an idiom in Go programs to convert the type of an expression to access a different set of methods.

- Interface conversions and type assertions
  - Type switches
  - Type Assertions
  - the "comma, ok" idiom

- Generality
  - If a type exists only to implement an interface and will never have exported methods beyond that interface,
    there is no need to export the type itself.
  - Exporting just the interface makes it clear the value has no interesting behavior beyond what is described in the interface.
  - In such cases, the constructor should return an interface value rather than the implementing type.

> 伍注：不太理解 Generality 这一节的应用意义，以后结合实践再理解一下。

### The blank identifier

- The blank identifier in multiple assignment
  - It is terrible practice to discard the error value in order to ignore the error.

- Unused imports and variables
  - When a program is under active development, unused imports and variables often arise
    and it can be annoying to delete them just to have the compilation proceed,
    only to have them be needed again later.
  - The blank identifier provides a workaround.

  ```go
  package main

  import (
      "fmt"
      "io"
      "log"
      "os"
  )

  var _ = fmt.Printf // For debugging; delete when done.
  var _ io.Reader    // For debugging; delete when done.
  ```

- Import for side effect
  - Sometimes it is useful to import a package only for its side effects, without any explicit use.
  - For example, during its init function, the `net/http/pprof` package registers HTTP handlers that provide debugging information.

- Interface checks
  - Use a global declaration with a blank identifier to check whether a type implements an interface

  ```go
  var _ json.Marshaler = (*RawMessage)(nil)
  ```

### Embedding

- Interface embedding

- Strct embedding

- Embedding types introduces the problem of name conflicts but the rules to resolve them are simple.
  - First, a field or method X hides any other item X in a more deeply nested part of the type.
  - Second, if the same name appears at the same nesting level, it is usually an error.
    However, if the duplicate name is never mentioned in the program outside the type definition, it is OK.

### Concurrency

- Share by communicating
  - Do not communicate by sharing memory; instead, share memory by communicating.
  - Although Go's approach to concurrency originates in Hoare's Communicating Sequential Processes (CSP),
    it can also be seen as a type-safe generalization of Unix pipes.

- Goroutines
  - A goroutine has a simple model:
    it is a function executing concurrently with other goroutines in the same address space.
  - It is lightweight, costing little more than the allocation of stack space.
    And the stacks start small, so they are cheap, and grow by allocating (and freeing) heap storage as required.
  - A function literal can be handy in a goroutine invocation.
    - In Go, function literals are closures:
      the implementation makes sure the variables referred to by the function survive as long as they are active.

- Channels
  - Unbuffered channels combine communication—the exchange of a value—with synchronization—
    guaranteeing that two calculations (goroutines) are in a known state.
  - A buffered channel can be used like a semaphore, for instance to limit throughput.
  - It may seem odd to write `req := req` but it's legal and idiomatic in Go to do this.

- Channels of channels
  - One of the most important properties of Go is that
    a channel is a first-class value that can be allocated and passed around like any other.
  - A common use of this property is to implement safe, parallel demultiplexing.
  - 伍注：Channels of channels 的一类情况是：我们可以向 channels 写一些数据，这些数据中又包含有 channels

- Parallelization
  - Parallelize a calculation across multiple CPU cores.
  - If the calculation can be broken into separate pieces that can execute independently,
    it can be parallelized, with a channel to signal when each piece completes.
  - Go is a concurrent language, not a parallel one, and not all parallelization problems fit Go's model.

### Error

- Error
  - When feasible, error strings should identify their origin,
    such as by having a prefix naming the operation or package that generated the error. 
  - Callers that care about the precise error details can use a type switch or a type assertion to look for specific errors and extract details.

- Panic
  - Real library functions should avoid panic.
  - One possible counterexample is during initialization:
    if the library truly cannot set itself up, it might be reasonable to panic, so to speak.

- Recover
  - When panic is called, including implicitly for run-time errors such as indexing a slice out of bounds or failing a type assertion,
    it immediately stops execution of the current function and begins unwinding the stack of the goroutine,
    running any deferred functions along the way.
    If that unwinding reaches the top of the goroutine's stack, the program dies.
  - A call to `recover` stops the unwinding and returns the argument passed to panic.
  - Because the only code that runs while unwinding is inside deferred functions,
    `recover` is only useful inside deferred functions.

## Q7：作者是怎么论述的

## Q8：作者解决了什么问题

## Q9：我有哪些疑问

### Q9.1: `append` 或 `make` 这些 built in 函数是怎么实现的

### Q9.2: Go channel 是怎样实现的

## Q10：这本书说得有道理吗？为什么

## Q11: 这本书讨论的知识的本质是什么

## Q12: 这本书讨论的知识的第一原则是什么

## Q13：这本书讨论的知识的结构是怎样的

## Q14：这本书讨论的知识为什么是这样的？为什么发展成这样？为什么需要它

## Q15：有哪些相似的知识？它们之间的联系是什么

## Q16：其他领域/学科有没有相关的知识？日常生活中有没有类似的现象

## Q17: 这本书对我有哪些用处/帮助/启示

## Q18: 我如何应用这本书的知识去解决问题

  [1]: https://go.dev/src/
  [2]: https://go.dev/doc/comment
  [3]: https://stackoverflow.com/a/46956348

