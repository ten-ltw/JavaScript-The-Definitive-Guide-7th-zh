# 第 3 章 类型、值和变量

Computer programs work by manipulating values, such as the number 3.14 or the text “Hello World.” The kinds of values that can be represented and manipulated in a programming language are known as types, and one of the most fundamental characteristics of a programming language is the set of types it supports. When a program needs to retain a value for future use, it assigns the value to (or “stores” the value in) a variable. Variables have names, and they allow use of those names in our programs to refer to values. The way that variables work is another fundamental characteristic of any programming language. This chapter explains types, values, and variables in JavaScript. It begins with an overview and some definitions.

> 计算机程序通过处理数值来工作，比如数字 3.14 或文本“Hello World”。在编程语言中可以表示和操作的值的种类称为类型，而编程语言最基本的特征之一就是它所支持的类型集。当程序需要保留一个值以供将来使用时，它将该值赋给（或将该值“存储”在）一个变量。变量有名称，它们允许在程序中使用这些名称来引用值。变量工作的方式是任何编程语言的另一个基本特征。本章解释了 JavaScript 中的类型、值和变量。它以概述和一些定义开始。

## 3.1 Overview and Definitions

JavaScript types can be divided into two categories: primitive types and object types. JavaScript’s primitive types include numbers, strings of text (known as strings), and Boolean truth values (known as booleans). A significant portion of this chapter is dedicated to a detailed explanation of the numeric (§3.2) and string (§3.3) types in JavaScript. Booleans are covered in §3.4.

> JavaScript 类型可以分为两类：基本类型和对象类型。JavaScript 的基本类型包括数字、文本字符串（称为字符串）和布尔真实性值（称为布尔值）。这一章的重要部分是专门详细解释 JavaScript 中的数字（§3.2）和字符串（§3.3）类型。在 §3.4 中介绍了布尔值。

The special JavaScript values null and undefined are primitive values, but they are not numbers, strings, or booleans. Each value is typically considered to be the sole member of its own special type. §3.5 has more about null and undefined. ES6 adds a new special-purpose type, known as Symbol, that enables the definition of language extensions without harming backward compatibility. Symbols are covered briefly in §3.6.

> 特殊的 JavaScript 值 null 和 undefined 是基本值，但它们不是数字、字符串或布尔值。每个值通常被认为是它自己特殊类型的唯一成员。§3.5 有更多关于 null 和 undefined 的内容。ES6 添加了一种新的特殊用途类型，称为 Symbol，它支持在不损害向后兼容性的情况下定义语言扩展。符号在§3.6中有简要介绍。

Any JavaScript value that is not a number, a string, a boolean, a symbol, null, or undefined is an object. An object (that is, a member of the type object) is a collection of properties where each property has a name and a value (either a primitive value or another object). One very special object, the global object, is covered in §3.7, but more general and more detailed coverage of objects is in Chapter 6.

> 任何不是数字、字符串、布尔值、Symbol、null 或 undefined 的 JavaScript 值都是对象。对象（即类型对象的成员）是属性的集合，其中每个属性都有一个名称和一个值（原始值或另一个对象）。一个非常特殊的对象，全局对象，在 §3.7 中介绍过了，但是在第 6 章中对对象进行了更广泛、更详细的介绍。

An ordinary JavaScript object is an unordered collection of named values. The language also defines a special kind of object, known as an array, that represents an ordered collection of numbered values. The JavaScript language includes special syntax for working with arrays, and arrays have some special behavior that distinguishes them from ordinary objects. Arrays are the subject of Chapter 7.

> 普通的 JavaScript 对象是命名值的无序集合。该语言还定义了一种特殊类型的对象，称为数组，它表示编号值的有序集合。JavaScript 语言包含处理数组的特殊语法，数组有一些特殊的行为将它们与普通对象区分开来。数组是第 7 章的主题。

In addition to basic objects and arrays, JavaScript defines a number of other useful object types. A Set object represents a set of values. A Map object represents a mapping from keys to values. Various “typed array” types facilitate operations on arrays of bytes and other binary data. The RegExp type represents textual patterns and enables sophisticated matching, searching, and replacing operations on strings. The Date type represents dates and times and supports rudimentary date arithmetic. Error and its subtypes represent errors that can arise when executing JavaScript code. All of these types are covered in Chapter 11.

> 除了基本对象和数组之外，JavaScript 还定义了许多其他有用的对象类型。Set 对象表示一组值。Map 对象表示从键到值的映射。各种“类型化数组”类型促进了对字节数组和其他二进制数据的操作。RegExp 类型表示文本模式，支持对字符串进行复杂的匹配、搜索和替换操作。Date 类型表示日期和时间，并支持基本的日期运算。Error 及其子类型表示在执行 JavaScript 代码时可能出现的错误。所有这些类型都在第 11 章中介绍。

JavaScript differs from more static languages in that functions and classes are not just part of the language syntax: they are themselves values that can be manipulated by JavaScript programs. Like any JavaScript value that is not a primitive value, functions and classes are a specialized kind of object. They are covered in detail in Chapters 8 and 9.

> JavaScript 与更静态的语言的不同之处在于，函数和类不仅仅是语言语法的一部分：它们本身是可由 JavaScript 程序操作的值。像任何不是基本值的 JavaScript 值一样，函数和类是一种特殊的对象。它们将在第 8 章和第 9 章中详细介绍。

The JavaScript interpreter performs automatic garbage collection for memory management. This means that a JavaScript programmer generally does not need to worry about destruction or deallocation of objects or other values. When a value is no longer reachable—when a program no longer has any way to refer to it—the interpreter knows it can never be used again and automatically reclaims the memory it was occupying. (JavaScript programmers do sometimes need to take care to ensure that values do not inadvertently remain reachable—and therefore nonreclaimable—longer than necessary.)

> JavaScript 解释器为内存管理执行自动垃圾收集。这意味着 JavaScript 程序员通常不需要担心对象或其他值的销毁或释放。当一个值不再可获得时——当程序不再有方法引用它时——解释器知道它再也不能被使用，并自动收回它所占用的内存。（JavaScript 程序员有时确实需要注意确保值不会意外地超时保持可用——导致不可收回。）

JavaScript supports an object-oriented programming style. Loosely, this means that rather than having globally defined functions to operate on values of various types, the types themselves define methods for working with values. To sort the elements of an array a, for example, we don’t pass a to a sort() function. Instead, we invoke the sort() method of a:

> JavaScript 支持面向对象的编程风格。不严格地说，这意味着不是用全局定义的函数来操作各种类型的值，而是由类型本身定义处理值的方法。例如，要对数组 a 的元素进行排序，我们不需要将 a 传递给 sort() 函数。相反，我们调用 sort() 方法：

```js
a.sort();       // The object-oriented version of sort(a).
```

Method definition is covered in Chapter 9. Technically, it is only JavaScript objects that have methods. But numbers, strings, boolean, and symbol values behave as if they have methods. In JavaScript, null and undefined are the only values that methods cannot be invoked on.

> 方法定义将在第 9 章中介绍。从技术上讲，只有 JavaScript 对象才有方法。但是数字、字符串、布尔值和符号值的行为就好像它们有方法一样。在 JavaScript 中，只有 null 和 undefined 值不能调用方法。

JavaScript’s object types are mutable and its primitive types are immutable. A value of a mutable type can change: a JavaScript program can change the values of object properties and array elements. Numbers, booleans, symbols, null, and undefined are immutable—it doesn’t even make sense to talk about changing the value of a number, for example. Strings can be thought of as arrays of characters, and you might expect them to be mutable. In JavaScript, however, strings are immutable: you can access the text at any index of a string, but JavaScript provides no way to alter the text of an existing string. The differences between mutable and immutable values are explored further in §3.8.

> JavaScript 的对象类型是可变的，它的基本类型是不可变的。可变类型的值可以更改：JavaScript 程序可以更改对象属性和数组元素的值。数字、布尔值、符号、null 和 undefined 都是不可更改的——例如，讨论更改某个数字的值甚至都没有意义。字符串可以看作是字符数组，您可能希望它们是可变的。然而，在 JavaScript 中，字符串是不可变的：您可以在字符串的任何索引处访问文本，但是 JavaScript 没有提供改变现有字符串文本的方法。可变值和不可变值之间的区别在 §3.8 中有进一步的探讨。

JavaScript liberally converts values from one type to another. If a program expects a string, for example, and you give it a number, it will automatically convert the number to a string for you. And if you use a non-boolean value where a boolean is expected, JavaScript will convert accordingly. The rules for value conversion are explained in §3.9. JavaScript’s liberal value conversion rules affect its definition of equality, and the == equality operator performs type conversions as described in §3.9.1. (In practice, however, the == equality operator is deprecated in favor of the strict equality operator ===, which does no type conversions. See §4.9.1 for more about both operators.)

> JavaScript 自由地将值从一种类型转换为另一种类型。例如，如果程序需要一个字符串，而您给了它一个数字，它会自动将数字转换为字符串。如果在需要布尔值的地方使用了非布尔值，JavaScript 将相应地进行转换。值转换的规则在 §3.9 中解释。JavaScript 的自由值转换规则会影响相等的定义，`==`相等运算符会执行 §3.9.1 中描述的类型转换。（然而，在实践中，== 相等运算符已弃用，而使用严格的相等运算符`===`，它不进行类型转换。关于这两个运算符的更多信息请参见 §4.9.1。）

Constants and variables allow you to use names to refer to values in your programs. Constants are declared with const and variables are declared with let (or with var in older JavaScript code). JavaScript constants and variables are untyped: declarations do not specify what kind of values will be assigned. Variable declaration and assignment are covered in §3.10.

> 常量和变量允许您在程序中使用名称来引用值。常量是用 const 声明的，变量是用 let 声明的（在旧的JavaScript代码中是用var声明的）。JavaScript 常量和变量都是无类型的：声明不指定要赋给哪种类型的值。变量声明和赋值见 §3.10。

As you can see from this long introduction, this is a wide-ranging chapter that explains many fundamental details about how data is represented and manipulated in JavaScript. We’ll begin by diving right in to the details of JavaScript numbers and text.

> 从这篇冗长的介绍中可以看出，这一章内容广泛，解释了关于如何在 JavaScript 中表示和操作数据的许多基本细节。首先，我们将深入了解 JavaScript 数字和文本的细节。

## 3.2 Number
JavaScript’s primary numeric type, Number, is used to represent integers and to approximate real numbers. JavaScript represents numbers using the 64-bit floating-point format defined by the IEEE 754 standard,1 which means it can represent numbers as large as ±1.7976931348623157 × 10308 and as small as ±5 × 10−324.

> JavaScript 的主要数字类型 Number 用于表示整数和近似实数。JavaScript 使用 IEEE 754 标准定义的64位浮点格式表示数字1，这意味着它可以表示大到±1.7976931348623157×10308，小到±5×10−324的数字。

The JavaScript number format allows you to exactly represent all integers between −9,007,199,254,740,992 (−253) and 9,007,199,254,740,992 (253), inclusive. If you use integer values larger than this, you may lose precision in the trailing digits. Note, however, that certain operations in JavaScript (such as array indexing and the bitwise operators described in Chapter 4) are performed with 32-bit integers. If you need to exactly represent larger integers, see §3.2.5.

> JavaScript 数字格式允许你精确地表示 9,007,199,254,740,992(−253) 和 9,007,199,254,740,992(253) 之间的所有整数。如果使用大于这个值的整数值，则可能会丢失末尾数字的精度。然而，请注意，JavaScript 中的某些操作（如数组索引和第 4 章中描述的位运算符）是用 32 位整数执行的。如果你需要精确地表示更大的整数，请参阅 §3.2.5。

When a number appears directly in a JavaScript program, it’s called a numeric literal. JavaScript supports numeric literals in several formats, as described in the following sections. Note that any numeric literal can be preceded by a minus sign (-) to make the number negative.

> 当一个数字直接出现在 JavaScript 程序中时，它被称为数字文字。JavaScript 支持几种格式的数字文字，如下面的章节所述。注意，任何数字文字前面都可以加一个减号(-)，以使数字为负。

### 3.2.1 Integer Literals
In a JavaScript program, a base-10 integer is written as a sequence of digits. For example:

> 在 JavaScript 程序中，以 10 为基数的整数被写成数字序列。例如：

```js
0
3
10000000
```

In addition to base-10 integer literals, JavaScript recognizes hexadecimal (base-16) values. A hexadecimal literal begins with 0x or 0X, followed by a string of hexadecimal digits. A hexadecimal digit is one of the digits 0 through 9 or the letters a (or A) through f (or F), which represent values 10 through 15. Here are examples of hexadecimal integer literals:

> 除了以 10 为基数的整数字面量之外，JavaScript 还可以识别十六进制（以 16 为基数）的值。以 0x 或 0x 开头的十六进制文字，后面跟着一串十六进制数字。16进制数字是数字 0 到 9 或字母 a（或A）到 f（或F）中的一个，表示值 10 到 15。以下是十六进制整数字面量的例子:

```js
0xff       // => 255: (15*16 + 15)
0xBADCAFE  // => 195939070
```

In ES6 and later, you can also express integers in binary (base 2) or octal (base 8) using the prefixes 0b and 0o (or 0B and 0O) instead of 0x:

> 在 ES6 及后续版本中，还可以使用前缀 0b 和 0o（或0B和0O）来表示二进制（以 2 为基数）或八进制（以 8 为基数）的整数，而不是 0x：

```js
0b10101  // => 21:  (1*16 + 0*8 + 1*4 + 0*2 + 1*1)
0o377    // => 255: (3*64 + 7*8 + 7*1)
```
### 3.2.2 Floating-Point Literals
Floating-point literals can have a decimal point; they use the traditional syntax for real numbers. A real value is represented as the integral part of the number, followed by a decimal point and the fractional part of the number.

> 浮点字面值可以有小数点；他们使用传统的实数语法。实数表示为数字的整数部分，然后是小数点和小数部分。

Floating-point literals may also be represented using exponential notation: a real number followed by the letter e (or E), followed by an optional plus or minus sign, followed by an integer exponent. This notation represents the real number multiplied by 10 to the power of the exponent.

> 浮点字量也可以用指数表示法表示：一个实数后面跟着字母 e（或 E），后面跟着一个可选的加号或减号，然后是一个整数指数。这种记数方法表示的数值，是由前面的实数乘以10的指数次幂。

More succinctly, the syntax is:

> 更简洁地说，语法是：

```js
[digits][.digits][(E|e)[(+|-)]digits]
```
For example:

> 例如:

```js
3.14
2345.6789
.333333333333333333
6.02e23        // 6.02 × 10²³
1.4738223E-32  // 1.4738223 × 10⁻³²
```
SEPARATORS IN NUMERIC LITERALS

You can use underscores within numeric literals to break long literals up into chunks that are easier to read:

> 你可以在数字字面值中使用下划线将长字面值分解成更容易阅读的块：
```js
let billion = 1_000_000_000;   // Underscore as a thousands separator.
let bytes = 0x89_AB_CD_EF;     // As a bytes separator.
let bits = 0b0001_1101_0111;   // As a nibble separator.
let fraction = 0.123_456_789;  // Works in the fractional part, too.
```

At the time of this writing in early 2020, underscores in numeric literals are not yet formally standardized as part of JavaScript. But they are in the advanced stages of the standardization process and are implemented by all major browsers and by Node.

> 在 2020 年初撰写本文时，数字字面值中的下划线还没有作为 JavaScript 的一部分正式标准化。但是它们处于标准化过程的高级阶段，所有主流浏览器和 Node 都实现了它们。

### 3.2.3 Arithmetic in JavaScript

JavaScript programs work with numbers using the arithmetic operators . that the language provides. These include + for addition, - for subtraction, * for multiplication, / for division, and % for modulo (remainder after division). ES2016 adds ** for exponentiation. Full details on these and other operators can be found in Chapter 4.

> JavaScript 程序使用算术运算符处理数字。这是语言提供的。这些参数包括 + 表示加法，- 表示减法，* 表示乘法，/ 表示除法，% 表示取模（除后的余数）。ES2016 为取幂添加了 **。关于这些运算符和其他运算符的详细信息可以在第 4 章中找到。

In addition to these basic arithmetic operators, JavaScript supports more complex mathematical operations through a set of functions and constants defined as properties of the Math object:

