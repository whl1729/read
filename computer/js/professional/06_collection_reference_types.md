# 《Professional JavaScript for Web Developers》分析笔记

## Chapter 6: Collection Reference Types

### Q1：这一章的内容是什么

### Q2：这一章的大纲是什么

- The Object Type
- The Array Type
- Typed Arrays
- The Map Type
- The WeakMap Type
- The Set Type
- The WeakSet Type
- Iteration and Spread Operators

### Q3：作者想要解决什么问题

### Q4：这一章的关键词是什么

### Q5：这一章的关键句是什么

- SameValueZero

#### 6.1 The Object Type

- Two ways to explicitly create an instance of Object
  - Use the new operator with the Object constructor
  - Use object literal notation

- Two ways to access object properties
  - dot notation
  - bracket notation

- When to use bracket notation
  - When you need to use variables for property access
  - When the property name contains characters that would be either a syntax error or a keyword/reserved word

#### 6.2 The Array Type

- ECMAScript arrays are ordered lists of data, and they can hold **any type of data** in each slot.

- Four ways to creagte an array
  - Use the Array constructor
  - Use array literal notation
  - `Array.from()` convert array-like constructs into an array instance
  - `Array.of()` convert a collection of arguments into an array instance

- When Use the Array constructor with a single argument that is
  - a number: it will create an array with the given number of items
  - any other type: it will create a one-item array that contains the specific value

- Array Holes
  - Due to their bizarre behavior and performance issues, avoid using array holes in your code.
  - Prefer to use an explicit undefined in place of a hole.
  - Initializing an array with an array literal allows you to create "holes" using sequential commas.

- Array length
  - By setting the length property,
    you can easily remove items from or add items to the end of the array.
  - Arrays can contain a maximum of 4,294,967,295 items.
  - If you try to add more than that number, an exception occurs.
  - Trying to create an array with an initial size approaching this maximum may cause a long-running script error.

- `Array.isArray`
  - Determining whether a given object is an array.

- Iterator Methods
  - `keys()`
  - `values()`
  - `entries`
  - Destructure: `for (const [index, element] of arr.entries()) {}`

- Copy and Fill Methods
  - `fill()`
  - `copyWithin()`

- Conversion Methods
  - `toString()`
  - `valueOf()`
  - `toLocaleString()` calls each item's toLocaleString() instead of toString() to get its string value
  - `join()` construct a string with a different separator
  - If an item in the array is null or undefined, it is represented by an empty string
    in the result of join(), toLocaleString(), toString(), and valueOf().

- Stack Methods
  - `push()`
  - `pop()`

- Queue Methods
  - `push()` Enqueue at the end
  - `shift()` Dequeue at the front
  - `unshift()` Enqueue at the front
  - `pop()` Dequeue at the end

- Reording Methods
  - `reverse()`
  - `sort()`
    - Calls the String() casting function on every item and then compares the strings to determine the correct order.
      So you need to define a comparison function if you want to sort numbers.
    - Allows you to pass in a comparison function.

- Manipulation Methods
  - `concat()` Set `Symbol.isConcatSpreadable` to false if you want to prevent flattening.
  - `slice()`
  - `splice()`
    - Deletion: `splice(0, 2)`
    - Insertion: `splice(2, 0, 'red', 'green')`
    - Replacement: `splice(2, 1, 'red', 'green')`
    - always returns an array that contains any items that were removed from the array
      (or an empty array if no items were removed)

- Search and Location Methods
  - `indexOf()`
  - `lastIndexOf()`
  - `includes()`
  - `find()`
  - `findIndex()`

- Iterative Methods
  - `every()` Runs the given function on every item in the array and
              returns true if the function returns true for every item.
  - `filter()` Runs the given function on every item in the array and
               returns an array of all items for which the function returns true.
  - `forEach()` Runs the given function on every item in the array.
                This method has no return value.
  - `map()` Runs the given function on every item in the array and
            returns the result of each function call in an array.
  - `some()` Runs the given function on every item in the array and
             returns true if the function returns true for any one item.

- Reduction Methods
  - `reduce()`
  - `reduceRight()`
  - Both methods accept two arguments:
    a function to call on each item and an optional initial value upon which the reduction is based.
  - The function passed into reduce() or reduceRight() accepts four arguments:
    - the previous value,
    - the current value,
    - the item’s index,
    - and the array object.
  - Any value returned from the function is automatically passed in as the first argument for the next item.

