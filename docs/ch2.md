# 第 2 章 词法结构

The lexical structure of a programming language is the set of elementary rules that specifies how you write programs in that language. It is the lowest-level syntax of a language: it specifies what variable names look like, the delimiter characters for comments, and how one program statement is separated from the next, for example. This short chapter documents the lexical structure of JavaScript. It covers:

> 编程语言的词法结构是一组基本规则，用于指定如何用该语言编写程序。它是一种语言的最低层次语法：例如，它指定变量名的样子，注释的分隔符字符，以及一个程序语句如何与下一个程序语句分隔。这个简短的章节描述了 JavaScript 的词法结构。它涵盖了：

- Case sensitivity, spaces, and line breaks
- Comments
- Literals
- Identifiers and reserved words
- Unicode
- Optional semicolons

## 2.1 The Text of a JavaScript Program

JavaScript is a case-sensitive language. This means that language keywords, variables, function names, and other identifiers must always be typed with a consistent capitalization of letters. The while keyword, for example, must be typed “while,” not “While” or “WHILE.” Similarly, online, Online, OnLine, and ONLINE are four distinct variable names.

> JavaScript 是一种区分大小写的语言。这意味着语言关键字、变量、函数名和其他标识符必须始终以一致的大小写输入。例如，while 关键字必须输入“while”，而不是“While”或“WHILE”。同样，online, Online，OnLine 和 ONLINE 是四个不同的变量名。

JavaScript ignores spaces that appear between tokens in programs. For the most part, JavaScript also ignores line breaks (but see §2.6 for an exception). Because you can use spaces and newlines freely in your programs, you can format and indent your programs in a neat and consistent way that makes the code easy to read and understand.

> JavaScript 忽略程序中标记之间出现的空格。在大多数情况下，JavaScript 也会忽略换行符（但是，关于一个例外，请参阅 §2.6）。由于您可以在程序中自由地使用空格和换行符，因此您可以以一种整洁和一致的方式对程序进行格式化和缩进，从而使代码易于阅读和理解。

In addition to the regular space character (`\u0020`), JavaScript also recognizes tabs, assorted ASCII control characters, and various Unicode space characters as whitespace. JavaScript recognizes newlines, carriage returns, and a carriage return/line feed sequence as line terminators.

> 除了常规的空格字符（`\u0020`）之外，JavaScript 还将制表符、各种 ASCII 控制字符和各种 Unicode 空格字符识别为空格。JavaScript 识别换行符、回车符和回车/换行序列作为行结束符。

## 2.2 Comments

JavaScript supports two styles of comments. Any text between a `//` and the end of a line is treated as a comment and is ignored by JavaScript. Any text between the characters `/*` and `*/` is also treated as a comment; these comments may span multiple lines but may not be nested. The following lines of code are all legal JavaScript comments:

> JavaScript 支持两种风格的注释。在 `//` 和行尾之间的任何文本都被 JavaScript 视为注释并被忽略。字符 `/*` 和 `*/` 之间的任何文本也被视为注释；这些注释可能跨越多行，但可能不是嵌套的。下面几行代码都是合法的 JavaScript 注释：

```js
// This is a single-line comment.

/* This is also a comment */  // and here is another comment.

/*
 * This is a multi-line comment. The extra * characters at the start of
 * each line are not a required part of the syntax; they just look cool!
 */
```

## 2.3 Literals

A literal is a data value that appears directly in a program. The following are all literals:

> 字面量是直接出现在程序中的数据值。以下都是字面量：

```js
12               // The number twelve
1.2              // The number one point two
"hello world"    // A string of text
'Hi'             // Another string
true             // A Boolean value
false            // The other Boolean value
null             // Absence of an object
```

Complete details on numeric and string literals appear in Chapter 3.

> 数值和字符串字面量的完整细节出现在第 3 章。

## 2.4 Identifiers and Reserved Words

