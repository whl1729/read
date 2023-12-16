# 《A Tour of Go》分析笔记

## Q1: 这个文档属于哪一类别的文档

计算机 / 编程语言 / Go

## Q2：这个文档的内容是什么

通过编程示例来简单介绍 Go 语言的基本知识。

## Q3：这个文档的大纲是什么

- Basics
  - Packages, variables, and functions
    - Packages
    - Imports
    - Exported names
    - Functions
    - Multiple results
    - Named return values
    - Variables
    - Variables with initializers
    - Short variable declarations
    - Basic types
    - Zero values
    - Type conversions
    - Type inference
    - Constants
    - Numeric Constants
  - Flow control statements: for, if, else, switch and defer
    - For
    - For is Go's "While"
    - Forever
    - If
    - If with a short statement
    - If and else
    - Switch
    - Switch evaluation order
    - Switch with no condition
    - Defer
    - Stacking defers
  - More types: structs, slices, and maps
    - Pointers
    - Structs
    - Struct Fields
    - Pointers to structs
    - Struct Literals
    - Arrays
    - Slices
    - Slices are like references to arrays
    - Slice literals
    - Slice defaults
    - Slice length and capacity
    - Nil Slices
    - Creating a slice with make
    - Slices of slices
    - Appending to a slice
    - Range
    - Maps
    - Map literals
    - Mutating Maps
    - Function values
    - Function closures

- Methods and interfaces
  - Methods
  - Methods are functions
  - Pointer receivers
  - Pointers and functions
  - Methods and pointer indirection
  - Choosing a value or pointer receiver
  - interfaces
  - interfaces are implemented implicitly
  - interface values
  - interface values with nil underlying values
  - Nil interface values
  - The empty interface
  - Type assertions
  - Type switches
  - Stringers
  - Errors
  - Readers

- Generics
  - Type parameters
  - Generic types

- Concurrency
  - Goroutines
  - Channels
  - Buffered Channels
  - Range and Close
  - Select
  - Default Selection
  - sync.Mutex

## Q4：作者想要解决什么问题

## Q5：这个文档的关键词是什么

- factored import statement
- exported name

## Q6：这个文档的关键句是什么

### 1 Basics

#### 1.1 Packages, variables, and functions

- Packages
  - Every Go program is made up of packages.
  - Programs start running in package main.
  - By convention, the package name is the same as the last element of the import path.
    For instance, the "math/rand" package comprises files that begin with the statement package rand.

- Imports
  - It is good style to group the imports into a parenthesized, "factored" import statement.

- Exported names
  - In Go, a name is exported if it begins with a capital letter.
  - When importing a package, you can refer only to its exported names.
  - Any "unexported" names are not accessible from outside the package.

- Functions
  - In Go's function declaration, the type comes after the variable name.
  - When two or more consecutive named function parameters share a type,
    you can omit the type from all but the last.
  - A function can return any number of results.
  - Go's return values may be named.
    If so, they are treated as variables defined at the top of the function.