#### 6.3 Typed Arrays

- What is Typed Arrays
  - The typed array is a construct designed for efficiently passing binary data to native libraries.
  - There is no actual "TypedArray" type in JavaScript—
    rather, the term refers to a collection of specialized arrays that contain numeric types.

- History
  - Rendering graphics-intensive applications inside the browser without requiring any plugins
  - The goal was to develop a JavaScript API that
    could make use of a 3D graphics API and GPU acceleration
    to enable rendering of complex graphics on a `<canvas>` element.
  - CanvasFloatArray -> Float32Array

- Using ArrayBuffers
  - An ArrayBuffer can never be resized once it is created.
  - However, you are able to copy all or part of an existing ArrayBuffer into a new instance using `slice()`.

- JavaScript's ArrayBuffer vs C++'s malloc
  - Failure Handling
    - When malloc() fails to allocate, it returns a null pointer.
    - If ArrayBuffer allocation fails, it throws an error.
  - Maximum size
    - A malloc() call can take advantage of virtual memory,
      so the maximum size of the allocation is only bounded by the addressable system memory.
    - ArrayBuffer allocation cannot exceed Number.MAX_SAFE_ INTEGER (2 ^ 53) bytes.
  - Initialization
    - A successful malloc() invocation performs no initialization of the actual addresses.
    - Declaring an ArrayBuffer initializes all the bits to 0s.
  - Garbage Collection
    - Heap memory allocated by malloc() cannot be used by the system until free() is invoked or the program exits.
    - Heap memory allocated by declaring an ArrayBuffer is still garbage collected—no manual memory management is required.

- DataViews
  - ElementType
    - get
    - set
    - byteOffset
  - Big-Endian vs Little-Endian
  - Corner Cases
    - A DataView will only complete a read or write if there is sufficient buffer space to do so;
      otherwise it throws a RangeError

- Typed Arrays
  - Typed arrays still use array buffers as their storage, and array buffers cannot be resized.
  - Therefore, the following methods are not supported by typed arrays:
    `concat, pop, push, shift, splice, unshift`
  - `set()` Copies the values from a provided array or typed array into the current typed array at the specified index.
  - `subarray()` Returns a new typed array with values copied out of the original.
  - Underflow and Overflow
    - `Uint8ClampedArray`

#### 6.4 The Map Type

- Basic API
  - `new Map()`
  - `has()`
  - `get()`
  - `set()`
  - `clear()`
  - `size`

- Order and Iteration
  - `entries()`
  - `Symbol.iterator`
  - `keys()`
  - `values()`

- Choosing Between Objects and Maps
  - For developers that care about memory and performance,
    there are notable differences between objects and maps that may be of interest.
  - Memory Profile: Map is better
    - Results may vary by browser,
      but given a fixed amount of memory,
      a Map will be able to store roughly 50 percent more key/value pairs than an Object.
  - Insertion Performance: Map is better
  - Lookup Performance: Object is better
  - Delete Performance: Map is Metter

#### 6.5 The WeakMap Type

- Why WeakMap
  - Avoid preventing garbage collection, so as to avoid memory leak

- WeakMap's keys
  - keys in a WeakMap are "weakly held,"
    meaning they are not counted as formal references that would otherwise prevent garbage collection.
  - Keys in a WeakMap can only be of type or inherit from Object.
  - If primitives were allowed,
    the WeakMap instance would have no way of differentiating
    between the string primitive that was initially used to set the key/value pair
    and an identical string primitive that was initialized later
    — an undesirable behavior. (Wu: Question: Not understand?)
  - Non-Iterable Keys

- Utility
  - Private Variables
  - DOM Node Metadata

#### 6.6 The Set Type

- Basic API
  - `new Set()`
  - `size()`
  - `add()`
  - `delete()`
  - `has()`

- Order and Iteration
  - A Set instance can provide an Iterator that contains the set contents in insertion order.
  - `values()`
  - `keys()` same as `values()`
  - `entries()` returns an iterator that contains a two-element array containing a duplicate of all values in the Set in insertion order
  - `Symbol.iterator`

#### 6.7 The WeakSet Type

- Similar to the WeakMap type.
- WeakSet are valuable to use for tagging objects.

### Q6：作者是怎么论述的

### Q7：作者解决了什么问题

### Q8：我有哪些疑问

### Q9：这一章说得有道理吗？为什么

### Q10：如何拓展这一章

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象

### Q11：这一章和我有什么关系