> 除了这些基本的算术运算符，JavaScript 还支持更加复杂的算术运算，这些复杂运算通过作为 Math 对象的属性定义的函数和常量来实现：

```js
Math.pow(2,53)           // => 9007199254740992: 2 to the power 53
Math.round(.6)           // => 1.0: round to the nearest integer
Math.ceil(.6)            // => 1.0: round up to an integer
Math.floor(.6)           // => 0.0: round down to an integer
Math.abs(-5)             // => 5: absolute value
Math.max(x,y,z)          // Return the largest argument
Math.min(x,y,z)          // Return the smallest argument
Math.random()            // Pseudo-random number x where 0 <= x < 1.0
Math.PI                  // π: circumference of a circle / diameter
Math.E                   // e: The base of the natural logarithm
Math.sqrt(3)             // => 3**0.5: the square root of 3
Math.pow(3, 1/3)         // => 3**(1/3): the cube root of 3
Math.sin(0)              // Trigonometry: also Math.cos, Math.atan, etc.
Math.log(10)             // Natural logarithm of 10
Math.log(100)/Math.LN10  // Base 10 logarithm of 100
Math.log(512)/Math.LN2   // Base 2 logarithm of 512
Math.exp(3)              // Math.E cubed
```

ES6 defines more functions on the Math object:

> ES6 在 Math 对象上定义了更多的函数:

```js
Math.cbrt(27)    // => 3: cube root
Math.hypot(3, 4) // => 5: square root of sum of squares of all arguments
Math.log10(100)  // => 2: Base-10 logarithm
Math.log2(1024)  // => 10: Base-2 logarithm
Math.log1p(x)    // Natural log of (1+x); accurate for very small x
Math.expm1(x)    // Math.exp(x)-1; the inverse of Math.log1p()
Math.sign(x)     // -1, 0, or 1 for arguments <, ==, or > 0
Math.imul(2,3)   // => 6: optimized multiplication of 32-bit integers
Math.clz32(0xf)  // => 28: number of leading zero bits in a 32-bit integer
Math.trunc(3.9)  // => 3: convert to an integer by truncating fractional part
Math.fround(x)   // Round to nearest 32-bit float number
Math.sinh(x)     // Hyperbolic sine. Also Math.cosh(), Math.tanh()
Math.asinh(x)    // Hyperbolic arcsine. Also Math.acosh(), Math.atanh()
```

Arithmetic in JavaScript does not raise errors in cases of overflow, underflow, or division by zero. When the result of a numeric operation is larger than the largest representable number (overflow), the result is a special infinity value, Infinity. Similarly, when the absolute value of a negative value becomes larger than the absolute value of the largest representable negative number, the result is negative infinity, -Infinity. The infinite values behave as you would expect: adding, subtracting, multiplying, or dividing them by anything results in an infinite value (possibly with the sign reversed).

> JavaScript 中的算术在溢出、下溢或除以 0 的情况下不会引发错误。当数值操作的结果大于最大可表示数（溢出）时，结果是一个特殊的无穷值，即 Infinity。同样，当一个负数的绝对值大于最大可表示负数的绝对值时，结果是负无穷，-Infinity。无穷值的行为与您预期的一样：加、减、乘或除任何值都会产生无穷值（可能符号颠倒）。

Underflow occurs when the result of a numeric operation is closer to zero than the smallest representable number. In this case, JavaScript returns 0. If underflow occurs from a negative number, JavaScript returns a special value known as “negative zero.” This value is almost completely indistinguishable from regular zero and JavaScript programmers rarely need to detect it.

> 当数值操作的结果比最小的可表示数字更接近于零时，就会发生下溢。在这种情况下，JavaScript 返回 0。如果下溢发生在负数，JavaScript 将返回一个特殊的值，称为“负零”。这个值与普通的 0 几乎没有区别，JavaScript 程序员几乎不需要检测它。

Division by zero is not an error in JavaScript: it simply returns infinity or negative infinity. There is one exception, however: zero divided by zero does not have a well-defined value, and the result of this operation is the special not-a-number value, NaN. NaN also arises if you attempt to divide infinity by infinity, take the square root of a negative number, or use arithmetic operators with non-numeric operands that cannot be converted to numbers.

> 在 JavaScript 中除以 0 不是错误：它只是返回无穷大或负无穷大。然而，有一个例外：0 除以 0 没有一个定义良好的值，这个操作的结果是一个特殊的非数字值 NaN。如果您试图将无穷除以无穷，取负数的平方根，或使用带有不能转换为数字的非数字操作数的算术运算符，则还会出现 NaN。

JavaScript predefines global constants Infinity and NaN to hold the positive infinity and not-a-number value, and these values are also available as properties of the Number object:

> JavaScript 预先定义了全局常量 Infinity 和 NaN 来保存正的无穷大和非数值，这些值也可以作为 Number 对象的属性：

```js
Infinity                    // A positive number too big to represent
Number.POSITIVE_INFINITY    // Same value
1/0                         // => Infinity
Number.MAX_VALUE * 2        // => Infinity; overflow

-Infinity                   // A negative number too big to represent
Number.NEGATIVE_INFINITY    // The same value
-1/0                        // => -Infinity
-Number.MAX_VALUE * 2       // => -Infinity

NaN                         // The not-a-number value
Number.NaN                  // The same value, written another way
0/0                         // => NaN
Infinity/Infinity           // => NaN

Number.MIN_VALUE/2          // => 0: underflow
-Number.MIN_VALUE/2         // => -0: negative zero
-1/Infinity                 // -> -0: also negative 0
-0

// The following Number properties are defined in ES6
Number.parseInt()       // Same as the global parseInt() function
Number.parseFloat()     // Same as the global parseFloat() function
Number.isNaN(x)         // Is x the NaN value?
Number.isFinite(x)      // Is x a number and finite?
Number.isInteger(x)     // Is x an integer?
Number.isSafeInteger(x) // Is x an integer -(2**53) < x < 2**53?
Number.MIN_SAFE_INTEGER // => -(2**53 - 1)
Number.MAX_SAFE_INTEGER // => 2**53 - 1
Number.EPSILON          // => 2**-52: smallest difference between numbers
```

The not-a-number value has one unusual feature in JavaScript: it does not compare equal to any other value, including itself. This means that you can’t write x === NaN to determine whether the value of a variable x is NaN. Instead, you must write x != x or Number.isNaN(x). Those expressions will be true if, and only if, x has the same value as the global constant NaN.

> 非数值在 JavaScript 中有一个不同寻常的特性：它不等于任何其他值，包括它自己。这意味着您不能编写`x === NaN`来确定变量 x 的值是否为 NaN。相反，你必须写`x != x`或`Number.isNaN(x)`。当且仅当 x 具有与全局常量 NaN 相同的值时，这些表达式将为真。

The global function isNaN() is similar to Number.isNaN(). It returns true if its argument is NaN, or if that argument is a non-numeric value that cannot be converted to a number. The related function Number.isFinite() returns true if its argument is a number other than NaN, Infinity, or -Infinity. The global isFinite() function returns true if its argument is, or can be converted to, a finite number.

> 全局函数 isNaN() 类似于 Number.isNaN()。如果它的实参是 NaN，或者该实参是一个不能转换为数字的非数字值，则返回 true。相关函数 Number.isFinite() 如果实参不是 NaN、Infinity 或 -Infinity，则返回 true。全局的 isFinite() 函数如果它的实参是一个有限数，或者可以转换为一个有限数，则返回 true。

The negative zero value is also somewhat unusual. It compares equal (even using JavaScript’s strict equality test) to positive zero, which means that the two values are almost indistinguishable, except when used as a divisor:

> 负零值也有些不寻常。它和正零值是相等的（甚至使用 JavaScript 的严格相等测试来判断）。这意味着这两个值几乎一模一样，除了作为除数之外：

```js
let zero = 0;         // Regular zero
let negz = -0;        // Negative zero
zero === negz         // => true: zero and negative zero are equal
1/zero === 1/negz     // => false: Infinity and -Infinity are not equal
```
### 3.2.4 Binary Floating-Point and Rounding Errors

There are infinitely many real numbers, but only a finite number of them (18,437,736,874,454,810,627, to be exact) can be represented exactly by the JavaScript floating-point format. This means that when you’re working with real numbers in JavaScript, the representation of the number will often be an approximation of the actual number.

> 有无穷多的实数，但只有有限的数（确切地说，18,437,736,874,454,810,627）可以用 JavaScript 浮点格式精确地表示。这意味着在 JavaScript 中处理实数时，数字的表示通常是实际数字的近似值。

The IEEE-754 floating-point representation used by JavaScript (and just about every other modern programming language) is a binary representation, which can exactly represent fractions like 1/2, 1/8, and 1/1024. Unfortunately, the fractions we use most commonly (especially when performing financial calculations) are decimal fractions: 1/10, 1/100, and so on. Binary floating-point representations cannot exactly represent numbers as simple as 0.1.

> JavaScript（以及几乎所有其他现代编程语言）使用的 IEEE-754 浮点表示法是二进制表示法，它可以精确地表示像 1/2、1/8 和 1/1024 这样的分数。不幸的是，我们最常用的分数（特别是在执行财务计算时）是十进制分数：1/10、1/100，等等。二进制浮点表示法不能精确地表示像 0.1 这样简单的数字。

JavaScript numbers have plenty of precision and can approximate 0.1 very closely. But the fact that this number cannot be represented exactly can lead to problems. Consider this code:

> JavaScript 数字有足够的精度，可以非常接近 0.1。但这个数字不能准确地表示，这可能会导致问题。考虑这段代码：

```js
let x = .3 - .2;    // thirty cents minus 20 cents
let y = .2 - .1;    // twenty cents minus 10 cents
x === y             // => false: the two values are not the same!
x === .1            // => false: .3-.2 is not equal to .1
y === .1            // => true: .2-.1 is equal to .1
```

Because of rounding error, the difference between the approximations of .3 and .2 is not exactly the same as the difference between the approximations of .2 and .1. It is important to understand that this problem is not specific to JavaScript: it affects any programming language that uses binary floating-point numbers. Also, note that the values x and y in the code shown here are very close to each other and to the correct value. The computed values are adequate for almost any purpose; the problem only arises when we attempt to compare values for equality.

> 由于舍入误差，.3 和 .2 的近似值与 .2 和 .1 的近似值之间的差并不完全相同。需要注意的是，这个问题并不是 JavaScript 特有的：它会影响任何使用二进制浮点数的编程语言。另外，请注意，这里显示的代码中的值 x 和 y 非常接近，也非常接近正确的值。计算的值几乎适用于任何目的；只有当我们试图比较平等的价值时，问题才会出现。

If these floating-point approximations are problematic for your programs, consider using scaled integers. For example, you might manipulate monetary values as integer cents rather than fractional dollars.

> 如果这些浮点逼使的程序出现问题时，请考虑使用缩放整数。例如，您可以将货币值转为整数美分，而不是小数美元。

### 3.2.5 Arbitrary Precision Integers with BigInt

One of the newest features of JavaScript, defined in ES2020, is a new numeric type known as BigInt. As of early 2020, it has been implemented in Chrome, Firefox, Edge, and Node, and there is an implementation in progress in Safari. As the name implies, BigInt is a numeric type whose values are integers. The type was added to JavaScript mainly to allow the representation of 64-bit integers, which are required for compatibility with many other programming languages and APIs. But BigInt values can have thousands or even millions of digits, should you have need to work with numbers that large. (Note, however, that BigInt implementations are not suitable for cryptography because they do not attempt to prevent timing attacks.)

> 在 ES2020 中定义的 JavaScript 最新特性之一是一种名为 BigInt 的新数字类型。到 2020 年初，它已经在 Chrome、Firefox、Edge 和 Node 中实现，Safari 也正在实现中。顾名思义，BigInt 是一种数值类型，其值为整数。该类型添加到 JavaScript 主要是为了支持 64 位整数的表示，这是与许多其他编程语言和 api 兼容所必需的。但是，如果需要处理这么大的数字，BigInt 值可以有数千甚至数百万位数字。（但是，请注意，BigInt 实现不适合密码学，因为它们不试图阻止计时攻击。）

BigInt literals are written as a string of digits followed by a lowercase letter n. By default, the are in base 10, but you can use the 0b, 0o, and 0x prefixes for binary, octal, and hexadecimal BigInts:

> Bigint 字面量以数字字符串编写，后跟小写字母 n。默认情况下，它是 10 进制的，但您可以将 0b、0o 和 0x 前缀用于二进制、八进制和十六进制 BigInts：

```js
1234n                // A not-so-big BigInt literal
0b111111n            // A binary BigInt
0o7777n              // An octal BigInt
0x8000000000000000n  // => 2n**63n: A 64-bit integer
```
You can use BigInt() as a function for converting regular JavaScript numbers or strings to BigInt values:

> 你可以使用 BigInt() 作为函数，将普通的 JavaScript 数字或字符串转换为 BigInt 值:

```js
BigInt(Number.MAX_SAFE_INTEGER)     // => 9007199254740991n
let string = "1" + "0".repeat(100); // 1 followed by 100 zeros.
BigInt(string)                      // => 10n**100n: one googol
```

Arithmetic with BigInt values works like arithmetic with regular JavaScript numbers, except that division drops any remainder and rounds down (toward zero):

> 使用 BigInt 值的算术运算与使用常规 JavaScript 数字的算术运算类似，只不过除法会去掉任何余数（归 0）:

```js
1000n + 2000n  // => 3000n
3000n - 2000n  // => 1000n
2000n * 3000n  // => 6000000n
3000n / 997n   // => 3n: the quotient is 3
3000n % 997n   // => 9n: and the remainder is 9
(2n ** 131071n) - 1n  // A Mersenne prime with 39457 decimal digits
```

Although the standard +, -, *, /, %, and ** operators work with BigInt, it is important to understand that you may not mix operands of type BigInt with regular number operands. This may seem confusing at first, but there is a good reason for it. If one numeric type was more general than the other, it would be easy to define arithmetic on mixed operands to simply return a value of the more general type. But neither type is more general than the other: BigInt can represent extraordinarily large values, making it more general than regular numbers. But BigInt can only represent integers, making the regular JavaScript number type more general. There is no way around this problem, so JavaScript sidesteps it by simply not allowing mixed operands to the arithmetic operators.

> 尽管标准的 +、-、*、/、% 和 ** 运算符可用于BigInt，但重要的是要理解不能将 BigInt 类型的操作数与常规的数字操作数混合使用。乍一看，这可能令人困惑，但这是有充分理由的。如果一种数字类型比另一种类型更通用，那么很容易在混合操作数上定义算术，只返回更通用类型的值。但是这两种类型都比另一种更通用：BigInt可以表示非常大的值，这使得它比普通数字更通用。但是 BigInt 只能表示整数，这使得常规的 JavaScript 数字类型更加通用。没有办法绕过这个问题，所以 JavaScript 只是通过不允许算术运算符使用混合操作数来绕过这个问题。

Comparison operators, by contrast, do work with mixed numeric types (but see §3.9.1 for more about the difference between == and ===):

> 相比之下，比较运算符适用于混合数值类型（关于 == 和 === 的区别，请参阅 §3.9.1）：

```js
1 < 2n     // => true
2 > 1n     // => true
0 == 0n    // => true
0 === 0n   // => false: the === checks for type equality as well
```

The bitwise operators (described in §4.8.3) generally work with BigInt operands. None of the functions of the Math object accept BigInt operands, however.

> 按位运算符（在 §4.8.3 中描述）通常用于 BigInt 操作数。但是，Math 对象的函数都不接受 BigInt 操作数。

### 3.2.6 Dates and Times
JavaScript defines a simple Date class for representing and manipulating the numbers that represent dates and times. JavaScript Dates are objects, but they also have a numeric representation as a timestamp that specifies the number of elapsed milliseconds since January 1, 1970:

> JavaScript 定义了一个简单的 Date 类，用于表示和操作表示日期和时间的数字。JavaScript 的日期是对象，但它们也有一个数字表示形式的时间戳，指定了自1970年1月1日以来经过的毫秒数：

```js
let timestamp = Date.now();  // The current time as a timestamp (a number).
let now = new Date();        // The current time as a Date object.
let ms = now.getTime();      // Convert to a millisecond timestamp.
let iso = now.toISOString(); // Convert to a string in standard format.
```
The Date class and its methods are covered in detail in §11.4. But we will see Date objects again in §3.9.3 when we examine the details of JavaScript type conversions.