- [Go's declaration syntax][1]
  - The left-to-right style gain clarity.
  - One merit of this left-to-right style is how well it works as the types become more complex.
  - Go’s pointer syntax is tied to the familiar C form, but those ties mean that
    we cannot break completely from using parentheses to disambiguate types and expressions in the grammar.

> 伍注：现代编程语言的声明语法大多数都采用了「类型声明后置」的方式，比如 Python、TypeScript 等。

- Variables
  - The `var` statement declares a list of variables.
  - A `var` statement can be at package or function level.
  - A `var` declaration can include initializers, one per variable.
  - If an initializer is present, the type can be omitted;
    the variable will take the type of the initializer.
  - Inside a function, 
    the `:=` short assignment statement can be used in place of a `var` declaration with implicit type.
  - Outside a function,
    every statement begins with a keyword (`var`, `func`, and so on) and
    so the `:=` construct is not available.

- Basic types
  - The `int`, `uint`, and `uintptr` types are usually 32 bits wide on 32-bit systems and 64 bits wide on 64-bit systems.
  - When you need an integer value you should use `int`
    unless you have a specific reason to use a sized or unsigned integer type.

  ```go
  bool

  string

  int  int8  int16  int32  int64
  uint uint8 uint16 uint32 uint64 uintptr

  byte // alias for uint8

  rune // alias for int32
       // represents a Unicode code point

  float32 float64

  complex64 complex128
  ```

- Zero values
  - Variables declared without an explicit initial value are given their zero value.
  - The zero value is:
    - `0` for numeric types,
    - `false` for the boolean type, and
    - `""` (the empty string) for strings.

- Type conversions
  - The expression `T(v)` converts the value v to the type T.
  - Unlike in C, in Go assignment between items of different type requires an **explicit** conversion.

- Type inference
  - When the right hand side of the declaration is typed, the new variable is of that same type
  - when the right hand side contains an untyped numeric constant,
    the new variable may be an `int`, `float64`, or `complex128` depending on the precision of the constant

- Constants
  - Constants are declared like variables, but with the `const` keyword.
  - Constants cannot be declared using the `:=` syntax.
  - An untyped constant has a default type
    which is the type to which the constant is implicitly converted in contexts where a typed value is required

> 伍注：untyped constant 的 default type 是根据上下文推断出来的，跟变量的类型推断类似。

- Numeric Constants
  - Numeric constants are high-precision values.
  - An untyped constant takes the type needed by its context.

#### 1.2 Flow control statements: for, if, else, switch and defer

- For
  - Go has only one looping construct, the `for` loop.
  - The basic for loop has three components separated by semicolons:
    - the init statement: executed before the first iteration
    - the condition expression: evaluated before every iteration
    - the post statement: executed at the end of every iteration
  - Unlike other languages like C, Java, or JavaScript
    there are **no parentheses** surrounding the three components of the `for` statement
    and the braces `{ }` are always required.
  - The init and post statements are optional.
  - For is Go's "While"
  - Forever
    - If you omit the loop condition it loops forever,
      so an infinite loop is compactly expressed.

- If
  - The expression need not be surrounded by parentheses `()` but the braces `{}` are required.
  - The if statement can start with a short statement to execute before the condition.
  - Variables declared inside an `if` short statement are also available inside any of the `else` blocks.

- Switch
  - Go's switch is like the one in C, C++, Java, JavaScript, and PHP,
    except that Go only runs the selected case, not all the cases that follow.
    In effect,
    the break statement that is needed at the end of each case in those languages is provided automatically in Go.
  - Another important difference is that Go's switch cases need not be constants,
    and the values involved need not be integers.
  - Switch cases evaluate cases from top to bottom, stopping when a case succeeds.
  - Switch without a condition is the same as `switch true`.
    This construct can be a clean way to write long if-then-else chains.

- Defer
  - A defer statement defers the execution of a function until the surrounding function returns.
  - **The deferred call's arguments are evaluated immediately**,
    but the function call is not executed until the surrounding function returns.
  - Deferred function calls are pushed onto a stack.
    When a function returns, its deferred calls are executed in last-in-first-out order.

> 伍注：defer 关键字后面跟的是一个函数调用，虽然这个函数调用是在原函数退出前才执行，
> 但这个函数调用的输入参数是立即计算的（并非原函数退出前才计算）。

  ```go
  // Output: "foo: 1"
  func testDefer() {
	foo := 1

	defer func(foo int) {
		fmt.Printf("foo: %d\n", foo)
	}(foo)

	foo = 2
  }
  ```

#### 1.3 More types: structs, slices, and maps

- Pointers
  - The `&` operator generates a pointer to its operand.
  - The `*` operator denotes the pointer's underlying value.
  - Unlike C, Go has no pointer arithmetic.

- Structs
  - A `struct` is a collection of fields.
  - Pointer to structs has a shorthand notation.
  - Struct Literals
    - A struct literal denotes a newly allocated struct value by listing the values of its fields.
    - You can list just a subset of fields by using the Name: syntax. 
      (And the order of named fields is irrelevant.)

  ```go
  p.X
  // is equivalent to
  (*p).X
  ```

- Arrays
  - An array's length is part of its type, so arrays cannot be resized.
  - Go's arrays are values.
  - An array variable denotes the entire array; it is not a pointer to the first array element
    (as would be the case in C).
  - This means that **when you assign or pass around an array value you will make a copy of its contents.**
    (To avoid the copy you could pass a pointer to the array, but then that’s a pointer to an array, not an array.)
  - One way to think about arrays is as a sort of struct but with indexed rather than named fields: a fixed-size composite value.

- Slices
  - A slice is a dynamically-sized, flexible view into the elements of an array.
  - `a[low, high]` selects a **half-open** range which includes the first element, but excludes the last one.
  - Slices are like references to arrays
    - A slice does not store any data, it just describes a section of an underlying array.
    - Changing the elements of a slice modifies the corresponding elements of its underlying array.
    - Other slices that share the same underlying array will see those changes.
  - Slice literals
    - A slice literal is like an array literal without the length.
      eg: `[]bool{true, true, false}`
  - Slice defaults
    - The default is zero for the low bound and the length of the slice for the high bound.
  - Slice length and capacity
    - A slice has both a length and a capacity.
    - The length of a slice is the number of elements it contains.
    - The capacity of a slice is the number of elements in the underlying array, counting from the first element in the slice.
    - The length and capacity of a slice s can be obtained using the expressions len(s) and cap(s).
    - You can extend a slice's length by re-slicing it, provided it has sufficient capacity. 
  - Nil Slices
    - The zero value of a slice is nil.
    - A nil slice has a length and capacity of 0 and has no underlying array.
  - Creating a slice with make
  - Slices of slices
    - 伍注：Slices of slices 的长度可以不相同。
  - Appending to a slice
    - If the backing array of s is too small to fit all the given values a bigger array will be allocated.
    - The returned slice will point to the newly allocated array.
  - Range
    - When ranging over a slice, two values are returned for each iteration.
      The first is the index, and the second is a copy of the element at that index.
    - You can skip the index or value by assigning to `_`.
    - If you only want the index, you can omit the second variable.

    ```go
    s := [][]int{
        []int{1, 2, 3, 4, 5},
        []int{6, 7, 8, 9},
        []int{10, 11, 12},
    }
    ```

- Maps
  - The zero value of a map is nil. A nil map has no keys, nor can keys be added.
  - The make function returns a map of the given type, initialized and ready for use.
  - Map literals are like struct literals, but the keys are required.
  - If the top-level type is just a type name, you can omit it from the elements of the literal.
  - Mutating Maps (See following code block)

  ```go
  type Vertex struct {
	Lat, Long float64
  }

  var m = map[string]Vertex{
      "Bell Labs": {40.68433, -74.39967},
      "Google":    {37.42202, -122.08408},
  }

  // You don't need to Repeat the "Vertex" like the following:
  var m = map[string]Vertex{
      "Bell Labs": Vertex{40.68433, -74.39967},
      "Google":    Vertex{37.42202, -122.08408},
  }
  ```

  ```go
  // Insert or update an element in map m:
  m[key] = elem

  // Retrieve an element:
  elem = m[key]

  // Delete an element:
  delete(m, key)

  // Test that a key is present with a two-value assignment:
  // If key is in m, ok is true. If not, ok is false.
  // If key is not in the map, then elem is the zero value for the map's element type.
  elem, ok = m[key]
  ```

> 伍注：索引 go map 时，如果 key 不存在，不会抛异常，只是返回空值，跟 JavaScript 类似；Python 则会抛异常。

- Function values
  - Functions are values too. They can be passed around just like other values.
  - Function values may be used as function arguments and return values.

- Function closures
  - Go functions may be closures.
  - A closure is a function value that references variables from outside its body.
  - The function may access and assign to the referenced variables; in this sense the function is "bound" to the variables.

### 2 Methods and interfaces

- Methods
  - Go does not have classes. However, you can define methods on types.
  - A method is a function with a special receiver argument.
  - The receiver appears in its own argument list between the func keyword and the method name.
  - You can declare a method on non-struct types, too.
  - You can only declare a method with a receiver whose type is defined in the same package as the method.
  - You cannot declare a method with a receiver whose type is defined in another package.

- Pointer receivers
  - There are two reasons to use a pointer receiver.
    - The first is so that the method can modify the value that its receiver points to.
    - The second is to avoid copying the value on each method call.
      This can be more efficient if the receiver is a large struct.
  - Methods with pointer receivers can modify the value to which the receiver points.
  - methods with pointer receivers take either a value or a pointer as the receiver when they are called.
  - methods with value receivers take either a value or a pointer as the receiver when they are called.

> 伍注：Go 语言在 method receiver 这里同样制造了语法糖，就像之前在 pointer dereference 制造的语法糖那样。

- Interfaces
  - An interface type is defined as a set of method signatures.
  - A value of interface type can hold any value that implements those methods.
  - Interfaces are implemented implicitly
    - A type implements an interface by implementing its methods.
    - There is no explicit declaration of intent, no "implements" keyword.
    - Implicit interfaces decouple the definition of an interface from its implementation,
      which could then appear in any package without prearrangement.

> 伍注：虽然在调用成员/函数/方法时可以混淆 value 和 pointer，但在接口实现时不能混淆两者。
> 比如，某个 value type 以 pointer receiver 的方式实现了某接口，
> 那么可以将该 value type 的 pointer 变量赋值给对应接口类型的变量，
> 但不可以将该 value type 的变量赋值给对应接口类型的变量。
> 实测发现，反过来则可以，感觉这里有点不一致。

- Interface values
  - Under the hood, interface values can be thought of as a tuple of a value and a concrete type:
    `(value, type)`
  - An interface value holds a value of a specific underlying concrete type.
  - Calling a method on an interface value executes the method of the same name on its underlying type.

- Interface values with nil underlying values
  - If the concrete value inside the interface itself is nil, the method will be called with a nil receiver.
  - In some languages this would trigger a null pointer exception,
    but in Go it is common to write methods that gracefully handle being called with a nil receiver

- Nil interface values
  - A nil interface value holds neither value nor concrete type.
  - Calling a method on a nil interface is a **run-time error**
    because there is no type inside the interface tuple to indicate which concrete method to call.

> 伍注：注意以上两种 interface values 的区别，前者是已经确定具体类型，只是该类型的变量的取值为空值；
> 后者是还没确认具体类型，并且取值为空值。后者调用方法时必然崩溃；前者要看方法里是否有解引用操作，
> 如果有则崩溃，否则不会崩溃。

- The empty interface
  - The interface type that specifies zero methods is known as the empty interface:
    `interface{}`
  - An empty interface may hold values of any type.
    (Every type implements at least zero methods.)
  - Empty interfaces are used by code that handles values of unknown type.
    For example, fmt.Print takes any number of arguments of type interface{}.

- Type assertions
  - A type assertion provides access to an interface value's underlying concrete value.
  - To test whether an interface value holds a specific type, a type assertion can return two values:
    the underlying value and a boolean value that reports whether the assertion succeeded.

  ```go
  // asserts that the interface value i holds the concrete type T
  // and assigns the underlying T value to the variable t.
  // If i does not hold a T, the statement will trigger a panic.
  t := i.(T)

  // If i holds a T, then t will be the underlying value and ok will be true.
  // If not, ok will be false and t will be the zero value of type T, and no panic occurs.
  t, ok := i.(T)
  ```

- Type switches
  - A type switch is a construct that permits several type assertions in series.

  ```go
  switch v := i.(type) {
  case T:
      // here v has type T
  case S:
      // here v has type S
  default:
      // no match; here v has the same type as i
  }
  ```

- Stringers
  - A Stringer is a type that can describe itself as a string.
  - The `fmt` package (and many others) look for this interface to print values.

  ```go
  type Stringer interface {
    String() string
  }
  ```

- Errors
  - Go programs express error state with `error` values.
  - The `error` type is a built-in interface similar to `fmt.Stringer`.
  - Functions often return an `error` value,
    and calling code should handle errors by testing whether the `error` equals `nil`.
  - A nil `error` denotes success; a non-nil `error` denotes failure.

  ```go
  type error interface {
    Error() string
  }
  ```

- Readers
  - The io package specifies the io.Reader interface,
    which represents the read end of a stream of data.

  ```go
  func (T) Read(b []byte) (n int, err error)
  ```

### 3 Generics

- Type parameters
- Generic types

### 4 Concurrency

- Goroutines
  - A goroutine is a lightweight thread managed by the Go runtime.
  - `go f(x, y, z)` starts a new goroutine running `f(x, y, z)`
  - The evaluation of f, x, y, and z happens in the current goroutine
    and the execution of f happens in the new goroutine.
  - Goroutines run in the same address space, so access to shared memory must be synchronized.
  - The `sync` package provides useful primitives,
    although you won't need them much in Go as there are other primitives.

- Channels
  - Channels are a typed conduit through which you can send and receive values with the channel operator, `<-`.
  - By default, sends and receives block until the other side is ready.
  - This allows goroutines to synchronize without explicit locks or condition variables.

  ```go
  ch <- v    // Send v to channel ch.
  v := <-ch  // Receive from ch, and
             // assign value to v.
  // (The data flows in the direction of the arrow.)
  ```

- Buffered Channels
  - Channels can be buffered.
  - Provide the buffer length as the second argument to make to initialize a buffered channel.
  - Sends to a buffered channel block only when the buffer is full.
  - Receives block when the buffer is empty.

  ```go
  ch := make(chan int, 100)
  ```

- Range and Close
  - A sender can close a channel to indicate that no more values will be sent.
  - Receivers can test whether a channel has been closed
    by assigning a second parameter to the receive expression:
  - The loop `for i := range c` receives values from the channel repeatedly until it is closed.
  - Only the sender should close a channel, never the receiver.
  - Sending on a closed channel will cause a panic.
  - Channels aren't like files; you don't usually need to close them.
  - Closing is only necessary when the receiver must be told there are no more values coming,
    such as to terminate a range loop.

    ```go
    v, ok := <-ch
    // ok is false if there are no more values to receive and the channel is closed.
    ```

- Select
  - The `select` statement lets a goroutine wait on multiple communication operations.
  - A `select` blocks until one of its cases can run, then it executes that case.
  - It chooses one at random if multiple are ready.

  ```go
  func fibonacci(c, quit chan int) {
      x, y := 0, 1
      for {
          select {
          case c <- x:
              x, y = y, x+y
          case <-quit:
              fmt.Println("quit")
              return
          }
      }
  }
  ```

- Default Selection
  - The default case in a select is run if no other case is ready.
  - Use a default case to try a send or receive without blocking:

  ```go
  select {
  case i := <-c:
      // use i
  default:
      // receiving from c would block
  }
  ```

- sync.Mutex
  - We can define a block of code to be executed in mutual exclusion
    by surrounding it with a call to Lock and Unlock as shown on the Inc method.
  - We can also use defer to ensure the mutex will be unlocked as in the Value method.

## Q7：作者是怎么论述的

## Q8：作者解决了什么问题

## Q9：我有哪些疑问

### Q9.1 为什么 defer 语句的函数输入参数是立即计算的

### Q9.2 为什么 修改 slice 的右边界不会导致容量变化，修改左边界会导致容量变化

根据[Go Slices: usage and internals][2]，slice 的内部实现描述如下：

> A slice is a descriptor of an array segment.
> It consists of a pointer to the array, the length of the segment, and its capacity (the maximum length of the segment).

可见，slice 内部指针指向的是左边界，容量只能从左边界开始计算，所以修改左边界后容量必须跟着变化。

## Q10：这个文档说得有道理吗？为什么

## Q11: 这个文档讨论的知识的本质是什么

## Q12: 这个文档讨论的知识的第一原则是什么

## Q13：这个文档讨论的知识的结构是怎样的

## Q14：这个文档讨论的知识为什么是这样的？为什么发展成这样？为什么需要它

## Q15：有哪些相似的知识？它们之间的联系是什么

## Q16：其他领域/学科有没有相关的知识？日常生活中有没有类似的现象

## Q17: 这个文档对我有哪些用处/帮助/启示

## Q18: 我如何应用这个文档的知识去解决问题

  [1]: https://go.dev/blog/declaration-syntax
  [2]: https://go.dev/blog/slices-intro

