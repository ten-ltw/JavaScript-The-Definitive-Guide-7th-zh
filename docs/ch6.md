# 第 6 章 对象

Objects are JavaScript’s most fundamental datatype, and you have already seen them many times in the chapters that precede this one. Because objects are so important to the JavaScript language, it is important that you understand how they work in detail, and this chapter provides that detail. It begins with a formal overview of objects, then dives into practical sections about creating objects and querying, setting, deleting, testing, and enumerating the properties of objects. These property-focused sections are followed by sections that explain how to extend, serialize, and define important methods on objects. Finally, the chapter concludes with a long section about new object literal syntax in ES6 and more recent versions of the language.

> 对象是 JavaScript 最基本的数据类型，在本章之前的章节中已经多次看到它们。因为对象对 JavaScript 语言非常重要，所以了解它们的工作原理非常重要，本章将提供这些细节。它从对象的正式概述开始，然后深入到关于创建对象以及查询、设置、删除、测试和枚举对象属性的实用部分。在这些以属性为中心的章节之后，将介绍如何扩展、序列化和定义对象上的重要方法。最后，本章以一大段关于 ES6 中的新对象文字语法和该语言的最新版本结尾。

## 6.1 Introduction to Objects

An object is a composite value: it aggregates multiple values (primitive values or other objects) and allows you to store and retrieve those values by name. An object is an unordered collection of properties, each of which has a name and a value. Property names are usually strings (although, as we’ll see in §6.10.3, property names can also be Symbols), so we can say that objects map strings to values. This string-to-value mapping goes by various names—you are probably already familiar with the fundamental data structure under the name “hash,” “hashtable,” “dictionary,” or “associative array.” An object is more than a simple string-to-value map, however. In addition to maintaining its own set of properties, a JavaScript object also inherits the properties of another object, known as its “prototype.” The methods of an object are typically inherited properties, and this “prototypal inheritance” is a key feature of JavaScript.

> 对象是一个复合值：它聚合了多个值（原始值或其他对象），并允许按名称存储和获取这些值。对象是属性的无序集合，每个属性都有一个名称和一个值。属性名通常是字符串（尽管，正如我们将在 §6.10.3 中看到的，属性名也可以是 Symbol），所以我们可以说对象将字符串映射到值。这种字符串到值的映射有不同的名称——可能已经熟悉这种基本数据结构的别的名称“散列”（hash）、“散列表”（hashtable）、“字典”（dictionary）或“关联数组”（associative array）。然而，对象不仅仅是简单的字符串到值的映射。除了维护自己的属性集，JavaScript 对象还继承另一个对象的属性，即它的“原型”。对象的方法通常是继承的属性，而这种“原型继承”是 JavaScript 的一个关键特性。

JavaScript objects are dynamic—properties can usually be added and deleted—but they can be used to simulate the static objects and “structs” of statically typed languages. They can also be used (by ignoring the value part of the string-to-value mapping) to represent sets of strings.

> JavaScript 对象是动态的——属性通常可以添加和删除——但它们可以用来模拟静态类型语言的静态对象和“结构体”（struct）。有时它们也用做字符串的集 合（忽略名/值对中的值）。

Any value in JavaScript that is not a string, a number, a Symbol, or true, false, null, or undefined is an object. And even though strings, numbers, and booleans are not objects, they can behave like immutable objects.

> JavaScript 中任何不是字符串、数字、Symbol 或 true、false、null 或 undefined 的值都是对象。即使字符串、数字和布尔值不是对象，它们的行为和不可变对象非常类似。

Recall from §3.8 that objects are mutable and manipulated by reference rather than by value. If the variable x refers to an object and the code let y = x; is executed, the variable y holds a reference to the same object, not a copy of that object. Any modifications made to the object through the variable y are also visible through the variable x.

> 回想一下 §3.8，对象是可变的，通过引用而不是值来操作。如果变量 x 指向一个对象的引用，执行 `y = x;` 时，变量 y 也是指向同一对象的引用，而不是该对象的副本。通过变量 y 修改这个对象也会对变量 x 造成影响。

The most common things to do with objects are to create them and set, query, delete, test, and enumerate their properties. These fundamental operations are described in the opening sections of this chapter. The sections after that cover more advanced topics.

> 对对象最常见的操作是创建它们并设置、查询、删除、测试和枚举它们的属性。这些基本的操作将在本章的开头部分进行描述。之后的部分将介绍更高级的主题。

A property has a name and a value. A property name may be any string, including the empty string (or any Symbol), but no object may have two properties with the same name. The value may be any JavaScript value, or it may be a getter or setter function (or both). We’ll learn about getter and setter functions in §6.10.6.

> 属性有一个名称和一个值。属性名可以是任何字符串，包括空字符串（或任何 Symbol），但任何对象都不能有两个同名的属性。值可以是任何 JavaScript 值，也可以是 getter 或 setter 函数（或两者都是）。我们将在 §6.10.6 中学习 getter 和 setter 函数。

It is sometimes important to be able to distinguish between properties defined directly on an object and those that are inherited from a prototype object. JavaScript uses the term own property to refer to non-inherited properties.

> 有时，能够区分直接在对象上定义的属性和从原型对象继承的属性是很重要的。JavaScript 使用术语“自有属性”来指代非继承属性。

In addition to its name and value, each property has three property attributes:

> 除了名称和值之外，每个属性还有三个属性属性:

- The writable attribute specifies whether the value of the property can be set.
- The enumerable attribute specifies whether the property name is returned by a for/in loop.
- The configurable attribute specifies whether the property can be deleted and whether its attributes can be altered.

---

- writable 属性指定是否可以设置属性的值。
- enumerable 属性指定 for/in 循环是否返回属性名称。
- 可配置属性指定该属性是否可以删除，是否可以修改其属性。

Many of JavaScript’s built-in objects have properties that are read-only, non-enumerable, or non-configurable. By default, however, all properties of the objects you create are writable, enumerable, and configurable. §14.1 explains techniques for specifying non-default property attribute values for your objects.

> 许多 JavaScript 的内置对象具有只读、不可枚举或不可配置的属性。但是，在默认情况下，创建的对象的所有属性都是可写、可枚举和可配置的。§14.1 解释了为对象指定非默认属性属性值的技巧。

## 6.2 Creating Objects

Objects can be created with object literals, with the new keyword, and with the Object.create() function. The subsections below describe each technique.

> 对象可以用对象字面量创建，也可以用 new 关键字和 Object.create() 函数来创建。接下来的几部分对这些技术一一讲述。

### 6.2.1 Object Literals

The easiest way to create an object is to include an object literal in your JavaScript code. In its simplest form, an object literal is a comma-separated list of colon-separated name:value pairs, enclosed within curly braces. A property name is a JavaScript identifier or a string literal (the empty string is allowed). A property value is any JavaScript expression; the value of the expression (it may be a primitive value or an object value) becomes the value of the property. Here are some examples:

> 创建对象最简单的方式就是在 JavaScript 代码中使用对象直接量。对象直接量是由若干名/值对组成的映射表，名/值对中间用冒号分隔，名/值对之间用逗号分隔，整个映射表用花括号括起来。属性名可以是 JavaScript 标识符也可以是字符串字面量（包括空字符串）。属性的值可以是任意类型的 JavaScript 表达式；表达式的值（可以是原始值也可以是对象值）变成这个属性的值。下面有一些例子：

```js
let empty = {};                          // An object with no properties
let point = { x: 0, y: 0 };              // Two numeric properties
let p2 = { x: point.x, y: point.y+1 };   // More complex values
let book = {
    "main title": "JavaScript",          // These property names include spaces,
    "sub-title": "The Definitive Guide", // and hyphens, so use string literals.
    for: "all audiences",                // for is reserved, but no quotes.
    author: {                            // The value of this property is
        firstname: "David",              // itself an object.
        surname: "Flanagan"
    }
};
```
A trailing comma following the last property in an object literal is legal, and some programming styles encourage the use of these trailing commas so you’re less likely to cause a syntax error if you add a new property at the end of the object literal at some later time.

> 对象文本中最后一个属性的尾随逗号是合法的，并且某些编程样式鼓励使用这些尾随逗号，因为，如果之后在对象文本的末尾添加新属性，则不太可能导致语法错误。

An object literal is an expression that creates and initializes a new and distinct object each time it is evaluated. The value of each property is evaluated each time the literal is evaluated. This means that a single object literal can create many new objects if it appears within the body of a loop or in a function that is called repeatedly, and that the property values of these objects may differ from each other.

> 对象字面量是一个表达式，它每次计算时都会创建和初始化一个新对象。每次字面量计算时，将计算每个属性的值。这意味着，如果单个对象字面量出现在循环体或重复调用的函数中，它能创建许多个新对象，并且这些对象的属性值可能彼此不同。

The object literals shown here use simple syntax that has been legal since the earliest versions of JavaScript. Recent versions of the language have introduced a number of new object literal features, which are covered in §6.10.

> 此处的简单语法对象字面量，自 JavaScript 最早的版本以来一直是合法的。最新版本引入了许多对象字面量的新的特性，这些特性在 §6.10 中介绍。

### 6.2.2 Creating Objects with new
The new operator creates and initializes a new object. The new keyword must be followed by a function invocation. A function used in this way is called a constructor and serves to initialize a newly created object. JavaScript includes constructors for its built-in types. For example:

> new 运算符创建并初始化一个新的对象。new 关键字必须紧跟一个函数调用。这种方式使用函数叫做构造函数调用，其提供初始化一个新创建的对象的服务。在 JavaScript 中，内置类型都包含相对应的构造函数。例如：

```js
let o = new Object();  // Create an empty object: same as {}.
let a = new Array();   // Create an empty array: same as [].
let d = new Date();    // Create a Date object representing the current time
let r = new Map();     // Create a Map object for key/value mapping
```
In addition to these built-in constructors, it is common to define your own constructor functions to initialize newly created objects. Doing so is covered in Chapter 9.