> Date 类及其方法在 §11.4 中有详细介绍。但在 §3.9.3 节中，我们会在讨论 JavaScript 类型转换的细节时再次看到 Date 对象。

## 3.3 Text

The JavaScript type for representing text is the string. A string is an immutable ordered sequence of 16-bit values, each of which typically represents a Unicode character. The length of a string is the number of 16-bit values it contains. JavaScript’s strings (and its arrays) use zero-based indexing: the first 16-bit value is at position 0, the second at position 1, and so on. The empty string is the string of length 0. JavaScript does not have a special type that represents a single element of a string. To represent a single 16-bit value, simply use a string that has a length of 1.

> 表示文本的 JavaScript 类型是字符串。字符串是由 16 位值组成的不可变有序序列，每个值通常代表一个 Unicode 字符。字符串的长度是它包含的 16 位值的个数。JavaScript 的字符串（及其数组）使用从零开始的索引：第一个 16 位的值位于位置 0，第二个位于位置 1，以此类推。空字符串是长度为 0 的字符串。JavaScript 没有特殊的类型来表示字符串的单个元素。要表示单个 16 位值，只需使用长度为 1 的字符串。

CHARACTERS, CODEPOINTS, AND JAVASCRIPT STRINGS

> **字符集，内码和JavaScript字符串**

JavaScript uses the UTF-16 encoding of the Unicode character set, and JavaScript strings are sequences of unsigned 16-bit values. The most commonly used Unicode characters (those from the “basic multilingual plane”) have codepoints that fit in 16 bits and can be represented by one element of a string. Unicode characters whose codepoints do not fit in 16 bits are encoded using the rules of UTF-16 as a sequence (known as a “surrogate pair”) of two 16-bit values. This means that a JavaScript string of length 2 (two 16-bit values) might represent only a single Unicode character:

> JavaScript 使用 Unicode 字符集的 UTF-16 编码，JavaScript 字符串是无符号的 16 位值序列。最常用的 Unicode 字符（来自“基本多语种平面”的字符）都是通过 16 位的内码表示，并代表字符串中的单个字符。那些不能表示为16位的 Unicode 字符则遵循 UTF-16 编码规则——用两个 16 位值组成的一个序列（亦称做“代理项对”）表示。这意味着一个长度为 2 的 JavaScript 字符串（两个 16 位值）有可能表 一个 Unicode 字符：

```js
let euro = "€";
let love = "❤";
euro.length   // => 1: this character has one 16-bit element
love.length   // => 2: UTF-16 encoding of ❤ is "\ud83d\udc99"
```

Most string-manipulation methods defined by JavaScript operate on 16-bit values, not characters. They do not treat surrogate pairs specially, they perform no normalization of the string, and don’t even ensure that a string is well-formed UTF-16.

> JavaScript 定义的大多数字符串操作方法操作的是 16 位值，而不是字符。它们没有特别对待代理对，它们没有对字符串执行规范化，甚至不确保字符串是格式良好的 UTF-16。

In ES6, however, strings are iterable, and if you use the for/of loop or ... operator with a string, it will iterate the actual characters of the string, not the 16-bit values.

> 然而，在 ES6 中，字符串是可迭代的，如果你使用 for/of 循环或 … 运算符，它将迭代字符串的实际字符，而不是 16 位值。

### 3.3.1 String Literals