An identifier is simply a name. In JavaScript, identifiers are used to name constants, variables, properties, functions, and classes and to provide labels for certain loops in JavaScript code. A JavaScript identifier must begin with a letter, an underscore (`_`), or a dollar sign (`$`). Subsequent characters can be letters, digits, underscores, or dollar signs. (Digits are not allowed as the first character so that JavaScript can easily distinguish identifiers from numbers.) These are all legal identifiers:

> 标识符只是一个名称。在 JavaScript 中，标识符用于命名常量、变量、属性、函数和类，并为 JavaScript 代码中的某些循环提供标签。JavaScript 标识符必须以字母、下划线（`_`）或美元符号（`$`）开头。后面的字符可以是字母、数字、下划线或美元符号。（数字不允许作为第一个字符，这样 JavaScript 可以很容易地将标识符与数字区分开来。）这些都是合法的标识符：

```
i
my_variable_name
v13
_dummy
$str
```

Like any language, JavaScript reserves certain identifiers for use by the language itself. These “reserved words” cannot be used as regular identifiers. They are listed in the next section.

> 与任何语言一样，JavaScript 保留某些标识符供语言本身使用。这些“保留字”不能用作常规标识符。它们将在下一节中列出。

### 2.4.1 Reserved Words

The following words are part of the JavaScript language. Many of these (such as if, while, and for) are reserved keywords that must not be used as the names of constants, variables, functions, or classes (though they can all be used as the names of properties within an object). Others (such as from, of, get, and set) are used in limited contexts with no syntactic ambiguity and are perfectly legal as identifiers. Still other keywords (such as let) can’t be fully reserved in order to retain backward compatibility with older programs, and so there are complex rules that govern when they can be used as identifiers and when they cannot. (let can be used as a variable name if declared with var outside of a class, for example, but not if declared inside a class or with const.) The simplest course is to avoid using any of these words as identifiers, except for from, set, and target, which are safe to use and are already in common use.

> 下面的单词是 JavaScript 语言的一部分。其中许多（如 if、while 和 for）是保留的关键字，不能用作常量、变量、函数或类的名称（尽管它们都可以用作对象中的属性名称）。其他的（如 from、of、get 和 set）则在有限的上下文中使用，没有语法歧义，作为标识符完全合法。还有一些关键字（比如let）不能被完全保留，以保持与旧程序的向后兼容性，因此有复杂的规则来管理何时可以将它们用作标识符，何时不能。（例如，如果在类外部用 var 声明，let 就可以用作变量名，但如果在类内部或用 const 声明，let 就不能用作变量名。）最简单的方法是避免使用这些词作为标识符，除了 from、set 和 target 之外，这些词使用起来很安全，而且已经很常用了。

```
as      const      export     get         null     target   void
async   continue   extends    if          of       this     while
await   debugger   false      import      return   throw    with
break   default    finally    in          set      true     yield
case    delete     for        instanceof  static   try
catch   do         from       let         super    typeof
class   else       function   new         switch   var
```

JavaScript also reserves or restricts the use of certain keywords that are not currently used by the language but that might be used in future versions:

> JavaScript 还保留或限制使用某些关键字，目前没有使用的语言，但可能会在未来的版本：

```
enum  implements  interface  package  private  protected  public
```

For historical reasons, arguments and eval are not allowed as identifiers in certain circumstances and are best avoided entirely.

> 由于历史原因，参数和 eval 在某些情况下不允许作为标识符，最好完全避免使用。

## 2.5 Unicode

JavaScript programs are written using the Unicode character set, and you can use any Unicode characters in strings and comments. For portability and ease of editing, it is common to use only ASCII letters and digits in identifiers. But this is a programming convention only, and the language allows Unicode letters, digits, and ideographs (but not emojis) in identifiers. This means that programmers can use mathematical symbols and words from non-English languages as constants and variables:

> JavaScript 程序是使用 Unicode 字符集编写的，您可以在字符串和注释中使用任何 Unicode 字符。为了便于移植和编辑，通常在标识符中只使用 ASCII 字母和数字。但这只是一种编程约定，该语言允许在标识符中使用 Unicode 字母、数字和表意文字（但不允许使用表情符号）。这意味着程序员可以使用来自非英语语言的数学符号和单词作为常量和变量：