> 除了这些内置构造函数，常常用自定义构造函数来初始化新对象。 第 9 章将详细讲述其中的细节。

### 6.2.3 Prototypes
Before we can cover the third object creation technique, we must pause for a moment to explain prototypes. Almost every JavaScript object has a second JavaScript object associated with it. This second object is known as a prototype, and the first object inherits properties from the prototype.

> 在讲述第三种对象创建技术之前，我们应当首先解释一下原型。每一个 JavaScript 对象都和另一个对象相关联。“另一个”对象就是我们熟知的原型，每一个对象都从原型继承属性。

All objects created by object literals have the same prototype object, and we can refer to this prototype object in JavaScript code as Object.prototype. Objects created using the new keyword and a constructor invocation use the value of the prototype property of the constructor function as their prototype. So the object created by new Object() inherits from Object.prototype, just as the object created by {} does. Similarly, the object created by new Array() uses Array.prototype as its prototype, and the object created by new Date() uses Date.prototype as its prototype. This can be confusing when first learning JavaScript. Remember: almost all objects have a prototype, but only a relatively small number of objects have a prototype property. It is these objects with prototype properties that define the prototypes for all the other objects.

> 所有通过对象字面量创建的对象都具有同一个原型对象，并可以通过 JavaScript 代码 Object.prototype 获得对原型对象的引用。通过关键字 new 和构造函数调用创建的对象的原型就是构造函数的 prototype 属性的值。因此，同使用 {} 创建对象一样，通过 new Object() 创建的对象也继承自Object.prototype。同样，通过 new Array() 创建的对象的原型就是 Array.prototype，通过 new Date() 创建的对象的原型就是 Date.prototype。当第一次学习 JavaScript 时，这可能令人困惑。请记住：几乎所有对象都有原型，但只有相对较少的对象具有原型属性。正是这些具有原型属性的对象定义了所有其他对象的原型。

Object.prototype is one of the rare objects that has no prototype: it does not inherit any properties. Other prototype objects are normal objects that do have a prototype. Most built-in constructors (and most user-defined constructors) have a prototype that inherits from Object.prototype. For example, Date.prototype inherits properties from Object.prototype, so a Date object created by new Date() inherits properties from both Date.prototype and Object.prototype. This linked series of prototype objects is known as a prototype chain.

> 没有原型的对象为数不多，Object.prototype就是其中之一：它不继承任何属性。其他原型对象都是普通对象，普通对象都具有原型。大部分的内置构造函数（以及大部分自定义的构造函数）都具有一个继承自 Object.prototype 的原型。例如， Date.prototype 的属性继承自 Object.prototype，因此由 new Date() 创建的 Date 对象的属性同时继承自 Date.prototype 和 Object.prototype。这一系列链接的原型对象就是所谓 “原型链”（prototype chain）。

An explanation of how property inheritance works is in §6.3.2. Chapter 9 explains the connection between prototypes and constructors in more detail: it shows how to define new “classes” of objects by writing a constructor function and setting its prototype property to the prototype object to be used by the “instances” created with that constructor. And we’ll learn how to query (and even change) the prototype of an object in §14.3.

> §6.3.2 节讲述属性继承的工作机制。第 9 章将会更详细地讨论原型和构造函数：包括如何通过编写构造函数定义对象的“类”，以及给构造函数的 prototype 属性赋值可以让其“实例”直接使用这个原型上的属性和方法。并且在 §14.3 我们会学习如何查询（甚至改变）对象的原型。

### 6.2.4 Object.create()
Object.create() creates a new object, using its first argument as the prototype of that object:

> Object.create() 创建一个新的对象，用第一个实参作为它的原型：

```js
let o1 = Object.create({x: 1, y: 2});     // o1 inherits properties x and y.
o1.x + o1.y                               // => 3
```
You can pass null to create a new object that does not have a prototype, but if you do this, the newly created object will not inherit anything, not even basic methods like toString() (which means it won’t work with the + operator either):

> 可以通过传入参数 null 来创建一个没有原型的新对象，但通过这种方式创建的对象不会继承任何东西，甚至不包括基础方法，比如 toString()，也就是说，它将不能和“+”运算符一起正常工作：

```js
let o2 = Object.create(null);             // o2 inherits no props or methods.
```
If you want to create an ordinary empty object (like the object returned by {} or new Object()), pass Object.prototype:

> 如果想创建一个普通的空对象（像通过 {} 或 new Object() 创建的对象），需要传入 Object.prototype：

```js
let o3 = Object.create(Object.prototype); // o3 is like {} or new Object().
```
The ability to create a new object with an arbitrary prototype is a powerful one, and we’ll use Object.create() in a number of places throughout this chapter. (Object.create() also takes an optional second argument that describes the properties of the new object. This second argument is an advanced feature covered in §14.1.)

> 可以通过任意原型创建新对象，这是一个强大的特性，并且本章我们会在很多地方使用 Object.create()。（Object.create() 也可以传入第二个可选实参来描述这个新的对象的属性。第二个实参是一个高级特性，在  §14.1 再进行描述。）

One use for Object.create() is when you want to guard against unintended (but nonmalicious) modification of an object by a library function that you don’t have control over. Instead of passing the object directly to the function, you can pass an object that inherits from it. If the function reads properties of that object, it will see the inherited values. If it sets properties, however, those writes will not affect the original object.

> Object.create() 其中一个用途是预防对象无意间（非恶意地）被无法支配的库函数篡改。可以创建一个继承它的对象来传递给函数，而不是将其直接传递给函数。当函数读取继承对象的属性时，实际上读取的是继承来的值。如果给继承对象的属性赋值，则这些属性只会影响这个继承对象自身，而不是原始对象：

```js
let o = { x: "don't change this value" };
library.function(Object.create(o));  // Guard against accidental modifications
```
To understand why this works, you need to know how properties are queried and set in JavaScript. These are the topics of the next section.

> 想要了解其工作原理，需要先知道 JavaScript 中属性的查询和设置机制。这是接下来这节的主题。

## 6.3 Querying and Setting Properties
To obtain the value of a property, use the dot (.) or square bracket ([]) operators described in §4.4. The lefthand side should be an expression whose value is an object. If using the dot operator, the righthand side must be a simple identifier that names the property. If using square brackets, the value within the brackets must be an expression that evaluates to a string that contains the desired property name:

> §4.4 已经提到，可以通过点（.）或方括号（[]）运算符来获取属性的值。运算符左侧应当是一个表达式，它返回一个对象。如果使用点运算符，右侧必须是一个以属性名称命名的简单标识符。如果使用方括号，方括号内必须是一个计算结果为字符串的表达式，这个字符串就是属性的名字：

```js
let author = book.author;       // Get the "author" property of the book.
let name = author.surname;      // Get the "surname" property of the author.
let title = book["main title"]; // Get the "main title" property of the book.
```
To create or set a property, use a dot or square brackets as you would to query the property, but put them on the lefthand side of an assignment expression:

> 和查询属性值的写法一样，通过点和方括号也可以创建属性或给属性赋值，但需要将它们放在赋值表达式的左侧：

```js
book.edition = 7;                   // Create an "edition" property of book.
book["main title"] = "ECMAScript";  // Change the "main title" property.
```
When using square bracket notation, we’ve said that the expression inside the square brackets must evaluate to a string. A more precise statement is that the expression must evaluate to a string or a value that can be converted to a string or to a Symbol (§6.10.3). In Chapter 7, for example, we’ll see that it is common to use numbers inside the square brackets.

> 当使用方括号时，我们说方括号内的表达式必须返回字符串。其实更严格地讲，表达式必须返回字符串或返回一个可以转换为字符串的值或 Symbol（§6.10.3）。在第 7 章里有一些例子中的方括号内使用了数字，这情况是非常常用的。

### 6.3.1 Objects As Associative Arrays
As explained in the preceding section, the following two JavaScript expressions have the same value:

> 上文提到，下面两个表达式有相同的值：

```js
object.property
object["property"]
```
The first syntax, using the dot and an identifier, is like the syntax used to access a static field of a struct or object in C or Java. The second syntax, using square brackets and a string, looks like array access, but to an array indexed by strings rather than by numbers. This kind of array is known as an associative array (or hash or map or dictionary). JavaScript objects are associative arrays, and this section explains why that is important.

> 第一种语法使用点运算符和一个标识符，这和 C 和 Java 中访问一个结构体或对象的静态字段非常类似。第二种语法使用方括号和一个字符串，看起来更像数组，只是这个数组元素是通过字符串索引而不是数字索引。这种数组就是我们所说的关联数组（associative array）（也称做散列、映射或字典）。JavaScript 对象都是关联数组，本节将讨论它的重要性。

In C, C++, Java, and similar strongly typed languages, an object can have only a fixed number of properties, and the names of these properties must be defined in advance. Since JavaScript is a loosely typed language, this rule does not apply: a program can create any number of properties in any object. When you use the . operator to access a property of an object, however, the name of the property is expressed as an identifier. Identifiers must be typed literally into your JavaScript program; they are not a datatype, so they cannot be manipulated by the program.

> 在 C、C++、Java 和一些强类型语言中，对象只能拥有固定数目的属性，并且这些属性的名称必须提前定义好。由于 JavaScript 是一个弱类型语言，因此不适用这条规则：对象在程序中可以创建任意数量的属性。当使用 . 运算符访问对象的属性时，属性名用一个标识符来表示。标识符必须直接出现在 JavaScript 程序中，它们不是数据类型，所以无法在程序中修改。

On the other hand, when you access a property of an object with the [] array notation, the name of the property is expressed as a string. Strings are JavaScript datatypes, so they can be manipulated and created while a program is running. So, for example, you can write the following code in JavaScript:

> 另一种方式，当通过 [] 来访问对象的属性时，属性名通过字符串来表示。字符串是 JavaScript 的数据类型，在程序运行时可以修改和创建它们。因此，可以在 JavaScript 中使用下面这种代码：

