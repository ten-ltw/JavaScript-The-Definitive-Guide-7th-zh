---
title: "第 1 章 JavaScript 概述"
date: 2020-11-02T22:18:42+08:00
---

JavaScript is the programming language of the web. The overwhelming majority of websites use JavaScript, and all modern web browsers—on desktops, tablets, and phones—include JavaScript interpreters, making JavaScript the most-deployed programming language in history. Over the last decade, Node.js has enabled JavaScript programming outside of web browsers, and the dramatic success of Node means that JavaScript is now also the most-used programming language among software developers. Whether you’re starting from scratch or are already using JavaScript professionally, this book will help you master the language.

> JavaScript 是 web 的编程语言。绝大多数的网站都使用 JavaScript，所有的现代网络浏览器——台式机、平板电脑和手机——都包括 JavaScript 解释器，这使得 JavaScript 成为历史上部署最多的编程语言。在过去的十年中，Node.js 使得 JavaScript 编程可以在 web 浏览器之外进行，Node 的巨大成功意味着 JavaScript 现在也是软件开发人员最常用的编程语言。无论你是从零开始还是已经开始专业地使用 JavaScript，这本书都会帮助你掌握这门语言。

If you are already familiar with other programming languages, it may help you to know that JavaScript is a high-level, dynamic, interpreted programming language that is well-suited to object-oriented and functional programming styles. JavaScript’s variables are untyped. Its syntax is loosely based on Java, but the languages are otherwise unrelated. JavaScript derives its first-class functions from Scheme and its prototype-based inheritance from the little-known language Self. But you do not need to know any of those languages, or be familiar with those terms, to use this book and learn JavaScript.

> 如果您已经熟悉了其他编程语言，那么了解 JavaScript 是一种高级的、动态的、解释的编程语言可能会对您有所帮助，它非常适合面向对象和函数式编程风格。JavaScript 的变量是无类型的。它的语法不严格地讲基于 Java，但是这两种语言在其他方面是无关的。JavaScript 的 first-class 类型函数衍生于 Scheme，从鲜为人知的 Self 继承基于原型的函数。但您不需要了解任何这些语言，或熟悉这些术语，以使用这本书和学习 JavaScript。

The name “JavaScript” is quite misleading. Except for a superficial syntactic resemblance, JavaScript is completely different from the Java programming language. And JavaScript has long since outgrown its scripting-language roots to become a robust and efficient general-purpose language suitable for serious software engineering and projects with huge codebases.

> “JavaScript”这个名称很容易引起误解。除了表面上的语法相似之外，JavaScript 与 Java 编程语言完全不同。而且 JavaScript 早已超越了它的脚本语言根基，成为一种健壮、高效的通用语言，适合于具有巨大代码库的严肃软件工程和项目。

#### JAVASCRIPT: NAMES, VERSIONS, AND MODES

JavaScript was created at Netscape in the early days of the web, and technically, “JavaScript” is a trademark licensed from Sun Microsystems (now Oracle) used to describe Netscape’s (now Mozilla’s) implementation of the language. Netscape submitted the language for standardization to ECMA—the European Computer Manufacturer’s Association—and because of trademark issues, the standardized version of the language was stuck with the awkward name “ECMAScript.” In practice, everyone just calls the language JavaScript. This book uses the name “ECMAScript” and the abbreviation “ES” to refer to the language standard and to versions of that standard.

> JavaScript 是在网络早期由网景公司创建的，从技术上讲，“JavaScript”是 Sun Microsystems（现在的 Oracle）授权的商标，用来描述 Netscape 公司（现在的Mozilla 公司）对该语言的实现。Netscape 公司将这种语言提交给欧洲计算机制造商协会（ecma）进行标准化，但由于商标问题，这种语言的标准化版本只能使用一个尴尬的名字“ECMAScript”。实际上，每个人都称这种语言为 JavaScript。本书使用名称“ECMAScript”和缩写“ES”来表示该语言标准和该标准的版本。

For most of the 2010s, version 5 of the ECMAScript standard has been supported by all web browsers. This book treats ES5 as the compatibility baseline and no longer discusses earlier versions of the language. ES6 was released in 2015 and added major new features—including class and module syntax—that changed JavaScript from a scripting language into a serious, general-purpose language suitable for large-scale software engineering. Since ES6, the ECMAScript specification has moved to a yearly release cadence, and versions of the language—ES2016, ES2017, ES2018, ES2019, and ES2020—are now identified by year of release.

> 对于2010年代的大多数版本，所有 web 浏览器都支持 ECMAScript 标准的第5版。本书将 ES5 作为兼容性基线，不再讨论该语言的早期版本。ES6 于2015年发布，增加了主要的新特性（包括类和模块语法），使 JavaScript 从一种脚本语言变成了一种严肃的、适用于大规模软件工程的通用语言。自 ES6 以来，ECMAScript 规范已经以每年发布一次为基调，该语言的版本——es2016、ES2017、ES2018、ES2019和es2020——现在以发布年份来确定。