```js
const π = 3.14;
const sí = true;
```

### 2.5.1 Unicode Escape Sequences

Some computer hardware and software cannot display, input, or correctly process the full set of Unicode characters. To support programmers and systems using older technology, JavaScript defines escape sequences that allow us to write Unicode characters using only ASCII characters. These Unicode escapes begin with the characters `\u` and are either followed by exactly four hexadecimal digits (using uppercase or lowercase letters A–F) or by one to six hexadecimal digits enclosed within curly braces. These Unicode escapes may appear in JavaScript string literals, regular expression literals, and identifiers (but not in language keywords). The Unicode escape for the character “`é,`” for example, is `\u00E9`; here are three different ways to write a variable name that includes this character:

> 一些计算机硬件和软件不能显示、输入或正确处理完整的 Unicode 字符集。为了支持使用较旧技术的程序员和系统，JavaScript 定义了转义序列，允许我们仅使用 ASCII 字符编写 Unicode 字符。这些 Unicode 转义以字符 `\u` 开始，后跟四个十六进制数字（使用大写或小写字母A-F），或者用大括号括起来的一到六个十六进制数字。这些 Unicode 转义可能以 JavaScript 字符串、正则表达式和标识符的形式出现（但不会以语言关键字的形式出现）。例如，Unicode 字符 “`é,`” 的转义是`\u00E9`；这里有三种不同的方式来写一个变量名，包括这个字符：

```js
let café = 1; // Define a variable using a Unicode character
caf\u00e9     // => 1; access the variable using an escape sequence
caf\u{E9}     // => 1; another form of the same escape sequence
```

Early versions of JavaScript only supported the four-digit escape sequence. The version with curly braces was introduced in ES6 to better support Unicode codepoints that require more than 16 bits, such as emoji:

> 早期版本的 JavaScript 只支持四位数转义序列。带花括号的版本是在 ES6 中引入的，目的是为了更好地支持需要超过16位元的 Unicode 码点，比如表情符号:

```js
console.log("\u{1F600}");  // Prints a smiley face emoji
```

Unicode escapes may also appear in comments, but since comments are ignored, they are simply treated as ASCII characters in that context and not interpreted as Unicode.

> Unicode 转义也可能出现在注释中，但是由于注释被忽略，因此它们在该上下文中只是作为 ASCII 字符处理，而不是解释为 Unicode。

### 2.5.2 Unicode Normalization

If you use non-ASCII characters in your JavaScript programs, you must be aware that Unicode allows more than one way of encoding the same character. The string “`é,`” for example, can be encoded as the single Unicode character `\u00E9` or as a regular ASCII “`e`” followed by the acute accent combining mark `\u0301`. These two encodings typically look exactly the same when displayed by a text editor, but they have different binary encodings, meaning that they are considered different by JavaScript, which can lead to very confusing programs:

> 如果在 JavaScript 程序中使用非 ASCII 字符，则必须知道 Unicode 允许对同一字符进行多种编码方式。例如，字符串 “`é,`” 可以编码为单个Unicode字符 `\u00E9`，或编码为后面跟着急性重音组合标记 `\u0301` 的正则ASCII “`e`”。这两种编码在文本编辑器中显示时看起来是完全一样的，但是它们有不同的二进制编码，这意味着它们被 JavaScript  认为是不同的，这可能会导致非常混乱的程序:

```js
const café = 1;  // This constant is named "caf\u{e9}"
const café = 2;  // This constant is different: "cafe\u{301}"
café  // => 1: this constant has one value
café  // => 2: this indistinguishable constant has a different value
```

The Unicode standard defines the preferred encoding for all characters and specifies a normalization procedure to convert text to a canonical form suitable for comparisons. JavaScript assumes that the source code it is interpreting has already been normalized and does not do any normalization on its own. If you plan to use Unicode characters in your JavaScript programs, you should ensure that your editor or some other tool performs Unicode normalization of your source code to prevent you from ending up with different but visually indistinguishable identifiers.

