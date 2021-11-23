# 《Professional JavaScript for Web Developers》分析笔记

## Chapter 8: Objects, Classes, and Object-Oriented Programming

### Q1：这一章的内容是什么？

### Q2：这一章的大纲是什么？

- Understanding Objects
  - Types of Properties
    - Data Properties
    - Accessor Properties
  - Defining Multiple Properties
    - `Object.defineProperties`
  - Reading Property Attributes
    - `Object.getOwnPropertyDescriptors`
  - Merging Objects
    - `Object.assign`
  - Object Identity and Equality
    - `Object.is` and `===`
  - Enhanced Object Syntax
    - Property Value Shorthand: `let person = { name }`
    - Computed Property Keys: `let person = { [nameKey]: 'Guo Jing' }`
    - Concise Method Syntax: omit the function keyword
  - Object Destructuring
    - Nested Destructuring
    - Partial Destructuring Completion
    - Parameter Context Matching
- Object creation
  - The Factory Pattern
    - `function createPerson(name, age, job) {}`
  - The Function Constructor Pattern
    - `let person = new Person('Guo Jing', 20, 'Soldier')`
    - Constructors as Functions
    - Problems with Constructors
      - Waste of memory
  - The Prototype Pattern
    - How Prototypes Work
      - `Person.prototype.constructor === Person`
      - `person1.__proto__ === Person.prototype`
    - Understanding the Prototype Hierarchy
      - First instance, then prototype
    - Prototypes and the "in" Operator
    - Property Enumeration Order
  - Object Iteration
    - Alternate Prototype Syntax
    - Dynamic Nature of Prototypes
    - Native Object Prototypes
    - Problems with Prototypes
- Inheritance
  - Prototype Chaining
    - Default Prototypes
      - An instance of `Object`
    - Prototype and Instance Relationships
    - Working with Methods
    - Problems with Prototype Chaining
  - Constructor Stealing
    - Passing Arguments
    - Problems with Constructor Stealing
  - Combination Inheritance
  - Prototypal Inheritance
  - Parasitic Inheritance
  - Parasitic Combination Inheritance
- Classes
  - Class Definition Basics
    - Class Composition
  - The Class Constructor
    - Instantiation
    - Understanding Classes as Special Functions
  - Instance, Prototype and Class Members
    - Instance Members
    - Prototype Methods and Accessors
    - Static Class Methods and Accessors
    - Non-Function Prototype and Class Members
    - Iterator and Generator Methods
  - Inheritance
    - Inheritance Basics
    - Constructors, HomeObjects, and super()
    - Abstract Base Classes
    - Inheriting from Built-in Types
    - Class Maxins

### Q3：作者想要解决什么问题？

### Q4：这一章的关键词是什么？

- Prototype
- Prototype Chaining
- Constructor Stealing
- Combination Inheritance
- Prototypal Inheritance
- Parasitic Inheritance
- Parasitic Combination Inheritance
- `apply()`
  - calls a function with a given this value, and arguments provided as an array.
- `call()`
  - calls a function with a given this value and arguments provided individually.
  - allows for a function/method belonging to one object to be assigned and called for a different object.

### Q5：这一章的关键句是什么？

- What is an object
  - An unordered collection of properties
  - An array of values in no particular order
  - Hash tables:
    nothing more than a grouping of name-value pairs
    where the value may be data or a function

#### 8.1 Understanding Objects

- Types of Properties
  - Data Properties: Contain a single location for a **data value**
    - `[[Configurable]]`
    - `[[Enumerable]]`
    - `[[Writable]]`
    - `[[Value]]`
  - Accessor Properties: contain a combination of a getter function and a setter function
    - `[[Configurable]]`
    - `[[Enumerable]]`
    - `[[Get]]`
    - `[[Set]]`

- Defining Multiple Properties
  - `Object.defineProperties()`

- Reading Property Attributes
  - `Object.getOwnPropertyDescriptor()`
  - `Object.getOwnPropertyDescriptors()`

- Merging Objects: `Object.assign()`
  - for each source object copies the enumerable and own  properties onto the destination object.
  - shallow copy

- Object Identity and Equality
  - `===`
  - `Object.is()`

- Enhanced Object Syntax
  - Property Value Shorthand
  - Computed Property Keys
  - Concise Method Syntax

- Object Destructuring
  - Nested Destructuring
  - Partial Destructing Completion
  - Parameter Context Matching

#### 8.2 Object creation

##### 8.2.2 The Function Constructor Pattern

- Calling a constructor using the new operator will do the following:
 - A new object is created in memory.
 - The new object's internal `[[Prototype]]` pointer is assigned to the constructor's prototype property.
 - The this value of the constructor is assigned to the new object (so this points to the new object).
 - The code inside the constructor is executed (adds properties to the new object).
 - If the constructor function returns a non-null value, that object is returned.
   Otherwise, the new object that was just created is returned.

- Constructor functions vs normal functions
  - The only difference is the way in which they are called
  - Any function that is called with the new operator acts as a constructor,
    whereas any function called without it acts as a normal function.

- The this object always points to the Global object (window in web browsers)
  when a function is called without an explicitly set this value
  (by being an object method or through `call()/apply()`).