As JavaScript evolved, the language designers attempted to correct flaws in the early (pre-ES5) versions. In order to maintain backward compatibility, it is not possible to remove legacy features, no matter how flawed. But in ES5 and later, programs can opt in to JavaScript’s strict mode in which a number of early language mistakes have been corrected. The mechanism for opting in is the “use strict” directive described in §5.6.3. That section also summarizes the differences between legacy JavaScript and strict JavaScript. In ES6 and later, the use of new language features often implicitly invokes strict mode. For example, if you use the ES6 class keyword or create an ES6 module, then all the code within the class or module is automatically strict, and the old, flawed features are not available in those contexts. This book will cover the legacy features of JavaScript but is careful to point out that they are not available in strict mode.

> 随着 JavaScript 的发展，语言设计者试图纠正早期版本（es5 之前）的缺陷。为了保持向后兼容性，不可能删除遗留特性，无论其缺陷有多大。但在 ES5 及以后版本中，程序可以选择使用 JavaScript 的严格模式，在这种模式中，早期的一些语言错误已经得到了纠正。选择加入的机制是 §5.6.3 中描述的“严格使用”指令。这一节还总结了传统 JavaScript 和严格 JavaScript 之间的区别。在 ES6 及以后版本中，使用新的语言特性通常会隐式地调用 strict 模式。例如，如果您使用 ES6 类关键字或创建 ES6 模块，那么类或模块中的所有代码将自动严格，并且在这些上下文中不能使用旧的、有缺陷的特性。这本书将涵盖 JavaScript 的遗留特性，但小心地指出，它们在严格模式下是不可用的。

To be useful, every language must have a platform, or standard library, for performing things like basic input and output. The core JavaScript language defines a minimal API for working with numbers, text, arrays, sets, maps, and so on, but does not include any input or output functionality. Input and output (as well as more sophisticated features, such as networking, storage, and graphics) are the responsibility of the “host environment” within which JavaScript is embedded.

> 每种语言都必须有一个平台或标准库来执行基本输入和输出之类的操作。核心 JavaScript 语言定义了一个极小的 API 处理数字、文本、数组、集合、映射等，但不包括任何输入或输出功能。输入和输出（以及更复杂的特性，如网络、存储和图形）由嵌入 JavaScript 的“宿主”负责。

The original host environment for JavaScript was a web browser, and this is still the most common execution environment for JavaScript code. The web browser environment allows JavaScript code to obtain input from the user’s mouse and keyboard and by making HTTP requests. And it allows JavaScript code to display output to the user with HTML and CSS.

> JavaScript 的原始宿主环境是一个 web 浏览器，这仍然是 JavaScript 代码最常见的执行环境。web 浏览器环境允许 JavaScript 代码通过发送 HTTP 请求从用户的鼠标和键盘获取输入。它允许 JavaScript 代码用 HTML 和 CSS 向用户显示输出。

Since 2010, another host environment has been available for JavaScript code. Instead of constraining JavaScript to work with the APIs provided by a web browser, Node gives JavaScript access to the entire operating system, allowing JavaScript programs to read and write files, send and receive data over the network, and make and serve HTTP requests. Node is a popular choice for implementing web servers and also a convenient tool for writing simple utility scripts as an alternative to shell scripts.

> 从2010年开始，另一个宿主已经可以用于 JavaScript 代码。Node 没有限制 JavaScript 使用 web 浏览器提供的 api，而是允许 JavaScript 访问整个操作系统，允许 JavaScript 程序读和写文件，通过网络发送和接收数据，以及发出和服务 HTTP 请求。Node 是实现 web 服务器的常用选择，也是编写简单实用程序脚本的方便工具，可以作为 shell 脚本的替代。

Most of this book is focused on the JavaScript language itself. Chapter 11 documents the JavaScript standard library, Chapter 15 introduces the web browser host environment, and Chapter 16 introduces the Node host environment.

> 这本书的大部分内容都集中在 JavaScript 语言本身。第 11 章介绍了 JavaScript 标准库，第 15 章介绍了 web 浏览器宿主，第 16 章介绍了 Node 宿主。

This book covers low-level fundamentals first, and then builds on those to more advanced and higher-level abstractions. The chapters are intended to be read more or less in order. But learning a new programming language is never a linear process, and describing a language is not linear either: each language feature is related to other features, and this book is full of cross-references—sometimes backward and sometimes forward—to related material. This introductory chapter makes a quick first pass through the language, introducing key features that will make it easier to understand the in-depth treatment in the chapters that follow. If you are already a practicing JavaScript programmer, you can probably skip this chapter. (Although you might enjoy reading Example 1-1 at the end of the chapter before you move on.)