```js
let addr = "";
for(let i = 0; i < 4; i++) {
    addr += customer[`address${i}`] + "\n";
}
```
This code reads and concatenates the address0, address1, address2, and address3 properties of the customer object.

> 这段代码读取 customer 对象的 address0、address1、address2 和 address3 属性，并将它们连接起来。

This brief example demonstrates the flexibility of using array notation to access properties of an object with string expressions. This code could be rewritten using the dot notation, but there are cases in which only the array notation will do. Suppose, for example, that you are writing a program that uses network resources to compute the current value of the user’s stock market investments. The program allows the user to type in the name of each stock they own as well as the number of shares of each stock. You might use an object named portfolio to hold this information. The object has one property for each stock. The name of the property is the name of the stock, and the property value is the number of shares of that stock. So, for example, if a user holds 50 shares of stock in IBM, the portfolio.ibm property has the value 50.

> 这个例子主要说明了通过字符串表达式使用数组标记来访问对象属性的灵活性。这段代码也可以通过点运算符来重写，但是一些场景只能使用数组写法来完成。假设你正在写一个程序，这个程序利用网络资源计算用户股票市场投资的当前价值。程序允许用户输入他们拥有的股票名称以及对应的数量。你可以用一个名为 portfolio 的对象来储存这些信息。每一个股票在对象中都有一个属性与之对应。属性名是股票名，属性值是股票持有份额。例如，如果用户持有 IBM 的 50 股，那么 portfolio.ibm 属性的值就为 50。

Part of this program might be a function for adding a new stock to the portfolio:

> 下面是程序的部分代码，这个函数用来给 portifolio 添加新的股票：

```js
function addstock(portfolio, stockname, shares) {
    portfolio[stockname] = shares;
}
```
Since the user enters stock names at runtime, there is no way that you can know the property names ahead of time. Since you can’t know the property names when you write the program, there is no way you can use the . operator to access the properties of the portfolio object. You can use the [] operator, however, because it uses a string value (which is dynamic and can change at runtime) rather than an identifier (which is static and must be hardcoded in the program) to name the property.

> 由于用户是在程序运行时输入股票名称，因此在之前无法得知这些股票的名称是什么。而由于在写程序的时候不知道属性名称，因此无法通过点运算符（.）来访问对象 portfolio 的属性。但可以使用 [] 运算符，因为它使用字符串值（字符串值是动态的，可以在运行时更改）而不是标识符（标识符是静态的，必须写死在程序中）作为索引对属性进行访问。

In Chapter 5, we introduced the for/in loop (and we’ll see it again shortly, in §6.6). The power of this JavaScript statement becomes clear when you consider its use with associative arrays. Here is how you would use it when computing the total value of a portfolio:

> 第 5 章介绍了 for/in 循环（§6.6 节还会进一步介绍）。当使用 for/in 循环遍历关联数组时，就可以清晰地体会到 for/in 的强大之处。下面的例子就是利用 for/in 计算  portfolio 的合计值：

```js
function computeValue(portfolio) {
    let total = 0.0;
    for(let stock in portfolio) {       // For each stock in the portfolio:
        let shares = portfolio[stock];  // get the number of shares
        let price = getQuote(stock);    // look up share price
        total += shares * price;        // add stock value to total value
    }
    return total;                       // Return total value.
}
```
JavaScript objects are commonly used as associative arrays as shown here, and it is important to understand how this works. In ES6 and later, however, the Map class described in §11.1.2 is often a better choice than using a plain object.

> 如本节所示，JavaScript 对象通常用作关联数组，理解其工作原理非常重要。但是，在 ES6 之后使用 Map 类常常是一个更好的选择，我们将在 §11.1.2 中进行描述。

### 6.3.2 Inheritance
JavaScript objects have a set of “own properties,” and they also inherit a set of properties from their prototype object. To understand this, we must consider property access in more detail. The examples in this section use the Object.create() function to create objects with specified prototypes. We’ll see in Chapter 9, however, that every time you create an instance of a class with new, you are creating an object that inherits properties from a prototype object.

> JavaScript 对象中有一组“自有属性”，也有一组属性是继承自它的原型对象。想要理解属性继承，必须更深入地了解属性访问的细节。这一节的例子通过使用 Object.create() 函数创建对象来指定它的原型。我们会在第 9 章再次看到它，但是，每次使用 new 创建类的实例时，都会创建一个从原型对象继承属性的对象。

Suppose you query the property x in the object o. If o does not have an own property with that name, the prototype object of o1 is queried for the property x. If the prototype object does not have an own property by that name, but has a prototype itself, the query is performed on the prototype of the prototype. This continues until the property x is found or until an object with a null prototype is searched. As you can see, the prototype attribute of an object creates a chain or linked list from which properties are inherited:

> 假设要查询对象 o 的属性 x。如果 o 中不存在 x 名称的自由属性，那么将会继续在 o 的原型对象中查询属性 x。如果原型对象中也没有 x，但这个原型对象也有原型，那么继续在这个原型对象的原型上执行查询，直到找到 x 或者查找到一个原型是 null 的对象为止。可以看到，对象的原型属性构成了一个“链”，通过这个“链”可以实现属性的继承。

```js
let o = {};               // o inherits object methods from Object.prototype
o.x = 1;                  // and it now has an own property x.
let p = Object.create(o); // p inherits properties from o and Object.prototype
p.y = 2;                  // and has an own property y.
let q = Object.create(p); // q inherits properties from p, o, and...
q.z = 3;                  // ...Object.prototype and has an own property z.
let f = q.toString();     // toString is inherited from Object.prototype
q.x + q.y                 // => 3; x and y are inherited from o and p
```
Now suppose you assign to the property x of the object o. If o already has an own (non-inherited) property named x, then the assignment simply changes the value of this existing property. Otherwise, the assignment creates a new property named x on the object o. If o previously inherited the property x, that inherited property is now hidden by the newly created own property with the same name.

> 现在假设给对象 o 的属性 x 赋值，如果 o 中已经有属性 x（这个属性不是继承来的），那么这个赋值操作只改变这个已有属性 x 的值。否则，赋值操作给 o 添加一个新属性 x。如果之前 o 继承自属性 x，那么这个继承的属性就被新创建的同名属性覆盖了。

Property assignment examines the prototype chain only to determine whether the assignment is allowed. If o inherits a read-only property named x, for example, then the assignment is not allowed. (Details about when a property may be set are in §6.3.3.) If the assignment is allowed, however, it always creates or sets a property in the original object and never modifies objects in the prototype chain. The fact that inheritance occurs when querying properties but not when setting them is a key feature of JavaScript because it allows us to selectively override inherited properties:

> 属性赋值操作检查原型链只是判断是否允许赋值操作。例如，如果 o 继承自一个只读属性 x，那么赋值操作是不允许的（§6.3.3 将对此进行详细讨论）。 如果允许属性赋值操作，它也总是在原始对象上创建属性或对已有的属性赋值，而不会去修改原型链。在 JavaScript 中，只有在查询属性时才会体会到继承的存在，而设置属性则和继承无关，这是 JavaScript 的一个重要特性，该特性让程序员可以有选择地重写继承的属性。

```js
let unitcircle = { r: 1 };         // An object to inherit from
let c = Object.create(unitcircle); // c inherits the property r
c.x = 1; c.y = 1;                  // c defines two properties of its own
c.r = 2;                           // c overrides its inherited property
unitcircle.r                       // => 1: the prototype is not affected
```
There is one exception to the rule that a property assignment either fails or creates or sets a property in the original object. If o inherits the property x, and that property is an accessor property with a setter method (see §6.10.6), then that setter method is called rather than creating a new property x in o. Note, however, that the setter method is called on the object o, not on the prototype object that defines the property, so if the setter method defines any properties, it will do so on o, and it will again leave the prototype chain unmodified.

> 属性赋值要么失败，要么创建一个属性，要么在原始对象中设置属性。但有一个例外，如果 o 继承自属性 x，而这个属性是一个具有 setter 方法的存取器属性（参照 §6.10.6），那么这时将调用 setter 方法而不是给 o 创建一个属性 x。需要注意的是，setter 方法是由对象 o 调用的，而不是定义这个属性的原型对象调用的。因此如果 setter 方法定义任意属性，这个操作只是针对 o 本身，并不会修改原型链。

### 6.3.3 Property Access Errors
Property access expressions do not always return or set a value. This section explains the things that can go wrong when you query or set a property.

> 属性访问表达式并不总是返回或设置一个值。本节讲述查询或设置属性时的一些出错情况。

It is not an error to query a property that does not exist. If the property x is not found as an own property or an inherited property of o, the property access expression o.x evaluates to undefined. Recall that our book object has a “sub-title” property, but not a “subtitle” property:

> 查询一个不存在的属性并不会报错，如果在对象 o 自身的属性或继承的属性中均未找到属性 x，属性访问表达式 o.x 返回 undefined。回想一下我们的 book 对象有属性“sub-title”，而没有属性“subtitle”：

```js
book.subtitle    // => undefined: property doesn't exist
```
It is an error, however, to attempt to query a property of an object that does not exist. The null and undefined values have no properties, and it is an error to query properties of these values. Continuing the preceding example:

> 但是，如果对象不存在，那么试图查询这个不存在的对象的属性就会报错。null 和 undefined 值都没有属性，因此查询这些值的属性会报错，接上例：

```js
let len = book.subtitle.length; // !TypeError: undefined doesn't have length
```
Property access expressions will fail if the lefthand side of the . is null or undefined. So when writing an expression like book.author.surname, you should be careful if you are not certain that book and book.author are actually defined. Here are two ways to guard against this kind of problem: 

> 如果 . 的左边是 null 或 undefined 时，其属性表达式会失败。所以当写一个像 book.author.surname 一样的表达式时，如果你不确定 book 和 book.author 确实被定义就要小心了。下面提供了两种避免出错的方法：

