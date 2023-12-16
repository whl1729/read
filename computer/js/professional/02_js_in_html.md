# 《Professional JavaScript for Web Developers》分析笔记

## Chapter 2: JavaScript in HTML

### Q1：这一章的内容是什么

### Q2：这一章的大纲是什么

- The `<script>` Element
  - Tag Placement
  - Deferred Scripts
  - Asynchronous Scripts
  - Dynamic Script Loading
  - Changes in XHTML
  - Deprecated Syntax
- Inline Code vs External Files
- Document Modes
- The `<noscript>` Element

### Q3：作者想要解决什么问题

- Using the `<script>` element
- Comparing inline and external scripts
- Examining how document modes affect JavaScript
- Preparing for JavaScript-disabled experiences

### Q4：这一章的关键词是什么

- Deferred Scripts
- Asynchronous Scripts
- Dynamic Script Loading
- XHTML
- XML
- `<noscript>`
- CORS(Cross-Origin Resource Sharing)
- MIME(Multipurpose Internet Mail Extensions)
  - A standard that indicates the nature and format of a document, file, or assortment of bytes.

### Q5：这一章的关键句是什么

#### 2.1 The `<script>` Element

- Attributes for the `<script>` element:
  - async
    - Optional.
    - Indicates that the script should begin downloading immediately
      but should not prevent other actions on the page such as downloading resources or
      waiting for other scripts to load.
    - Valid only for external script files.
  - crossorigin
    - Optional.
    - Configures the CORS settings for the associated request; by default, CORS is not used at all.
    - `crossorigin="anonymous"` will configure the request for the file to not have the credentials flag set.
    - `crossorigin="use-credentials"` will set the credentials flag, meaning the outgoing request will include credentials.
  - defer
    - Optional.
    - Indicates that the execution of the script can safely be deferred until
      after the document’s content has been completely parsed and displayed.
    - Valid only for external scripts.
  - type
    - Optional.
    - Indicates the content type (also called MIME type) of the scripting language being used by the code block.
    - Traditionally, this value has always been "text/javascript".
    - If the value is module, the code is treated as an ES6 module and only then is eligible to use the import and export keywords.

- There are two ways to use the `<script>` element:
  - Embed JavaScript code directly into the page
    - You cannot have the string `</script>` anywhere in your code.
  - Include JavaScript from an external file.
  - Never mix the two ways.
    - A `<script>` element using the src attribute shouldn't include additional JavaScript code between the `<script>` and `</script>` tags.
    - If both are provided, the script file is downloaded and executed while the inline code is ignored.
  - The `<script>` element can include JavaScript files from outside domains.
  - The `<script>` elements are interpreted in the order in which they appear in the page
    so long as the defer and async attributes are not present.

- Tag Placement
  - Modern web applications typically include all JavaScript references in the `<body>` element, after the page content.

- Deferred Scripts
  - The purpose of defer is to indicate that a script won’t be changing the structure of the page as it executes.
  - It signals to the browser that download should begin immediately but execution should be deferred.
  - The scripts should also be executed in the order in which they appear.
  - In reality, though, deferred scripts don’t always execute in order or before the DOMContentLoaded event,
    so it’s best to include just one when possible.

- Asynchronous Scripts
  - similar to defer, async applies only to external scripts and signals the browser to begin downloading the file immediately.
  - Unlike defer, scripts marked as async are not guaranteed to execute in the order in which they are specified.
  - Purpose: Indicate that the page need not wait for the script to be downloaded and executed before continuing to load,
    and it also need not wait for another script to load and execute before it can do the same.
  - They should not modify the DOM as they are loading.
  - They are guaranteed to execute before the page’s load event and may execute before or after DOMContentLoaded.

- Dynamic Script Loading
  - You can create script elements and attaching them to the DOM.
  - By default, scripts that are created in this fashion are async.
  - To unify the dynamic script loading behavior, you can explicitly mark the tag as synchronous.

- Deprecated Syntax
  - Unless you are using XHTML or the `<script>` tag requests or wraps non-JavaScript,
    the best practice is to not specify a type attribute at all.

#### 2.2 Inline Code vs External Files

- It's a best practice to include as much JavaScript as possible using external files.
  - Maintainability
  - Caching
  - Future-proof

#### 2.3 Document Modes

- There are now three modes used by the layout engines in web browsers:
  - Quirks mode. Layout emulates nonstandard behavior in Navigator 4 and Internet Explorer 5.
  - Almost standards mode. There are only a very small number of quirks implemented.
  - Full standards mode. The behavior is (hopefully) the behavior described by the HTML and CSS specifications.

- To ensure that your page uses full standards mode, make sure that your page has a DOCTYPE like this: `<!DOCTYPE html>`

#### 2.4 The `<noscript>` Element

- The `<noscript>` HTML element defines a section of HTML to be inserted
  if a script type on the page is unsupported or if scripting is currently turned off in the browser.

### Q6：作者是怎么论述的

### Q7：作者解决了什么问题

### Q8：我有哪些疑问

### Q9：这一章说得有道理吗？为什么

### Q10：如何拓展这一章

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象

### Q11：这一章和我有什么关系