> 这本书首先介绍了底层基础知识，然后在这些基础上构建更高级和更高级别的抽象。这些章节的目的是让读者或多或少地按顺序阅读。但是学习一种新的编程语言从来都不是一个线性的过程，描述一种语言也不是线性的：每一种语言的特性都与其他特性相关，这本书充满了交叉引用——有时向后，有时向前的相关材料。这一介绍性章节对该语言进行了一次快速的介绍，并介绍了一些关键特性，这些特性将使后续章节的深入处理更容易理解。如果你已经是一个实践 JavaScript 程序员，你可以跳过这一章。（尽管你可能会喜欢阅读本章末尾的示例 1-1，然后再继续阅读。）

## 1.1 Exploring JavaScript

When learning a new programming language, it’s important to try the examples in the book, then modify them and try them again to test your understanding of the language. To do that, you need a JavaScript interpreter.

> 在学习一门新的编程语言时，试一试书中的示例是很重要的，然后修改它们，再试一次来测试你对这门语言的理解。为此，需要一个 JavaScript 解释器。

The easiest way to try out a few lines of JavaScript is to open up the web developer tools in your web browser (with F12, Ctrl-Shift-I, or Command-Option-I) and select the Console tab. You can then type code at the prompt and see the results as you type. Browser developer tools often appear as panes at the bottom or right of the browser window, but you can usually detach them as separate windows (as pictured in Figure 1-1), which is often quite convenient.

> 尝试几行 JavaScript 的最简单方法是在web浏览器中打开 web developer 工具（使用 F12、Ctrl-Shift-I 或 Command-Option-I）并选择 Console 选项卡。然后可以在提示符处键入代码，并在键入时查看结果。浏览器开发人员工具通常以窗格的形式出现在浏览器窗口的底部或右侧，但是您通常可以将它们分离为单独的窗口（如图1-1所示），这通常非常方便。

<Figures figure="1-1">The JavaScript console in Firefox’s Developer Tools</Figures>

Another way to try out JavaScript code is to download and install Node from https://nodejs.org. Once Node is installed on your system, you can simply open a Terminal window and type node to begin an interactive JavaScript session like this one:

> 另一种尝试 JavaScript 代码的方法是从[https://nodejs.org](https://nodejs.org)下载并安装 Node。一旦在你的系统上安装了 Node，你可以简单地打开一个终端窗口，输入 Node 来开始一个交互式的 JavaScript 会话，就像这样：

```sh
$ node
Welcome to Node.js v12.13.0.
Type ".help" for more information.
> .help
.break    Sometimes you get stuck, this gets you out
.clear    Alias for .break
.editor   Enter editor mode
.exit     Exit the repl
.help     Print this help message
.load     Load JS from a file into the REPL session
.save     Save all evaluated commands in this REPL session to a file

Press ^C to abort current expression, ^D to exit the repl
> let x = 2, y = 3;
undefined
> x + y
5
> (x === 2) && (y === 3)
true
> (x > 3) || (y < 3)
false
```
## 1.2 Hello World

When you are ready to start experimenting with longer chunks of code, these line-by-line interactive environments may no longer be suitable, and you will probably prefer to write your code in a text editor. From there, you can copy and paste to the JavaScript console or into a Node session. Or you can save your code to a file (the traditional filename extension for JavaScript code is .js) and then run that file of JavaScript code with Node:

> 当您准备开始尝试更长的代码块时，这些逐行交互环境可能不再适合，您可能更喜欢在文本编辑器中编写代码。从那里，您可以复制并粘贴到JavaScript控制台或节点会话中。或者你可以将你的代码保存到一个文件中（传统的 JavaScript 代码的文件名扩展名是 .js），然后用 Node 运行该 JavaScript 代码文件:

```sh
$ node snippet.js
```

If you use Node in a noninteractive manner like this, it won’t automatically print out the value of all the code you run, so you’ll have to do that yourself. You can use the function console.log() to display text and other JavaScript values in your terminal window or in a browser’s developer tools console. So, for example, if you create a hello.js file containing this line of code:

> 如果像这样以非交互的方式使用 Node，它不会自动打印出您运行的所有代码的值，因此您必须自己执行。可以使用 console.log() 函数在终端窗口或浏览器的 developer tools 控制台中显示文本和其他 JavaScript 值。因此，例如，如果你创建一个 hello.js 文件，其中包含这行代码:

```js
console.log("Hello World!");
```

and execute the file with node hello.js, you’ll see the message “Hello World!” printed out.

> 并执行 `node hello.js` ，你会看到消息“Hello World!”打印出来。

If you want to see that same message printed out in the JavaScript console of a web browser, create a new file named hello.html, and put this text in it:

> 如果您想在 web 浏览器的 JavaScript 控制台中看到同样的消息打印出来，那么创建一个名为 hello.html 的文件，并把这段文字放进去：

```js
<script src="hello.js"></script>
```

Then load hello.html into your web browser using a `file://` URL like this one:

> 然后使用 `file://` URL将 hello.html 加载到浏览器中，如下图所示：

```
file:///Users/username/javascript/hello.html
```

Open the developer tools window to see the greeting in the console.

> 打开 developer tools 窗口，在控制台中查看问候语。

## 1.3 A Tour of JavaScript

This section presents a quick introduction, through code examples, to the JavaScript language. After this introductory chapter, we dive into JavaScript at the lowest level: Chapter 2 explains things like JavaScript comments, semicolons, and the Unicode character set. Chapter 3 starts to get more interesting: it explains JavaScript variables and the values you can assign to those variables.

> 本节通过代码示例快速介绍 JavaScript 语言。在这一介绍性章节之后，我们将深入到 JavaScript 的底层:第 2 章说明了 JavaScript 注释、分号和 Unicode 字符集等内容。第 3 章开始变得更有趣：它说明了 JavaScript 变量和你可以为这些变量赋值的值。

Here’s some sample code to illustrate the highlights of those two chapters:

> 下面是一些示例代码，演示这两章的重点内容：

```js
// Anything following double slashes is an English-language comment.
// Read the comments carefully: they explain the JavaScript code.

// A variable is a symbolic name for a value.
// Variables are declared with the let keyword:
let x;                     // Declare a variable named x.

// Values can be assigned to variables with an = sign
x = 0;                     // Now the variable x has the value 0
x                          // => 0: A variable evaluates to its value.

// JavaScript supports several types of values
x = 1;                     // Numbers.
x = 0.01;                  // Numbers can be integers or reals.
x = "hello world";         // Strings of text in quotation marks.
x = 'JavaScript';          // Single quote marks also delimit strings.
x = true;                  // A Boolean value.
x = false;                 // The other Boolean value.
x = null;                  // Null is a special value that means "no value."
x = undefined;             // Undefined is another special value like null.
```

Two other very important types that JavaScript programs can manipulate are objects and arrays. These are the subjects of Chapters 6 and 7, but they are so important that you’ll see them many times before you reach those chapters:

> JavaScript 程序可以操作的另外两种非常重要的类型是对象和数组。这些是第 6 章和第 7 章的主题，但它们非常重要，在你读到这些章节之前，你会多次看到它们：

```js
// JavaScript's most important datatype is the object.
// An object is a collection of name/value pairs, or a string to value map.
let book = {               // Objects are enclosed in curly braces.
    topic: "JavaScript",   // The property "topic" has value "JavaScript."
    edition: 7             // The property "edition" has value 7
};                         // The curly brace marks the end of the object.

// Access the properties of an object with . or []:
book.topic                 // => "JavaScript"
book["edition"]            // => 7: another way to access property values.
book.author = "Flanagan";  // Create new properties by assignment.
book.contents = {};        // {} is an empty object with no properties.

// Conditionally access properties with ?. (ES2020):
book.contents?.ch01?.sect1 // => undefined: book.contents has no ch01 property.

// JavaScript also supports arrays (numerically indexed lists) of values:
let primes = [2, 3, 5, 7]; // An array of 4 values, delimited with [ and ].
primes[0]                  // => 2: the first element (index 0) of the array.
primes.length              // => 4: how many elements in the array.
primes[primes.length-1]    // => 7: the last element of the array.
primes[4] = 9;             // Add a new element by assignment.
primes[4] = 11;            // Or alter an existing element by assignment.
let empty = [];            // [] is an empty array with no elements.
empty.length               // => 0

// Arrays and objects can hold other arrays and objects:
let points = [             // An array with 2 elements.
    {x: 0, y: 0},          // Each element is an object.
    {x: 1, y: 1}
];
let data = {                 // An object with 2 properties
    trial1: [[1,2], [3,4]],  // The value of each property is an array.
    trial2: [[2,3], [4,5]]   // The elements of the arrays are arrays.
};
```

#### COMMENT SYNTAX IN CODE EXAMPLES

You may have noticed in the preceding code that some of the comments begin with an arrow (=>). These show the value produced by the code before the comment and are my attempt to emulate an interactive JavaScript environment like a web browser console in a printed book.

> 您可能已经注意到，在前面的代码中，一些注释以箭头开头（=>）。这些代码显示了注释之前代码产生的值，我试图模拟交互式 JavaScript 环境，就像印刷书籍中的 web 浏览器控制台一样。

Those // => comments also serve as an assertion, and I’ve written a tool that tests the code and verifies that it produces the value specified in the comment. This should help, I hope, to reduce errors in the book.

> 那些 // => 注释也用作断言，我编写了一个工具来测试代码并验证它是否生成注释中指定的值。我希望这有助于减少书中的错误。

There are two related styles of comment/assertion. If you see a comment of the form // a == 42, it means that after the code before the comment runs, the variable a will have the value 42. If you see a comment of the form // !, it means that the code on the line before the comment throws an exception (and the rest of the comment after the exclamation mark usually explains what kind of exception is thrown).

> 注释和断言有两种相关的风格。如果您看到 `// a == 42` 形式的注释，这意味着在注释运行之前的代码之后，变量a的值将是42。如果您看到 `// !` 形式的注释，这意味着注释前一行的代码抛出一个异常（感叹号之后的注释的其余部分通常解释抛出的是哪种异常）。

You’ll see these comments used throughout the book.

> 您将在整本书中看到这些注释。

The syntax illustrated here for listing array elements within square braces or mapping object property names to property values inside curly braces is known as an initializer expression, and it is just one of the topics of Chapter 4. An expression is a phrase of JavaScript that can be evaluated to produce a value. For example, the use of . and [] to refer to the value of an object property or array element is an expression.

> 这里演示的在方括号内列出数组元素或在花括号内将对象属性名映射到属性值的语法称为初始化表达式，它只是第 4 章的主题之一。表达式是 JavaScript 的一个短语，可以计算它来产生一个值。例如，的使用。和 [] 引用对象属性或数组元素的值是一个表达式。

One of the most common ways to form expressions in JavaScript is to use operators:

> 在 JavaScript 中形成表达式最常见的方法之一是使用运算符：

```js
// Operators act on values (the operands) to produce a new value.
// Arithmetic operators are some of the simplest:
3 + 2                      // => 5: addition
3 - 2                      // => 1: subtraction
3 * 2                      // => 6: multiplication
3 / 2                      // => 1.5: division
points[1].x - points[0].x  // => 1: more complicated operands also work
"3" + "2"                  // => "32": + adds numbers, concatenates strings

// JavaScript defines some shorthand arithmetic operators
let count = 0;             // Define a variable
count++;                   // Increment the variable
count--;                   // Decrement the variable
count += 2;                // Add 2: same as count = count + 2;
count *= 3;                // Multiply by 3: same as count = count * 3;
count                      // => 6: variable names are expressions, too.

// Equality and relational operators test whether two values are equal,
// unequal, less than, greater than, and so on. They evaluate to true or false.
let x = 2, y = 3;          // These = signs are assignment, not equality tests
x === y                    // => false: equality
x !== y                    // => true: inequality
x < y                      // => true: less-than
x <= y                     // => true: less-than or equal
x > y                      // => false: greater-than
x >= y                     // => false: greater-than or equal
"two" === "three"          // => false: the two strings are different
"two" > "three"            // => true: "tw" is alphabetically greater than "th"
false === (x > y)          // => true: false is equal to false

// Logical operators combine or invert boolean values
(x === 2) && (y === 3)     // => true: both comparisons are true. && is AND
(x > 3) || (y < 3)         // => false: neither comparison is true. || is OR
!(x === y)                 // => true: ! inverts a boolean value
```

If JavaScript expressions are like phrases, then JavaScript statements are like full sentences. Statements are the topic of Chapter 5. Roughly, an expression is something that computes a value but doesn’t do anything: it doesn’t alter the program state in any way. Statements, on the other hand, don’t have a value, but they do alter the state. You’ve seen variable declarations and assignment statements above. The other broad category of statement is control structures, such as conditionals and loops. You’ll see examples below, after we cover functions.

> 如果 JavaScript 表达式像短语，那么 JavaScript 语句就像完整的句子。这部分是第 5 章的主题。粗略地说，表达式不做任何事情只计算一个值：它不以任何方式改变程序状态。另一方面，语句没有值，但是它们可以改变状态。您已经在上面看到了变量声明和赋值语句。语句的另一大类是控制结构，比如条件语句和循环。在介绍函数之后，您将看到下面的示例。

A function is a named and parameterized block of JavaScript code that you define once, and can then invoke over and over again. Functions aren’t covered formally until Chapter 8, but like objects and arrays, you’ll see them many times before you get to that chapter. Here are some simple examples:

> 函数是一个已命名和参数化的 JavaScript 代码块，您只定义一次，然后可以反复调用它。函数直到第 8 章才正式介绍，但就像对象和数组一样，在进入这一章之前，您将多次看到它们。下面是一些简单的例子：

```js
// Functions are parameterized blocks of JavaScript code that we can invoke.
function plus1(x) {        // Define a function named "plus1" with parameter "x"
    return x + 1;          // Return a value one larger than the value passed in
}                          // Functions are enclosed in curly braces

plus1(y)                   // => 4: y is 3, so this invocation returns 3+1

let square = function(x) { // Functions are values and can be assigned to vars
    return x * x;          // Compute the function's value
};                         // Semicolon marks the end of the assignment.

square(plus1(y))           // => 16: invoke two functions in one expression
```

In ES6 and later, there is a shorthand syntax for defining functions. This concise syntax uses => to separate the argument list from the function body, so functions defined this way are known as arrow functions. Arrow functions are most commonly used when you want to pass an unnamed function as an argument to another function. The preceding code looks like this when rewritten to use arrow functions:

> 在 ES6 及以后版本中，有一种用于定义函数的快捷语法。这种简洁的语法使用 => 将参数列表与函数体分开，因此以这种方式定义的函数称为箭头函数。当您希望将一个未命名的函数作为参数传递给另一个函数时，最常用的是箭头函数。前面的代码看起来像这样，当重写使用箭头函数：

```js
const plus1 = x => x + 1;   // The input x maps to the output x + 1
const square = x => x * x;  // The input x maps to the output x * x
plus1(y)                    // => 4: function invocation is the same
square(plus1(y))            // => 16
```

When we use functions with objects, we get methods:

> 当我们使用函数和对象时，我们得到方法：

```js
// When functions are assigned to the properties of an object, we call
// them "methods."  All JavaScript objects (including arrays) have methods:
let a = [];                // Create an empty array
a.push(1,2,3);             // The push() method adds elements to an array
a.reverse();               // Another method: reverse the order of elements

// We can define our own methods, too. The "this" keyword refers to the object
// on which the method is defined: in this case, the points array from earlier.
points.dist = function() { // Define a method to compute distance between points
    let p1 = this[0];      // First element of array we're invoked on
    let p2 = this[1];      // Second element of the "this" object
    let a = p2.x-p1.x;     // Difference in x coordinates
    let b = p2.y-p1.y;     // Difference in y coordinates
    return Math.sqrt(a*a + // The Pythagorean theorem
                     b*b); // Math.sqrt() computes the square root
};
points.dist()              // => Math.sqrt(2): distance between our 2 points
```

Now, as promised, here are some functions whose bodies demonstrate common JavaScript control structure statements:

> 现在，如前所述，下面是一些函数，它们的主体演示了常见的 JavaScript 控制结构语句：

```js
// JavaScript statements include conditionals and loops using the syntax
// of C, C++, Java, and other languages.
function abs(x) {          // A function to compute the absolute value.
    if (x >= 0) {          // The if statement...
        return x;          // executes this code if the comparison is true.
    }                      // This is the end of the if clause.
    else {                 // The optional else clause executes its code if
        return -x;         // the comparison is false.
    }                      // Curly braces optional when 1 statement per clause.
}                          // Note return statements nested inside if/else.
abs(-10) === abs(10)       // => true

function sum(array) {      // Compute the sum of the elements of an array
    let sum = 0;           // Start with an initial sum of 0.
    for(let x of array) {  // Loop over array, assigning each element to x.
        sum += x;          // Add the element value to the sum.
    }                      // This is the end of the loop.
    return sum;            // Return the sum.
}
sum(primes)                // => 28: sum of the first 5 primes 2+3+5+7+11

function factorial(n) {    // A function to compute factorials
    let product = 1;       // Start with a product of 1
    while(n > 1) {         // Repeat statements in {} while expr in () is true
        product *= n;      // Shortcut for product = product * n;
        n--;               // Shortcut for n = n - 1
    }                      // End of loop
    return product;        // Return the product
}
factorial(4)               // => 24: 1*4*3*2

function factorial2(n) {   // Another version using a different loop
    let i, product = 1;    // Start with 1
    for(i=2; i <= n; i++)  // Automatically increment i from 2 up to n
        product *= i;      // Do this each time. {} not needed for 1-line loops
    return product;        // Return the factorial
}
factorial2(5)              // => 120: 1*2*3*4*5
```

JavaScript supports an object-oriented programming style, but it is significantly different than “classical” object-oriented programming languages. Chapter 9 covers object-oriented programming in JavaScript in detail, with lots of examples. Here is a very simple example that demonstrates how to define a JavaScript class to represent 2D geometric points. Objects that are instances of this class have a single method, named distance(), that computes the distance of the point from the origin:

> JavaScript 支持面向对象的编程风格，但它与“经典的”面向对象编程语言有显著的不同。第 9 章详细介绍了 JavaScript 的面向对象编程，并提供了很多示例。下面是一个非常简单的示例，演示了如何定义一个 JavaScript 类来表示 2D 几何点。作为这个类的实例的对象有一个名为 distance() 的方法，它计算点到原点的距离：

```js
class Point {              // By convention, class names are capitalized.
    constructor(x, y) {    // Constructor function to initialize new instances.
        this.x = x;        // This keyword is the new object being initialized.
        this.y = y;        // Store function arguments as object properties.
    }                      // No return is necessary in constructor functions.

    distance() {           // Method to compute distance from origin to point.
        return Math.sqrt(  // Return the square root of x² + y².
            this.x * this.x +  // this refers to the Point object on which
            this.y * this.y    // the distance method is invoked.
        );
    }
}

// Use the Point() constructor function with "new" to create Point objects
let p = new Point(1, 1);   // The geometric point (1,1).

// Now use a method of the Point object p
p.distance()               // => Math.SQRT2
```

This introductory tour of JavaScript’s fundamental syntax and capabilities ends here, but the book continues with self-contained chapters that cover additional features of the language:

> 关于 JavaScript 基本语法和能力的介绍到此结束，但这本书继续以自成体系的章节介绍该语言的其他特性:

Chapter 10, Modules

Shows how JavaScript code in one file or script can use JavaScript functions and classes defined in other files or scripts.

> 演示一个文件或脚本中的 JavaScript 代码如何使用在其他文件或脚本中定义的 JavaScript 函数和类。

Chapter 11, The JavaScript Standard Library

Covers the built-in functions and classes that are available to all JavaScript programs. This includes important data stuctures like maps and sets, a regular expression class for textual pattern matching, functions for serializing JavaScript data structures, and much more.

> 介绍所有 JavaScript 程序可用的内置函数和类。这包括重要的数据结构，如映射和集合、用于文本模式匹配的正则表达式类、用于序列化 JavaScript 数据结构的函数等等。

Chapter 12, Iterators and Generators

Explains how the for/of loop works and how you can make your own classes iterable with for/of. It also covers generator functions and the yield statement.

> 解释 for/of 循环是如何工作的，以及如何使用 for/of 使您自己的类可迭代。它还包括生成器函数和 yield 语句。

Chapter 13, Asynchronous JavaScript

This chapter is an in-depth exploration of asynchronous programming in JavaScript, covering callbacks and events, Promise-based APIs, and the async and await keywords. Although the core JavaScript language is not asynchronous, asynchronous APIs are the default in both web browsers and Node, and this chapter explains the techniques for working with those APIs.

> 本章对 JavaScript 中的异步编程进行了深入的探索，涵盖了回调和事件、基于承诺的 api 以及异步和等待关键字。尽管核心 JavaScript 语言不是异步的，异步 api 在 web 浏览器和节点中都是默认的，本章解释了使用这些 api 的技术。

Chapter 14, Metaprogramming

Introduces a number of advanced features of JavaScript that may be of interest to programmers writing libraries of code for other JavaScript programmers to use.

> 介绍了 JavaScript 的许多高级特性，编写代码库供其他 JavaScript 程序员使用的程序员可能会对这些特性感兴趣。

Chapter 15, JavaScript in Web Browsers

Introduces the web browser host environment, explains how web browsers execute JavaScript code, and covers the most important of the many APIs defined by web browsers. This is by far the longest chapter in the book.

> 介绍 web 浏览器宿主，解释 web 浏览器如何执行 JavaScript 代码，并涵盖 web 浏览器定义的许多 api 中最重要的一个。这是书中最长的一章。

Chapter 16, Server-Side JavaScript with Node

Introduces the Node host environment, covering the fundamental programming model and the data structures and APIs that are most important to understand.

> 介绍 Node 宿主，涵盖基本编程模型以及需要理解的最重要的数据结构和 api。

Chapter 17, JavaScript Tools and Extensions

Covers tools and language extensions that are worth knowing about because they are widely used and may make you a more productive programmer.

> 涵盖了值得了解的工具和语言扩展，因为它们被广泛使用，可能使您成为更有生产力的程序员。

## 1.4 Example: Character Frequency Histograms

This chapter concludes with a short but nontrivial JavaScript program. Example 1-1 is a Node program that reads text from standard input, computes a character frequency histogram from that text, and then prints out the histogram. You could invoke the program like this to analyze the character frequency of its own source code:

> 本章以一个简短但不平凡的 JavaScript 程序结束。示例 1-1 是一个节点程序，它从标准输入中读取文本，根据文本计算字符频率直方图，然后打印该直方图。你可以调用这样的程序来分析字符频率自己的源代码：

```sh
$ node charfreq.js < charfreq.js
T: ########### 11.22%
E: ########## 10.15%
R: ####### 6.68%
S: ###### 6.44%
A: ###### 6.16%
N: ###### 5.81%
O: ##### 5.45%
I: ##### 4.54%
H: #### 4.07%
C: ### 3.36%
L: ### 3.20%
U: ### 3.08%
/: ### 2.88%
```

This example uses a number of advanced JavaScript features and is intended to demonstrate what real-world JavaScript programs can look like. You should not expect to understand all of the code yet, but be assured that all of it will be explained in the chapters that follow.

> 这个示例使用了许多高级 JavaScript 特性，旨在演示真实的 JavaScript 程序是什么样的。你不应该期望理解所有的代码，但是要确保所有的代码将在下面的章节中被解释。

Example 1-1. Computing character frequency histograms with JavaScript

```js
/**
 * This Node program reads text from standard input, computes the frequency
 * of each letter in that text, and displays a histogram of the most
 * frequently used characters. It requires Node 12 or higher to run.
 *
 * In a Unix-type environment you can invoke the program like this:
 *    node charfreq.js < corpus.txt
 */

// This class extends Map so that the get() method returns the specified
// value instead of null when the key is not in the map
class DefaultMap extends Map {
    constructor(defaultValue) {
        super();                          // Invoke superclass constructor
        this.defaultValue = defaultValue; // Remember the default value
    }

    get(key) {
        if (this.has(key)) {              // If the key is already in the map
            return super.get(key);        // return its value from superclass.
        }
        else {
            return this.defaultValue;     // Otherwise return the default value
        }
    }
}

// This class computes and displays letter frequency histograms
class Histogram {
    constructor() {
        this.letterCounts = new DefaultMap(0);  // Map from letters to counts
        this.totalLetters = 0;                  // How many letters in all
    }

    // This function updates the histogram with the letters of text.
    add(text) {
        // Remove whitespace from the text, and convert to upper case
        text = text.replace(/\s/g, "").toUpperCase();

        // Now loop through the characters of the text
        for(let character of text) {
            let count = this.letterCounts.get(character); // Get old count
            this.letterCounts.set(character, count+1);    // Increment it
            this.totalLetters++;
        }
    }

    // Convert the histogram to a string that displays an ASCII graphic
    toString() {
        // Convert the Map to an array of [key,value] arrays
        let entries = [...this.letterCounts];

        // Sort the array by count, then alphabetically
        entries.sort((a,b) => {              // A function to define sort order.
            if (a[1] === b[1]) {             // If the counts are the same
                return a[0] < b[0] ? -1 : 1; // sort alphabetically.
            } else {                         // If the counts differ
                return b[1] - a[1];          // sort by largest count.
            }
        });

        // Convert the counts to percentages
        for(let entry of entries) {
            entry[1] = entry[1] / this.totalLetters*100;
        }

        // Drop any entries less than 1%
        entries = entries.filter(entry => entry[1] >= 1);

        // Now convert each entry to a line of text
        let lines = entries.map(
            ([l,n]) => `${l}: ${"#".repeat(Math.round(n))} ${n.toFixed(2)}%`
        );

        // And return the concatenated lines, separated by newline characters.
        return lines.join("\n");
    }
}

// This async (Promise-returning) function creates a Histogram object,
// asynchronously reads chunks of text from standard input, and adds those chunks to
// the histogram. When it reaches the end of the stream, it returns this histogram
async function histogramFromStdin() {
    process.stdin.setEncoding("utf-8"); // Read Unicode strings, not bytes
    let histogram = new Histogram();
    for await (let chunk of process.stdin) {
        histogram.add(chunk);
    }
    return histogram;
}

// This one final line of code is the main body of the program.
// It makes a Histogram object from standard input, then prints the histogram.
histogramFromStdin().then(histogram => { console.log(histogram.toString()); });
```

## 1.5 Summary

This book explains JavaScript from the bottom up. This means that we start with low-level details like comments, identifiers, variables, and types; then build to expressions, statements, objects, and functions; and then cover high-level language abstractions like classes and modules. I take the word definitive in the title of this book seriously, and the coming chapters explain the language at a level of detail that may feel off-putting at first. True mastery of JavaScript requires an understanding of the details, however, and I hope that you will make time to read this book cover to cover. But please don’t feel that you need to do that on your first reading. If you find yourself feeling bogged down in a section, simply skip to the next. You can come back and master the details once you have a working knowledge of the language as a whole.

> 这本书从下至上地说明了 JavaScript。这意味着我们从底层细节开始，比如注释、标识符、变量和类型；然后构建表达式、语句、对象和函数；然后介绍高级语言抽象，比如类和模块。我在这本书的标题中认真地使用了“权威”这个词，接下来的章节会详细地解释这种语言，一开始可能会让人感到不快。然而，真正掌握 JavaScript 需要了解细节，我希望您能抽出时间从头到尾阅读这本书。但请不要觉得在第一次阅读时就需要这样做。如果你发现自己在某个章节陷入困境，直接跳到下一个章节。一旦你对语言有了整体的应用知识，你可以回过头来掌握细节。