```js
// A verbose and explicit technique
let surname = undefined;
if (book) {
    if (book.author) {
        surname = book.author.surname;
    }
}

// A concise and idiomatic alternative to get surname or null or undefined
surname = book && book.author && book.author.surname;
```
To understand why this idiomatic expression works to prevent TypeError exceptions, you might want to review the short-circuiting behavior of the && operator in §4.10.1.

> 为了理解为什么这里的第二种方法可以避免类型错误异常，可以参照 §4.10.1节 中关于 && 运算符的短路行为。

As described in §4.4.1, ES2020 supports conditional property access with ?., which allows us to rewrite the previous assignment expression as:

> 如 §4.4.1 中所描述，ES2020 支持用 ?. 条件属性访问，它允许这样重写上面的赋值表达式：

```js
let surname = book?.author?.surname;
```
Attempting to set a property on null or undefined also causes a TypeError. Attempts to set properties on other values do not always succeed, either: some properties are read-only and cannot be set, and some objects do not allow the addition of new properties. In strict mode (§5.6.3), a TypeError is thrown whenever an attempt to set a property fails. Outside of strict mode, these failures are usually silent.

> 当然，给 null 和 undefined 设置属性也会报类型错误。给其他值设置属性也不总是成功，有一些属性是只读的，不能重新赋值，有一些对象不允许新增属性。在严格模式下（§5.6.3），属性设定失败时会抛出 TypeError 异常。在非严格模式下，这些失败的处理经常没有任何反应。

The rules that specify when a property assignment succeeds and when it fails are intuitive but difficult to express concisely. An attempt to set a property p of an object o fails in these circumstances:

> 尽管属性赋值成功或失败的规律看起来很简单，但要描述清楚并不容易。在这些场景下给对象 o 设置属性 p 会失败：

o has an own property p that is read-only: it is not possible to set read-only properties.

> o 中的属性 p 是只读的：不能给只读属性重新赋值。

o has an inherited property p that is read-only: it is not possible to hide an inherited read-only property with an own property of the same name.

> o 中的属性 p 是继承属性，且它是只读的：不能通过同名自有属性覆盖只读的继承属性。

o does not have an own property p; o does not inherit a property p with a setter method, and o’s extensible attribute (see §14.2) is false. Since p does not already exist in o, and if there is no setter method to call, then p must be added to o. But if o is not extensible, then no new properties can be defined on it.

> o 中不存在自有属性 p：o 没有使用 setter 方法继承属性 p，并且o的可扩展性是（见 §14.2）false。如果 o 中不存在 p，而且没有 setter 方法可供调用，则 p 一定会添加至 o 中。但如果 o 不是可扩展的，那么在 o 中不能定义新属性。

## 6.4 Deleting Properties
The delete operator (§4.13.4) removes a property from an object. Its single operand should be a property access expression. Surprisingly, delete does not operate on the value of the property but on the property itself:

> 删除运算符（§4.13.4）能删除对象中的属性。它的操作数应当是一个属性访问表达式。令人意外的是，delete 没有操作属性的值，而是操作属性的属性：

```js
delete book.author;          // The book object now has no author property.
delete book["main title"];   // Now it doesn't have "main title", either.
```
The delete operator only deletes own properties, not inherited ones. (To delete an inherited property, you must delete it from the prototype object in which it is defined. Doing this affects every object that inherits from that prototype.)

> delete 运算符只删除自有属性，不删除继承属性。（想要删除一个继承属性，必须从定义这个属性的原型对象上删除它。这会影响所有继承这个原型的对象。）

A delete expression evaluates to true if the delete succeeded or if the delete had no effect (such as deleting a nonexistent property). delete also evaluates to true when used (meaninglessly) with an expression that is not a property access expression:

> 如果删除成功或删除没有任何影响时删除表达式计算结果是 true（如删除不存在的属性）。delete 作用于非属性访问表达式（无用代码）时也返回 true。

```js
let o = {x: 1};    // o has own property x and inherits property toString
delete o.x         // => true: deletes property x
delete o.x         // => true: does nothing (x doesn't exist) but true anyway
delete o.toString  // => true: does nothing (toString isn't an own property)
delete 1           // => true: nonsense, but true anyway
```
delete does not remove properties that have a configurable attribute of false. Certain properties of built-in objects are non-configurable, as are properties of the global object created by variable declaration and function declaration. In strict mode, attempting to delete a non-configurable property causes a TypeError. In non-strict mode, delete simply evaluates to false in this case:

> delete 不能删除那些可配置性为 false 的属性。某些内置对象的属性是不可配置的，比如通过变量声明和函数声明创建的全局对象的属性。在严格模式中，删除一个不可配置属性会报一个类型错误。在非严格模式中，在这些情况下的 delete 操作会返回 false：

```js
// In strict mode, all these deletions throw TypeError instead of returning false
delete Object.prototype // => false: property is non-configurable
var x = 1;              // Declare a global variable
delete globalThis.x     // => false: can't delete this property
function f() {}         // Declare a global function
delete globalThis.f     // => false: can't delete this property either
```
When deleting configurable properties of the global object in non-strict mode, you can omit the reference to the global object and simply follow the delete operator with the property name:

> 当在非严格模式中删除全局对象的可配值属性时，可以省略对全局对象的引用，直接在 delete 操作符后跟随要删除的属性名即可：

```js
globalThis.x = 1;       // Create a configurable global property (no let or var)
delete x                // => true: this property can be deleted
```
In strict mode, however, delete raises a SyntaxError if its operand is an unqualified identifier like x, and you have to be explicit about the property access:

> 然而在严格模式中，delete 后跟随一个非法的操作数（比如 x），则会报一个语法错误，因此必须显式指定对象及其属性：

```js
delete x;               // SyntaxError in strict mode
delete globalThis.x;    // This works
```
## 6.5 Testing Properties
JavaScript objects can be thought of as sets of properties, and it is often useful to be able to test for membership in the set—to check whether an object has a property with a given name. You can do this with the in operator, with the hasOwnProperty() and propertyIsEnumerable() methods, or simply by querying the property. The examples shown here all use strings as property names, but they also work with Symbols (§6.10.3).

> JavaScript 对象可以看作属性的集合，我们经常会检测集合中成员的所属关系——判断某个属性是否存在于某个对象中。可以用 in 运算符、hasOwnPreperty() 和  propertyIsEnumerable() 方法来完成这个工作，甚至仅通过属性查询也可以做到这一点。这节的例子都是用字符串作为属性名称，但是也可以用 Symbol 作为属性名（§6.10.3）。

The in operator expects a property name on its left side and an object on its right. It returns true if the object has an own property or an inherited property by that name:

> in 运算符的左侧是属性名，右侧是对象。如果对象的自有属性或继承属性中包含这个属性则返回 true：

```js
let o = { x: 1 };
"x" in o         // => true: o has an own property "x"
"y" in o         // => false: o doesn't have a property "y"
"toString" in o  // => true: o inherits a toString property
```
The hasOwnProperty() method of an object tests whether that object has an own property with the given name. It returns false for inherited properties:

> 对象的 hasOwnProperty() 方法用来检测给定的名字是否是对象的自有属性。对于继承属性它将返回 false：

```js
let o = { x: 1 };
o.hasOwnProperty("x")        // => true: o has an own property x
o.hasOwnProperty("y")        // => false: o doesn't have a property y
o.hasOwnProperty("toString") // => false: toString is an inherited property
```
The propertyIsEnumerable() refines the hasOwnProperty() test. It returns true only if the named property is an own property and its enumerable attribute is true. Certain built-in properties are not enumerable. Properties created by normal JavaScript code are enumerable unless you’ve used one of the techniques shown in §14.1 to make them non-enumerable.

> propertyIsEnumerable() 是 hasOwnProperty() 的增强版。只有检测到是自有属性且这个属性的可枚举性为 true 时它才返回 true。某些内置属性是不可枚举的。通常由 JavaScript 代码创建的属性都是可枚举的，除非使用  §14.1 中介绍的技术来让它们不可枚举。

```js
let o = { x: 1 };
o.propertyIsEnumerable("x")  // => true: o has an own enumerable property x
o.propertyIsEnumerable("toString")  // => false: not an own property
Object.prototype.propertyIsEnumerable("toString") // => false: not enumerable
```
Instead of using the in operator, it is often sufficient to simply query the property and use !== to make sure it is not undefined:

> 除了使用 in 运算符之外，另一种更简便的方法是使用 !== 判断一个属性是否是 undefined：

```js
let o = { x: 1 };
o.x !== undefined        // => true: o has a property x
o.y !== undefined        // => false: o doesn't have a property y
o.toString !== undefined // => true: o inherits a toString property
```
There is one thing the in operator can do that the simple property access technique shown here cannot do. in can distinguish between properties that do not exist and properties that exist but have been set to undefined. Consider this code:

> 然而有一种场景只能使用 in 运算符而不能使用上述属性访问的方式。in 可以区分不存在的属性和存在但值为 undefined 的属性。例如下面的代码：

```js
let o = { x: undefined };  // Property is explicitly set to undefined
o.x !== undefined          // => false: property exists but is undefined
o.y !== undefined          // => false: property doesn't even exist
"x" in o                   // => true: the property exists
"y" in o                   // => false: the property doesn't exist
delete o.x;                // Delete the property x
"x" in o                   // => false: it doesn't exist anymore
```
## 6.6 Enumerating Properties
Instead of testing for the existence of individual properties, we sometimes want to iterate through or obtain a list of all the properties of an object. There are a few different ways to do this.

> 除了检测对象的属性是否存在，我们还会经常遍历对象的属性。有几种不同的方法可以做到这一点。

The for/in loop was covered in §5.4.5. It runs the body of the loop once for each enumerable property (own or inherited) of the specified object, assigning the name of the property to the loop variable. Built-in methods that objects inherit are not enumerable, but the properties that your code adds to objects are enumerable by default. For example:

> §5.4.5 讨论过 for/in 循环，其可以在循环体中遍历指定对象中所有可枚举的属性（包括自有属性和继承的属性），把属性名称赋值给循环变量。对象继承的 内置方法不可枚举的，但在代码中给对象添加的属性都是可枚举的（除非用下文中提到的一个方法将它们转换为不可枚举的）。例如：