> Unicode 标准定义了所有字符的首选编码，并指定了将文本转换为适合于比较的规范形式的标准化过程。JavaScript 假设它要解释的源代码已经被规范化了，它自己不做任何规范化。如果您计划在 JavaScript 程序中使用 Unicode 字符，那么应该确保您的编辑器或其他工具对源代码执行 Unicode 规范化，以防止出现不同但视觉上无法区分的标识符。

## 2.6 Optional Semicolons

Like many programming languages, JavaScript uses the semicolon (;) to separate statements (see Chapter 5) from one another. This is important for making the meaning of your code clear: without a separator, the end of one statement might appear to be the beginning of the next, or vice versa. In JavaScript, you can usually omit the semicolon between two statements if those statements are written on separate lines. (You can also omit a semicolon at the end of a program or if the next token in the program is a closing curly brace: }.) Many JavaScript programmers (and the code in this book) use semicolons to explicitly mark the ends of statements, even where they are not required. Another style is to omit semicolons whenever possible, using them only in the few situations that require them. Whichever style you choose, there are a few details you should understand about optional semicolons in JavaScript.

> 像许多编程语言一样，JavaScript 使用分号（;）来分隔语句（参见第 5 章）。这对于明确代码的含义非常重要：如果没有分隔符，一条语句的结尾可能会是下一条语句的开始，反之亦然。在 JavaScript 中，如果两个语句写在不同的行上，通常可以省略这两个语句之间的分号。（如果程序的下一个标记是右花括号 }，也可以省略在程序末尾的分号。）许多 JavaScript 程序员（以及本书中的代码）使用分号来显式地标记语句的结束，即使在不需要分号的地方也是如此。另一种风格是尽可能省略分号，只在少数需要分号的情况下使用。无论您选择哪种样式，关于 JavaScript 中的可选分号，您都应该了解一些细节。

Consider the following code. Since the two statements appear on separate lines, the first semicolon could be omitted:

> 考虑下面的代码。由于这两个语句出现在不同的行中，第一个分号可以省略：

```js
a = 3;
b = 4;
```

Written as follows, however, the first semicolon is required:

> 但是，如写如下，第一个分号是必需的:

```js
a = 3; b = 4;
```

Note that JavaScript does not treat every line break as a semicolon: it usually treats line breaks as semicolons only if it can’t parse the code without adding an implicit semicolon. More formally (and with three exceptions described a bit later), JavaScript treats a line break as a semicolon if the next nonspace character cannot be interpreted as a continuation of the current statement. Consider the following code:

> 请注意，JavaScript 并不把每个断行符都当作分号来处理：它通常只在不添加隐式分号而无法解析代码时才把断行符当作分号来处理。更正式的说法是，如果下一个非空格字符不能解释为当前语句的延续，JavaScript将换行符视为分号。考虑以下代码:

```js
let a
a
=
3
console.log(a)
```

JavaScript interprets this code like this:

> JavaScript 这样解释这段代码：

```js
let a; a = 3; console.log(a);
```

JavaScript does treat the first line break as a semicolon because it cannot parse the code let a a without a semicolon. The second a could stand alone as the statement a;, but JavaScript does not treat the second line break as a semicolon because it can continue parsing the longer statement a = 3;.

> JavaScript 确实把第一个换行符当作分号，因为它不能解析没有分号的代码。第二个 a 可以单独作为语句 a;，但 JavaScript 不会将第二个换行符作为分号处理，因为它可以继续解析较长的语句 a = 3;。

These statement termination rules lead to some surprising cases. This code looks like two separate statements separated with a newline:

> 这些语句终止规则会导致一些奇怪的情况。这段代码看起来像用换行符分隔的两个单独的语句：

```js
let y = x + f
(a+b).toString()
```

But the parentheses on the second line of code can be interpreted as a function invocation of f from the first line, and JavaScript interprets the code like this:

> 但是第二行括号可以解释为第一行 f 的函数调用，JavaScript 是这样解释的：

```js
let y = x + f(a+b).toString();
```

More likely than not, this is not the interpretation intended by the author of the code. In order to work as two separate statements, an explicit semicolon is required in this case.

> 很可能，这不是代码作者想要的解释。为了作为两个独立的语句工作，在这种情况下需要显式的分号。

In general, if a statement begins with (, [, /, +, or -, there is a chance that it could be interpreted as a continuation of the statement before. Statements beginning with /, +, and - are quite rare in practice, but statements beginning with ( and [ are not uncommon at all, at least in some styles of JavaScript programming. Some programmers like to put a defensive semicolon at the beginning of any such statement so that it will continue to work correctly even if the statement before it is modified and a previously terminating semicolon removed:

> 通常，如果一个语句以 (、[、/、+ 或 - 开头，那么它有可能被解释为之前语句的延续。在实践中，以 /、+ 和 - 开头的语句非常少见，但是以 ( 和 [ 开头的语句并不少见，至少在某些 JavaScript 编程风格中是这样的。一些程序员喜欢在任何这样的语句的开头放一个防御分号，这样即使在修改之前的语句和删除之前的终止分号时，它也能继续正确工作:

```js
let x = 0                         // Semicolon omitted here
;[x,x+1,x+2].forEach(console.log) // Defensive ; keeps this statement separate
```

There are three exceptions to the general rule that JavaScript interprets line breaks as semicolons when it cannot parse the second line as a continuation of the statement on the first line. The first exception involves the return, throw, yield, break, and continue statements (see Chapter 5). These statements often stand alone, but they are sometimes followed by an identifier or expression. If a line break appears after any of these words (before any other tokens), JavaScript will always interpret that line break as a semicolon. For example, if you write:

> 当 JavaScript 不能将第二行解析为第一行语句的延续时，它会将换行符解释为分号。第一个异常涉及到 return、throw、yield、break 和 continue 语句（参见第 5 章），这些语句通常是独立的，但有时会后跟一个标识符或表达式。如果一个换行符出现在这些单词之后（在任何其他标记之前），JavaScript 总是将该换行符解释为分号。例如，如果你写：

```js
return
true;
```

JavaScript assumes you meant:

> JavaScript 假设您的意思是：

```js
return; true;
```

However, you probably meant:

> 不过，你的意思可能是：

```js
return true;
```

This means that you must not insert a line break between return, break, or continue and the expression that follows the keyword. If you do insert a line break, your code is likely to fail in a nonobvious way that is difficult to debug.

> 这意味着不能在 return、break 或 continue 和关键字后面的表达式之间插入换行符。如果您确实插入了一个换行符，那么您的代码很可能会以一种难以调试的不明显的方式失败。

The second exception involves the ++ and −− operators (§4.8). These operators can be prefix operators that appear before an expression or postfix operators that appear after an expression. If you want to use either of these operators as postfix operators, they must appear on the same line as the expression they apply to. The third exception involves functions defined using concise “arrow” syntax: the => arrow itself must appear on the same line as the parameter list.

> 第二个例外涉及到 ++ 和 -- 运算符（§4.8）。这些运算符可以是出现在表达式之前的前缀运算符，也可以是出现在表达式之后的后缀运算符。如果要使用这些运算符中的任何一个作为后缀运算符，则它们必须与应用它们的表达式出现在同一行。第三个异常涉及使用简洁的“箭头”语法定义的函数：=> 箭头本身必须与参数列表出现在同一行。

## 2.7 Summary

This chapter has shown how JavaScript programs are written at the lowest level. The next chapter takes us one step higher and introduces the primitive types and values (numbers, strings, and so on) that serve as the basic units of computation for JavaScript programs.

> 本章展示了 JavaScript 程序是如何在底层编写的。下一章将进一步介绍作为 JavaScript 程序基本计算单元的基本类型和值（数字、字符串等）。