To include a string in a JavaScript program, simply enclose the characters of the string within a matched pair of single or double quotes or backticks (' or " or `). Double-quote characters and backticks may be contained within strings delimited by single-quote characters, and similarly for strings delimited by double quotes and backticks. Here are examples of string literals:

> 要在 JavaScript 程序中包含字符串，只需将字符串的字符包含在匹配的单引号或双引号或反引号（' or " or `）中。双引号字符和反引号可以包含在由单引号字符分隔的字符串中，由双引号和反引号分隔的字符串也是如此。以下是字符串字面量的例子:

```js
""  // The empty string: it has zero characters
'testing'
"3.14"
'name="myform"'
"Wouldn't you prefer O'Reilly's book?"
"τ is the ratio of a circle's circumference to its radius"
`"She said 'hi'", he said.`
```

Strings delimited with backticks are a feature of ES6, and allow JavaScript expressions to be embedded within (or interpolated into) the string literal. This expression interpolation syntax is covered in §3.3.4.

> 用反引号包含的字符串是 ES6 的一个特性，它允许 JavaScript 表达式嵌入（或插入）字符串字面量。这种表达式插值语法在 §3.3.4 中介绍。

The original versions of JavaScript required string literals to be written on a single line, and it is common to see JavaScript code that creates long strings by concatenating single-line strings with the + operator. As of ES5, however, you can break a string literal across multiple lines by ending each line but the last with a backslash `(\)`. Neither the backslash nor the line terminator that follow it are part of the string literal. If you need to include a newline character in a single-quoted or double-quoted string literal, use the character sequence \n (documented in the next section). The ES6 backtick syntax allows strings to be broken across multiple lines, and in this case, the line terminators are part of the string literal:

> 最初的 JavaScript 版本要求将字符串文字写在单行上，通常会看到 JavaScript 代码通过使用 + 运算符连接单行字符串来创建长字符串。但是，在 ES5 中，您可以通过在每行末尾使用反斜杠（`\`）来将字符串分隔成多行。反斜杠及其后面的行结束符都不是字符串字面值的一部分。如果需要在单引号或双引号的字符串文字中包含换行字符，请使用字符序列 \n（在下一节中介绍）。ES6 反引号语法允许字符串跨多行分割，在这种情况下，行结束符是字符串字面值的一部分：

```js
// A string representing 2 lines written on one line:
'two\nlines'

// A one-line string written on 3 lines:
"one\
 long\
 line"

// A two-line string written on two lines:
`the newline character at the end of this line
is included literally in this string`
```

Note that when you use single quotes to delimit your strings, you must be careful with English contractions and possessives, such as can’t and O’Reilly’s. Since the apostrophe is the same as the single-quote character, you must use the backslash character (`\`) to “escape” any apostrophes that appear in single-quoted strings (escapes are explained in the next section).

> 注意，当您使用单引号来分隔字符串时，必须小心使用英语缩写和所有格，如 can't 和 O'Reilly's。由于撇号与单引号字符相同，必须使用反斜杠字符（`\`）来“转义”出现在单引号字符串中的任何撇号（转义将在下一节中解释）。

In client-side JavaScript programming, JavaScript code may contain strings of HTML code, and HTML code may contain strings of JavaScript code. Like JavaScript, HTML uses either single or double quotes to delimit its strings. Thus, when combining JavaScript and HTML, it is a good idea to use one style of quotes for JavaScript and the other style for HTML. In the following example, the string “Thank you” is single-quoted within a JavaScript expression, which is then double-quoted within an HTML event-handler attribute:

> 在客户端 JavaScript 编程中，JavaScript 代码可能包含 HTML 代码字符串，HTML 代码可能包含 JavaScript 代码字符串。和 JavaScript 一样，HTML 也使用单引号或双引号来分隔字符串。因此，在组合 JavaScript 和 HTML 时，最好使用一种风格的引号用于 JavaScript，另一种风格的引号用于 HTML。在下面的例子中，字符串“Thank you”在 JavaScript 表达式中被单引号引用，然后在 HTML 事件处理程序属性中被双引号引用:

```js
<button onclick="alert('Thank you')">Click Me</button>
```
### 3.3.2 Escape Sequences in String Literals

The backslash character `(\)` has a special purpose in JavaScript strings. Combined with the character that follows it, it represents a character that is not otherwise representable within the string. For example, \n is an escape sequence that represents a newline character.

> 反斜杠字符（`\`）在 JavaScript 字符串中有特殊用途。与它后面的字符相结合，它表示字符串中不能以其他方式表示的字符。例如，\n 是表示换行符的转义序列。

Another example, mentioned earlier, is the \' escape, which represents the single quote (or apostrophe) character. This escape sequence is useful when you need to include an apostrophe in a string literal that is contained within single quotes. You can see why these are called escape sequences: the backslash allows you to escape from the usual interpretation of the single-quote character. Instead of using it to mark the end of the string, you use it as an apostrophe:

> 前面提到的另一个例子是 \' 转义符，它表示单引号（或撇号）字符。当您需要在包含在单引号中的字符串文本中包含撇号时，这个转义序列非常有用。您可以看到为什么它们被称为转义序列：反斜杠允许您转义单引号字符的通常解释。不是用它来标记字符串的结束，而是用它作为撇号：

```js
'You\'re right, it can\'t be a quote'
```
Table 3-1 lists the JavaScript escape sequences and the characters they represent. Three escape sequences are generic and can be used to represent any character by specifying its Unicode character code as a hexadecimal number. For example, the sequence \xA9 represents the copyright symbol, which has the Unicode encoding given by the hexadecimal number A9. Similarly, the \u escape represents an arbitrary Unicode character specified by four hexadecimal digits or one to five digits when the digits are enclosed in curly braces: \u03c0 represents the character π, for example, and \u{1f600} represents the “grinning face” emoji.

> JavaScript 转义序列及其代表的字符如表 3-1 所示。三个转义序列是通用的，可以通过将 Unicode 字符代码指定为十六进制数来表示任何字符。例如，序列 \xA9 表示版权符号，它具有由十六进制数字 A9 给出的 Unicode 编码。同样，\u 转义表示由四个十六进制数字或用花括号括起来的 1 ~ 5 个数字指定的任意 Unicode 字符：例如，\u03c0 表示字符 π，\u{1f600} 表示“龇牙笑”表情。

Table 3-1. JavaScript escape sequences

| Sequence | Character represented                                                                                                   |
| -------- | ----------------------------------------------------------------------------------------------------------------------- |
| \0       | The NUL character (\u0000)                                                                                              |
| \b       | Backspace (\u0008)                                                                                                      |
| \t       | Horizontal tab (\u0009)                                                                                                 |
| \n       | Newline (\u000A)                                                                                                        |
| \v       | Vertical tab (\u000B)                                                                                                   |
| \f       | Form feed (\u000C)                                                                                                      |
| \r       | Carriage return (\u000D)                                                                                                |
| \"       | Double quote (\u0022)                                                                                                   |
| \'       | Apostrophe or single quote (\u0027)                                                                                     |
| `\\`     | Backslash (\u005C)                                                                                                      |
| \xnn     | The Unicode character specified by the two hexadecimal digits nn                                                        |
| \unnnn   | The Unicode character specified by the four hexadecimal digits nnnn                                                     |
| \u{n}    | The Unicode character specified by the codepoint n, where n is one to six hexadecimal digits between 0 and 10FFFF (ES6) |

If the \ character precedes any character other than those shown in Table 3-1, the backslash is simply ignored (although future versions of the language may, of course, define new escape sequences). For example, `\#` is the same as #. Finally, as noted earlier, ES5 allows a backslash before a line break to break a string literal across multiple lines.

> 如果 \ 字符在表 3-1 中以外的任何字符之前，反斜杠将被忽略（当然，未来版本的语言可能会定义新的转义序列）。例如，`\#` 和 # 是一样的。最后，如前所述，ES5 允许在换行之前使用反斜杠来跨多行分割字符串字面量。

### 3.3.3 Working with Strings

One of the built-in features of JavaScript is the ability to concatenate strings. If you use the + operator with numbers, it adds them. But if you use this operator on strings, it joins them by appending the second to the first. For example:

> JavaScript 的内置特性之一是连接字符串的能力。如果您对数字使用 + 运算符，它将它们相加。但是如果你在字符串上使用这个运算符，它通过将第二个运算符附加到第一个运算符上来连接字符串。例如：

```js
let msg = "Hello, " + "world";   // Produces the string "Hello, world"
let greeting = "Welcome to my blog," + " " + name;
```
Strings can be compared with the standard === equality and !== inequality operators: two strings are equal if and only if they consist of exactly the same sequence of 16-bit values. Strings can also be compared with the <, <=, >, and >= operators. String comparison is done simply by comparing the 16-bit values. (For more robust locale-aware string comparison and sorting, see §11.7.3.)

> 字符串可以与标准的 === 相等和 !== 不等运算符进行比较：当且仅当两个字符串由完全相同的 16 位值序列组成时，它们才相等。字符串还可以与 <、<=、> 和 >= 运算符进行比较。字符串比较简单地通过比较 16 位值来完成。（更健壮的语言环境感知字符串比较和排序，见 §11.7.3。）

To determine the length of a string—the number of 16-bit values it contains—use the length property of the string:

> 要确定一个字符串的长度——它包含的 16 位值的数量——使用字符串的 length 属性：

```js
s.length
```

In addition to this length property, JavaScript provides a rich API for working with strings:

> 除了这个 length 属性，JavaScript 还提供了一个丰富的 API 来处理字符串：

```js
let s = "Hello, world"; // Start with some text.

// Obtaining portions of a string
s.substring(1,4)        // => "ell": the 2nd, 3rd, and 4th characters.
s.slice(1,4)            // => "ell": same thing
s.slice(-3)             // => "rld": last 3 characters
s.split(", ")           // => ["Hello", "world"]: split at delimiter string

// Searching a string
s.indexOf("l")          // => 2: position of first letter l
s.indexOf("l", 3)       // => 3: position of first "l" at or after 3
s.indexOf("zz")         // => -1: s does not include the substring "zz"
s.lastIndexOf("l")      // => 10: position of last letter l

// Boolean searching functions in ES6 and later
s.startsWith("Hell")    // => true: the string starts with these
s.endsWith("!")         // => false: s does not end with that
s.includes("or")        // => true: s includes substring "or"

// Creating modified versions of a string
s.replace("llo", "ya")  // => "Heya, world"
s.toLowerCase()         // => "hello, world"
s.toUpperCase()         // => "HELLO, WORLD"
s.normalize()           // Unicode NFC normalization: ES6
s.normalize("NFD")      // NFD normalization. Also "NFKC", "NFKD"

// Inspecting individual (16-bit) characters of a string
s.charAt(0)             // => "H": the first character
s.charAt(s.length-1)    // => "d": the last character
s.charCodeAt(0)         // => 72: 16-bit number at the specified position
s.codePointAt(0)        // => 72: ES6, works for codepoints > 16 bits

// String padding functions in ES2017
"x".padStart(3)         // => "  x": add spaces on the left to a length of 3
"x".padEnd(3)           // => "x  ": add spaces on the right to a length of 3
"x".padStart(3, "*")    // => "**x": add stars on the left to a length of 3
"x".padEnd(3, "-")      // => "x--": add dashes on the right to a length of 3

// Space trimming functions. trim() is ES5; others ES2019
" test ".trim()         // => "test": remove spaces at start and end
" test ".trimStart()    // => "test ": remove spaces on left. Also trimLeft
" test ".trimEnd()      // => " test": remove spaces at right. Also trimRight

// Miscellaneous string methods
s.concat("!")           // => "Hello, world!": just use + operator instead
"<>".repeat(5)          // => "<><><><><>": concatenate n copies. ES6
```

Remember that strings are immutable in JavaScript. Methods like replace() and toUpperCase() return new strings: they do not modify the string on which they are invoked.

> 记住，字符串在 JavaScript 中是不可变的。像 replace() 和 toUpperCase() 这样的方法返回新的字符串：它们不会修改调用它们的字符串。

Strings can also be treated like read-only arrays, and you can access individual characters (16-bit values) from a string using square brackets instead of the charAt() method:

> 字符串也可以像只读数组一样处理，你可以使用方括号而不是 charAt() 方法从字符串中访问单个字符（16 位值）:

```js
let s = "hello, world";
s[0]                  // => "h"
s[s.length-1]         // => "d"
```
### 3.3.4 Template Literals

In ES6 and later, string literals can be delimited with backticks:

> 在 ES6 及以后的版本中，字符串文字可以用反引号分隔：
```js
let s = `hello world`;
```
This is more than just another string literal syntax, however, because these template literals can include arbitrary JavaScript expressions. The final value of a string literal in backticks is computed by evaluating any included expressions, converting the values of those expressions to strings and combining those computed strings with the literal characters within the backticks:

> 然而，这不仅仅是另一种字符串字面量语法，因为这些模板字面量可以包含任意的 JavaScript 表达式。反引号中的字符串字面量的原始值是通过计算包含的表达式来计算的，将这些表达式的值转换为字符串，并将这些计算出来的字符串与反引号中的字面量字符组合起来:

```js
let name = "Bill";
let greeting = `Hello ${ name }.`;  // greeting == "Hello Bill."
```

Everything between the ${ and the matching } is interpreted as a JavaScript expression. Everything outside the curly braces is normal string literal text. The expression inside the braces is evaluated and then converted to a string and inserted into the template, replacing the dollar sign, the curly braces, and everything in between them.

> ${ 和匹配 } 之间的所有内容都被解释为 JavaScript 表达式。大括号之外的都是普通的字符串文本。括号内的表达式被求值，然后转换为字符串并插入到模板中，替换美元符号、花括号以及它们之间的所有内容。

A template literal may include any number of expressions. It can use any of the escape characters that normal strings can, and it can span any number of lines, with no special escaping required. The following template literal includes four JavaScript expressions, a Unicode escape sequence, and at least four newlines (the expression values may include newlines as well):

> 模板字面量可以包含任意数量的表达式。它可以使用普通字符串可以使用的任何转义字符，并且可以跨任意数量的行，不需要特殊转义。下面的模板文字包含四个 JavaScript 表达式，一个 Unicode 转义序列，以及至少四个换行符（表达式值也可以包含换行符）：

```js
let errorMessage = `\
\u2718 Test failure at ${filename}:${linenumber}:
${exception.message}
Stack trace:
${exception.stack}
`;
```

The backslash at the end of the first line here escapes the initial newline so that the resulting string begins with the Unicode ✘ character (\u2718) rather than a newline.

> 第一行末尾的反斜杠转义了最初的换行符，这样产生的字符串以 Unicode 符合英语习惯的字符（\u2718）开始，而不是换行符。

TAGGED TEMPLATE LITERALS

> **标签模版字面量**

A powerful but less commonly used feature of template literals is that, if a function name (or “tag”) comes right before the opening backtick, then the text and the values of the expressions within the template literal are passed to the function. The value of this “tagged template literal” is the return value of the function. This could be used, for example, to apply HTML or SQL escaping to the values before substituting them into the text.

> 模板字面值的一个强大但不太常用的特性是，如果一个函数名（或“标签”）恰好出现在开始的反勾之前，那么模板字面值中的文本和表达式的值就会传递给该函数。这个“标记模板字面量”的值是函数的返回值。例如，这可以用于在将值替换到文本之前对值应用 HTML 或 SQL 转义。

ES6 has one built-in tag function: String.raw(). It returns the text within backticks without any processing of backslash escapes:

> ES6 有一个内置的标记函数：String.raw()。它在不处理任何反斜杠转义的情况下返回带有反引号的文本:

```js
`\n`.length            // => 1: the string has a single newline character
String.raw`\n`.length  // => 2: a backslash character and the letter n
```

Note that even though the tag portion of a tagged template literal is a function, there are no parentheses used in its invocation. In this very specific case, the backtick characters replace the open and close parentheses.

> 请注意，尽管标记模板文字的标记部分是一个函数，但在调用它时没有使用圆括号。在这个非常特定的例子中，反勾字符替换了开括号和闭括号。

The ability to define your own template tag functions is a powerful feature of JavaScript. These functions do not need to return strings, and they can be used like constructors, as if defining a new literal syntax for the language. We’ll see an example in §14.5.

> 定义自己的模板标记函数的能力是 JavaScript 的一个强大特性。这些函数不需要返回字符串，它们可以像构造函数一样使用，就像为语言定义新的文字语法一样。我们将在 §14.5 中看到一个例子。

### 3.3.5 Pattern Matching

JavaScript defines a datatype known as a regular expression (or RegExp) for describing and matching patterns in strings of text. RegExps are not one of the fundamental datatypes in JavaScript, but they have a literal syntax like numbers and strings do, so they sometimes seem like they are fundamental. The grammar of regular expression literals is complex and the API they define is nontrivial. They are documented in detail in §11.3. Because RegExps are powerful and commonly used for text processing, however, this section provides a brief overview.

> JavaScript 定义了一种称为正则表达式（或RegExp）的数据类型，用于描述和匹配文本字符串中的模式。regexp 并不是 JavaScript 中的基本数据类型之一，但它们像数字和字符串一样有字面语法，所以有时看起来它们似乎是基本类型。正则表达式字面量的语法很复杂，它们定义的 API 也很重要。它们在 §11.3 中有详细的记录。但是，由于 regexp 功能强大，通常用于文本处理，因此本节提供一个简要概述。

Text between a pair of slashes constitutes a regular expression literal. The second slash in the pair can also be followed by one or more letters, which modify the meaning of the pattern. For example:

> 一对斜杠之间的文本构成了正则表达式字面量。对中的第二个斜杠还可以后跟一个或多个字母，它们修改了模式的含义。例如：

```js
/^HTML/;             // Match the letters H T M L at the start of a string
/[1-9][0-9]*/;       // Match a nonzero digit, followed by any # of digits
/\bjavascript\b/i;   // Match "javascript" as a word, case-insensitive
```

RegExp objects define a number of useful methods, and strings also have methods that accept RegExp arguments. For example:

> RegExp 对象定义了许多有用的方法，字符串也有接受 RegExp 实参的方法。例如：

```js
let text = "testing: 1, 2, 3";   // Sample text
let pattern = /\d+/g;            // Matches all instances of one or more digits
pattern.test(text)               // => true: a match exists
text.search(pattern)             // => 9: position of first match
text.match(pattern)              // => ["1", "2", "3"]: array of all matches
text.replace(pattern, "#")       // => "testing: #, #, #"
text.split(/\D+/)                // => ["","1","2","3"]: split on nondigits
```
## 3.4 Boolean Values

A boolean value represents truth or falsehood, on or off, yes or no. There are only two possible values of this type. The reserved words true and false evaluate to these two values.

> 布尔值表示真或假、开或关、是或否。这种类型只有两个可能的值。保留字 true 和 false 计算这两个值。

Boolean values are generally the result of comparisons you make in your JavaScript programs. For example:

> 布尔值通常是你在 JavaScript 程序中进行比较的结果。例如：

```js
a === 4
```

This code tests to see whether the value of the variable a is equal to the number 4. If it is, the result of this comparison is the boolean value true. If a is not equal to 4, the result of the comparison is false.

> 这段代码测试变量 a 的值是否等于数字 4。如果是，则此比较的结果为布尔值 true。如果 a 不等于 4，则比较的结果为 false。

Boolean values are commonly used in JavaScript control structures. For example, the if/else statement in JavaScript performs one action if a boolean value is true and another action if the value is false. You usually combine a comparison that creates a boolean value directly with a statement that uses it. The result looks like this:

> 布尔值通常用于 JavaScript 的控制结构中。例如，JavaScript 中的 if/else 语句在布尔值为 true 时执行一个动作，在值为 false 时执行另一个动作。通常将直接创建布尔值的比较与使用它的语句组合在一起。结果是这样的：

```js
if (a === 4) {
    b = b + 1;
} else {
    a = a + 1;
}
```

This code checks whether a equals 4. If so, it adds 1 to b; otherwise, it adds 1 to a.

> 这段代码检查 a 是否等于 4。如果是，则给 b 加 1；否则，它给 a 加 1。

As we’ll discuss in §3.9, any JavaScript value can be converted to a boolean value. The following values convert to, and therefore work like, false:

> 正如我们将在 §3.9 中讨论的，任何 JavaScript 值都可以转换为布尔值。下面的值会转换为 false，因此工作方式类似于 false：

```js
undefined
null
0
-0
NaN
""  // the empty string
```

All other values, including all objects (and arrays) convert to, and work like, true. false, and the six values that convert to it, are sometimes called falsy values, and all other values are called truthy. Any time JavaScript expects a boolean value, a falsy value works like false and a truthy value works like true.

> 所有其他值，包括所有对象（和数组）都转换为 true，并像 true 一样工作。假值，以及转换为假值的六个值，有时被称为假值，其他所有值都被称为真值。任何时候 JavaScript 期望一个布尔值，都可以将假值作为 false 使用，真值作为 true。

As an example, suppose that the variable o either holds an object or the value null. You can test explicitly to see if o is non-null with an if statement like this:

> 例如，假设变量 o 保存一个对象或值为 null。你可以使用如下的 if 语句来显式测试 o 是否非空：

```js
if (o !== null) ...
```

The not-equal operator !== compares o to null and evaluates to either true or false. But you can omit the comparison and instead rely on the fact that null is falsy and objects are truthy:

> 不相等运算符 !== 将 o 与 null 进行比较，然后求值为 true 或 false。但是你可以忽略比较，而是依赖 null 是假的，对象是真的：

```js
if (o) ...
```

In the first case, the body of the if will be executed only if o is not null. The second case is less strict: it will execute the body of the if only if o is not false or any falsy value (such as null or undefined). Which if statement is appropriate for your program really depends on what values you expect to be assigned to o. If you need to distinguish null from 0 and "", then you should use an explicit comparison.

> 在第一种情况下，if 函数体只有在 o 不为空时才会执行。第二种情况不那么严格：它只在 o 不为假值或任何假值（如 null 或 undefined）时执行 if 语句体。哪个 if 语句适合你的程序实际上取决于你希望给 o 赋什么值。如果你需要区分 null 和 0 和 ""，那么你应该使用显式比较。

Boolean values have a toString() method that you can use to convert them to the strings “true” or “false”, but they do not have any other useful methods. Despite the trivial API, there are three important boolean operators.

> 布尔值有一个 toString() 方法，可以用来将它们转换为字符串“true”或“false”，但它们没有任何其他有用的方法。尽管 API 很简单，但是有三个重要的布尔运算符。

The && operator performs the Boolean AND operation. It evaluates to a truthy value if and only if both of its operands are truthy; it evaluates to a falsy value otherwise. The || operator is the Boolean OR operation: it evaluates to a truthy value if either one (or both) of its operands is truthy and evaluates to a falsy value if both operands are falsy. Finally, the unary ! operator performs the Boolean NOT operation: it evaluates to true if its operand is falsy and evaluates to false if its operand is truthy. For example:

> && 运算符执行布尔和运算。当且仅当它的两个操作数都为真时，它的计算结果为真值；否则它将计算为假值。|| 运算符是布尔或运算符：如果其中一个操作数（或两个操作数）为真，则计算为真值；如果两个操作数都为假，则计算为假值。最后，一元 ! 运算符执行布尔的 NOT 操作：如果操作数为假，则计算为真；如果操作数为真，则计算为假。例如：

```js
if ((x === 0 && y === 0) || !(z === 0)) {
    // x and y are both zero or z is non-zero
}
```
Full details on these operators are in §4.10.

> 关于这些运算符的全部细节见 §4.10。

## 3.5 null and undefined

null is a language keyword that evaluates to a special value that is usually used to indicate the absence of a value. Using the typeof operator on null returns the string “object”, indicating that null can be thought of as a special object value that indicates “no object”. In practice, however, null is typically regarded as the sole member of its own type, and it can be used to indicate “no value” for numbers and strings as well as objects. Most programming languages have an equivalent to JavaScript’s null: you may be familiar with it as NULL, nil, or None.

> null 是一个语言关键字，其计算结果为一个特殊值，该值通常用于指示没有值。对 null 使用 typeof 运算符返回字符串“object”，表示 null 可以被认为是一个特殊的对象值，表示“没有对象”。然而，在实践中，null 通常被视为它自己类型的唯一成员，它可以用来表示数字、字符串和对象的“无值”。大多数编程语言都有一个等价于 JavaScript 的 null：您可能熟悉它为 NULL、nil 或 None。

JavaScript also has a second value that indicates absence of value. The undefined value represents a deeper kind of absence. It is the value of variables that have not been initialized and the value you get when you query the value of an object property or array element that does not exist. The undefined value is also the return value of functions that do not explicitly return a value and the value of function parameters for which no argument is passed. undefined is a predefined global constant (not a language keyword like null, though this is not an important distinction in practice) that is initialized to the undefined value. If you apply the typeof operator to the undefined value, it returns “undefined”, indicating that this value is the sole member of a special type.

> JavaScript 还有第二个值，表示没有值。undefined 值代表一种更深层次的缺席。它是尚未初始化的变量的值，以及在查询不存在的对象属性或数组元素的值时获得的值。未定义的值也是没有显式返回值的函数的返回值，以及没有传递实参的函数形参的值。undefined 是一个预定义的全局常量（不是像 null 这样的语言关键字，虽然这在实践中不是一个重要的区别），它被初始化为 undefined 值。如果对未定义的值应用 typeof 运算符，它将返回“undefined”，表明该值是特殊类型的唯一成员。

Despite these differences, null and undefined both indicate an absence of value and can often be used interchangeably. The equality operator == considers them to be equal. (Use the strict equality operator === to distinguish them.) Both are falsy values: they behave like false when a boolean value is required. Neither null nor undefined have any properties or methods. In fact, using . or [] to access a property or method of these values causes a TypeError.

> 尽管存在这些差异，null 和 undefined 都表示没有值，并且经常可以互换使用。相等运算符 == 认为它们相等。（使用严格的相等运算符 === 来区分它们。）两者都是假值：当需要布尔值时，它们的行为类似于假值。null 和 undefined 都没有任何属性或方法。事实上，使用。或 [] 访问这些值的属性或方法会导致 TypeError。

I consider undefined to represent a system-level, unexpected, or error-like absence of value and null to represent a program-level, normal, or expected absence of value. I avoid using null and undefined when I can, but if I need to assign one of these values to a variable or property or pass or return one of these values to or from a function, I usually use null. Some programmers strive to avoid null entirely and use undefined in its place wherever they can.

> 我认为 undefined 表示系统级的、意外的或类似错误的值缺失，null 表示程序级的、正常的或预期的值缺失。我尽可能避免使用 null 和 undefined，但如果我需要分配这些值给一个变量或属性，或函数传递或返回一个这些值，我通常使用 null。一些程序员避免使用 null，而使用 undefined。

## 3.6 Symbols

Symbols were introduced in ES6 to serve as non-string property names. To understand Symbols, you need to know that JavaScript’s fundamental Object type is an unordered collection of properties, where each property has a name and a value. Property names are typically (and until ES6, were exclusively) strings. But in ES6 and later, Symbols can also serve this purpose:

> Symbol 在 ES6 中被引入，用作非字符串属性名。要理解 Symbol，您需要知道 JavaScript 的基本对象类型是属性的无序集合，其中每个属性都有一个名称和一个值。属性名通常是字符串（在 ES6 之前专有的）。但是在 ES6 和以后的版本中，Symbol 也可以达到这个目的：

```js
let strname = "string name";      // A string to use as a property name
let symname = Symbol("propname"); // A Symbol to use as a property name
typeof strname                    // => "string": strname is a string
typeof symname                    // => "symbol": symname is a symbol
let o = {};                       // Create a new object
o[strname] = 1;                   // Define a property with a string name
o[symname] = 2;                   // Define a property with a Symbol name
o[strname]                        // => 1: access the string-named property
o[symname]                        // => 2: access the symbol-named property
```

The Symbol type does not have a literal syntax. To obtain a Symbol value, you call the Symbol() function. This function never returns the same value twice, even when called with the same argument. This means that if you call Symbol() to obtain a Symbol value, you can safely use that value as a property name to add a new property to an object and do not need to worry that you might be overwriting an existing property with the same name. Similarly, if you use symbolic property names and do not share those symbols, you can be confident that other modules of code in your program will not accidentally overwrite your properties.

> Symbol 类型没有文字语法。要获取符号值，可以调用 Symbol() 函数。这个函数不会两次返回相同的值，即使调用时带有相同的实参。这意味着，如果您调用 Symbol() 来获得一个 Symbol 值，您可以安全地使用该值作为属性名，向对象添加一个新属性，而不需要担心可能会用相同的名称覆盖现有的属性。同样，如果您使用 Symbol 属性名而不共享这些符号，您可以确信程序中的其他模块不会意外地覆盖您的属性。

In practice, Symbols serve as a language extension mechanism. When ES6 introduced the for/of loop (§5.4.4) and iterable objects (Chapter 12), it needed to define standard method that classes could implement to make themselves iterable. But standardizing any particular string name for this iterator method would have broken existing code, so a symbolic name was used instead. As we’ll see in Chapter 12, Symbol.iterator is a Symbol value that can be used as a method name to make an object iterable.

> 实际上，Symbol 是一种语言扩展机制。当 ES6 引入 for/of 循环（ §5.4.4 ）和可迭代对象（第 12 章）时，它需要定义标准方法使类可以迭代。但用任何特定的字符串标准化命名这个迭代器方法都会破坏现有的代码，所以使用了一个符号名称代替。我们将在第 12 章 中看到。Symbol.iterator 是一个 Symbol 值，可以用作方法名，使对象可迭代。

The Symbol() function takes an optional string argument and returns a unique Symbol value. If you supply a string argument, that string will be included in the output of the Symbol’s toString() method. Note, however, that calling Symbol() twice with the same string produces two completely different Symbol values.

> Symbol() 函数接受一个可选的字符串实参，并返回一个唯一的符号值。如果提供一个字符串实参，该字符串将包含在符号的 toString() 方法的输出中。但是请注意，对同一个字符串调用 Symbol() 两次会产生两个完全不同的符号值。

```js
let s = Symbol("sym_x");
s.toString()             // => "Symbol(sym_x)"
```
toString() is the only interesting method of Symbol instances. There are two other Symbol-related functions you should know about, however. Sometimes when using Symbols, you want to keep them private to your own code so you have a guarantee that your properties will never conflict with properties used by other code. Other times, however, you might want to define a Symbol value and share it widely with other code. This would be the case, for example, if you were defining some kind of extension that you wanted other code to be able to participate in, as with the Symbol.iterator mechanism described earlier.

> toString() 是 Symbol 实例中唯一有趣的方法。但是，您还应该了解另外两个与符号相关的函数。有时在使用符号时，您希望将它们保留为自己的代码的私有属性，这样就可以保证属性不会与其他代码使用的属性发生冲突。然而，在其他时候，可能想要定义一个 Symbol 值并与其他代码广泛共享它。例如，如果您正在定义某种希望其他代码能够参与的扩展，就像前面描述的 Symbol.iterator 机制。

To serve this latter use case, JavaScript defines a global Symbol registry. The Symbol.for() function takes a string argument and returns a Symbol value that is associated with the string you pass. If no Symbol is already associated with that string, then a new one is created and returned; otherwise, the already existing Symbol is returned. That is, the Symbol.for() function is completely different than the Symbol() function: Symbol() never returns the same value twice, but Symbol.for() always returns the same value when called with the same string. The string passed to Symbol.for() appears in the output of toString() for the returned Symbol, and it can also be retrieved by calling Symbol.keyFor() on the returned Symbol.

> 为了满足后一个用例，JavaScript 定义了一个全局 Symbol 注册表。Symbol.for() 函数接受一个字符串实参，并返回与所传递的字符串相关联的 Symbol 值。如果没有与该字符串相关联的符号，则创建并返回一个新的符号；否则，返回已经存在的符号。也就是说，Symbol.for() 函数与 Symbol() 函数完全不同：Symbol() 不会两次返回相同的值，但 Symbol.for() 在使用相同的字符串调用时总是返回相同的值。传递给 Symbol.for() 的字符串出现在返回符号的 toString() 的输出中，也可以通过调用返回符号的 Symbol.keyfor() 来检索它。

```js
let s = Symbol.for("shared");
let t = Symbol.for("shared");
s === t          // => true
s.toString()     // => "Symbol(shared)"
Symbol.keyFor(t) // => "shared"
```
## 3.7 The Global Object
The preceding sections have explained JavaScript’s primitive types and values. Object types—objects, arrays, and functions—are covered in chapters of their own later in this book. But there is one very important object value that we must cover now. The global object is a regular JavaScript object that serves a very important purpose: the properties of this object are the globally defined identifiers that are available to a JavaScript program. When the JavaScript interpreter starts (or whenever a web browser loads a new page), it creates a new global object and gives it an initial set of properties that define:

> 前面的章节已经说明了 JavaScript 的基本类型和值。对象类型——对象、数组和函数——将在本书后面的章节中介绍。但是有一个非常重要的对象值，我们现在必须讲一下。全局对象是一个常规的 JavaScript 对象，它有一个非常重要的用途：该对象的属性是 JavaScript 程序可用的全局定义的标识符。当 JavaScript 解释器启动时(或者每当 web 浏览器加载一个新页面时)，它会创建一个新的全局对象，并为其提供一组初始属性，这些属性定义：

- Global constants like undefined, Infinity, and NaN
- Global functions like isNaN(), parseInt() (§3.9.2), and eval() (§4.12)
- Constructor functions like Date(), RegExp(), String(), Object(), and Array() (§3.9.2)
- Global objects like Math and JSON (§6.8)

---

> - 全局常量，如 undefined、Infinity 和 NaN
> - 全局函数，如 isNaN()、 parseInt()（§3.9.2）和 eval()（§4.12）
> - 构造函数，如 Date()、 RegExp()、 String()、 Object() 和 Array()（§3.9.2）
> - 全局对象，如 Math 和 JSON（§6.8）

The initial properties of the global object are not reserved words, but they deserve to be treated as if they are. This chapter has already described some of these global properties. Most of the others will be covered elsewhere in this book.

> 全局对象的初始属性不是保留字，但是它们应该被当作保留字来对待。本章已经描述了其中一些全局属性。其余的大部分将在本书的其他地方讨论。

In Node, the global object has a property named global whose value is the global object itself, so you can always refer to the global object by the name global in Node programs.

> 在 Node 中，全局对象有一个名为 global 的属性，该属性的值就是全局对象本身，因此在 Node 程序中始终可以通过名称 global 来引用全局对象。

In web browsers, the Window object serves as the global object for all JavaScript code contained in the browser window it represents. This global Window object has a self-referential window property that can be used to refer to the global object. The Window object defines the core global properties, but it also defines quite a few other globals that are specific to web browsers and client-side JavaScript. Web worker threads (§15.13) have a different global object than the Window with which they are associated. Code in a worker can refer to its global object as self.

> 在 web 浏览器中，Window 对象充当它所代表的浏览器窗口中包含的所有 JavaScript 代码的全局对象。这个全局窗口对象有一个自引用窗口属性，可以用来引用全局对象。Window 对象定义了核心的全局属性，但是它也定义了一些其他的全局属性，这些全局属性是特定于 web 浏览器和客户端 JavaScript 的。Web worker 线程（§15.13）有一个与它们相关联的窗口不同的全局对象。worker 中的代码可以将其全局对象引用为 self。

ES2020 finally defines globalThis as the standard way to refer to the global object in any context. As of early 2020, this feature has been implemented by all modern browsers and by Node.

> ES2020 最终定义了 globalThis 作为在任何上下文中引用全局对象的标准方式。到 2020 年初，所有现代浏览器和 Node 都实现了该特性。

## 3.8 Immutable Primitive Values and Mutable Object References

There is a fundamental difference in JavaScript between primitive values (undefined, null, booleans, numbers, and strings) and objects (including arrays and functions). Primitives are immutable: there is no way to change (or “mutate”) a primitive value. This is obvious for numbers and booleans—it doesn’t even make sense to change the value of a number. It is not so obvious for strings, however. Since strings are like arrays of characters, you might expect to be able to alter the character at any specified index. In fact, JavaScript does not allow this, and all string methods that appear to return a modified string are, in fact, returning a new string value. For example:

> JavaScript 中的原始值（undefined、null、布尔值、数字和字符串）与对象（包 括数组和函数）有着根本区别。原始值是不可更改的：任何方法都无法更改（或“突变”）一个原始值。对数字和布尔值来说显然如此——改变数字的值本身就说不通，而对字符串来说就不那么明显了，因为字符串看起来像由字符组成的数组，我们期望可以通过指定索引来修改字符串中的字符。实际上，JavaScript 是禁止这样做的。字符串中所有的方法看上去返回了一个修改后的字符串，实际上返回的 是一个新的字符串值。例如：

```js
let s = "hello";   // Start with some lowercase text
s.toUpperCase();   // Returns "HELLO", but doesn't alter s
s                  // => "hello": the original string has not changed
```

Primitives are also compared by value: two values are the same only if they have the same value. This sounds circular for numbers, booleans, null, and undefined: there is no other way that they could be compared. Again, however, it is not so obvious for strings. If two distinct string values are compared, JavaScript treats them as equal if, and only if, they have the same length and if the character at each index is the same.

> 原始值的比较是值的比较：只有在它们的值相等时它们才相等。这对数字、布尔值、null 和 undefined 来说听起来有点儿难懂，并没有其他办法来比较它们。同样，对于字符串来说则并不明显：如果比较两个单独的字符串，当且仅当它们的长度相等且每个索引的字符都相等时，JavaScript 才认为它们相等。

Objects are different than primitives. First, they are mutable—their values can change:

> 对象和原始值不同，首先，它们是可变的——它们的值是可修改的：

```js
let o = { x: 1 };  // Start with an object
o.x = 2;           // Mutate it by changing the value of a property
o.y = 3;           // Mutate it again by adding a new property

let a = [1,2,3];   // Arrays are also mutable
a[0] = 0;          // Change the value of an array element
a[3] = 4;          // Add a new array element
```

Objects are not compared by value: two distinct objects are not equal even if they have the same properties and values. And two distinct arrays are not equal even if they have the same elements in the same order:

> 对象的比较并非值的比较：即使两个对象包含同样的属性及相同的值，它们也是不相等的。各个索引元素完全相等的两个数组也不相等。

```js
let o = {x: 1}, p = {x: 1};  // Two objects with the same properties
o === p                      // => false: distinct objects are never equal
let a = [], b = [];          // Two distinct, empty arrays
a === b                      // => false: distinct arrays are never equal
```

Objects are sometimes called reference types to distinguish them from JavaScript’s primitive types. Using this terminology, object values are references, and we say that objects are compared by reference: two object values are the same if and only if they refer to the same underlying object.

> 我们有时将对象称为引用类型（reference type），以此来和 JavaScript 的基本类型区分开来。依照术语的叫法，对象值都是引用（reference），对象的比较均是引用的比较：当且仅当它们引用同一个基对象时，它们才相等。

```js
let a = [];   // The variable a refers to an empty array.
let b = a;    // Now b refers to the same array.
b[0] = 1;     // Mutate the array referred to by variable b.
a[0]          // => 1: the change is also visible through variable a.
a === b       // => true: a and b refer to the same object, so they are equal.
```

As you can see from this code, assigning an object (or array) to a variable simply assigns the reference: it does not create a new copy of the object. If you want to make a new copy of an object or array, you must explicitly copy the properties of the object or the elements of the array. This example demonstrates using a for loop (§5.4.3):

> 就像你刚看到的如上代码，将对象（或数组）赋值给一个变量，仅仅是赋值的引用值：对象本身并没有复制一次。如果你想得到一个对象或数组的副本，则必须显式复制对象的每个属性或数组的每个元素。下面这个例子则是通过循环来完成数组复制（§5.4.3）：

```js
let a = ["a","b","c"];              // An array we want to copy
let b = [];                         // A distinct array we'll copy into
for(let i = 0; i < a.length; i++) { // For each index of a[]
    b[i] = a[i];                    // Copy an element of a into b
}
let c = Array.from(b);              // In ES6, copy arrays with Array.from()
```

Similarly, if we want to compare two distinct objects or arrays, we must compare their properties or elements. This code defines a function to compare two arrays:

> 同样的，如果我们想比较两个单独的对象或者数组，则必须比较它们的属性或元素。下面这段代码定义了一个比较两个数组的函数：

```js
function equalArrays(a, b) {
    if (a === b) return true;                // Identical arrays are equal
    if (a.length !== b.length) return false; // Different-size arrays not equal
    for(let i = 0; i < a.length; i++) {      // Loop through all elements
        if (a[i] !== b[i]) return false;     // If any differ, arrays not equal
    }
    return true;                             // Otherwise they are equal
}
```
## 3.9 Type Conversions

JavaScript is very flexible about the types of values it requires. We’ve seen this for booleans: when JavaScript expects a boolean value, you may supply a value of any type, and JavaScript will convert it as needed. Some values (“truthy” values) convert to true and others (“falsy” values) convert to false. The same is true for other types: if JavaScript wants a string, it will convert whatever value you give it to a string. If JavaScript wants a number, it will try to convert the value you give it to a number (or to NaN if it cannot perform a meaningful conversion).

> JavaScript 中取值所需类型非常灵活。从布尔值上就能看出这一点：当 JavaScript 需要一个布尔值时，你可以提供任何类型的值，JavaScript 会根据需要进行转换。一些值（真值）转换为 true，其他值（假值）转换为 false。这在 其他类型中同样适用：如果 JavaScript 期望使用一个字符串，它把给定的值将转换为字符串。如果 JavaScript 期望使用一个数字，它把给定的值将转换为数字（如果转换结果无意义的话将返回NaN）。

Some examples:

> 一些例子如下:

```js
10 + " objects"     // => "10 objects":  Number 10 converts to a string
"7" * "4"           // => 28: both strings convert to numbers
let n = 1 - "x";    // n == NaN; string "x" can't convert to a number
n + " objects"      // => "NaN objects": NaN converts to string "NaN"
```

Table 3-2 summarizes how values convert from one type to another in JavaScript. Bold entries in the table highlight conversions that you may find surprising. Empty cells indicate that no conversion is necessary and none is performed.

> 表 3-2 简要说明了在 JavaScript 中如何进行类型转换。表 3-2 中的粗体部分突出显示了那些让你倍感意外的类型转换。空单元格表示不必要也没有执行转换。

Table 3-2. JavaScript type conversions

> 表 3-2 JavaScript类型转换

| Value                         | to String         | to Number  | to Boolean |
| ----------------------------- | ----------------- | ---------- | ---------- |
| undefined                     | "undefined"       | NaN        | false      |
| null                          | "null"            | **0**      | false      |
| true                          | "true"            | **1**      |            |
| false                         | "false"           | **0**      |            |
| "" (empty string)             |                   | **0**      | **false**  |
| "1.2" (nonempty, numeric)     |                   | 1.2        | true       |
| "one" (nonempty, non-numeric) |                   | NaN        | true       |
| 0                             | "0"               |            | **false**  |
| -0                            | "0"               |            | **false**  |
| 1 (finite, non-zero)          | "1"               |            | true       |
| Infinity                      | "Infinity"        |            | true       |
| -Infinity                     | "-Infinity"       |            | true       |
| NaN                           | "NaN"             |            | **false**  |
| {} (any object)               | see §3.9.3        | see §3.9.3 | true       |
| [] (empty array)              | ""                | **0**      | true       |
| [9] (one numeric element)     | "9"               | **9**      | true       |
| ['a'] (any other array)       | use join() method | NaN        | true       |
| function(){} (any function)   | see §3.9.3        | NaN        | true       |

The primitive-to-primitive conversions shown in the table are relatively straightforward. Conversion to boolean was already discussed in §3.4. Conversion to strings is well defined for all primitive values. Conversion to numbers is just a little trickier. Strings that can be parsed as numbers convert to those numbers. Leading and trailing spaces are allowed, but any leading or trailing nonspace characters that are not part of a numeric literal cause the string-to-number conversion to produce NaN. Some numeric conversions may seem surprising: true converts to 1, and false and the empty string convert to 0.

> 表中提到的原始值到原始值的转换相对简单，我们已经在 §3.4 讨论过转换为布尔值的情况了。所有原始值转换为字符串的情形也已经明确定义。转换为数字的情形比较微妙。那些以数字表示的字符串可以直接转换为数字，也允许在开始和结尾处带有空格。但在开始和结尾处的任意非空格字符都不会被当成数字直接量的一部分，进而造成字符串转换为数字的结果为 NaN。有一些数字转换看起来让人奇怪：true 转换为 1，false、空字符串 ”” 转换为 0。

Object-to-primitive conversion is somewhat more complicated, and it is the subject of §3.9.3.

> 对象到原始值的转换要复杂一些，它是 §3.9.3 的主题。

### 3.9.1 Conversions and Equality

JavaScript has two operators that test whether two values are equal. The “strict equality operator,” ===, does not consider its operands to be equal if they are not of the same type, and this is almost always the right operator to use when coding. But because JavaScript is so flexible with type conversions, it also defines the == operator with a flexible definition of equality. All of the following comparisons are true, for example:

> JavaScript 有两个运算符来测试两个值是否相等。“严格的相等运算符”=== 的操作数不是同一类型则不认为它们是相等的，在编码时，这几乎总是正确的运算符。但是，由于 JavaScript 在类型转换方面非常灵活，所以它还定义了灵活相等运算符 ==。下面所有的比较都是正确的，例如：

```js
null == undefined // => true: These two values are treated as equal.
"0" == 0          // => true: String converts to a number before comparing.
0 == false        // => true: Boolean converts to number before comparing.
"0" == false      // => true: Both operands convert to 0 before comparing!
```

§4.9.1 explains exactly what conversions are performed by the == operator in order to determine whether two values should be considered equal.

> §4.9.1 详细说明了 == 运算符执行什么转换来确定两个值是否应该被认为相等。

Keep in mind that convertibility of one value to another does not imply equality of those two values. If undefined is used where a boolean value is expected, for example, it will convert to false. But this does not mean that undefined == false. JavaScript operators and statements expect values of various types and perform conversions to those types. The if statement converts undefined to false, but the == operator never attempts to convert its operands to booleans.

> 需要特别注意的是，一个值转换为另一个值并不意味着两个值相等。比如，如果在期望使用布尔值的地方使用了 undefined，它将会转换为 false，但这并不表明 undefined == false。JavaScript 运算符和语句期望使用多样化的数据类型，并可以相互转换。if 语句将 undefined 转换为 false，但“==”运算符从不试图将其操作数转换为布尔值。

### 3.9.2 Explicit Conversions

Although JavaScript performs many type conversions automatically, you may sometimes need to perform an explicit conversion, or you may prefer to make the conversions explicit to keep your code clearer.

> 尽管 JavaScript 可以自动做许多类型转换，但有时仍需要做显式转换，或者为了使代码变得清晰易读而做显式转换。

The simplest way to perform an explicit type conversion is to use the Boolean(), Number(), and String() functions:

> 执行显式类型转换的最简单方法是使用 Boolean()、Number() 和 String() 函数:

```js
Number("3")    // => 3
String(false)  // => "false":  Or use false.toString()
Boolean([])    // => true
```

Any value other than null or undefined has a toString() method, and the result of this method is usually the same as that returned by the String() function.

> 除null或undefined之外的任何值都有toString()方法，该方法的结果通常与String()函数返回的结果相同。

As an aside, note that the Boolean(), Number(), and String() functions can also be invoked—with new—as constructor. If you use them this way, you’ll get a “wrapper” object that behaves just like a primitive boolean, number, or string value. These wrapper objects are a historical leftover from the earliest days of JavaScript, and there is never really any good reason to use them.

> 顺便说一下，Boolean()、Number() 和 String() 函数可以作为构造函数调用（用 new 关键字）。如果以这种方式调用它们，就会得到一个行为类似原始布尔值、数字或字符串值的“包装器”对象。这些包装器对象是 JavaScript 早期遗留下来的，并且从来没有一个好的场景来使用他们。

Certain JavaScript operators perform implicit type conversions and are sometimes used explicitly for the purpose of type conversion. If one operand of the + operator is a string, it converts the other one to a string. The unary + operator converts its operand to a number. And the unary ! operator converts its operand to a boolean and negates it. These facts lead to the following type conversion idioms that you may see in some code:

> JavaScript 中的某些运算符会做隐式的类型转换，有时用于类型转换。如果“+”运算符的一个操作数是字符串，它将会把另外一个操作数转换为字符串。一元“+”运算符将其操作数转换为数字。同样，一元“！”运算符将其操作数转换为布尔值并取反。在代码中会经常见到这种类型转换的惯用法：

```js
x + ""   // => String(x)
+x       // => Number(x)
x-0      // => Number(x)
!!x      // => Boolean(x): Note double !
```

Formatting and parsing numbers are common tasks in computer programs, and JavaScript has specialized functions and methods that provide more precise control over number-to-string and string-to-number conversions.

> 在计算机程序中数字的解析和格式化是非常普通的工作，JavaScript 中提供了专门的函数和方法用来做更加精确的数字到字符串和字符串到数字的转换。

The toString() method defined by the Number class accepts an optional argument that specifies a radix, or base, for the conversion. If you do not specify the argument, the conversion is done in base 10. However, you can also convert numbers in other bases (between 2 and 36). For example:

> Number 类定义的 toString() 方法可以接收表示转换基数的可选实参，如果不指定此实参，转换规则将是基于十进制。同样，亦可以将数字转换为其他进制数（范围在2～36之间），例如：

```js
let n = 17;
let binary = "0b" + n.toString(2);  // binary == "0b10001"
let octal = "0o" + n.toString(8);   // octal == "0o21"
let hex = "0x" + n.toString(16);    // hex == "0x11"
```

When working with financial or scientific data, you may want to convert numbers to strings in ways that give you control over the number of decimal places or the number of significant digits in the output, or you may want to control whether exponential notation is used. The Number class defines three methods for these kinds of number-to-string conversions. toFixed() converts a number to a string with a specified number of digits after the decimal point. It never uses exponential notation. toExponential() converts a number to a string using exponential notation, with one digit before the decimal point and a specified number of digits after the decimal point (which means that the number of significant digits is one larger than the value you specify). toPrecision() converts a number to a string with the number of significant digits you specify. It uses exponential notation if the number of significant digits is not large enough to display the entire integer portion of the number. Note that all three methods round the trailing digits or pad with zeros as appropriate. Consider the following examples:

> 当处理财务或科学数据的时候，在做数字到字符串的转换过程中，你期望自己控制输出中小数点位置和有效数字位数，或者决定是否需要指数记数法。Number 类为这种数字到字符串的类型转换场景定义了三个方法。toFixed() 根据小数点后的指定位数将数字转换为字符串，它从不使用指数记数法。toExponential() 使用指数记数法将数字转换为指数形式的字符串，其中小数点前只有一位，小数点后的位数则由参数指定（也就是说有效数字位数比指定的位数要多一位），toPrecision() 根据指定的有效数字位数将数字转换成字符串。如果有效数字的位数少于数字整数部分的位数，则转换成指数形式。我们注意到，所有三个方法都会适当地进行四舍五入或填充 0。看一下下面几个例子：

```js
let n = 123456.789;
n.toFixed(0)         // => "123457"
n.toFixed(2)         // => "123456.79"
n.toFixed(5)         // => "123456.78900"
n.toExponential(1)   // => "1.2e+5"
n.toExponential(3)   // => "1.235e+5"
n.toPrecision(4)     // => "1.235e+5"
n.toPrecision(7)     // => "123456.8"
n.toPrecision(10)    // => "123456.7890"
```

In addition to the number-formatting methods shown here, the Intl.NumberFormat class defines a more general, internationalized number-formatting method. See §11.7.1 for details.

> 除了这里显示的数字格式方法外，Intl.NumberFormat 类定义了一个更通用的、国际化的数字格式化方法。详情见 §11.7.1。

If you pass a string to the Number() conversion function, it attempts to parse that string as an integer or floating-point literal. That function only works for base-10 integers and does not allow trailing characters that are not part of the literal. The parseInt() and parseFloat() functions (these are global functions, not methods of any class) are more flexible. parseInt() parses only integers, while parseFloat() parses both integers and floating-point numbers. If a string begins with “0x” or “0X”, parseInt() interprets it as a hexadecimal number. Both parseInt() and parseFloat() skip leading whitespace, parse as many numeric characters as they can, and ignore anything that follows. If the first nonspace character is not part of a valid numeric literal, they return NaN:

> 如果通过 Number() 转换函数传入一个字符串，它会试图将其转换为一个整数或浮点数直接量，这个方法只能基于十进制数进行转换，并且不能出现非法的尾随字符。parseInt() 函数和 parseFloat() 函数（它们是全局函数，不从属于任何类的方法）更加灵活。parseInt() 只解析整数，而 parseFloat() 则可以解析整数和浮点数。如果字符串前缀是“0x”或者“0X”，parseInt() 将其解释为十六进制数，parseInt() 和 parseFloat() 都会跳过任意数量的前导空格，尽可能解析更多数值字符，并忽略后面的内容。如果第一个非空格字符是非法的数字直接量，将最终返回 NaN：

```js
parseInt("3 blind mice")     // => 3
parseFloat(" 3.14 meters")   // => 3.14
parseInt("-12.34")           // => -12
parseInt("0xFF")             // => 255
parseInt("0xff")             // => 255
parseInt("-0XFF")            // => -255
parseFloat(".1")             // => 0.1
parseInt("0.1")              // => 0
parseInt(".1")               // => NaN: integers can't start with "."
parseFloat("$72.47")         // => NaN: numbers can't start with "$"
```

parseInt() accepts an optional second argument specifying the radix (base) of the number to be parsed. Legal values are between 2 and 36. For example:

> parseInt() 接受第二个可选实参，指定数字转换的基数。合法值在2到36之间。例如:

```js
parseInt("11", 2)     // => 3: (1*2 + 1)
parseInt("ff", 16)    // => 255: (15*16 + 15)
parseInt("zz", 36)    // => 1295: (35*36 + 35)
parseInt("077", 8)    // => 63: (7*8 + 7)
parseInt("077", 10)   // => 77: (7*10 + 7)
```
### 3.9.3 Object to Primitive Conversions

The previous sections have explained how you can explicitly convert values of one type to another type and have explained JavaScript’s implicit conversions of values from one primitive type to another primitive type. This section covers the complicated rules that JavaScript uses to convert objects to primitive values. It is long and obscure, and if this is your first reading of this chapter, you should feel free to skip ahead to §3.10.

> 前几节说明了如何显式地将一种类型的值转换为另一种类型，并说明了 JavaScript 如何将值从一种原始类型隐式转换为另一种原始类型。本节介绍 JavaScript 用于将对象转换为原始值的复杂规则。它很长，晦涩难懂，如果这是你第一次阅读这一章，你可以直接跳到 §3.10。

One reason for the complexity of JavaScript’s object-to-primitive conversions is that some types of objects have more than one primitive representation. Date objects, for example, can be represented as strings or as numeric timestamps. The JavaScript specification defines three fundamental algorithms for converting objects to primitive values:

> JavaScript 的对象到原始值转换复杂的一个原因是某些类型的对象有不止一个原始表现。例如，日期对象可以表示为字符串或数字时间戳。JavaScript 规范定义了将对象转换为基本值的三种基本算法：

prefer-string
This algorithm returns a primitive value, preferring a string value, if a conversion to string is possible.

> 偏好字符串 prefer-string
> 如果可以转换成字符串，这个算法会返回一个原始值，提供一个字符串。

prefer-number
This algorithm returns a primitive value, preferring a number, if such a conversion is possible.

> 偏好数字 prefer-number
> 如果可以转换，这个算法会返回一个原始值，提供一个数字。

no-preference
This algorithm expresses no preference about what type of primitive value is desired, and classes can define their own conversions. Of the built-in JavaScript types, all except Date implement this algorithm as prefer-number. The Date class implements this algorithm as prefer-string.

> 无偏好 no-preference
> 此算法表示不对任何类型原始值有偏好，并且可以定义自己的转换。在内置的 JavaScript 类型中，除 Date 之外，其他所有类型都将此算法实现为偏好数字。Date 类将偏好字符串作为无偏好转换算法。

The implementation of these object-to-primitive conversion algorithms is explained at the end of this section. First, however, we explain how the algorithms are used in JavaScript.

> 这些对象到原语转换算法的实现将在本节的末尾进行解释。但是，我们首先解释如何在JavaScript中使用这些算法。

OBJECT-TO-BOOLEAN CONVERSIONS

Object-to-boolean conversions are trivial: all objects convert to true. Notice that this conversion does not require the use of the object-to-primitive algorithms described, and that it literally applies to all objects, including empty arrays and even the wrapper object new Boolean(false).

> 对象到布尔的转换很简单：所有对象都转换为true。注意，这种转换不需要使用前面所描述的对象到原始值算法，它实际上适用于所有对象，包括空数组，甚至包装器对象 new Boolean(false)。

OBJECT-TO-STRING CONVERSIONS

When an object needs to be converted to a string, JavaScript first converts it to a primitive using the prefer-string algorithm, then converts the resulting primitive value to a string, if necessary, following the rules in Table 3-2.

> 当一个对象需要转换为字符串时，JavaScript 首先使用 prefer-string 算法将其转换为原始值，然后根据表 3-2 的规则将得到的原语值转换为字符串。

This kind of conversion happens, for example, if you pass an object to a built-in function that expects a string argument, if you call String() as a conversion function, and when you interpolate objects into template literals (§3.3.4).

> 例如，如果你将一个对象传递给一个需要 string 实参的内置函数，如果你调用 String() 作为一个转换函数，以及当你将对象插入到模板字面量（§3.3.4）时，这种转换就会发生。

OBJECT-TO-NUMBER CONVERSIONS

When an object needs to be converted to a number, JavaScript first converts it to a primitive value using the prefer-number algorithm, then converts the resulting primitive value to a number, if necessary, following the rules in Table 3-2.

> 当一个对象需要转换为数字时，JavaScript首先使用prefer-number算法将其转换为一个原始值，然后根据表3-2的规则将结果原始值转换为数字。

Built-in JavaScript functions and methods that expect numeric arguments convert object arguments to numbers in this way, and most (see the exceptions that follow) JavaScript operators that expect numeric operands convert objects to numbers in this way as well.

> 期望数字实参的内置JavaScript函数和方法以这种方式将对象实参转换为数字，大多数期望数字操作数的JavaScript运算符(参见后面的异常)也以这种方式将对象转换为数字。

SPECIAL CASE OPERATOR CONVERSIONS

Operators are covered in detail in Chapter 4. Here, we explain the special case operators that do not use the basic object-to-string and object-to-number conversions described earlier.

> 运算符将在第 4 章中详细介绍。这里，我们解释不使用前面描述的基本对象-字符串和对象-数字转换的特殊情况运算符。

The + operator in JavaScript performs numeric addition and string concatenation. If either of its operands is an object, JavaScript converts them to primitive values using the no-preference algorithm. Once it has two primitive values, it checks their types. If either argument is a string, it converts the other to a string and concatenates the strings. Otherwise, it converts both arguments to numbers and adds them.

> JavaScript中的+运算符执行数字相加和字符串连接。如果它的任意一个操作数是对象，JavaScript会使用无优先级算法将它们转换为原始值。一旦它有了两个原始值，它就检查它们的类型。如果其中一个实参是字符串，它将另一个实参转换为字符串并连接字符串。否则，它将两个实参都转换为数字并相加。

The == and != operators perform equality and inequality testing in a loose way that allows type conversions. If one operand is an object and the other is a primitive value, these operators convert the object to primitive using the no-preference algorithm and then compare the two primitive values.

> ==和!=运算符以一种允许类型转换的不严格方式执行相等和不相等的测试。如果一个操作数是对象，另一个是基元值，这些运算符使用无优先级算法将对象转换为基元值，然后比较两个基元值。

Finally, the relational operators <, <=, >, and >= compare the order of their operands and can be used to compare both numbers and strings. If either operand is an object, it is converted to a primitive value using the prefer-number algorithm. Note, however, that unlike the object-to-number conversion, the primitive values returned by the prefer-number conversion are not then converted to numbers.

> 最后，关系运算符<、<=、>和>=比较其操作数的顺序，可用于比较数字和字符串。如果其中一个操作数是对象，则使用prefer-number算法将其转换为原始值。但是，请注意，与对象到数字的转换不同，preferred -number转换返回的原始值随后不会转换为数字。

Note that the numeric representation of Date objects is meaningfully comparable with < and >, but the string representation is not. For Date objects, the no-preference algorithm converts to a string, so the fact that JavaScript uses the prefer-number algorithm for these operators means that we can use them to compare the order of two Date objects.

> 请注意，Date对象的数字表示可以与<和>进行有意义的比较，但字符串表示不能。对于Date对象，no-preference算法会转换为字符串，因此JavaScript对这些运算符使用prefer-number算法的事实意味着我们可以使用它们来比较两个Date对象的顺序。

THE TOSTRING() AND VALUEOF() METHODS

All objects inherit two conversion methods that are used by object-to-primitive conversions, and before we can explain the prefer-string, prefer-number, and no-preference conversion algorithms, we have to explain these two methods.

> 所有对象都继承了两种用于对象到原语转换的转换方法，在解释prefer-string、prefer-number和no-preference转换算法之前，我们必须解释这两种方法。

The first method is toString(), and its job is to return a string representation of the object. The default toString() method does not return a very interesting value (though we’ll find it useful in §14.4.3):

> 第一个方法是toString()，它的任务是返回对象的字符串表示。默认的toString()方法不会返回一个非常有趣的值(尽管我们会在14.4.3节中发现它很有用):

```js
({x: 1, y: 2}).toString()    // => "[object Object]"
```

Many classes define more specific versions of the toString() method. The toString() method of the Array class, for example, converts each array element to a string and joins the resulting strings together with commas in between. The toString() method of the Function class converts user-defined functions to strings of JavaScript source code. The Date class defines a toString() method that returns a human-readable (and JavaScript-parsable) date and time string. The RegExp class defines a toString() method that converts RegExp objects to a string that looks like a RegExp literal:

> 许多类定义了toString()方法的更特定版本。例如，Array类的toString()方法将每个数组元素转换为字符串，并使用逗号将结果字符串连接在一起。函数类的toString()方法将用户定义的函数转换为JavaScript源代码的字符串。Date类定义了一个toString()方法，该方法返回一个人类可读(javascript可解析)的日期和时间字符串。RegExp类定义了一个toString()方法，该方法将RegExp对象转换为看起来像RegExp字面量的字符串:

```js
[1,2,3].toString()                  // => "1,2,3"
(function(x) { f(x); }).toString()  // => "function(x) { f(x); }"
/\d+/g.toString()                   // => "/\\d+/g"
let d = new Date(2020,0,1);
d.toString()  // => "Wed Jan 01 2020 00:00:00 GMT-0800 (Pacific Standard Time)"
```

The other object conversion function is called valueOf(). The job of this method is less well defined: it is supposed to convert an object to a primitive value that represents the object, if any such primitive value exists. Objects are compound values, and most objects cannot really be represented by a single primitive value, so the default valueOf() method simply returns the object itself rather than returning a primitive. Wrapper classes such as String, Number, and Boolean define valueOf() methods that simply return the wrapped primitive value. Arrays, functions, and regular expressions simply inherit the default method. Calling valueOf() for instances of these types simply returns the object itself. The Date class defines a valueOf() method that returns the date in its internal representation: the number of milliseconds since January 1, 1970:

> 另一个对象转换函数称为valueOf()。这个方法的工作没有很好地定义:它被假定将一个对象转换为表示该对象的原始值(如果存在这样的原始值的话)。对象是复合值，大多数对象不能真正用单个原始值表示，因此默认的valueOf()方法只是返回对象本身，而不是返回一个原始值。包装类，如String、Number和布尔值define valueOf()方法，它们只是返回包装的原语值。数组、函数和正则表达式只是继承默认方法。对这些类型的实例调用valueOf()只会返回对象本身。Date类定义了一个valueOf()方法，以其内部表示形式返回日期:

```js
let d = new Date(2010, 0, 1);   // January 1, 2010, (Pacific time)
d.valueOf()                     // => 1262332800000
```

OBJECT-TO-PRIMITIVE CONVERSION ALGORITHMS

With the toString() and valueOf() methods explained, we can now explain approximately how the three object-to-primitive algorithms work (the complete details are deferred until §14.4.7):

> 在说明了toString()和valueOf()方法之后，我们现在可以大致解释这三种从对象到原语的算法是如何工作的(完整的细节将在§14.4.7中给出):

- The prefer-string algorithm first tries the toString() method. If the method is defined and returns a primitive value, then JavaScript uses that primitive value (even if it is not a string!). If toString() does not exist or if it returns an object, then JavaScript tries the valueOf() method. If that method exists and returns a primitive value, then JavaScript uses that value. Otherwise, the conversion fails with a TypeError.
- The prefer-number algorithm works like the prefer-string algorithm, except that it tries valueOf() first and toString() second.
- The no-preference algorithm depends on the class of the object being converted. If the object is a Date object, then JavaScript uses the prefer-string algorithm. For any other object, JavaScript uses the prefer-number algorithm.

---

> - prefer-string算法首先尝试toString()方法。如果该方法被定义并返回一个原语值，那么JavaScript将使用该原语值(即使它不是字符串!)如果toString()不存在或者它返回一个对象，那么JavaScript会尝试valueOf()方法。如果该方法存在并返回一个原始值，那么JavaScript将使用该值。否则，转换将失败，并出现TypeError。
> - prefer-number算法的工作原理与prefer-string算法相似，不同之处是它首先尝试valueOf()，然后尝试toString()。
> - 无优先级算法取决于被转换对象的类。如果对象是Date对象，那么JavaScript使用prefer-string算法。对于任何其他对象，JavaScript都使用prefer-number算法。

The rules described here are true for all built-in JavaScript types and are the default rules for any classes you define yourself. §14.4.7 explains how you can define your own object-to-primitive conversion algorithms for the classes you define.

> 这里描述的规则适用于所有内置JavaScript类型，并且是您自己定义的任何类的默认规则。§14.4.7解释了如何为你定义的类定义自己的对象到原语的转换算法。

Before we leave this topic, it is worth noting that the details of the prefer-number conversion explain why empty arrays convert to the number 0 and single-element arrays can also convert to numbers:

> 在我们结束这个主题之前，值得注意的是，prefer-number转换的细节解释了为什么空数组可以转换为数字0，而单元素数组也可以转换为数字:

```js
Number([])    // => 0: this is unexpected!
Number([99])  // => 99: really?
```

The object-to-number conversion first converts the object to a primitive using the prefer-number algorithm, then converts the resulting primitive value to a number. The prefer-number algorithm tries valueOf() first and then falls back on toString(). But the Array class inherits the default valueOf() method, which does not return a primitive value. So when we try to convert an array to a number, we end up invoking the toString() method of the array. Empty arrays convert to the empty string. And the empty string converts to the number 0. An array with a single element converts to the same string that that one element does. If an array contains a single number, that number is converted to a string, and then back to a number.

> 对象到数字的转换首先使用prefer-number算法将对象转换为原语，然后将结果原语值转换为数字。prefer-number算法首先尝试valueOf()，然后返回到toString()。但是Array类继承了默认的valueOf()方法，该方法不返回原语值。因此，当我们尝试将数组转换为数字时，我们最终会调用数组的toString()方法。空数组转换为空字符串。空字符串转换为数字0。具有单个元素的数组将转换为与该元素相同的字符串。如果数组包含单个数字，则该数字将被转换为字符串，然后再转换回数字。

## 3.10 Variable Declaration and Assignment

One of the most fundamental techniques of computer programming is the use of names—or identifiers—to represent values. Binding a name to a value gives us a way to refer to that value and use it in the programs we write. When we do this, we typically say that we are assigning a value to a variable. The term “variable” implies that new values can be assigned: that the value associated with the variable may vary as our program runs. If we permanently assign a value to a name, then we call that name a constant instead of a variable.

> 计算机编程最基本的技术之一是使用名称或标识符来表示值。将名称绑定到一个值提供了一种引用该值并在编写的程序中使用它的方法。当我们这样做的时候，我们通常说我们给一个变量赋值。术语“变量”意味着可以分配新值:与变量相关的值可能随着程序运行而变化。如果我们将一个值永久地赋给一个名称，那么我们将该名称称为常量而不是变量。

Before you can use a variable or constant in a JavaScript program, you must declare it. In ES6 and later, this is done with the let and const keywords, which we explain next. Prior to ES6, variables were declared with var, which is more idiosyncratic and is explained later on in this section.

> 在JavaScript程序中使用变量或常量之前，必须声明它。在ES6及以后的版本中，这是通过let和const关键字来完成的，我们将在下文中解释。在ES6之前，变量是用var声明的，var更特殊，在本节后面解释。

### 3.10.1 Declarations with let and const

In modern JavaScript (ES6 and later), variables are declared with the let keyword, like this:

> 在现代JavaScript (ES6及以后的版本)中，变量是用let关键字声明的，就像这样:

```js
let i;
let sum;
```

You can also declare multiple variables in a single let statement:

> 你也可以在一个let语句中声明多个变量:

```js
let i, sum;
```

It is a good programming practice to assign an initial value to your variables when you declare them, when this is possible:

> 在声明变量时，给它们赋一个初始值是一个很好的编程实践，这是可能的:

```js
let message = "hello";
let i = 0, j = 0, k = 0;
let x = 2, y = x*x; // Initializers can use previously declared variables
```

If you don’t specify an initial value for a variable with the let statement, the variable is declared, but its value is undefined until your code assigns a value to it.

> 如果没有使用let语句为变量指定初始值，则声明变量，但在代码为其赋值之前，变量的值是未定义的。

To declare a constant instead of a variable, use const instead of let. const works just like let except that you must initialize the constant when you declare it:

> 要声明常量而不是变量，请使用const而不是let。const的工作方式与let类似，只是在声明常量时必须初始化它:

```js
const H0 = 74;         // Hubble constant (km/s/Mpc)
const C = 299792.458;  // Speed of light in a vacuum (km/s)
const AU = 1.496E8;    // Astronomical Unit: distance to the sun (km)
```

As the name implies, constants cannot have their values changed, and any attempt to do so causes a TypeError to be thrown.

> 顾名思义，常量不能改变它们的值，任何这样做的尝试都会引发TypeError。

It is a common (but not universal) convention to declare constants using names with all capital letters such as H0 or HTTP_NOT_FOUND as a way to distinguish them from variables.

> 通常(但不是通用的)约定是使用全大写字母(如H0或HTTP_NOT_FOUND)的名称来声明常量，以将它们与变量区分开来。

WHEN TO USE CONST

There are two schools of thought about the use of the const keyword. One approach is to use const only for values that are fundamentally unchanging, like the physical constants shown, or program version numbers, or byte sequences used to identify file types, for example. Another approach recognizes that many of the so-called variables in our program don’t actually ever change as our program runs. In this approach, we declare everything with const, and then if we find that we do actually want to allow the value to vary, we switch the declaration to let. This may help prevent bugs by ruling out accidental changes to variables that we did not intend.

> 关于const关键字的使用有两种思想流派。一种方法是仅对基本不变的值使用const，例如所示的物理常量、程序版本号或用于标识文件类型的字节序列。另一种方法认为，程序中许多所谓的变量实际上不会随着程序的运行而改变。在这种方法中，我们用const声明所有内容，然后如果发现我们确实希望允许值变化，我们将声明切换为let。这可以通过排除我们无意中对变量的意外更改来防止错误。

In one approach, we use const only for values that must not change. In the other, we use const for any value that does not happen to change. I prefer the former approach in my own code.

> 在一种方法中，我们只对不能改变的值使用const。在另一种情况下，对于任何不会发生变化的值都使用const。在我自己的代码中，我更喜欢前一种方法。

In Chapter 5, we’ll learn about the for, for/in, and for/of loop statements in JavaScript. Each of these loops includes a loop variable that gets a new value assigned to it on each iteration of the loop. JavaScript allows us to declare the loop variable as part of the loop syntax itself, and this is another common way to use let:

> 在第五章，我们将学习JavaScript中的for、for/ In和for/of循环语句。每个循环都包含一个循环变量，该变量在循环的每次迭代中都赋给它一个新值。JavaScript允许我们将循环变量声明为循环语法本身的一部分，这是使用let的另一种常见方式:

```js
for(let i = 0, len = data.length; i < len; i++) console.log(data[i]);
for(let datum of data) console.log(datum);
for(let property in object) console.log(property);
```

It may seem surprising, but you can also use const to declare the loop “variables” for for/in and for/of loops, as long as the body of the loop does not reassign a new value. In this case, the const declaration is just saying that the value is constant for the duration of one loop iteration:

> 你可能会觉得奇怪，但是你也可以使用const来声明for/in和for/of循环的循环“变量”，只要循环体不重新赋值。在这种情况下，const声明只是表示该值在循环迭代的持续时间内为常量:

```js
for(const datum of data) console.log(datum);
for(const property in object) console.log(property);
```

VARIABLE AND CONSTANT SCOPE

The scope of a variable is the region of your program source code in which it is defined. Variables and constants declared with let and const are block scoped. This means that they are only defined within the block of code in which the let or const statement appears. JavaScript class and function definitions are blocks, and so are the bodies of if/else statements, while loops, for loops, and so on. Roughly speaking, if a variable or constant is declared within a set of curly braces, then those curly braces delimit the region of code in which the variable or constant is defined (though of course it is not legal to reference a variable or constant from lines of code that execute before the let or const statement that declares the variable). Variables and constants declared as part of a for, for/in, or for/of loop have the loop body as their scope, even though they technically appear outside of the curly braces.

> 变量的范围是定义变量的程序源代码的区域。用let和const声明的变量和常量是块作用域的。这意味着它们只在出现let或const语句的代码块中定义。JavaScript类和函数定义都是块，if/else语句体、while循环体、for循环体等等也是块。粗略地说,如果一个变量或常量声明一组花括号内,那么这些花括号划定的地区代码定义的变量或常数(当然这不是法律引用一个变量或常量的代码执行前让声明变量或常量声明)。作为for、for/in或for/of循环的一部分声明的变量和常量都有循环体作为它们的作用域，即使它们在技术上出现在花括号之外。

When a declaration appears at the top level, outside of any code blocks, we say it is a global variable or constant and has global scope. In Node and in client-side JavaScript modules (see Chapter 10), the scope of a global variable is the file that it is defined in. In traditional client-side JavaScript, however, the scope of a global variable is the HTML document in which it is defined. That is: if one `<script>` declares a global variable or constant, that variable or constant is defined in all of the `<script>` elements in that document (or at least all of the scripts that execute after the let or const statement executes).

> 当声明出现在顶层，在任何代码块之外时，我们说它是一个全局变量或常量，具有全局作用域。在Node和客户端JavaScript模块中(见第 10 章)，全局变量的作用域是定义它的文件。然而，在传统的客户端JavaScript中，全局变量的作用域是定义它的HTML文档。也就是说:如果一个 `<script>` 声明一个全局变量或常量，该变量或常量定义在该文档中的所有 `<script>` 该文档中的元素(或至少在let或const语句之后执行的所有脚本)。

REPEATED DECLARATIONS

It is a syntax error to use the same name with more than one let or const declaration in the same scope. It is legal (though a practice best avoided) to declare a new variable with the same name in a nested scope:

> 在同一个作用域中对多个let或const声明使用相同的名称是一个语法错

```js
const x = 1;        // Declare x as a global constant
if (x === 1) {
    let x = 2;      // Inside a block x can refer to a different value
    console.log(x); // Prints 2
}
console.log(x);     // Prints 1: we're back in the global scope now
let x = 3;          // ERROR! Syntax error trying to re-declare x
```
DECLARATIONS AND TYPES

If you’re used to statically typed languages such as C or Java, you may think that the primary purpose of variable declarations is to specify the type of values that may be assigned to a variable. But, as you have seen, there is no type associated with JavaScript’s variable declarations.2 A JavaScript variable can hold a value of any type. For example, it is perfectly legal (but generally poor programming style) in JavaScript to assign a number to a variable and then later assign a string to that variable:

> 如果您习惯了静态类型语言，比如C或Java，那么您可能认为变量声明的主要目的是指定可以赋给变量的值的类型。但是，如您所见，没有与JavaScript的变量声明相关联的类型。一个JavaScript变量可以保存任何类型的值。例如，在JavaScript中，先给变量赋一个数字，然后再给该变量赋一个字符串，这是完全合法的(但通常是糟糕的编程风格):

```js
let i = 10;
i = "ten";
```
### 3.10.2 Variable Declarations with var

In versions of JavaScript before ES6, the only way to declare a variable is with the var keyword, and there is no way to declare constants. The syntax of var is just like the syntax of let:

> 在ES6之前的JavaScript版本中，声明变量的唯一方法是使用var关键字，而没有方法声明常量。var的语法就像let的语法一样:

```js
var x;
var data = [], count = data.length;
for(var i = 0; i < count; i++) console.log(data[i]);
```

Although var and let have the same syntax, there are important differences in the way they work:

> 虽然var和let有相同的语法，但它们的工作方式有重要的不同:

- Variables declared with var do not have block scope. Instead, they are scoped to the body of the containing function no matter how deeply nested they are inside that function.
- If you use var outside of a function body, it declares a global variable. But global variables declared with var differ from globals declared with let in an important way. Globals declared with var are implemented as properties of the global object (§3.7). The global object can be referenced as globalThis. So if you write var x = 2; outside of a function, it is like you wrote globalThis.x = 2;. Note however, that the analogy is not perfect: the properties created with global var declarations cannot be deleted with the delete operator (§4.13.4). Global variables and constants declared with let and const are not properties of the global object.
- Unlike variables declared with let, it is legal to declare the same variable multiple times with var. And because var variables have function scope instead of block scope, it is actually common to do this kind of redeclaration. The variable i is frequently used for integer values, and especially as the index variable of for loops. In a function with multiple for loops, it is typical for each one to begin for(var i = 0; .... Because var does not scope these variables to the loop body, each of these loops is (harmlessly) re-declaring and re-initializing the same variable.
- One of the most unusual features of var declarations is known as hoisting. When a variable is declared with var, the declaration is lifted up (or “hoisted”) to the top of the enclosing function. The initialization of the variable remains where you wrote it, but the definition of the variable moves to the top of the function. So variables declared with var can be used, without error, anywhere in the enclosing function. If the initialization code has not run yet, then the value of the variable may be undefined, but you won’t get an error if you use the variable before it is initialized. (This can be a source of bugs and is one of the important misfeatures that let corrects: if you declare a variable with let but attempt to use it before the let statement runs, you will get an actual error instead of just seeing an undefined value.)

---

> - 用var声明的变量没有块作用域。相反，它们的作用域是包含函数的主体，无论它们嵌套在函数内部有多深。
> - 如果你在函数体之外使用var，它会声明一个全局变量。但是用var声明的全局变量与用let声明的全局变量在一个重要的方面不同。用var声明的全局变量是作为全局对象的属性实现的(§3.7)。全局对象可以引用为globalThis。如果你写var x = 2;在函数之外，它就像你写的globalThis。x = 2,。但是注意，这个类比并不完美:用全局var声明创建的属性不能用delete运算符删除(§4.13.4)。用let和const声明的全局变量和常量不是全局对象的属性。
> - 与用let声明的变量不同，用var多次声明同一个变量是合法的。而且因为var变量具有函数作用域而不是块作用域，所以这种类型的重声明实际上是很常见的。变量i经常被用来表示整数值，特别是作为for循环的索引变量。在有多个for循环的函数中，每个循环都以for(var i = 0;…因为var没有将这些变量作用域限定在循环体中，所以每个循环都(无害地)重新声明并初始化同一个变量。
> - var声明最不寻常的特性之一就是吊装。当用var声明一个变量时，这个声明会被提升(或“悬挂”)到外围函数的顶部。变量的初始化保持在编写它的地方，但变量的定义移到函数的顶部。因此，用var声明的变量可以在外围函数的任何位置使用，不会出错。如果初始化代码还没有运行，那么变量的值可能是未定义的，但如果在变量初始化之前使用它，则不会出现错误。(这可能是bug的来源，也是let纠正的重要错误特性之一:如果你用let声明了一个变量，但试图在let语句运行之前使用它，你将得到一个实际的错误，而不仅仅是看到一个未定义的值。)

USING UNDECLARED VARIABLES

In strict mode (§5.6.3), if you attempt to use an undeclared variable, you’ll get a reference error when you run your code. Outside of strict mode, however, if you assign a value to a name that has not been declared with let, const, or var, you’ll end up creating a new global variable. It will be a global no matter now deeply nested within functions and blocks your code is, which is almost certainly not what you want, is bug-prone, and is one of the best reasons for using strict mode!

> 在严格模式(§5.6.3)，如果你试图使用一个未声明的变量，你会得到一个引用错误，当你运行你的代码。但是，在严格模式之外，如果您将一个值赋给一个没有使用let、const或var声明的名称，那么您最终将创建一个新的全局变量。它将是全局的，无论你的代码是嵌套在函数和块中，这几乎肯定不是你想要的，它是容易出错的，这是使用严格模式的最佳原因之一!

Global variables created in this accidental way are like global variables declared with var: they define properties of the global object. But unlike the properties defined by proper var declarations, these properties can be deleted with the delete operator (§4.13.4).

> 以这种偶然方式创建的全局变量与用var声明的全局变量类似:它们定义全局对象的属性。但与正确的var声明定义的属性不同，这些属性可以通过delete运算符删除(§4.13.4)。

### 3.10.3 Destructuring Assignment

ES6 implements a kind of compound declaration and assignment syntax known as destructuring assignment. In a destructuring assignment, the value on the righthand side of the equals sign is an array or object (a “structured” value), and the lefthand side specifies one or more variable names using a syntax that mimics array and object literal syntax. When a destructuring assignment occurs, one or more values are extracted (“destructured”) from the value on the right and stored into the variables named on the left. Destructuring assignment is perhaps most commonly used to initialize variables as part of a const, let, or var declaration statement, but it can also be done in regular assignment expressions (with variables that have already been declared). And, as we’ll see in §8.3.5, destructuring can also be used when defining the parameters to a function.

> ES6 实现了一种复合声明和赋值语法，称为解构赋值。在解构赋值中，等号右边的值是一个数组或对象（“结构化的”值），左边使用模仿数组和对象字面量语法的语法指定一个或多个变量名。当发生解构赋值时，将从右边的值中提取一个或多个值（“解构”），并存储到左边命名的变量中。解构赋值可能常用来初始化 const、let 或 var 的声明，但它也可以用在正则赋值表达式中（使用已经声明的变量）。而且，我们将在 §8.3.5 中看到的，解构也可以用于定义函数的形参。

Here are simple destructuring assignments using arrays of values:

> 下面是使用数组值的简单解构赋值：

```js
let [x,y] = [1,2];  // Same as let x=1, y=2
[x,y] = [x+1,y+1];  // Same as x = x + 1, y = y + 1
[x,y] = [y,x];      // Swap the value of the two variables
[x,y]               // => [3,2]: the incremented and swapped values
```

Notice how destructuring assignment makes it easy to work with functions that return arrays of values:

> 请注意，解构赋值使返回数组值的函数变得很容易：

```js
// Convert [x,y] coordinates to [r,theta] polar coordinates
function toPolar(x, y) {
    return [Math.sqrt(x*x+y*y), Math.atan2(y,x)];
}

// Convert polar to Cartesian coordinates
function toCartesian(r, theta) {
    return [r*Math.cos(theta), r*Math.sin(theta)];
}

let [r,theta] = toPolar(1.0, 1.0);  // r == Math.sqrt(2); theta == Math.PI/4
let [x,y] = toCartesian(r,theta);   // [x, y] == [1.0, 1,0]
```

We saw that variables and constants can be declared as part of JavaScript’s various for loops. It is possible to use variable destructuring in this context as well. Here is a code that loops over the name/value pairs of all properties of an object and uses destructuring assignment to convert those pairs from two-element arrays into individual variables:

> 我们看到变量和常量可以声明为 JavaScript 的各种 for 循环的一部分。在这个上下文中也可以使用变量解构。下面的代码循环遍历对象的所有属性的名称/值对，并使用解构赋值将这些对从两个元素数组转换为单独的变量：

```js
let o = { x: 1, y: 2 }; // The object we'll loop over
for(const [name, value] of Object.entries(o)) {
    console.log(name, value); // Prints "x 1" and "y 2"
}
```

The number of variables on the left of a destructuring assignment does not have to match the number of array elements on the right. Extra variables on the left are set to undefined, and extra values on the right are ignored. The list of variables on the left can include extra commas to skip certain values on the right:

> 解构赋值左边的变量数量不必与右边的数组元素数量相匹配。左边的额外变量被设置为 undefined，右边的额外值被忽略。左边的变量列表可以包含额外的逗号，以跳过右边的某些值：

```js
let [x,y] = [1];     // x == 1; y == undefined
[x,y] = [1,2,3];     // x == 1; y == 2
[,x,,y] = [1,2,3,4]; // x == 2; y == 4
```

If you want to collect all unused or remaining values into a single variable when destructuring an array, use three dots (...) before the last variable name on the left-hand side:

> 如果你想在解构数组时将所有未使用的或剩余的值收集到一个变量中，在左边最后一个变量名之前使用三个点（…）：

```js
let [x, ...y] = [1,2,3,4];  // y == [2,3,4]
```

We’ll see three dots used this way again in §8.3.2, where they are used to indicate that all remaining function arguments should be collected into a single array.

> 在 §8.3.2 中，我们将再次看到以这种方式使用的三个点，它们用于指示所有剩余的函数实参收集到一个数组中。

Destructuring assignment can be used with nested arrays. In this case, the lefthand side of the assignment should look like a nested array literal:

> 解构赋值可用于嵌套数组。在这种情况下，赋值的左边应该看起来像一个嵌套的数组字面量：

```js
let [a, [b, c]] = [1, [2,2.5], 3]; // a == 1; b == 2; c == 2.5
```

A powerful feature of array destructuring is that it does not actually require an array! You can use any iterable object (Chapter 12) on the righthand side of the assignment; any object that can be used with a for/of loop (§5.4.4) can also be destructured:

> 数组解构的一个强大特性是它实际上不必须是个数组！你可以在赋值语句的右侧使用任何可迭代对象（第 12 章）;任何可以与 for/of 循环一起使用的对象（§5.4.4）也可以被解构:

```js
let [first, ...rest] = "Hello"; // first == "H"; rest == ["e","l","l","o"]
```

Destructuring assignment can also be performed when the righthand side is an object value. In this case, the lefthand side of the assignment looks something like an object literal: a comma-separated list of variable names within curly braces:

> 当右边是对象值时，也可以执行解构赋值。在这种情况下，赋值的左边看起来像一个对象字面量：花括号包含用逗号分隔的变量名列表：

```js
let transparent = {r: 0.0, g: 0.0, b: 0.0, a: 1.0}; // A RGBA color
let {r, g, b} = transparent;  // r == 0.0; g == 0.0; b == 0.0
```

The next example copies global functions of the Math object into variables, which might simplify code that does a lot of trigonometry:

> 下一个示例将 Math 对象的全局函数复制到变量中，这可能会简化执行大量三角函数的代码：

```js
// Same as const sin=Math.sin, cos=Math.cos, tan=Math.tan
const {sin, cos, tan} = Math;
```

Notice in the code here that the Math object has many properties other than the three that are destructured into individual variables. Those that are not named are simply ignored. If the lefthand side of this assignment had included a variable whose name was not a property of Math, that variable would simply be assigned undefined.

> 请注意，在这里的代码中，Math 对象有许多属性，而不是被解构为单个变量的三个属性。那些没有被命名的就被忽略了。如果这个赋值的左边包含了一个名称不是 Math 属性的变量，那么这个变量的赋值将是 undefined。

In each of these object destructuring examples, we have chosen variable names that match the property names of the object we’re destructuring. This keeps the syntax simple and easy to understand, but it is not required. Each of the identifiers on the lefthand side of an object destructuring assignment can also be a colon-separated pair of identifiers, where the first is the name of the property whose value is to be assigned and the second is the name of the variable to assign it to:

> 在每个对象解构示例中，我们都选择了与要解构的对象的属性名匹配的变量名。这使语法保持简单和易于理解，但这不是必需的。每个对象解构赋值也可以用冒号分割的一对标识符，冒号左边是属性的名字，冒号右边是被赋值的变量名：

```js
// Same as const cosine = Math.cos, tangent = Math.tan;
const { cos: cosine, tan: tangent } = Math;
```

I find that object destructuring syntax becomes too complicated to be useful when the variable names and property names are not the same, and I tend to avoid the shorthand in this case. If you choose to use it, remember that property names are always on the left of the colon, in both object literals and on the left of an object destructuring assignment.

> 这样写对象解构语法变得太复杂，但我发现，当变量名和属性名不相同时就非常有用，在这种情况下我倾向于避免使用简写。如果选择使用它，请记住无论是对象字面量还是对象解构赋值，属性名总是在冒号的左边。

Destructuring assignment becomes even more complicated when it is used with nested objects, or arrays of objects, or objects of arrays, but it is legal:

> 当与嵌套对象、对象数组或数组对象解构赋值时会变得更加复杂，但它是合法的：

```js
let points = [{x: 1, y: 2}, {x: 3, y: 4}];     // An array of two point objects
let [{x: x1, y: y1}, {x: x2, y: y2}] = points; // destructured into 4 variables.
(x1 === 1 && y1 === 2 && x2 === 3 && y2 === 4) // => true
```

Or, instead of destructuring an array of objects, we could destructure an object of arrays:

> 或者，我们可以对数组对象进行解构，而不是对数组对象进行解构：

```js
let points = { p1: [1,2], p2: [3,4] };         // An object with 2 array props
let { p1: [x1, y1], p2: [x2, y2] } = points;   // destructured into 4 vars
(x1 === 1 && y1 === 2 && x2 === 3 && y2 === 4) // => true
```

Complex destructuring syntax like this can be hard to write and hard to read, and you may be better off just writing out your assignments explicitly with traditional code like `let x1 = points.p1[0];`.

> 像这样复杂的解构语法可能很难写，也很难读，最好使用传统的代码，如`let x1 = points.p1[0];`来显式地写出你的赋值。

UNDERSTANDING COMPLEX DESTRUCTURING

> **理解复杂的解构**

If you find yourself working with code that uses complex destructuring assignments, there is a useful regularity that can help you make sense of the complex cases. Think first about a regular (single-value) assignment. After the assignment is done, you can take the variable name from the lefthand side of the assignment and use it as an expression in your code, where it will evaluate to whatever value you assigned it. The same thing is true for destructuring assignment. The lefthand side of a destructuring assignment looks like an array literal or an object literal (§6.2.1 and §6.10). After the assignment has been done, the lefthand side will actually work as a valid array literal or object literal elsewhere in your code. You can check that you’ve written a destructuring assignment correctly by trying to use the lefthand side on the righthand side of another assignment expression:

> 如果发现自己正在处理使用复杂解构赋值的代码，那么有一个有用的规则可以帮助您理解复杂的情况。首先想象常规（单值）赋值。在赋值完成后，可以从赋值的左边取变量名，并在代码中使用它作为表达式，它将计算赋给它的任何值。对于解构赋值也是一样的。解构赋值的左边看起来像数组字面量或对象字面量（§6.2.1 和 §6.10）。赋值完成后，左边将在代码的任何地方作为有效的数组字面量或对象字面量。你可以通过尝试在另一个赋值表达式的右边使用解构赋值表达式的左边来检查你是否正确地编写了一个解构赋值：

```js
// Start with a data structure and a complex destructuring
let points = [{x: 1, y: 2}, {x: 3, y: 4}];
let [{x: x1, y: y1}, {x: x2, y: y2}] = points;

// Check your destructuring syntax by flipping the assignment around
let points2 = [{x: x1, y: y1}, {x: x2, y: y2}]; // points2 == points
```
## 3.11 Summary

Some key points to remember about this chapter:

> 关于本章需要记住的一些要点:

- How to write and manipulate numbers and strings of text in JavaScript.
- How to work with JavaScript’s other primitive types: booleans, Symbols, null, and undefined.
- The differences between immutable primitive types and mutable reference types.
- How JavaScript converts values implicitly from one type to another and how you can do so explicitly in your programs.
- How to declare and initialize constants and variables (including with destructuring assignment) and the lexical scope of the variables and constants you declare.

---

> - 如何在JavaScript中编写和操作数字和文本字符串。
> - 如何使用JavaScript的其他原始类型:布尔型，符号，空，和未定义。
> - 不可变基元类型和可变引用类型的区别。
> - JavaScript如何隐式地将值从一种类型转换为另一种类型，以及你如何在你的程序中显式地这样做。
> - 如何声明和初始化常量和变量(包括解构赋值)和变量和常量的词法范围你声明。

---

1. This is the format for numbers of type double in Java, C++, and most modern programming languages.
2. There are JavaScript extensions, such as TypeScript and Flow (§17.8), that allow types to be specified as part of variable declarations with syntax like let x: number = 0;.