```js
let o = {x: 1, y: 2, z: 3};          // Three enumerable own properties
o.propertyIsEnumerable("toString")   // => false: not enumerable
for(let p in o) {                    // Loop through the properties
    console.log(p);                  // Prints x, y, and z, but not toString
}
```
To guard against enumerating inherited properties with for/in, you can add an explicit check inside the loop body:

> 为了防止 for/in 枚举到继承属性，可以在循环中添加显示检查：

```js
for(let p in o) {
    if (!o.hasOwnProperty(p)) continue;       // Skip inherited properties
}

for(let p in o) {
    if (typeof o[p] === "function") continue; // Skip all methods
}
```
As an alternative to using a for/in loop, it is often easier to get an array of property names for an object and then loop through that array with a for/of loop. There are four functions you can use to get an array of property names:

> 作为使用 for/in 循环的替代方法，通常使用 for/of 循环遍历易获取对象的属性名称数组。可以使用四个函数获取属性名称数组：

Object.keys() returns an array of the names of the enumerable own properties of an object. It does not include non-enumerable properties, inherited properties, or properties whose name is a Symbol (see §6.10.3).

> Object.keys() 返回对象的可枚举自有属性名称数组集合。数组内不包含不可枚举属性、继承属性或属性名称是 Symbol（见 §6.10.3）的属性

Object.getOwnPropertyNames() works like Object.keys() but returns an array of the names of non-enumerable own properties as well, as long as their names are strings.

> Object.getOwnPropertyNames() 用起来和 Object.keys() 类似，但是它返回数组中也包含不可迭代的自有属性，只要它们的名称是字符串。

Object.getOwnPropertySymbols() returns own properties whose names are Symbols, whether or not they are enumerable.

> Object.getOwnPropertySymbols() 返回名称是 Symbol 的自有属性，无论它们是否可枚举。

Reflect.ownKeys() returns all own property names, both enumerable and non-enumerable, and both string and Symbol. (See §14.6.)

> Reflect.ownKeys() 返回所有的自由属性名称，包括可枚举和不可枚举类型，也包括字符串和 Symbol（见 §14.6）。

There are examples of the use of Object.keys() with a for/of loop in §6.7.

> 在 §6.7 中有例子使用 for/of 循环 Object.keys()。

### 6.6.1 Property Enumeration Order
ES6 formally defines the order in which the own properties of an object are enumerated. Object.keys(), Object.getOwnPropertyNames(), Object.getOwnPropertySymbols(), Reflect.ownKeys(), and related methods such as JSON.stringify() all list properties in the following order, subject to their own additional constraints about whether they list non-enumerable properties or properties whose names are strings or Symbols:

> ES6 正式定义元素的自有属性的枚举顺序。Object.keys()、Object.getOwnPropertyNames()、Object.getOwnPropertyNames()、Object.getOwnPropertySymbols()、Reflect.ownKeys() 和相关方法如 JSON.stringify() 属性列表都按以下顺序排列的，受它们自身是否是不可枚举属性列表或者属性是字符串或者 Symbol 影响：

String properties whose names are non-negative integers are listed first, in numeric order from smallest to largest. This rule means that arrays and array-like objects will have their properties enumerated in order.

> 首先列出名称为非负整数的字符串属性，按从最小到最大的数字顺序列出。此规则意味着数组和数组类对象将按顺序枚举其属性。

After all properties that look like array indexes are listed, all remaining properties with string names are listed (including properties that look like negative numbers or floating-point numbers). These properties are listed in the order in which they were added to the object. For properties defined in an object literal, this order is the same order they appear in the literal.

> 列出所有看起来像数组索引的属性后，将列出所有具有字符串名称的剩余属性（包括看起来像负数或浮点数字的属性）。这些属性按添加到对象的顺序列出。对于在对象字面量中定义的属性，此顺序与它们在文本中显示的顺序相同。

Finally, the properties whose names are Symbol objects are listed in the order in which they were added to the object.

> 最后，其名称为 Symbol 对象的属性按添加到对象的顺序列出。

The enumeration order for the for/in loop is not as tightly specified as it is for these enumeration functions, but implementations typically enumerate own properties in the order just described, then travel up the prototype chain enumerating properties in the same order for each prototype object. Note, however, that a property will not be enumerated if a property by that same name has already been enumerated, or even if a non-enumerable property by the same name has already been considered.

> for/in 循环的枚举顺序不像这些枚举函数那样严格指定，但实现通常按刚才描述的顺序枚举自己的属性，然后向上移动原型链按相同顺序枚举每个原型对象的属性。但是请注意，如果已枚举具有相同名称的属性，或者不可枚举属性已经被检测过再次枚举到相同名称的属性，都不会再次枚举。

## 6.7 Extending Objects
A common operation in JavaScript programs is needing to copy the properties of one object to another object. It is easy to do that with code like this:

> 在 JavaScript 代码中有一个很常见的操作，需要将一个对象中的属性拷贝到另外一个对象。以下面的代码很容易实现：

```js
let target = {x: 1}, source = {y: 2, z: 3};
for(let key of Object.keys(source)) {
    target[key] = source[key];
}
target  // => {x: 1, y: 2, z: 3}
```
But because this is a common operation, various JavaScript frameworks have defined utility functions, often named extend(), to perform this copying operation. Finally, in ES6, this ability comes to the core JavaScript language in the form of Object.assign().

> 但是因为这个是个常用的操作，各种 JavaScript 框架定义公用函数，经常将其命名为 extend() 来执行这个拷贝操作。最后在 ES6 中，这个功能以 Object.assign() 的形式被添加到 JavaScript 核心语言中。

Object.assign() expects two or more objects as its arguments. It modifies and returns the first argument, which is the target object, but does not alter the second or any subsequent arguments, which are the source objects. For each source object, it copies the enumerable own properties of that object (including those whose names are Symbols) into the target object. It processes the source objects in argument list order so that properties in the first source object override properties by the same name in the target object and properties in the second source object (if there is one) override properties with the same name in the first source object.

> Object.assign() 需要两个或多个对象作为其实参。它修改并返回第一个实参，即目标对象，但不会改变第二个或任何后续参数，这些参数是源对象。对于每个源对象，它将该对象的可枚举自有属性（包括名称为 Symbol 的属性）复制到目标对象中。它按源对象在实参列表顺序中的顺序处理，所以第一个源对象中的属性会重写在目标对象中的同名属性，然后以第二个源对象中的同名属性（如果有第二个源对象）再次重写第一个源对象重写后的属性。

Object.assign() copies properties with ordinary property get and set operations, so if a source object has a getter method or the target object has a setter method, they will be invoked during the copy, but they will not themselves be copied.

> Object.assign() 通过普通属性的 get 和 set 操作复制属性，因此，如果源对象具有 getter 方法或目标对象具有 setter 方法，则将在复制期间调用它们，但不会复制方法本身。

One reason to assign properties from one object into another is when you have an object that defines default values for many properties and you want to copy those default properties into another object if a property by that name does not already exist in that object. Using Object.assign() naively will not do what you want:

> 看这样一个场景，有一个对象定义许多属性的默认值，希望将这些默认属性中不存在于目标对象中的属性复制到目标对象中，使用 Object.assign() 不会得到想要的结果：

```js
Object.assign(o, defaults);  // overwrites everything in o with defaults
```
Instead, what you can do is to create a new object, copy the defaults into it, and then override those defaults with the properties in o:

> 想得到这个效果需要创建一个新的对象，将默认值拷贝到其中，然后用 o 的属性重写默认值中的属性：

```js
o = Object.assign({}, defaults, o);
```
We’ll see in §6.10.4 that you can also express this object copy-and-override operation using the ... spread operator like this:

> 我们会在 §6.10.4 见到，可以用 ... 展开操作符如下操作这个对象拷贝并重写：

```js
o = {...defaults, ...o};
```
We could also avoid the overhead of the extra object creation and copying by writing a version of Object.assign() that copies properties only if they are missing:

> 为了避免对象创建和复制的额外开销，我们还可以通过编写一个 Object.assign() 仅在缺少属性时复制属性：

```js
// Like Object.assign() but doesn't override existing properties
// (and also doesn't handle Symbol properties)
function merge(target, ...sources) {
    for(let source of sources) {
        for(let key of Object.keys(source)) {
            if (!(key in target)) { // This is different than Object.assign()
                target[key] = source[key];
            }
        }
    }
    return target;
}
Object.assign({x: 1}, {x: 2, y: 2}, {y: 3, z: 4})  // => {x: 2, y: 3, z: 4}
merge({x: 1}, {x: 2, y: 2}, {y: 3, z: 4})          // => {x: 1, y: 2, z: 4}
```
It is straightforward to write other property manipulation utilities like this merge() function. A restrict() function could delete properties of an object if they do not appear in another template object, for example. Or a subtract() function could remove all of the properties of one object from another object.

> 编写其他属性操作公共函数很简单，就是像这个 merge() 函数。例如，如果对象的属性不出现在另一个模板对象中，则 restrict() 函数会删除这些属性。或者，subtract() 函数可以从其他对象中删除一个对象的所有属性。

## 6.8 Serializing Objects
Object serialization is the process of converting an object’s state to a string from which it can later be restored. The functions JSON.stringify() and JSON.parse() serialize and restore JavaScript objects. These functions use the JSON data interchange format. JSON stands for “JavaScript Object Notation,” and its syntax is very similar to that of JavaScript object and array literals:

> 对象序列化（serialization）是指将对象的状态转换为字符串，也可将字符串还原为对象。函数 JSON.stringify() 和 JSON.parse() 用来序列化和还原 JavaScript 对象。这些方法都使用 JSON 作为数据交换格式，JSON 的全称是“JavaScript Object Notation”——JavaScript 对象表示法，它的语法和 JavaScript 对象与数组字面量的语法非常相近：

