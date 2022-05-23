# 《Professional JavaScript for Web Developers》笔记

## Chapter 01: What Is JavaScript

### Q1：这一章的内容是什么？

### Q2：这一章的大纲是什么？

- JavaScript History
- JavaScript Implementations
  - ECMAScript
  - The Document Object Model
  - The Browser Object Model
- JavaScript Versions

### Q3：作者想要解决什么问题？

### Q4：这一章的关键词是什么？

- ECMA(European Computer Manufacturers Association)
- TC39(Technical Committee #39)

### Q5：这一章的关键句是什么？

- JavaScript as a Client-side language

  - When JavaScript first appeared in 1995,
    its main purpose was to handle some of the input validation that had previously been left to server-side languages such as Perl.

- To begin down the path to using JavaScript’s full potential, it is important to understand its nature, history, and limitations.

#### 1.1 A Short History

- JavaScript was designed by a Netscape developer named **Brendan Eich** in 1995.

- How the name changed

  - Mocha -> LiveScript -> JavaScript
  - Netscape changed LiveScript’s name to JavaScript to capitalize on the buzz that Java was receiving from the press.

- Two JavaScript Versions

  - Shortly after Netscape Navigator 3 was released,
    Microsoft introduced Internet Explorer 3 with a JavaScript implementation called JScript in August 1996.
  - So there were two different JavaScript versions floating around:
    JavaScript in Netscape Navigator and JScript in Internet Explorer.

- JavaScript Standard

  - In 1997, JavaScript 1.1 was submitted to the European Computer Manufacturers Association (Ecma) as a proposal.
  - [Technical Committee #39 (TC39)][tc39] was assigned to "standardize the syntax and semantics of a general purpose, cross-platform, vendor-neutral scripting language".
  - Made up of programmers from Netscape, Sun, Microsoft, Borland, NOMBAS, and other companies with interest in the future of scripting,
    TC39 met for months to hammer out **ECMA-262**, a standard defining a new scripting language named **ECMAScript** (often pronounced as “ek-ma-script”).
  - The following year, the ISO/IEC  also adopted ECMAScript as a standard (ISO/IEC-16262).
  - Since that time, browsers have tried, with varying degrees of success, to use ECMAScript as a basis for their JavaScript implementations.

    [tc39]: www.ecma-international.org/memento/TC39.htm

> 伍注：
> 1. "ECMA-262"代表 JavaScript 的一个标准，其中的 262 是 ECMA 的标准代号，而不是版本号。
> 2. "ECMA-262, 6th edition"则代表我们说的 ES6 标准，其中的 6 才是版本号。
> 3. ISO/IEC: International Organization for Standardization and International Electrotechnical Commission

#### 1.2 JavaScript Implementations

- A complete JavaScript implementation is made up of the following three distinct parts:

  - The Core (ECMAScript)
  - The Document Object Model (DOM)
  - The Browser Object Model (BOM)

- ECMAScript's host environment

  - ECMAScript isn’t tied to web browsers.
  - Its host environments includes: web browsers, NodeJS, Adobe Flash and so on.

- On a very basic level, ECMAScript describes the following parts of the language:
  - Syntax
  - Types
  - Statements
  - Keywords
  - Reserved words
  - Operators
  - Global objects

##### 1.2.1 ECMAScript

##### 1.2.1.1 ECMAScript Editions

- The different versions of ECMAScript are defined as **editions**.

- The 1st edition, 1997
  - The first edition of ECMA-262 was essentially the same as Netscape's JavaScript 1.1
    but with all references to browser-specific code removed and a few minor changes:
    ECMA-262 required support for the Unicode standard (to support multiple languages) and that objects be platform-independent.

- The 2nd edition, 1998
  - The second edition of ECMA-262 was largely editorial.
  - The standard was updated to get into strict agreement with ISO/IEC-16262 and didn’t feature any additions, changes, or omissions.

- The 3rd edition, 1999
  - The third edition of ECMA-262 was the first real update to the standard.
  - It provided updates to string handling, the definition of errors, and numeric outputs.
  - It also added support for regular expressions, new control statements, try-catch exception handling, and small changes to better prepare the standard for internationalization.
  - To many, this marked the arrival of ECMAScript as a true programming language.

- The 4th edition (abandoned)
  - The fourth edition of ECMA-262 was a complete overhaul of the language.
  - The resulting specification defined an almost completely new language based on the third edition.
  - The fourth edition includes
    - strongly typed variables
    - new statements and data structures
    - true classes and classical inheritance
    - new ways to interact with data
  - The fourth edition of ECMA-262 was abandoned before officially being published.

- The 5th edition, 2009
  - The fifth edition sought to clarify perceived ambiguities of the third edition and introduce additional functionality.
  - The new functionality includes a native JSON object for parsing and serializing JSON data,
    methods for inheritance and advanced property definition,
    and the inclusion of a new strict mode that slightly augments how ECMAScript engines interpret and execute code.

- The 6th edition, 2015
  - Contains arguably the most important collection of enhancements to the specification since its inception.
  - ES6 adds formal support for classes, modules, iterators, generators, arrow functions, promises, reflection, proxies, and a host of new data types.

- The 7th edition, 2016
  - Included only a handful of syntactical additions such as `Array.prototype.includes` and the exponentiation operator.

- The 8th edition, 2017
  - Introduced Async Functions, Shared Memory, and Atomics along with smaller language and library enhancements, bug fixes, and editorial updates.
  - It also included new static methods on Object: `Object.values`, `Object.entries`, and `Object.getOwnPropertyDescriptors`.

> 伍注：本书只介绍到 2017 年，2018 年—2021 年的介绍摘自 ecma 官网和维基百科。

- The 9th Edition, 2018
  - New features include the spread operator, rest parameters, asynchronous iteration, Promise.prototype.finally and additions to RegExp.

- The 10th Edition, 2019
  - Added features include, but are not limited to, `Array.prototype.flat`, `Array.prototype.flatMap`, changes to `Array.sort` and `Object.fromEntries`.

- The 11th Edition, 2020
  - new functions
  - a `BigInt` primitive type for arbitrary-sized integers
  - the nullish coalescing operator
  - the globalThis object

- The 12th Edition, 2021
  - This version introduces the `replaceAll` method for strings;
  - `Promise.any`, a promise combinator that short-circuits when an input value is fulfilled;
  - `AggregateError`, a new error type to represent multiple errors at once;
  - logical assignment operators (`??=, &&=, ||=`);
  - `WeakRef`, for referring to a target object without preserving it from garbage collection,
  - `FinalizationRegistry`, to manage registration and unregistration of cleanup operations performed when target objects are garbage collected;
  - separators for numeric literals (1_000);
  - `Array.prototype.sort` was made more precise, reducing the amount of cases that result in an implementation-defined sort order.

##### 1.2.1.2 What Does ECMAScript Conformance Mean

- ECMA-262 lays out the definition of ECMAScript conformance.

- To be considered an implementation of ECMAScript, an implementation must do the following:
  - Support all "types, values, objects, properties, functions, and program syntax and semantics" as they are described in ECMA-262.
  - Support the Unicode character standard.

- Additionally, a conforming implementation may do the following:
  - Add "additional types, values, objects, properties, and functions" that are not specified in ECMA-262.
    ECMA-262 describes these additions as primarily new objects or new properties of objects not given in the specification.
  - Support "program and regular expression syntax" that is not defined in ECMA-262
    (meaning that the built-in regular-expression support is allowed to be altered and extended).

##### 1.2.1.3 ECMAScript Support in Web Browsers

- By 2008, the five major web browsers (Internet Explorer, Firefox, Safari, Chrome, and Opera) all complied with the third edition of ECMA-262.

#### 1.2.2 The Document Object Model

- The Document Object Model (DOM) is an application programming interface (API) for XML that was extended for use in HTML.

- The DOM maps out an entire page as a hierarchy of nodes.
  Each part of an HTML or XML page is a type of node containing different kinds of data.

- Why the DOM Is Necessary
  - something had to be done to preserve the cross-platform nature of the web.
  - The fear was that if someone didn’t rein in Netscape and Microsoft,
    the web would develop into two distinct factions that were exclusive to targeted browsers.

- DOM vs JavaScript
  - The DOM is not JavaScript-specific and indeed has been implemented in numerous other languages.
  - For web browsers, however, the DOM has been implemented using ECMAScript and now makes up a large part of the JavaScript language.

> 伍注：DOM 作为一个标准，并不只存在于 JavaScript 中（还有不少语言也实现了这个标准），也不只应用于浏览器场景。

##### 1.2.2.1 DOM Levels

- DOM Level 0
  - Note that there is no standard called DOM Level 0; it is simply a reference point in the history of the DOM.
  - DOM Level 0 is considered to be the original DHTML supported in Internet Explorer 4.0 and Netscape Navigator 4.0.

- DOM Level 1
  - DOM Level 1 became a W3C recommendation in October 1998.
  - It consisted of two modules:
    - The DOM Core, which provided a way to map the structure of an XML-based document to allow for easy access to and manipulation of any part of a document,
    - The DOM HTML, which extended the DOM Core by adding HTML-specific objects and methods.

- DOM Level 2
  - Added support for mouse and userinterface events (long supported by DHTML), ranges, and traversals (methods to iterate over a DOM document),
    and support for Cascading Style Sheets (CSS) through object interfaces.
  - The original DOM Core introduced in Level 1 was also extended to include support for XML namespaces.
  - Introduced the following new modules of the DOM to deal with new types of interfaces:
    - DOM views: Describes interfaces to keep track of the various views of a document (the document before and after CSS styling, for example)
    - DOM events: Describes interfaces for events and event handling
    - DOM style: Describes interfaces to deal with CSS-based styling of elements
    - DOM traversal and range: Describes interfaces to traverse and manipulate a document tree

- DOM Level 3
  - Further extends the DOM with the introduction of methods to load and save documents in a uniform way (contained in a new module called DOM Load and Save)
    and methods to validate adocument (DOM Validation).
  - The DOM Core is extended to support all of XML 1.0, including XML Infoset, XPath, and XML Base.

- DOM4
  - Presently, the W3C no longer maintains the DOM as a set of levels, but rather as the DOM Living Standard, snapshots of which are termed DOM4.
  - Among its introductions is the addition of Mutation Observers to replace Mutation Events.

##### 1.2.2.2 Other DOMs

- Aside from the DOM Core and DOM HTML interfaces, several other languages have had their own DOM standards published.

- The languages in the following list are XML-based, and each DOM adds methods and interfaces unique to a particular language:
  - Scalable Vector Graphics (SVG) 1.0
  - Mathematical Markup Language (MathML) 1.0
  - Synchronized Multimedia Integration Language (SMIL)

- Additionally, other languages have developed their own DOM implementations, such as Mozilla’s XML User Interface Language (XUL).
  - However, only the languages in the preceding list are standard recommendations from W3C.

##### 1.2.2.3 DOM Support in Web Browsers

- The DOM had been a standard for some time before web browsers started implementing it.

#### 1.2.3 The Browser Object Model

- The Internet Explorer 3 and Netscape Navigator 3 browsers featured a Browser Object Model (BOM) that allowed access and manipulation of the browser window.

- Using the BOM, developers can interact with the browser outside of the context of its displayed page.

- BOM Standard
  - What made the BOM truly unique, and often problematic, was that it was the only part of a JavaScript implementation that had **no related standard**.
  - This changed with the introduction of **HTML5**, which sought to codify much of the BOM as part of a formal specification.
  - Thanks to HTML5, a lot of the confusion surrounding the BOM has dissipated.

- Primarily, the BOM deals with the browser window and frames, but generally any browser-specific extension to JavaScript is considered to be a part of the BOM.

- The following are some such extensions:
  - The capability to pop up new browser windows
  - The capability to move, resize, and close browser windows
  - The `navigator` object, which provides detailed information about the browser
  - The `location` object, which gives detailed information about the page loaded in the browser
  - The `screen` object, which gives detailed information about the user’s screen resolution
  - The `performance` object, which gives detailed information about the browser’s memory consumption, navigational behavior, and timing statistics
  - Support for cookies
  - Custom objects such as `XMLHttpRequest` and Internet Explorer’s `ActiveXObject`

#### 1.3 JavaScript Versions

- Mozilla, as a descendant from the original Netscape, is the only browser vendor that has continued the original JavaScript version-numbering sequence.

> 伍注：Mozilla 维护的 JavaScript 版本与 ECMAScript 版本没有关联。事实上我们不必关注这一节，知道有这么一回事就可以了。

### Q6：作者是怎么论述的？

### Q7：作者解决了什么问题？

### Q8：我有哪些疑问？

### Q9：这一章说得有道理吗？为什么？

### Q10：如何拓展这一章？

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它？

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么？

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象？

### Q11：这一章和我有什么关系？