- The major downside to constructors is that methods are created once for each instance.

##### 8.2.3 The Prototype Pattern

- Each function is created with a prototype property,
  which is an object containing properties and methods that should be available to instances of a particular reference type.

- The benefit of using the prototype is that all of its properties and methods are shared among object instances.

- How Prototypes Work
  - All prototypes automatically get a property called constructor
    that points back to the function on which it is a property.
    E.g., `Person.prototype.constructor === Person`
  - A direct link exists between the instance and the constructor’s prototype: `__proto__`
  - `isPrototypeOf`
  - `getPrototypeOf`
  - `setPrototypeOf`

- Understanding the Prototype Hierarchy
  - The search begins on the object instance first, then on the prototype.
  - Property name shadowing
    - Once a property is added to the object instance, it shadows any properties of the same name on the prototype.
    - Use the delete operator to remove the instance property, which allows the prototype property to be accessed again.
    - The `hasOwnProperty()` method determines if a property exists on the instance or on the prototype.

- Prototype and the "in" Operator
  - the in operator returns true when a property of the given name is accessible by the object,
    which is to say that the property may exist on the instance or on the prototype.
  - `Object.keys()` returns a list of all **enumerable instance properties** on an object.
  - `Object.getOwnPropertyNames()` returns a list of all instance properties.
  - `Object.getOwnPropertySymbols()` returns a list of all instance symbols.

- Property Enumeration Order
  - `for-in, Object.keys()`
    - no deterministic order of enumeration
  - `Object.getOwnPropertyNames(), Object.getOwnPropertySymbols(), Object.assign()`
    - First number keys
    - Then string and symbol keys enumerated in insertion order

##### 8.2.4 Object Iteration

- Converting an object's contents
  - `Object.values()` returns an array of the object's values.
  - `Object.entries()` returns an array of array pairs, each representing a `[key, value]` pair in the object.

- Alternate Prototype Syntax
  - `Person.prototype = {}` the constructor property no longer points to Person.

- Dynamic Nature of Prototypes
  - Overwriting the prototype on the constructor means that new instances will reference the new prototype
    while any previously existing object instances still reference the old prototype.

- Problems with Prototypes
  - it negates the ability to pass initialization arguments into the constructor,
    meaning that all instances get the same property values by default.
  - All properties on the prototype are shared among instances.

#### 8.3 Inheritance

##### 8.3.1 Prototype Chaining

- Default Prototypes
  - All reference types inherit from Object by default, which is accomplished through prototype chaining.
  - The default prototype for any function is an instance of Object.

- Prototype and Instance Relationships
  - `instanceof` returns true whenever an instance is used with a constructor that appears in its prototype chain
  - `isPrototypeOf` returns true for an instance in the prototype chain

- Working with Methods
  - The object literal approach to creating prototype methods cannot be used with prototype chaining
    because you end up overwriting the chain.

- Problems with Prototype Chaining
  - Prototype properties containing reference values are shared with all instances.
  - You cannot pass arguments into the supertype constructor when the subtype instance is being created.

##### 8.3.2 Constructor Stealing

- Basic idea
  - call the supertype constructor from within the subtype constructor.

- Implementation
  - the apply() and call() methods can be used to execute a constructor on the newly created object.

- One advantage that constructor stealing offers over prototype chaining
  - the ability to **pass arguments** into the supertype constructor from within the subtype constructor.

- Problems with Constructor Stealing
  - Methods must be defined inside the constructor, so there's no function reuse.
  - Methods defined on the supertype's prototype are not accessible on the subtype,
    so all types can use only the constructor pattern.

##### 8.3.3 Combination Inheritance

- Definition
  - combines prototype chaining and constructor stealing to get the best of each approach.

- Basic idea
  - use prototype chaining to inherit properties and methods on the prototype and
    use constructor stealing to inherit instance properties.

- Problems
  - The supertype constructor is always called twice:
    - once to create the subtype’s prototype,
    - once inside the subtype constructor.

##### 8.3.4 Prototypal Inheritance

- `Object.create()` accepts two arguments
  - The first is an object to use as the prototype for a new object
  - The second is an optional object defining additional properties to apply to the new object

- Problems
  - Properties containing reference values will always share those values

##### 8.3.5 Parasitic Inheritance

- Basic Idea
  - create a function that does the inheritance,
    augments the object in some way,
    and then returns the object as if it did all the work.

- Problems
  - Adding functions to objects using parasitic inheritance leads to inefficiencies related to function reuse.

##### 8.3.6 Parasitic Combination Inheritance

- Basic Idea
  - Instead of calling the supertype constructor to assign the subtype’s prototype,
    all you need is a copy of the supertype’s prototype.

#### 8.4 Classes

### Q6：作者是怎么论述的？

### Q7：作者解决了什么问题？

### Q8：我有哪些疑问？

#### Q8.1: P255 "Defining Multiple Properties"一节的例子中，为什么修改year失败？

### Q9：这一章说得有道理吗？为什么？

### Q10：如何拓展这一章？

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它？

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么？

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象？

### Q11：这一章和我有什么关系？