```js
let o = {x: 1, y: {z: [false, null, ""]}}; // Define a test object
let s = JSON.stringify(o);   // s == '{"x":1,"y":{"z":[false,null,""]}}'
let p = JSON.parse(s);       // p == {x: 1, y: {z: [false, null, ""]}}
```
JSON syntax is a subset of JavaScript syntax, and it cannot represent all JavaScript values. Objects, arrays, strings, finite numbers, true, false, and null are supported and can be serialized and restored. NaN, Infinity, and -Infinity are serialized to null. Date objects are serialized to ISO-formatted date strings (see the Date.toJSON() function), but JSON.parse() leaves these in string form and does not restore the original Date object. Function, RegExp, and Error objects and the undefined value cannot be serialized or restored. JSON.stringify() serializes only the enumerable own properties of an object. If a property value cannot be serialized, that property is simply omitted from the stringified output. Both JSON.stringify() and JSON.parse() accept optional second arguments that can be used to customize the serialization and/or restoration process by specifying a list of properties to be serialized, for example, or by converting certain values during the serialization or stringification process. Complete documentation for these functions is in §11.6.

> JSON 的语法是 JavaScript 语法的子集，它并不能表示 JavaScript 里的所有值。支持对象、数组、字符串、无穷大数字、true、false 和 null，并且它们可以序列化和还原。NaN、Infinity 和 -Infinity 序列化的结果是 null，日期对象序列化的结果是 ISO 格式的日期字符串（参照 Date.toJSON() 函数），但 JSON.parse() 依然保留它们的字符串形态，而不会将它们还原为原始日期对象。函数、RegExp、Error 对象和 undefined 值不能序列化和还原。JSON.stringify() 只能序列化对象可枚举的自有属性。对于一个不能序列化的属性来说，在序列化后的输出字符串中会将这个属性省略掉。JSON.stringify() 和 JSON.parse() 都可以接收第二个可选实参，通过传入需要序列化或还原的属性列表来定制自定义的序列化或还原操作。§11.6 有关于这些函数的详细文档。

## 6.9 Object Methods
As discussed earlier, all JavaScript objects (except those explicitly created without a prototype) inherit properties from Object.prototype. These inherited properties are primarily methods, and because they are universally available, they are of particular interest to JavaScript programmers. We’ve already seen the hasOwnProperty() and propertyIsEnumerable() methods, for example. (And we’ve also already covered quite a few static functions defined on the Object constructor, such as Object.create() and Object.keys().) This section explains a handful of universal object methods that are defined on Object.prototype, but which are intended to be replaced by other, more specialized implementations. In the sections that follow, we show examples of defining these methods on a single object. In Chapter 9, you’ll learn how to define these methods more generally for an entire class of objects.

> 上文已经讨论过，所有的 JavaScript 对象都从 Object.prototype 继承属性（除了那些不通过原型显式创建的对象）。这些继承属性主要是方法，因为 JavaScript 程序员普遍对继承方法更感兴趣。例如我们已经见过的 hasOwnProperty() 和 propertyIsEnumerable() 方法。（并且我们也已经提到了一小部分定义在对象构造函数中的静态函数，像 Object.create() 和 Object.keys()。）本节介绍在 Object.prototype 上定义的少数通用对象方法，但是这些方法经常会被更专业的实现所取代。在下面的各节中，我们将展示在单个对象上定义这些方法的示例。在第 9 章中，将学习如何更常规化地为整个对象类定义这些方法。

### 6.9.1 The toString() Method
The toString() method takes no arguments; it returns a string that somehow represents the value of the object on which it is invoked. JavaScript invokes this method of an object whenever it needs to convert the object to a string. This occurs, for example, when you use the + operator to concatenate a string with an object or when you pass an object to a method that expects a string.

> toString() 方法没有实参，它将返回一个表示调用这个方法的对象值的字符串。在需要将对象转换为字符串的时候，JavaScript 都会调用这个方法。比如，当使用 + 运算符连接一个字符串和一个对象时或者在希望使用字符串的方法中使用了对象时都会调用 toString()。

The default toString() method is not very informative (though it is useful for determining the class of an object, as we will see in §14.4.3). For example, the following line of code simply evaluates to the string “[object Object]”:

> 默认的 toString() 方法的返回值带有的信息量很少（尽管它在检测对象的类型时非常有用，参照 §14.4.3），例如，下面这行代码的计算结果为字符串”[object Object]”：

```js
let s = { x: 1, y: 1 }.toString();  // s == "[object Object]"
```
Because this default method does not display much useful information, many classes define their own versions of toString(). For example, when an array is converted to a string, you obtain a list of the array elements, themselves each converted to a string, and when a function is converted to a string, you obtain the source code for the function. You might define your own toString() method like this:

> 由于默认的 toString() 方法并不会输出很多有用的信息，因此很多类都带有自定义的 toString()。例如，当数组转换为字符串的时候，结果是一个数组元素列表，只是每个元素都转换成了字符串，再比如，当函数转换为字符串的时候，得到函数的源代码。可以像下面这样自定义 toString() 方法：

```js
let point = {
    x: 1,
    y: 2,
    toString: function() { return `(${this.x}, ${this.y})`; }
};
String(point)    // => "(1, 2)": toString() is used for string conversions
```
### 6.9.2 The toLocaleString() Method
In addition to the basic toString() method, objects all have a toLocaleString(). The purpose of this method is to return a localized string representation of the object. The default toLocaleString() method defined by Object doesn’t do any localization itself: it simply calls toString() and returns that value. The Date and Number classes define customized versions of toLocaleString() that attempt to format numbers, dates, and times according to local conventions. Array defines a toLocaleString() method that works like toString() except that it formats array elements by calling their toLocaleString() methods instead of their toString() methods. You might do the same thing with a point object like this:

> 除了基本的 toString() 方法之外，对象都包含 toLocaleString() 方法，这个方法返回一个表示这个对象的本地化字符串。Object 中默认的 toLocaleString() 方法并不做任何本地化自身的操作，它仅调用 toString() 方法并返回对应值。Date 和 Number 类对 toLocaleString() 方法做了定制，可以用它对数字、日期和时间做本地化的转换。 Array 类的 toLocaleString() 方法和 toString() 方法很像，唯一的不同是每个数组元素会调用 toLocaleString() 方法转换为字符串，而不是调用各自的 toString() 方法。可以像这样使用 point 对象做到同样的效果：

```js
let point = {
    x: 1000,
    y: 2000,
    toString: function() { return `(${this.x}, ${this.y})`; },
    toLocaleString: function() {
        return `(${this.x.toLocaleString()}, ${this.y.toLocaleString()})`;
    }
};
point.toString()        // => "(1000, 2000)"
point.toLocaleString()  // => "(1,000, 2,000)": note thousands separators
```
The internationalization classes documented in §11.7 can be useful when implementing a toLocaleString() method.

> 在 §11.7 的国际化类中，toLocaleString() 方法的实现是非常有用的。

### 6.9.3 The valueOf() Method
The valueOf() method is much like the toString() method, but it is called when JavaScript needs to convert an object to some primitive type other than a string—typically, a number. JavaScript calls this method automatically if an object is used in a context where a primitive value is required. The default valueOf() method does nothing interesting, but some of the built-in classes define their own valueOf() method. The Date class defines valueOf() to convert dates to numbers, and this allows Date objects to be chronologically compared with < and >. You could do something similar with a point object, defining a valueOf() method that returns the distance from the origin to the point:

> valueOf() 方法和 toString() 方法非常类似，但往往当 JavaScript 需要将对象转换为某种原始值而非字符串的时候才会调用它，尤其是转换为数字的时候。如果在需要使用原始值的上下文中使用了对象，JavaScript 就会自动调用这个方法。默认的 valueOf() 方法不足为奇，但有些内置类自定义了 valueOf() 方法. Date 类定义 valueOf() 将日期转化成数值型，并且这允许 Date 对象使用 < 和 > 按时间先手顺序比较。可以对 point 对象做同样的事，定义一个 valueOf() 方法返回原点到点的距离：

```js
let point = {
    x: 3,
    y: 4,
    valueOf: function() { return Math.hypot(this.x, this.y); }
};
Number(point)  // => 5: valueOf() is used for conversions to numbers
point > 4      // => true
point > 5      // => false
point < 6      // => true
```
### 6.9.4 The toJSON() Method
Object.prototype does not actually define a toJSON() method, but the JSON.stringify() method (see §6.8) looks for a toJSON() method on any object it is asked to serialize. If this method exists on the object to be serialized, it is invoked, and the return value is serialized, instead of the original object. The Date class (§11.4) defines a toJSON() method that returns a serializable string representation of the date. We could do the same for our Point object like this:

> Object.prototype 实际上没有定义 toJSON() 方法，但对于需要执行序列化的对象来说，JSON.stringify() 方法（见 §6.8）会调用 toJSON() 方法。如果在待序列化的对象中存在这 个方法，则调用它，返回值即是序列化的结果，而不是原始的对象。Date 类（§11.4）定义了 toJSON() 方法返回日期的序列化字符串。我们可以这样对 point 对象做同样的事：

```js
let point = {
    x: 1,
    y: 2,
    toString: function() { return `(${this.x}, ${this.y})`; },
    toJSON: function() { return this.toString(); }
};
JSON.stringify([point])   // => '["(1, 2)"]'
```
## 6.10 Extended Object Literal Syntax
Recent versions of JavaScript have extended the syntax for object literals in a number of useful ways. The following subsections explain these extensions.

> JavaScript 的最新版本扩展了许多有用的对象字面量相关的语法。以下小节解释这些扩展。

### 6.10.1 Shorthand Properties
Suppose you have values stored in variables x and y and want to create an object with properties named x and y that hold those values. With basic object literal syntax, you’d end up repeating each identifier twice:

> 假设值存储在变量 x 和 y 中，并且想要创建具有名为 x 和 y 的属性的对象，这些属性包含这些值。使用基本对象字面量语法，最终会重复每个标识符两次：

