# 《Professional JavaScript for Web Developers》分析笔记

## Chapter 4: Variables, Scope, and Memory

### Q1：这一章的内容是什么？

### Q2：这一章的大纲是什么？

#### 一级大纲

- Primitive and Reference Values
- Execution Context and Scope
- Garbage Collection

#### 二级大纲

- Primitive and Reference Values
  - Dynamic Properties
  - Copying Values
  - Argument Passing
  - Determining Type
- Execution Context and Scope
  - Scope Chain Augmentation
  - Variable Declaration
- Garbage Collection
  - Mark-and-Sweep
  - Reference Counting
  - Performance
  - Managing Memory
  - Object churn

### Q3：作者想要解决什么问题？

- Working with primitive and reference values in variables
- Understanding execution context
- Understanding garbage collection

### Q4：这一章的关键词是什么？

- Execution Context
- Scope Chain Augmentation
- Garbage Collection
- Hidden Class

### Q5：这一章的关键句是什么？

#### 4.1 Primitive and Reference Values

- ECMAScript variables may contain two different types of data:
  - Primitive values
    - Simple atomic pieces of data
    - The six primitive types: Undefined, Null, Boolean, Number, String and Symbol
  - Reference values
    - Objects that may be made up of multiple values.
    - JavaScript does not permit direct access of memory locations,
      so direct manipulation of the object’s memory space is not allowed.
    - When you manipulate an object,
      you’re really working on a reference to that object rather than the actual object itself.

- Strings are primitive values in ECMAScript
  - In many languages,
    strings are represented by objects and are therefore considered to be reference types.
  - ECMAScript breaks away from this tradition.

- Primitive vs Reference Values
  - Changing Properties
    - For reference values, you can add, change, or delete properties and methods at any time.
    - Primitive values can’t have properties added to them even though attempting to do so won’t cause an error. 
  - Coping Values
    - For primitive value,
      once the operation is complete, two variables can be used separately with no side effects.
    - For reference value, it is actually a pointer to an object stored on the heap.
      Once the operation is complete, two variables point to exactly the same object,
      so changes to one are reflected on the other.
  - If you were to use the new keyword, JavaScript will create an Object type.

  ```javascript
  let name1 = "Nicholas";
  let name2 = new String("Matt");
  name1.age = 27;
  name2.age = 26;
  console.log(name1.age); // undefined
  console.log(name2.age); // 26
  console.log(typeof name1); // string
  console.log(typeof name2); // object
  ```

- Argument Passing
  - All function arguments in ECMAScript are passed by value.
  - Think of function arguments in ECMAScript as nothing more than local variables.

- Determining Type
  - `typeof`
  - `instanceof`
    - Usage: `result = variable instanceof constructor`
    - Returns true if the variable is an instance of the given reference type.
    - Returns false if the variable is primitive value.
    - All reference values, by definition, are instances of Object.

#### 4.2 Execution Context and Scope

- Execution context
  - The execution context of a variable or function defines what other data it has access to,
    as well as how it should behave.
  - Each execution context has an associated variable object upon which all of its defined variables and functions exist.
  - This object is not accessible by code but is used behind the scenes to handle data.
  - When an execution context has executed all of its code, it is destroyed,
    taking with it all of the variables and functions defined within it

- The global execution context
  - In web browsers
    - The global context is the window object.
    - All global variables and functions defined with var are created as properties and methods on the window object.
    - Declarations using let and const at the top level are not defined in the global context.
  - In nodejs
    - The global context is the `global` object.

- Each function call has its own execution context.
  - context stack

- Scope chain
  - When code is executed in a context, a scope chain of variable objects is created.
  - The purpose of the scope chain is to provide ordered access to all variables and functions that an execution context has access to.
  - The front of the scope chain is always the variable object of the context whose code is executing.
  - The last of the scope chain is always the global context’s variable object.

- Activation object
  - If the context is a function, then the activation object is used as the variable object.
  - An activation object starts with a single defined variable called arguments.

- Identifier Resolution
  - Identifiers are resolved by navigating the scope chain in search of the identifier name.
  - The search always begins at the front of the chain and proceeds to the back until the identifier is found.

##### 4.2.1 Scope Chain Augmentation

- Two statements that add a variable object to the front of the scope chain
  - The catch block in a try-catch statement
  - A with statement

##### 4.2.2 Variable Declaration

- Scope Declaration
  - Global Scope: When a variable is initialized without first being declared
  - Function Scope Declaration Using `var`
  - Block Scope Declaration Using `let`
  - Constant Block Scope Declaration Using `const`

- `var` Hoisting
  - A var declaration will be brought to the top of the function or global scope and before any existing code inside it.

- The const declaration only applies to the top-level primitive or object.
  - A const variable assigned to an object cannot be reassigned to another reference value,
    but the keys inside that object are not protected.
  - If you wish to make the entire object immutable, you can use `Object.freeze()`,
    **although attempted property assignment will not raise errors; it will just silently fail.**

  ```javascript
  const o3 = Object.freeze({});
  o3.name = 'Jake';  // silently fail
  console.log(o3.name); // undefined
  ```

> Wu: Why not raise errors? I think this is a terrible design!

- Best practices for declaration
  - Use const as often as possible unless you really need a variable that can undergo reassignment.
  - This will allow you to catch an entire vein of reassignment bugs much earlier than you normally would.

- Identifier Lookup
  - Objects in the scope chain also have a **prototype chain**,
    so searching may include each object’s prototype chain.

#### 4.3 Garbage Collection

- Two Strategies for Garbage Collection
  - Mark-and-Sweep
  - Reference Counting
    - A serious issue: circular references

- Managing Memory
  - keep around only data that is necessary for the execution of your code.
  - When data is no longer necessary, it’s best to **set the value to null**, freeing up the reference—
    this is called dereferencing the value.
  - Performance Boosts with const and let Declarations.
  - Hidden Classes and the delete Operation.
    - During runtime, V8 will associate hidden classes for every object created to keep track of the shape of its properties.
    - Avoid JavaScript’s ready-fire-aim dynamic property assignment and instead declare all properties inside the constructor.
  - Memory Leaks
    - Accidentally declaring global variables
    - Interval timers
    - Closures
  - Static Allocation and Object Pools
    - For performance, you should minimize the number of garbage collection operations the browser performs.
    - One important metric measured by the browser to decide when to schedule garbage collection is the rate of **object churn**.
    - Object pool
    - In most cases, this is a form of premature optimization and is not appropriate.

  ```javascript
  let name = 'Jake';
  setInterval(() => {
    console.log(name);
  }, 100);
  ```

  ```javascript
  let outer = function() {
    let name = 'Jake';
    return function() {
      return name;
    };
  };
  ```

### Q6：作者是怎么论述的？

### Q7：作者解决了什么问题？

### Q8：我有哪些疑问？

#### Q8.1: What is execution context?

#### Q8.2: What is scope chain augmentation?

#### Q8.3: What is prototype chain?

### Q9：这一章说得有道理吗？为什么？

### Q10：如何拓展这一章？

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它？

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么？

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象？

### Q11：这一章和我有什么关系？

