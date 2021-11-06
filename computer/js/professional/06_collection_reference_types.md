# 《Professional JavaScript for Web Developers》分析笔记

## Chapter 6: Collection Reference Types

### Q1：这一章的内容是什么？

### Q2：这一章的大纲是什么？

- The Object Type
- The Array Type
- Typed Arrays
- The Map Type
- The WeakMap Type
- The Set Type
- The WeakSet Type
- Iteration and Spread Operators

### Q3：作者想要解决什么问题？

### Q4：这一章的关键词是什么？

### Q5：这一章的关键句是什么？

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
  -  Both methods accept two arguments:
     a function to call on each item and an optional initial value upon which the reduction is based.
  -  The function passed into reduce() or reduceRight() accepts four arguments:
    - the previous value,
    - the current value,
    - the item’s index,
    - and the array object.
  - Any value returned from the function is automatically passed in as the first argument for the next item.

#### 6.3 Typed Arrays

#### 6.4 The Map Type

#### 6.5 The WeakMap Type

#### 6.6 The Set Type

#### 6.7 The WeakSet Type

#### 6.8 Iteration and Spread Operators

### Q6：作者是怎么论述的？

### Q7：作者解决了什么问题？

### Q8：我有哪些疑问？

### Q9：这一章说得有道理吗？为什么？

### Q10：如何拓展这一章？

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它？

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么？

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象？

### Q11：这一章和我有什么关系？