```js
let x = 1, y = 2;
let o = {
    x: x,
    y: y
};
```
In ES6 and later, you can drop the colon and one copy of the identifier and end up with much simpler code:

> 在 ES6 之后，可以删除标识符的冒号和一个副本，最终使用更简单的代码：

```js
let x = 1, y = 2;
let o = { x, y };
o.x + o.y  // => 3
```
### 6.10.2 Computed Property Names
Sometimes you need to create an object with a specific property, but the name of that property is not a compile-time constant that you can type literally in your source code. Instead, the property name you need is stored in a variable or is the return value of a function that you invoke. You can’t use a basic object literal for this kind of property. Instead, you have to create an object and then add the desired properties as an extra step:

> 有时需要创建具有特定属性的对象，但该属性的名称不是可以在源代码中键入的编译时常量。相反，需要的属性名称存储在变量中，或者是调用的函数的返回值。不能对此类属性使用基本对象字面量。而必须创建一个对象，通过额外的步骤，添加所需的属性：

```js
const PROPERTY_NAME = "p1";
function computePropertyName() { return "p" + 2; }

let o = {};
o[PROPERTY_NAME] = 1;
o[computePropertyName()] = 2;
```
It is much simpler to set up an object like this with an ES6 feature known as computed properties that lets you take the square brackets from the preceding code and move them directly into the object literal:

> 使用称为计算属性的 ES6 特性设置这样的对象要简单得多，该功能允许从前面的代码写入方括内并直接移动到对象字面量中：

```js
const PROPERTY_NAME = "p1";
function computePropertyName() { return "p" + 2; }

let p = {
    [PROPERTY_NAME]: 1,
    [computePropertyName()]: 2
};

p.p1 + p.p2 // => 3
```
With this new syntax, the square brackets delimit an arbitrary JavaScript expression. That expression is evaluated, and the resulting value (converted to a string, if necessary) is used as the property name.

> 使用这种新语法，方括号将其分隔成 JavaScript 表达式。计算该表达式，并将结果值（如有必要转换为字符串）用作属性名称。

One situation where you might want to use computed properties is when you have a library of JavaScript code that expects to be passed objects with a particular set of properties, and the names of those properties are defined as constants in that library. If you are writing code to create the objects that will be passed to that library, you could hardcode the property names, but you’d risk bugs if you type the property name wrong anywhere, and you’d risk version mismatch issues if a new version of the library changes the required property names. Instead, you might find that it makes your code more robust to use computed property syntax with the property name constants defined by the library.

> 可能想要使用计算属性的一个情况是，有一个 JavaScript 代码库，该库希望传递具有一组特定属性的对象，并且这些属性的名称定义为该库中的常量。如果要编写代码以创建将传递给该库的对象，可以硬编码属性名称，但如果在任何地方键入错误的属性名称，则存在错误风险；如果库的新版本更改了所需的属性名称，则存在版本不匹配问题的风险。相反，可能会发现，使用计算属性语法与库定义的属性名称常量时，它使代码更加健壮。

### 6.10.3 Symbols as Property Names
The computed property syntax enables one other very important object literal feature. In ES6 and later, property names can be strings or symbols. If you assign a symbol to a variable or constant, then you can use that symbol as a property name using the computed property syntax:

> 计算属性语法启用了另一个非常重要的对象字面量特性。在 ES6 之后，属性名称可以是字符串或 Symbol。如果将 Symbol 分配给变量或常量，则可以使用计算属性语法将该 Symbol 用作属性名称：

```js
const extension = Symbol("my extension symbol");
let o = {
    [extension]: { /* extension data stored in this object */ }
};
o[extension].x = 0; // This won't conflict with other properties of o
```
As explained in §3.6, Symbols are opaque values. You can’t do anything with them other than use them as property names. Every Symbol is different from every other Symbol, however, which means that Symbols are good for creating unique property names. Create a new Symbol by calling the Symbol() factory function. (Symbols are primitive values, not objects, so Symbol() is not a constructor function that you invoke with new.) The value returned by Symbol() is not equal to any other Symbol or other value. You can pass a string to Symbol(), and this string is used when your Symbol is converted to a string. But this is a debugging aid only: two Symbols created with the same string argument are still different from one another.

> 如 §3.6 中所述，符号是不透明值。除了将它们用作属性名称，不能对它们进行任何其他处理。但是，每个 Symbol 都不同于所有其他 Symbol，这意味着 Symbol 适合创建唯一的属性名称。通过调用 Symbol() 工厂函数创建新 Symbol。（Symbol 是原始值，而不是对象，因此 Symbol() 不是使用 new 调用的构造函数。）Symbol() 返回的值不等于任何其他 Symbol 或其他值。可以将字符串传递给 Symbol()，当 Symbol 转换为字符串时，将使用此字符串。但是，这只是一个调试帮助：使用同一字符串参数创建的两个 Symbol 仍然彼此不同。

The point of Symbols is not security, but to define a safe extension mechanism for JavaScript objects. If you get an object from third-party code that you do not control and need to add some of your own properties to that object but want to be sure that your properties will not conflict with any properties that may already exist on the object, you can safely use Symbols as your property names. If you do this, you can also be confident that the third-party code will not accidentally alter your symbolically named properties. (That third-party code could, of course, use Object.getOwnPropertySymbols() to discover the Symbols you’re using and could then alter or delete your properties. This is why Symbols are not a security mechanism.)

> Symbol 的要点不是安全性，而是为 JavaScript 对象定义一个安全的扩展机制。如果从第三方代码获取对象，您无法控制该对象，并且需要向该对象添加自己的一些属性，但希望确保属性不会与对象上可能存在的任何属性冲突，可以安全地使用 Symbol 作为属性名称。如果这样做，还可以确信第三方代码不会意外更改 Symbol 命名的属性。（当然，该第三方代码可以使用 Object.getOwnPropertySymbols() 来发现你使用的 Symbol，然后可以更改或删除你的属性。这就是为什么符号不是安全机制。）

### 6.10.4 Spread Operator
In ES2018 and later, you can copy the properties of an existing object into a new object using the “spread operator” ... inside an object literal:

> 在 ES2018 之后，可以使用展开运算符 ... 将现有的对象中的属性复制到新的对象中：

```js
let position = { x: 0, y: 0 };
let dimensions = { width: 100, height: 75 };
let rect = { ...position, ...dimensions };
rect.x + rect.y + rect.width + rect.height // => 175
```
In this code, the properties of the position and dimensions objects are “spread out” into the rect object literal as if they had been written literally inside those curly braces. Note that this ... syntax is often called a spread operator but is not a true JavaScript operator in any sense. Instead, it is a special-case syntax available only within object literals. (Three dots are used for other purposes in other JavaScript contexts, but object literals are the only context where the three dots cause this kind of interpolation of one object into another one.)

> 在此代码中，position 和 dimensions 对象的属性被展开到 rect 对象字面量中，就像它们以字面量的方式写入这些大括号中一样。请注意，... 语法通常称为展开运算符，但在任何情况下都不是真正的 JavaScript 运算符。相反，它是一种特殊情况下语法，仅在对象文本中可用。（... 在别的 JavaScript 上下文中有其他用途，但是对象字面量上下文中只有这一种用法。）

If the object that is spread and the object it is being spread into both have a property with the same name, then the value of that property will be the one that comes last:

> 如果展开的目标对象和源对象中具有相同的名称，则该属性的值将是位置处于后面的值：

```js
let o = { x: 1 };
let p = { x: 0, ...o };
p.x   // => 1: the value from object o overrides the initial value
let q = { ...o, x: 2 };
q.x   // => 2: the value 2 overrides the previous value from o.
```
Also note that the spread operator only spreads the own properties of an object, not any inherited ones:

> 还有注意展开运算符只展开对象的自有属性，不展开继承属性：

```js
let o = Object.create({x: 1}); // o inherits the property x
let p = { ...o };
p.x                            // => undefined
```
Finally, it is worth noting that, although the spread operator is just three little dots in your code, it can represent a substantial amount of work to the JavaScript interpreter. If an object has n properties, the process of spreading those properties into another object is likely to be an O(n) operation. This means that if you find yourself using ... within a loop or recursive function as a way to accumulate data into one large object, you may be writing an inefficient O(n2) algorithm that will not scale well as n gets larger.

> 最后，值得注意的是，虽然展开运算符在代码中只是三个小点，但它对 JavaScript 解释器来说可以代表大量的工作。如果对象具有 n 个属性，则将这些属性分散到另一个对象的过程很可能是 O(n) 操作。这意味着，如果你发现自己在使用 ... 在循环或递归函数中，类似将数据累积到一个大对象中的方法，您可能正在编写一个低效的 O(n2) 算法，该算法不会随着 n 变大而扩展。

### 6.10.5 Shorthand Methods
When a function is defined as a property of an object, we call that function a method (we’ll have a lot more to say about methods in Chapters 8 and 9). Prior to ES6, you would define a method in an object literal using a function definition expression just as you would define any other property of an object:

> 当函数被定义为对象的属性时，我们称该函数为方法（我们将在第 8 章和第 9 章中对方法有更多的描述）。在 ES6 之前，在对象字面量中用函数定义表达式定义一个方法和在对象中定义其他属性一样：

```js
let square = {
    area: function() { return this.side * this.side; },
    side: 10
};
square.area() // => 100
```
In ES6, however, the object literal syntax (and also the class definition syntax we’ll see in Chapter 9) has been extended to allow a shortcut where the function keyword and the colon are omitted, resulting in code like this:

> 但是，在 ES6 中，对象字面量语法（以及我们将在第 9 章中看到的类定义语法）已扩展成允许省略函数关键字和冒号的快捷方式，可以写成这样的代码：

```js
let square = {
    area() { return this.side * this.side; },
    side: 10
};
square.area() // => 100
```
Both forms of the code are equivalent: both add a property named area to the object literal, and both set the value of that property to the specified function. The shorthand syntax makes it clearer that area() is a method and not a data property like side.

> 两种形式是相同的：在对象字面量中添加一个名为 area 的属性，并指定一个函数为这个属性的值。速记语法更清晰的看出 area() 是一个方法而不是一个像 side 一样的数据属性。

When you write a method using this shorthand syntax, the property name can take any of the forms that are legal in an object literal: in addition to a regular JavaScript identifier like the name area above, you can also use string literals and computed property names, which can include Symbol property names:

> 使用此速记语法编写方法时，属性名称可以采用对象字面量中的任何合法形式：除了像上面的名称 area 这样的常规 JavaScript 标识符外，还可以使用字符串字面量和计算属性名称，包括 Symbol 属性名称：

```js
const METHOD_NAME = "m";
const symbol = Symbol();
let weirdMethods = {
    "method With Spaces"(x) { return x + 1; },
    [METHOD_NAME](x) { return x + 2; },
    [symbol](x) { return x + 3; }
};
weirdMethods["method With Spaces"](1)  // => 2
weirdMethods[METHOD_NAME](1)           // => 3
weirdMethods[symbol](1)                // => 4
```
Using a Symbol as a method name is not as strange as it seems. In order to make an object iterable (so it can be used with a for/of loop), you must define a method with the symbolic name Symbol.iterator, and there are examples of doing exactly that in Chapter 12.

> 使用 Symbol 作为方法名称并不像看起来那么奇怪。为了使对象可迭代（因此它可以与 for/of 循环一起使用），必须定义一个具有符号名称 Symbol.iterator 的方法，并且在第 12 章中有这样做的示例。

### 6.10.6 Property Getters and Setters
All of the object properties we’ve discussed so far in this chapter have been data properties with a name and an ordinary value. JavaScript also supports accessor properties, which do not have a single value but instead have one or two accessor methods: a getter and/or a setter.

> 到目前为止，本节我们所讨论的所有的对象都是具有名称和普通值的数据属性。JavaScript 还支持存取器属性，这些属性没有单个值，而是具有一个或两个存取器方法：getter 和或是或 setter。

When a program queries the value of an accessor property, JavaScript invokes the getter method (passing no arguments). The return value of this method becomes the value of the property access expression. When a program sets the value of an accessor property, JavaScript invokes the setter method, passing the value of the righthand side of the assignment. This method is responsible for “setting,” in some sense, the property value. The return value of the setter method is ignored.

> 当程序查询存取器属性的值时，JavaScript 调用 getter 方法（无实参）。这个方法的返回值就是属性存取表达式的值。当程序设置一个存取器属性的值时， JavaScript 调用 setter 方法，将赋值表达式右侧的值当做参数传入 setter。从某种意义上讲，这个方法负责“设置”属性值。可以忽略 setter 方法的返回值。

If a property has both a getter and a setter method, it is a read/write property. If it has only a getter method, it is a read-only property. And if it has only a setter method, it is a write-only property (something that is not possible with data properties), and attempts to read it always evaluate to undefined.

> 如果属性同时有 getter 和 setter 方法，则它是一个可读写属性。如果它只含有 getter 方法，它是一个只读属性。如果它只有 setter 方法，它是一个只可写属性（这对一个数据属性来说是不可能的），如果尝试去读它，计算结果永远是 undefined。

Accessor properties can be defined with an extension to the object literal syntax (unlike the other ES6 extensions we’ve seen here, getters and setters were introduced in ES5):

> 存储器属性可以通过表达式在对象字面量语法中定义（不像我们在这里看到的其他 ES6 扩展，getter 和 setter 是 ES5 中的内容）：

```js
let o = {
    // An ordinary data property
    dataProp: value,

    // An accessor property defined as a pair of functions.
    get accessorProp() { return this.dataProp; },
    set accessorProp(value) { this.dataProp = value; }
};
```
Accessor properties are defined as one or two methods whose name is the same as the property name. These look like ordinary methods defined using the ES6 shorthand except that getter and setter definitions are prefixed with get or set. (In ES6, you can also use computed property names when defining getters and setters. Simply replace the property name after get or set with an expression in square brackets.)

> 存储器属性定义为名称与属性名称相同的一个或两个方法。这些方法看起来像使用 ES6 速记定义的普通方法，只不过 getter 和 setter 定义使用 get 或 set 前缀。（在 ES6 中，在定义 getter 和 setter 时还可以使用计算属性名称。只需将带方括号的表达式替换属性名称即可。

The accessor methods defined above simply get and set the value of a data property, and there is no reason to prefer the accessor property over the data property. But as a more interesting example, consider the following object that represents a 2D Cartesian point. It has ordinary data properties to represent the x and y coordinates of the point, and it has accessor properties that give the equivalent polar coordinates of the point:

> 上面定义的存储器方法只需获取并设置数据属性的值，没有理由将存储器属性替换数据属性。但作为一个更有趣的示例，请考虑以下表示 2D 笛卡尔点的对象。它具有表示点的 x 和 y 坐标的普通数据属性，并且具有提供点等效极坐标的存储器属性：

```js
let p = {
    // x and y are regular read-write data properties.
    x: 1.0,
    y: 1.0,

    // r is a read-write accessor property with getter and setter.
    // Don't forget to put a comma after accessor methods.
    get r() { return Math.hypot(this.x, this.y); },
    set r(newvalue) {
        let oldvalue = Math.hypot(this.x, this.y);
        let ratio = newvalue/oldvalue;
        this.x *= ratio;
        this.y *= ratio;
    },

    // theta is a read-only accessor property with getter only.
    get theta() { return Math.atan2(this.y, this.x); }
};
p.r     // => Math.SQRT2
p.theta // => Math.PI / 4
```
Note the use of the keyword this in the getters and setter in this example. JavaScript invokes these functions as methods of the object on which they are defined, which means that within the body of the function, this refers to the point object p. So the getter method for the r property can refer to the x and y properties as this.x and this.y. Methods and the this keyword are covered in more detail in §8.2.2.

> 请注意，在本示例中的 getter 和 setter 中使用 this 关键字。JavaScript 以对象的方法的方式调用这些函数，这意味着在函数体中，this 指的是点对象 p。因此，r 属性的 getter 方法通过 this.x 和 this.y 获取到 x 和 y 属性的引用。方法以及 this 关键字在 §8.2.2 中详细介绍。

Accessor properties are inherited, just as data properties are, so you can use the object p defined above as a prototype for other points. You can give the new objects their own x and y properties, and they’ll inherit the r and theta properties:

> 存储器属性是可继承的，就像数据属性一样，因此可以使用上面定义的对象 p 作为其他点的原型。可以为新对象提供自有的 x 和 y 属性，它们将继承 r 和 theta 属性：

```js
let q = Object.create(p); // A new object that inherits getters and setters
q.x = 3; q.y = 4;         // Create q's own data properties
q.r                       // => 5: the inherited accessor properties work
q.theta                   // => Math.atan2(4, 3)
```
The code above uses accessor properties to define an API that provides two representations (Cartesian coordinates and polar coordinates) of a single set of data. Other reasons to use accessor properties include sanity checking of property writes and returning different values on each property read:

> 上述代码使用存储器属性定义一个 API，该 API 提供一组数据的两种表示形式（笛卡尔坐标和极坐标）。使用存储器属性的其他场景包括属性写入的稳健性检测以及在每个属性上返回不同的值：

```js
// This object generates strictly increasing serial numbers
const serialnum = {
    // This data property holds the next serial number.
    // The _ in the property name hints that it is for internal use only.
    _n: 0,

    // Return the current value and increment it
    get next() { return this._n++; },

    // Set a new value of n, but only if it is larger than current
    set next(n) {
        if (n > this._n) this._n = n;
        else throw new Error("serial number can only be set to a larger value");
    }
};
serialnum.next = 10;    // Set the starting serial number
serialnum.next          // => 10
serialnum.next          // => 11: different value each time we get next
```
Finally, here is one more example that uses a getter method to implement a property with “magical” behavior:

> 最后，下面是使用 getter 方法实现具有"魔幻"行为的属性的示例：

```js
// This object has accessor properties that return random numbers.
// The expression "random.octet", for example, yields a random number
// between 0 and 255 each time it is evaluated.
const random = {
    get octet() { return Math.floor(Math.random()*256); },
    get uint16() { return Math.floor(Math.random()*65536); },
    get int16() { return Math.floor(Math.random()*65536)-32768; }
};
```
## 6.11 Summary
This chapter has documented JavaScript objects in great detail, covering topics that include:

Basic object terminology, including the meaning of terms like enumerable and own property.

Object literal syntax, including the many new features in ES6 and later.

How to read, write, delete, enumerate, and check for the presence of the properties of an object.

How prototype-based inheritance works in JavaScript and how to create an object that inherits from another object with Object.create().

How to copy properties from one object into another with Object.assign().

All JavaScript values that are not primitive values are objects. This includes both arrays and functions, which are the topics of the next two chapters.

> 本章非常详细地记录了 JavaScript 对象，涵盖的主题包括：

> 基本对象术语，包括可枚举和自有属性等术语的含义。

> 对象字面量语法，包括 ES6 及以后的许多新特性。

> 如何读取、写入、删除、枚举和检查对象属性是否存在。

> 基于原型的继承是如何在 JavaScript 中工作，以及如何使用 Object.create() 创建一个从另一个对象继承的对象。

> 如何使用 Object.assign() 将属性从一个对象复制到另一个对象。

> 所有 JavaScript 的非原始值都是对象。这包括数组和函数，这是接下来两章的主题。

---

1. Remember; almost all objects have a prototype but most do not have a property named prototype. JavaScript inheritance works even if you can’t access the prototype object directly. But see §14.3 if you want to learn how to do that.

> 1. 记住，几乎所有对象都有一个原型，但大多数对象没有名为 prototype 的属性。即使不能直接访问原型对象，JavaScript 继承依然工作。但是，如果你想学习如何做到这一点，请参阅 §14.3。