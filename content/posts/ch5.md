---
title: "第 5 章 语句"
date: 2020-11-02T22:18:38+08:00
---

Chapter 4 described expressions as JavaScript phrases. By that analogy, statements are JavaScript sentences or commands. Just as English sentences are terminated and separated from one another with periods, JavaScript statements are terminated with semicolons (§2.6). Expressions are evaluated to produce a value, but statements are executed to make something happen.

> 第 4 章将表达式描述为 JavaScript 短语。根据这个比喻，语句就是 JavaScript 句子或命令。就像英语句子以句点结尾并彼此分开一样，JavaScript 语句以分号结尾（§2.6）。表达式计算来产生一个值，但是语句被执行则使某些事情发生。

One way to “make something happen” is to evaluate an expression that has side effects. Expressions with side effects, such as assignments and function invocations, can stand alone as statements, and when used this way are known as expression statements. A similar category of statements are the declaration statements that declare new variables and define new functions.

> “使某事发生”的一种方法是对有副作用的表达式求值。带有副作用（如赋值和函数调用）的表达式可以单独作为语句使用，以这种方式使用时称为表达式语句。类似的语句是声明语句，它声明新的变量和定义的新函数。

JavaScript programs are nothing more than a sequence of statements to execute. By default, the JavaScript interpreter executes these statements one after another in the order they are written. Another way to “make something happen” is to alter this default order of execution, and JavaScript has a number of statements or control structures that do just this:

> JavaScript 程序只不过是一系列顺序执行的语句。默认情况下，JavaScript 解释器按照语句的编写顺序依次执行这些语句。另一种“让事情发生”的方法是改变默认的执行顺序，JavaScript 有很多语句或控制结构就是这样做的:

Conditionals
> 条件
Statements like if and switch that make the JavaScript interpreter execute or skip other statements depending on the value of an expression
> 类似 if 和 switch 语句，让 JavaScript 解释器根据一个表达式的值计算或跳过一些语句

Loops
> 循环
Statements like while and for that execute other statements repetitively
> 类似 while 和 for 语句，重复执行一些语句

Jumps
> 跳转
Statements like break, return, and throw that cause the interpreter to jump to another part of the program
> 类似 break、return 和 throw 语句，引发解释器跳转到程序的另一部分

The sections that follow describe the various statements in JavaScript and explain their syntax. Table 5-1, at the end of the chapter, summarizes the syntax. A JavaScript program is simply a sequence of statements, separated from one another with semicolons, so once you are familiar with the statements of JavaScript, you can begin writing JavaScript programs.

> 接下来的小结讲解各种各样的 JavaScript 语句并解释它们的语法。本章最后表 5-1 总结了语法。JavaScript 程序是简单的顺序语句，被分号分隔，所以一旦熟悉了 JavaScript 语句，就可以开始编写 JavaScript 程序了。

## 5.1 Expression Statements

The simplest kinds of statements in JavaScript are expressions that have side effects. This sort of statement was shown in Chapter 4. Assignment statements are one major category of expression statements. For example:

> JavaScript 中最简单的语句是表达式，它们有副作用。下面这个简短的语句在第 4 章出现过。赋值语句是表达式语句分类中主要的语句之一。例如：

```js
greeting = "Hello " + name;
i *= 3;
```
The increment and decrement operators, ++ and --, are related to assignment statements. These have the side effect of changing a variable value, just as if an assignment had been performed:

> 递增和递减运算符 ++ 和 -- 与赋值语句有关。这些具有更改变量值的副作用，就像执行了赋值一样：

```js
counter++;
```
The delete operator has the important side effect of deleting an object property. Thus, it is almost always used as a statement, rather than as part of a larger expression:

> delete 运算符具有删除对象属性的重要副作用。因此，它几乎总是用作语句，而不是用作较大表达式的一部分：

```js
delete o.x;
```
Function calls are another major category of expression statements. For example:

> 函数调用是表达式语句的另一个主要类别。例如：

```js
console.log(debugMessage);
displaySpinner(); // A hypothetical function to display a spinner in a web app.
```
These function calls are expressions, but they have side effects that affect the host environment or program state, and they are used here as statements. If a function does not have any side effects, there is no sense in calling it, unless it is part of a larger expression or an assignment statement. For example, you wouldn’t just compute a cosine and discard the result:

> 这些函数调用是表达式，但是它们具有影响主机环境或程序状态的副作用，在这里用作语句。如果函数没有任何副作用，则除非有任何较大的表达式或赋值语句的一部分，否则调用该函数没有任何意义。例如，您不会仅计算余弦并丢弃结果：

```js
Math.cos(x);
```
But you might well compute the value and assign it to a variable for future use:

> 但是可能会计算出该值并将其分配给变量以供将来使用：

```js
cx = Math.cos(x);
```
Note that each line of code in each of these examples is terminated with a semicolon.

> 请注意，这些示例中的每行代码均以分号结尾。

## 5.2 Compound and Empty Statements
Just as the comma operator (§4.13.7) combines multiple expressions into a single expression, a statement block combines multiple statements into a single compound statement. A statement block is simply a sequence of statements enclosed within curly braces. Thus, the following lines act as a single statement and can be used anywhere that JavaScript expects a single statement:

> 正如逗号运算符（§4.13.7）将多个表达式组合成一个表达式一样，一个语句块将多个语句组合成一个复合语句。语句块只是括在花括号内的一系列语句。因此，以下几行充当单个语句，并且可以在 JavaScript 需要单个语句的任何地方使用：

```js
{
    x = Math.PI;
    cx = Math.cos(x);
    console.log("cos(π) = " + cx);
}
```
There are a few things to note about this statement block. First, it does not end with a semicolon. The primitive statements within the block end in semicolons, but the block itself does not. Second, the lines inside the block are indented relative to the curly braces that enclose them. This is optional, but it makes the code easier to read and understand.

> 关于此语句块需要注意一些事项。首先，它不以分号结尾。块中的原始语句以分号结尾，但是块本身没有。其次，相对于包围它们的花括号将块内的行缩进。这是可选的，但是它使代码更易于阅读和理解。

Just as expressions often contain subexpressions, many JavaScript statements contain substatements. Formally, JavaScript syntax usually allows a single substatement. For example, the while loop syntax includes a single statement that serves as the body of the loop. Using a statement block, you can place any number of statements within this single allowed substatement.

> 正如表达式通常包含子表达式一样，许多 JavaScript 语句也包含子语句。正式地，JavaScript 语法通常允许单个子语句。例如，while 循环语法包括一个用作循环主体的语句。使用语句块，可以在此单个允许的子语句中放置任意数量的语句。

A compound statement allows you to use multiple statements where JavaScript syntax expects a single statement. The empty statement is the opposite: it allows you to include no statements where one is expected. The empty statement looks like this:

> 复合语句允许在 JavaScript 语法要求使用单个语句的情况下使用多个语句。空语句则相反：它允许在期望的位置不包含任何语句。空语句如下所示：

```js
;
```
The JavaScript interpreter takes no action when it executes an empty statement. The empty statement is occasionally useful when you want to create a loop that has an empty body. Consider the following for loop (for loops will be covered in §5.4.3):

> JavaScript解释器执行空语句时不执行任何操作。当要创建一个包含空主体的循环时，空语句有时会很有用。考虑以下 for 循环（for 循环将在 §5.4.3 中介绍）：

```js
// Initialize an array a
for(let i = 0; i < a.length; a[i++] = 0) ;
```
In this loop, all the work is done by the expression `a[i++] = 0`, and no loop body is necessary. JavaScript syntax requires a statement as a loop body, however, so an empty statement—just a bare semicolon—is used.

> 在此循环中，所有工作均由表达式 `a[i++] = 0` 完成，并且不需要循环体。JavaScript 语法需要一个语句作为循环体，因此使用一个空语句（仅一个裸分号）。

Note that the accidental inclusion of a semicolon after the right parenthesis of a for loop, while loop, or if statement can cause frustrating bugs that are difficult to detect. For example, the following code probably does not do what the author intended:

> 请注意，在 for 循环，while 循环或 if 语句的右括号后面意外地包含分号，可能导致令人沮丧的错误，难以检测。例如，以下代码可能不符合作者的意图：

```js
if ((a === 0) || (b === 0));  // Oops! This line does nothing...
    o = null;                 // and this line is always executed.
```
When you intentionally use the empty statement, it is a good idea to comment your code in a way that makes it clear that you are doing it on purpose. For example:

> 当有意使用空语句时，以下注释代码是一种清楚表明是故意这样做的方式的好主意。 例如：

```js
for(let i = 0; i < a.length; a[i++] = 0) /* empty */ ;
```
## 5.3 Conditionals
Conditional statements execute or skip other statements depending on the value of a specified expression. These statements are the decision points of your code, and they are also sometimes known as “branches.” If you imagine a JavaScript interpreter following a path through your code, the conditional statements are the places where the code branches into two or more paths and the interpreter must choose which path to follow.

> 条件语句根据指定表达式的值执行或跳过其他语句。这些语句是代码的决策点，有时也称为“分支”。如果想象 JavaScript 解释器遵循代码路径，则条件语句是代码分支到两个或更多路径的位置，并且解释器必须选择要遵循的路径。

The following subsections explain JavaScript’s basic conditional, the if/else statement, and also cover switch, a more complicated, multiway branch statement.

> 以下小节介绍了 JavaScript 的基本条件，if / else 语句，还介绍了 switch，更复杂的多路分支语句。

### 5.3.1 if
The if statement is the fundamental control statement that allows JavaScript to make decisions, or, more precisely, to execute statements conditionally. This statement has two forms. The first is:

> if 语句是基本的控制语句，它允许 JavaScript 进行决策，或更准确地说，可以有条件地执行语句。该语句有两种形式。 第一个是：

```js
if (expression)
    statement
```
In this form, expression is evaluated. If the resulting value is truthy, statement is executed. If expression is falsy, statement is not executed. (See §3.4 for a definition of truthy and falsy values.) For example:

> 以这种形式，表达式被评估。如果结果值为真，则执行语句。如果 expression 是假，则不执行语句。（有关真实值和假值的定义，请参见 §3.4。）例如：

```js
if (username == null)       // If username is null or undefined,
    username = "John Doe";  // define it
Or similarly:

// If username is null, undefined, false, 0, "", or NaN, give it a new value
if (!username) username = "John Doe";
```
Note that the parentheses around the expression are a required part of the syntax for the if statement.

> 请注意，表达式周围的括号是 if 语句语法的必需部分。

JavaScript syntax requires a single statement after the if keyword and parenthesized expression, but you can use a statement block to combine multiple statements into one. So the if statement might also look like this:

> JavaScript 语法在 if 关键字和带括号的表达式之后需要一个语句，但是可以使用语句块将多个语句组合为一个。因此，if 语句也可能如下所示：

```js
if (!address) {
    address = "";
    message = "Please specify a mailing address.";
}
```
The second form of the if statement introduces an else clause that is executed when expression is false. Its syntax is:

> if 语句的第二种形式引入了 else 子句，当 expression 为 false 时将执行该子句。 它的语法是：

```js
if (expression)
    statement1
else
    statement2
```
This form of the statement executes statement1 if expression is truthy and executes statement2 if expression is falsy. For example:

> 如果 expression 为真，则此语句形式执行 statement1；如果 expression 为 false，则执行 statement2。 例如：

```js
if (n === 1)
    console.log("You have 1 new message.");
else
    console.log(`You have ${n} new messages.`);
```
When you have nested if statements with else clauses, some caution is required to ensure that the else clause goes with the appropriate if statement. Consider the following lines:

> 当将带有 if 子句的 if 语句嵌套时，需要格外小心，以确保 else 子句与适当的 if 语句一起使用。考虑以下几行：

```js
i = j = 1;
k = 2;
if (i === j)
    if (j === k)
        console.log("i equals k");
else
    console.log("i doesn't equal j");    // WRONG!!
```
In this example, the inner if statement forms the single statement allowed by the syntax of the outer if statement. Unfortunately, it is not clear (except from the hint given by the indentation) which if the else goes with. And in this example, the indentation is wrong, because a JavaScript interpreter actually interprets the previous example as:

> 在此示例中，内部 if 语句形成外部 if 语句的语法允许的单个语句。不幸的是，不清楚（除非缩进提示）else 接连在哪个 if 后。 在此示例中，缩进是错误的，因为 JavaScript 解释器实际上将前面的示例解释为：

```js
if (i === j) {
    if (j === k)
        console.log("i equals k");
    else
        console.log("i doesn't equal j");    // OOPS!
}
```
The rule in JavaScript (as in most programming languages) is that by default an else clause is part of the nearest if statement. To make this example less ambiguous and easier to read, understand, maintain, and debug, you should use curly braces:

> JavaScript 中的规则（与大多数编程语言一样）在默认情况下，else 子句是最接近的 if 语句的一部分。为了使此示例不太含糊且易于阅读、理解、维护和调试，应使用花括号： 

```js
if (i === j) {
    if (j === k) {
        console.log("i equals k");
    }
} else {  // What a difference the location of a curly brace makes!
    console.log("i doesn't equal j");
}
```
Many programmers make a habit of enclosing the bodies of if and else statements (as well as other compound statements, such as while loops) within curly braces, even when the body consists of only a single statement. Doing so consistently can prevent the sort of problem just shown, and I advise you to adopt this practice. In this printed book, I place a premium on keeping example code vertically compact, and I do not always follow my own advice on this matter.

> 许多程序员习惯将 if 和 else 语句（以及其他复合语句，例如 while 循环）的主体括在花括号内，即使主体仅由一个语句组成也是如此。始终如一地这样做可以防止出现刚才显示的问题，我建议采用这种做法。在这本书中，我非常重视保持示例代码在垂直方向上的紧凑性，并且在此问题上，我并不总是遵循自己的建议。

### 5.3.2 else if
The if/else statement evaluates an expression and executes one of two pieces of code, depending on the outcome. But what about when you need to execute one of many pieces of code? One way to do this is with an else if statement. else if is not really a JavaScript statement, but simply a frequently used programming idiom that results when repeated if/else statements are used:

> if/else 语句根据结果评估表达式并执行两段代码之一。但是，当需要执行许多代码之一时，该怎么办呢？一种方法是使用 else if 语句。else if 并不是真正的 JavaScript 语句，而只是一个经常使用的编程习惯用法，当使用重复的 if/else 语句时会产生该习惯用法：

```js
if (n === 1) {
    // Execute code block #1
} else if (n === 2) {
    // Execute code block #2
} else if (n === 3) {
    // Execute code block #3
} else {
    // If all else fails, execute block #4
}
```
There is nothing special about this code. It is just a series of if statements, where each following if is part of the else clause of the previous statement. Using the else if idiom is preferable to, and more legible than, writing these statements out in their syntactically equivalent, fully nested form:

> 此代码没有什么特别的。 它只是一系列的 if 语句，其后的每个 if 都是前一条语句的 else 子句的一部分。 使用 else if 惯用语比以语法上等效的完全嵌套形式写出这些语句更好，更易读：

```js
if (n === 1) {
    // Execute code block #1
}
else {
    if (n === 2) {
        // Execute code block #2
    }
    else {
        if (n === 3) {
            // Execute code block #3
        }
        else {
            // If all else fails, execute block #4
        }
    }
}
```
### 5.3.3 switch
An if statement causes a branch in the flow of a program’s execution, and you can use the else if idiom to perform a multiway branch. This is not the best solution, however, when all of the branches depend on the value of the same expression. In this case, it is wasteful to repeatedly evaluate that expression in multiple if statements.

> if 语句会导致程序执行流程中的分支，可以使用 else if 惯用法来执行多路分支。但是，当所有分支都依赖于同一表达式的值时，这不是最佳解决方案。在这种情况下，在多个 if 语句中重复评估该表达式是浪费性能的。

The switch statement handles exactly this situation. The switch keyword is followed by an expression in parentheses and a block of code in curly braces:

> switch 语句完全可以处理这种情况。switch 关键字后跟一个括号中的表达式和一个花括号中的代码块：

```js
switch(expression) {
    statements
}
```
However, the full syntax of a switch statement is more complex than this. Various locations in the block of code are labeled with the case keyword followed by an expression and a colon. When a switch executes, it computes the value of expression and then looks for a case label whose expression evaluates to the same value (where sameness is determined by the === operator). If it finds one, it starts executing the block of code at the statement labeled by the case. If it does not find a case with a matching value, it looks for a statement labeled default:. If there is no default: label, the switch statement skips the block of code altogether.

> 但是，switch 语句的完整语法比这更复杂。代码块中的各个位置都用 case 关键字标记，后跟一个表达式和一个冒号。switch 执行时，它将计算表达式的值，然后查找其表达式计算为相同值（其中相同性由 === 运算符确定）的case标签。如果找到一个，它将开始在由 case 标记的语句处执行代码块。如果找不到与值匹配的个案，则查找标记为 default: 的语句。 如果没有 default: 标签，则 switch 语句将完全跳过该代码块。

switch is a confusing statement to explain; its operation becomes much clearer with an example. The following switch statement is equivalent to the repeated if/else statements shown in the previous section:

> switch 是一个令人困惑的陈述，难以解释；举个例子，它的操作变得更加清晰。以下 switch 语句等效于上一节中重复 if/else 语句：

```js
switch(n) {
case 1:                        // Start here if n === 1
    // Execute code block #1.
    break;                     // Stop here
case 2:                        // Start here if n === 2
    // Execute code block #2.
    break;                     // Stop here
case 3:                        // Start here if n === 3
    // Execute code block #3.
    break;                     // Stop here
default:                       // If all else fails...
    // Execute code block #4.
    break;                     // Stop here
}
```
Note the break keyword used at the end of each case in this code. The break statement, described later in this chapter, causes the interpreter to jump to the end (or “break out”) of the switch statement and continue with the statement that follows it. The case clauses in a switch statement specify only the starting point of the desired code; they do not specify any ending point. In the absence of break statements, a switch statement begins executing its block of code at the case label that matches the value of its expression and continues executing statements until it reaches the end of the block. On rare occasions, it is useful to write code like this that “falls through” from one case label to the next, but 99% of the time you should be careful to end every case with a break statement. (When using switch inside a function, however, you may use a return statement instead of a break statement. Both serve to terminate the switch statement and prevent execution from falling through to the next case.)

> 请注意此代码中每种情况结尾处使用的 break 关键字。在本章后面介绍的 break 语句使解释器跳到 switch 语句的末尾（或“中断”），并继续其后的语句。 switch 语句中的 case 子句仅指定所需代码的起点；他们没有指定任何终点。在没有 break 语句的情况下，switch 语句在与其表达式值匹配的 case 标签处开始执行其代码块，并继续执行语句，直到到达该块的末尾为止。在极少数情况下，编写这样的代码（从一个案例标签到另一个案例）“贯穿”是很有用的，但是在 99％ 的使用中，应小心以 break 语句结束每个案例。（但是，在函数内部使用 switch 时，可以使用 return 语句而不是 break 语句。两者都可用于终止 switch 语句并防止执行陷入下一种情况。）

Here is a more realistic example of the switch statement; it converts a value to a string in a way that depends on the type of the value:

> 这是 switch 语句的一个更实际的示例；它将值转换为字符串的方式取决于值的类型：

```js
function convert(x) {
    switch(typeof x) {
    case "number":            // Convert the number to a hexadecimal integer
        return x.toString(16);
    case "string":            // Return the string enclosed in quotes
        return '"' + x + '"';
    default:                  // Convert any other type in the usual way
        return String(x);
    }
}
```
Note that in the two previous examples, the case keywords are followed by number and string literals, respectively. This is how the switch statement is most often used in practice, but note that the ECMAScript standard allows each case to be followed by an arbitrary expression.

> 请注意，在前面的两个示例中，case 关键字后面分别跟有数字和字符串文字。这是实践中最经常使用 switch 语句的方式，但是请注意，ECMAScript 标准允许每种情况后面都可以有一个任意表达式。

The switch statement first evaluates the expression that follows the switch keyword and then evaluates the case expressions, in the order in which they appear, until it finds a value that matches.1 The matching case is determined using the === identity operator, not the == equality operator, so the expressions must match without any type conversion.

> switch 语句首先评估 switch 关键字后面的表达式，然后按它们出现的顺序评估 case 表达式，直到找到匹配的值。[^1] 匹配的 case 是使用 === 恒等运算符确定的，而不是 == 相等运算符，因此表达式必须匹配，且不进行任何类型转换。

Because not all of the case expressions are evaluated each time the switch statement is executed, you should avoid using case expressions that contain side effects such as function calls or assignments. The safest course is simply to limit your case expressions to constant expressions.

> 由于并非每次执行 switch 语句时都会评估所有的 case 表达式，因此应避免使用包含副作用的 case 表达式，例如函数调用或赋值。最安全的方法只是将 case 表达式限制为常量表达式。

As explained earlier, if none of the case expressions match the switch expression, the switch statement begins executing its body at the statement labeled default:. If there is no default: label, the switch statement skips its body altogether. Note that in the examples shown, the default: label appears at the end of the switch body, following all the case labels. This is a logical and common place for it, but it can actually appear anywhere within the body of the statement.

> 如前所述，如果所有 case 表达式都不与 switch 表达式匹配，则 switch 语句将在标有 default: 的语句处开始执行其主体。如果没有 default: 标签，则 switch语句将完全跳过其主体。请注意，在所示示例中，default: 标签出现在 switch 主体的末尾，紧随所有案例标签之后。这是一个逻辑上通用的地方，但实际上它可以出现在语句主体内的任何位置。

## 5.4 Loops
To understand conditional statements, we imagined the JavaScript interpreter following a branching path through your source code. The looping statements are those that bend that path back upon itself to repeat portions of your code. JavaScript has five looping statements: while, do/while, for, for/of (and its for/await variant), and for/in. The following subsections explain each in turn. One common use for loops is to iterate over the elements of an array. §7.6 discusses this kind of loop in detail and covers special looping methods defined by the Array class.

> 为了理解条件语句，我们假设 JavaScript 解释器遵循源代码中的分支路径。循环语句是那些使该路径重新弯曲以重复代码部分的语句。JavaScript 有五个循环语句：while、do/while、for、for/of（及其 for/await 变体）和 for/in。以下小节依次解释。循环的一种常见用法是遍历数组的元素。§7.6 详细讨论了这种循环，并涵盖了 Array 类定义的特殊循环方法。

### 5.4.1 while
Just as the if statement is JavaScript’s basic conditional, the while statement is JavaScript’s basic loop. It has the following syntax:

> 正如 if 语句是 JavaScript 的基本条件一样，while 语句也是 JavaScript 的基本循环。它具有以下语法：

```js
while (expression)
    statement
```
To execute a while statement, the interpreter first evaluates expression. If the value of the expression is falsy, then the interpreter skips over the statement that serves as the loop body and moves on to the next statement in the program. If, on the other hand, the expression is truthy, the interpreter executes the statement and repeats, jumping back to the top of the loop and evaluating expression again. Another way to say this is that the interpreter executes statement repeatedly while the expression is truthy. Note that you can create an infinite loop with the syntax while(true).

> 要执行 while 语句，解释器首先对表达式求值。如果表达式的值是假值，则解释器将跳过用作循环主体的语句，然后继续执行程序中的下一条语句。另一方面，如果表达式是真值，则解释器将执行该语句并重复，跳回到循环的顶部并再次评估表达式。另一种说法是，解释器在表达式为真时重复执行语句。请注意，可以使用 while(true) 语法创建无限循环。

Usually, you do not want JavaScript to perform exactly the same operation over and over again. In almost every loop, one or more variables change with each iteration of the loop. Since the variables change, the actions performed by executing statement may differ each time through the loop. Furthermore, if the changing variable or variables are involved in expression, the value of the expression may be different each time through the loop. This is important; otherwise, an expression that starts off truthy would never change, and the loop would never end! Here is an example of a while loop that prints the numbers from 0 to 9:

> 通常，不希望 JavaScript 一次又一次地执行完全相同的操作。在几乎每个循环中，一个或多个变量随循环的每次迭代而变化。由于变量会发生变化，因此每次循环执行时，执行语句所执行的动作可能会有所不同。此外，如果表达式中包含一个或多个变化的变量，则每次循环时表达式的值可能会有所不同。这个很重要；否则，以 true 开始的表达式将永远不会改变，循环永远不会结束！这是一个while循环的示例，该循环打印从 0 到 9 的数字：

```js
let count = 0;
while(count < 10) {
    console.log(count);
    count++;
}
```
As you can see, the variable count starts off at 0 and is incremented each time the body of the loop runs. Once the loop has executed 10 times, the expression becomes false (i.e., the variable count is no longer less than 10), the while statement finishes, and the interpreter can move on to the next statement in the program. Many loops have a counter variable like count. The variable names i, j, and k are commonly used as loop counters, though you should use more descriptive names if it makes your code easier to understand.

> 如你所见，变量计数从 0 开始，并在每次循环主体运行时递增。循环执行 10 次后，表达式变为 false（即变量计数不小于 10），while 语句结束，解释器可以继续执行程序中的下一个语句。许多循环都有一个计数器变量，例如 count。变量名 i、j 和 k 通常用作循环计数器，但是如果可以使代码更易于理解，则应使用更具描述性的名称。

### 5.4.2 do/while
The do/while loop is like a while loop, except that the loop expression is tested at the bottom of the loop rather than at the top. This means that the body of the loop is always executed at least once. The syntax is:

> do/while 循环类似于 while 循环，除了循环表达式是在循环的底部而不是顶部进行测试的。这意味着循环的主体始终至少执行一次。语法为：

```js
do
    statement
while (expression);
```
The do/while loop is less commonly used than its while cousin—in practice, it is somewhat uncommon to be certain that you want a loop to execute at least once. Here’s an example of a do/while loop:

> do/while 循环不如 while 常用——在实践中，确定要至少执行一次循环在某种程度上并不常见。这是 do/while 循环的示例：

```js
function printArray(a) {
    let len = a.length, i = 0;
    if (len === 0) {
        console.log("Empty Array");
    } else {
        do {
            console.log(a[i]);
        } while(++i < len);
    }
}
```
There are a couple of syntactic differences between the do/while loop and the ordinary while loop. First, the do loop requires both the do keyword (to mark the beginning of the loop) and the while keyword (to mark the end and introduce the loop condition). Also, the do loop must always be terminated with a semicolon. The while loop doesn’t need a semicolon if the loop body is enclosed in curly braces.

> do/while 循环和普通的 while 循环之间在语法上有一些区别。首先，do 循环需要同时使用do关键字（以标记循环的开始）和while关键字（以标记结束并引入循环条件）。 另外，do 循环必须始终以分号终止。如果循环主体用花括号括起来，则 while 循环不需要分号。

### 5.4.3 for
The for statement provides a looping construct that is often more convenient than the while statement. The for statement simplifies loops that follow a common pattern. Most loops have a counter variable of some kind. This variable is initialized before the loop starts and is tested before each iteration of the loop. Finally, the counter variable is incremented or otherwise updated at the end of the loop body, just before the variable is tested again. In this kind of loop, the initialization, the test, and the update are the three crucial manipulations of a loop variable. The for statement encodes each of these three manipulations as an expression and makes those expressions an explicit part of the loop syntax:

> for 语句提供了一个循环构造，通常比 while 语句更方便。 for 语句简化了遵循通用模式的循环。大多数循环都有某种计数器变量。在循环开始之前初始化此变量，并在每次循环迭代之前对其进行测试。最后，在再次测试变量之前，计数器变量在循环主体的末尾增加或更新。在这种循环中，初始化、测试和更新是循环变量的三个关键操作。for 语句将这三个操作中的每一个都编码为一个表达式，并使这些表达式成为循环语法的显式部分：

```js
for(initialize ; test ; increment)
    statement
```
initialize, test, and increment are three expressions (separated by semicolons) that are responsible for initializing, testing, and incrementing the loop variable. Putting them all in the first line of the loop makes it easy to understand what a for loop is doing and prevents mistakes such as forgetting to initialize or increment the loop variable.

> 初始化、测试和递增三个表达式（用分号分隔）。将它们全部放入循环的第一行可轻松了解 for 循环的作用，并防止诸如忘记初始化或增加循环变量之类的错误。

The simplest way to explain how a for loop works is to show the equivalent while loop:2

> 解释 for 循环如何工作的最简单方法是显示等效的while循环：[^2]

```js
initialize;
while(test) {
    statement
    increment;
}
```
In other words, the initialize expression is evaluated once, before the loop begins. To be useful, this expression must have side effects (usually an assignment). JavaScript also allows initialize to be a variable declaration statement so that you can declare and initialize a loop counter at the same time. The test expression is evaluated before each iteration and controls whether the body of the loop is executed. If test evaluates to a truthy value, the statement that is the body of the loop is executed. Finally, the increment expression is evaluated. Again, this must be an expression with side effects in order to be useful. Generally, it is either an assignment expression, or it uses the ++ or -- operators.

> 换句话说，在循环开始之前，对初始化表达式进行一次求值。该表达式必须具有副作用（通常是赋值）。JavaScript 还允许将初始化用作变量声明语句，以便可以同时声明和初始化循环计数器。测试表达式在每次迭代之前进行评估，并控制是否执行循环主体。如果测试评估为真值，则执行作为循环主体的语句。最后，计算增量表达式。同样，该表达式必须是具有副作用的表达式才有效。通常，它可以是赋值表达式，也可以使用 ++ 或 -- 运算符。

We can print the numbers from 0 to 9 with a for loop like the following. Contrast it with the equivalent while loop shown in the previous section:

> 我们可以使用如下所示的 for 循环打印 0 到 9 之间的数字。 将其与上一节中显示的等效 while 循环进行对比：

```js
for(let count = 0; count < 10; count++) {
    console.log(count);
}
```
Loops can become a lot more complex than this simple example, of course, and sometimes multiple variables change with each iteration of the loop. This situation is the only place that the comma operator is commonly used in JavaScript; it provides a way to combine multiple initialization and increment expressions into a single expression suitable for use in a for loop:

> 当然，循环比这个简单的例子要复杂得多，有时循环的每次迭代都会改变多个变量。这种情况是在 JavaScript 中唯一使用逗号运算符的地方。它提供了一种将多个初始化和增量表达式组合成适合在 for 循环中使用的单个表达式的方法：

```js
let i, j, sum = 0;
for(i = 0, j = 10 ; i < 10 ; i++, j--) {
    sum += i * j;
}
```
In all our loop examples so far, the loop variable has been numeric. This is quite common but is not necessary. The following code uses a for loop to traverse a linked list data structure and return the last object in the list (i.e., the first object that does not have a next property):

> 到目前为止，在我们所有的循环示例中，循环变量都是数字。这是很常见的，但不是必需的。以下代码使用 for 循环遍历链接列表数据结构并返回列表中的最后一个对象（即第一个不具有 next 属性的对象）：

```js
function tail(o) {                          // Return the tail of linked list o
    for(; o.next; o = o.next) /* empty */ ; // Traverse while o.next is truthy
    return o;
}
```
Note that this code has no initialize expression. Any of the three expressions may be omitted from a for loop, but the two semicolons are required. If you omit the test expression, the loop repeats forever, and for(;;) is another way of writing an infinite loop, like while(true).

> 请注意，此代码没有初始化表达式。for 循环可以省略三个表达式中的任何一个，但是需要两个分号。如果省略测试表达式，则循环将永远重复，而 for（;;）是编写无限循环的另一种方式，例如 while(true)。

### 5.4.4 for/of
ES6 defines a new loop statement: for/of. This new kind of loop uses the for keyword but is a completely different kind of loop than the regular for loop. (It is also completely different than the older for/in loop that we’ll describe in §5.4.5.)

> ES6 定义了一个新的循环语句：for/of。这种新的循环使用 for 关键字，但是与常规的 for 循环完全不同。（它也与我们在 §5.4.5 中描述的较早的 for/in 循环完全不同。）

The for/of loop works with iterable objects. We’ll explain exactly what it means for an object to be iterable in Chapter 12, but for this chapter, it is enough to know that arrays, strings, sets, and maps are iterable: they represent a sequence or set of elements that you can loop or iterate through using a for/of loop.

> for/of 循环适用于可迭代对象。我们将在第 12 章中确切解释对象可迭代的含义，但是对于本章而言，知道数组、字符串、set 和 map 是可迭代的足以：它们代表了所需要可以使用 for/of 循环的序列或元素集合。

Here, for example, is how we can use for/of to loop through the elements of an array of numbers and compute their sum:

> 例如，这里是我们如何使用 for/of 遍历数字数组的元素并计算它们的总和的方法：

```js
let data = [1, 2, 3, 4, 5, 6, 7, 8, 9], sum = 0;
for(let element of data) {
    sum += element;
}
sum       // => 45
```
Superficially, the syntax looks like a regular for loop: the for keyword is followed by parentheses that contain details about what the loop should do. In this case, the parentheses contain a variable declaration (or, for variables that have already been declared, simply the name of the variable) followed by the of keyword and an expression that evaluates to an iterable object, like the data array in this case. As with all loops, the body of a for/of loop follows the parentheses, typically within curly braces.

> 从表面上看，语法看起来像是常规的 for 循环：for 关键字后面是括号，其中包含有关循环应执行的操作的详细信息。在这种情况下，括号中包含一个变量声明（或者对于已经声明的变量，仅是变量的名称），后跟 of 关键字和一个表达式，该表达式的结果为可迭代对象，例如本例中的数据数组。与所有循环一样，for/of 循环的主体跟随括号后，通常在花括号内。

In the code just shown, the loop body runs once for each element of the data array. Before each execution of the loop body, the next element of the array is assigned to the element variable. Array elements are iterated in order from first to last.

> 在刚刚显示的代码中，循环主体为数据数组的每个元素运行一次。在每次执行循环主体之前，将数组的下一个元素分配给 element 变量。数组元素从第一个到最后一个顺序进行迭代。

Arrays are iterated “live”—changes made during the iteration may affect the outcome of the iteration. If we modify the preceding code by adding the line data.push(sum); inside the loop body, then we create an infinite loop because the iteration can never reach the last element of the array.

> 数组是“实时”迭代的，在迭代过程中进行的更改可能会影响迭代的结果。如果我们通过添加行 `data.push(sum);` 在循环体内修改前面的代码，我们则创建一个无限循环，因为迭代永远无法到达数组的最后一个元素。

#### FOR/OF WITH OBJECTS

Objects are not (by default) iterable. Attempting to use for/of on a regular object throws a TypeError at runtime:

> 对象是不可迭代的（默认情况下）。尝试在常规对象上使用 for/of 会在运行时引发 TypeError：

```js
let o = { x: 1, y: 2, z: 3 };
for(let element of o) { // Throws TypeError because o is not iterable
    console.log(element);
}
```
If you want to iterate through the properties of an object, you can use the for/in loop (introduced in §5.4.5), or use for/of with the Object.keys() method:

> 如果要遍历对象的属性，则可以使用 for/in 循环（在 §5.4.5 中介绍），或通过 Object.keys() 方法使用 for/of：

```js
let o = { x: 1, y: 2, z: 3 };
let keys = "";
for(let k of Object.keys(o)) {
    keys += k;
}
keys  // => "xyz"
```
This works because Object.keys() returns an array of property names for an object, and arrays are iterable with for/of. Note also that this iteration of the keys of an object is not live as the array example above was—changes to the object o made in the loop body will have no effect on the iteration. If you don’t care about the keys of an object, you can also iterate through their corresponding values like this:

> 之所以可行，是因为 Object.keys() 返回一个对象的属性名称数组，并且该数组可以使用 for/of 进行迭代。还要注意，对象的键的这种迭代不像上面的数组示例那样有效——在循环主体中对对象 o 所做的更改将对该迭代没有影响。 如果您不关心对象的键，也可以像下面这样遍历它们的对应值：

```js
let sum = 0;
for(let v of Object.values(o)) {
    sum += v;
}
sum // => 6
```
And if you are interested in both the keys and the values of an object’s properties, you can use for/of with Object.entries() and destructuring assignment:

> 而且，如果对对象属性的键和值都感兴趣，则可以将 Object.entries() 与 for/of 一起使用，并销毁赋值：

```js
let pairs = "";
for(let [k, v] of Object.entries(o)) {
    pairs += k + v;
}
pairs  // => "x1y2z3"
```
Object.entries() returns an array of arrays, where each inner array represents a key/value pair for one property of the object. We use destructuring assignment in this code example to unpack those inner arrays into two individual variables.

> Object.entries() 返回一个数组的数组，其中每个内部数组代表对象一个属性的键 / 值对。在此代码示例中，我们使用解构将这些内部数组拆成两个单独的变量。

#### FOR/OF WITH STRINGS

Strings are iterable character-by-character in ES6:

> 在 ES6 中，字符串是一个一个字符可迭代对象：

```js
let frequency = {};
for(let letter of "mississippi") {
    if (frequency[letter]) {
        frequency[letter]++;
    } else {
        frequency[letter] = 1;
    }
}
frequency   // => {m: 1, i: 4, s: 4, p: 2}
```
Note that strings are iterated by Unicode codepoint, not by UTF-16 character. The string “I ❤ ” has a .length of 5 (because the two emoji characters each require two UTF-16 characters to represent). But if you iterate that string with for/of, the loop body will run three times, once for each of the three code points “I”, “❤”, and “.”

> 请注意，字符串是通过 Unicode 麻点而不是 UTF-16 字符进行迭代的。字符串“ I❤”的长度为 5（因为两个表情符号字符每个都需要两个 UTF-16 字符来表示）。但是，如果使用 for/of 迭代该字符串，则循环主体将运行三次，对于三个麻点“ I”，“❤”和“.”中的每一个都运行一次。

#### FOR/OF WITH SET AND MAP

The built-in ES6 Set and Map classes are iterable. When you iterate a Set with for/of, the loop body runs once for each element of the set. You could use code like this to print the unique words in a string of text:

> ES6 内置的 Set 和 Map 类是可迭代的。当使用 for/of 迭代 Set 时，循环主体对 set 的每个元素运行一次。可以使用如下代码在文本字符串中打印出唯一的单词：

```js
let text = "Na na na na na na na na Batman!";
let wordSet = new Set(text.split(" "));
let unique = [];
for(let word of wordSet) {
    unique.push(word);
}
unique // => ["Na", "na", "Batman!"]
```
Maps are an interesting case because the iterator for a Map object does not iterate the Map keys, or the Map values, but key/value pairs. Each time through the iteration, the iterator returns an array whose first element is a key and whose second element is the corresponding value. Given a Map m, you could iterate and destructure its key/value pairs like this:

> Map 是一种有趣的情况，因为 Map 对象的迭代器不会迭代 Map 键或 Map 值，而是键 / 值对。每次迭代时，迭代器都会返回一个数组，该数组的第一个元素是键，而第二个元素是对应的值。给定一个 Map m，可以像这样迭代和解构其键 / 值对：

```js
let m = new Map([[1, "one"]]);
for(let [key, value] of m) {
    key    // => 1
    value  // => "one"
}
```
#### ASYNCHRONOUS ITERATION WITH FOR/AWAIT

ES2018 introduces a new kind of iterator, known as an asynchronous iterator, and a variant on the for/of loop, known as the for/await loop that works with asynchronous iterators.

> ES2018 引入了一种新型的迭代器，称为异步迭代器，以及 for/of 循环的一种变体，即与异步迭代器一起使用的 for/await 循环。

You’ll need to read Chapters 12 and 13 in order to understand the for/await loop, but here is how it looks in code:

> 需要阅读第 12 章和第 13 章，才能了解 for/await 循环，这里展示一下它的代码：

```js
// Read chunks from an asynchronously iterable stream and print them out
async function printStream(stream) {
    for await (let chunk of stream) {
        console.log(chunk);
    }
}
```
### 5.4.5 for/in
A for/in loop looks a lot like a for/of loop, with the of keyword changed to in. While a for/of loop requires an iterable object after the of, a for/in loop works with any object after the in. The for/of loop is new in ES6, but for/in has been part of JavaScript since the very beginning (which is why it has the more natural sounding syntax).

> for/in 循环看起来很像 for/of 循环，将 of 关键字更改为 in。for/of 循环在 of 之后需要可迭代的对象，而 for/in 循环则在 in 之后可用于任何对象。for/of 循环是 ES6 中的新功能，但是 for/in 从一开始就已经是 JavaScript 的一部分（这就是为什么它具有更自然的发音语法）。

The for/in statement loops through the property names of a specified object. The syntax looks like this:

> for/in 语句循环遍历指定对象的属性名称。语法如下所示：

```js
for (variable in object)
    statement
```
variable typically names a variable, but it may be a variable declaration or anything suitable as the left-hand side of an assignment expression. object is an expression that evaluates to an object. As usual, statement is the statement or statement block that serves as the body of the loop.

> 变量通常命名为变量，但它可以是变量声明或任何适合作为赋值表达式左侧的内容。object 是一个计算结果为对象的表达式。像往常一样，statement 是用作循环正文的语句或语句块。

And you might use a for/in loop like this:

> 可能会使用如下所示的 for/in 循环：

```js
for(let p in o) {      // Assign property names of o to variable p
    console.log(o[p]); // Print the value of each property
}
```
To execute a for/in statement, the JavaScript interpreter first evaluates the object expression. If it evaluates to null or undefined, the interpreter skips the loop and moves on to the next statement. The interpreter now executes the body of the loop once for each enumerable property of the object. Before each iteration, however, the interpreter evaluates the variable expression and assigns the name of the property (a string value) to it.

> 为了执行 for/in 语句，JavaScript 解释器首先评估对象表达式。如果评估结果为 null 或未定义，则解释器将跳过循环并继续执行下一条语句。现在，解释器对对象的每个可枚举属性执行一次循环主体。但是，在每次迭代之前，解释器都会对变量表达式求值，并为其分配属性名称（字符串值）。

Note that the variable in the for/in loop may be an arbitrary expression, as long as it evaluates to something suitable for the left side of an assignment. This expression is evaluated each time through the loop, which means that it may evaluate differently each time. For example, you can use code like the following to copy the names of all object properties into an array:

> 请注意，for/in 循环中的变量可以是任意表达式，只要它的计算结果适合于赋值的左侧即可。每次通过循环都会对该表达式进行求值，这意味着它每次都可能会进行不同的求值。例如，可以使用以下代码将所有对象属性的名称复制到数组中：

```js
let o = { x: 1, y: 2, z: 3 };
let a = [], i = 0;
for(a[i++] in o) /* empty */;
```
JavaScript arrays are simply a specialized kind of object, and array indexes are object properties that can be enumerated with a for/in loop. For example, following the previous code with this line enumerates the array indexes 0, 1, and 2:

> JavaScript 数组只是一种特殊的对象，而数组索引是可以用 for/in 循环枚举的对象属性。例如，在前面的代码之后加上此行，将枚举数组索引 0、1 和 2：

```js
for(let i in a) console.log(i);
```
I find that a common source of bugs in my own code is the accidental use of for/in with arrays when I meant to use for/of. When working with arrays, you almost always want to use for/of instead of for/in.

> 我发现我自己的代码中常见的错误源是当我打算使用 for/of 时偶然将 for/in 与数组结合使用。使用数组时，几乎总是要使用 for/of 而不是 for/in。

The for/in loop does not actually enumerate all properties of an object. It does not enumerate properties whose names are symbols. And of the properties whose names are strings, it only loops over the enumerable properties (see §14.1). The various built-in methods defined by core JavaScript are not enumerable. All objects have a toString() method, for example, but the for/in loop does not enumerate this toString property. In addition to built-in methods, many other properties of the built-in objects are non-enumerable. All properties and methods defined by your code are enumerable, by default. (You can make them non-enumerable using techniques explained in §14.1.)

> for/in 循环实际上并未枚举对象的所有属性。它不枚举名称为符号的属性。在名称为字符串的属性中，它仅循环可枚举的属性（请参见第14.1节）。核心 JavaScript 定义的各种内置方法是无法枚举的。例如，所有对象都具有 toString() 方法，但是 for/in 循环不会枚举此 toString 属性。除了内置方法之外，内置对象的许多其他属性也是不可枚举的。 默认情况下，代码定义的所有属性和方法都是可枚举的。（可以使用 §14.1 中介绍的技术使它们不可枚举。）

Enumerable inherited properties (see §6.3.2) are also enumerated by the for/in loop. This means that if you use for/in loops and also use code that defines properties that are inherited by all objects, then your loop may not behave in the way you expect. For this reason, many programmers prefer to use a for/of loop with Object.keys() instead of a for/in loop.

> for/in 循环还枚举了可枚举的继承属性（参见 §6.3.2）。这意味着，如果使用 for/in 循环，并且还使用定义所有对象都继承的属性的代码，则的循环可能无法按照您期望的方式运行。因此，许多程序员更喜欢对 Object.keys() 使用 for/of 循环，而不是 for/in 循环。

If the body of a for/in loop deletes a property that has not yet been enumerated, that property will not be enumerated. If the body of the loop defines new properties on the object, those properties may or may not be enumerated. See §6.6.1 for more information on the order in which for/in enumerates the properties of an object.

> 如果 for/in 循环的主体删除了尚未枚举的属性，则不会枚举该属性。如果循环的主体在对象上定义了新属性，则这些属性可能会也可能不会被枚举。有关 for/in 枚举对象属性的顺序的更多信息，请参见 §6.6.1。

## 5.5 Jumps
Another category of JavaScript statements are jump statements. As the name implies, these cause the JavaScript interpreter to jump to a new location in the source code. The break statement makes the interpreter jump to the end of a loop or other statement. continue makes the interpreter skip the rest of the body of a loop and jump back to the top of a loop to begin a new iteration. JavaScript allows statements to be named, or labeled, and break and continue can identify the target loop or other statement label.

> JavaScript 语句的另一类是跳转语句。顾名思义，这些会导致 JavaScript 解释器跳至源代码中的新位置。break 语句使解释器跳到循环或其他语句的末尾。continue 使解释器跳过循环主体的其余部分，然后跳回到循环的顶部以开始新的迭代。JavaScript 允许对语句进行命名或标记，并且 break 和 continue 可以标识目标循环或其他语句标签。

The return statement makes the interpreter jump from a function invocation back to the code that invoked it and also supplies the value for the invocation. The throw statement is a kind of interim return from a generator function. The throw statement raises, or throws, an exception and is designed to work with the try/catch/finally statement, which establishes a block of exception-handling code. This is a complicated kind of jump statement: when an exception is thrown, the interpreter jumps to the nearest enclosing exception handler, which may be in the same function or up the call stack in an invoking function.

> return 语句使解释器从函数调用跳回到调用它的代码，并提供该调用的值。throw 语句是生成器函数的一种临时返回。throw 语句引发或抛出异常，并设计为与 try/catch/finally 语句一起使用，该语句建立一个异常处理代码块。这是一种复杂的跳转语句：抛出异常时，解释器将跳转到最近的封闭异常处理程序，该处理程序可以在同一函数中，也可以在调用函数中的调用堆栈中向上移动。

Details about each of these jump statements are in the sections that follow.

> 有关这些跳转语句的详细信息，请参见以下各节。

### 5.5.1 Labeled Statements
Any statement may be labeled by preceding it with an identifier and a colon:

> 任何语句都可以在其前面加上标识符和冒号来标记：

identifier: statement

> 标识符: 语句

By labeling a statement, you give it a name that you can use to refer to it elsewhere in your program. You can label any statement, although it is only useful to label statements that have bodies, such as loops and conditionals. By giving a loop a name, you can use break and continue statements inside the body of the loop to exit the loop or to jump directly to the top of the loop to begin the next iteration. break and continue are the only JavaScript statements that use statement labels; they are covered in the following subsections. Here is an example of a labeled while loop and a continue statement that uses the label.

> 通过给语句加标签，可以为它指定一个名称，可以使用该名称在程序的其他位置引用它。可以标记任何语句，尽管只有于标记具有主体（例如循环和条件）的语句才有用。通过给循环命名，可以在循环体内使用 break 和 continue 语句退出循环或直接跳转到循环顶部以开始下一个迭代。break 和 continue 是唯一使用语句标签的 JavaScript 语句；它们在以下小节中介绍。这是一个带有标签的 while 循环和一个使用该标签的 continue 语句的示例。

```js
mainloop: while(token !== null) {
    // Code omitted...
    continue mainloop;  // Jump to the next iteration of the named loop
    // More code omitted...
}
```
The identifier you use to label a statement can be any legal JavaScript identifier that is not a reserved word. The namespace for labels is different than the namespace for variables and functions, so you can use the same identifier as a statement label and as a variable or function name. Statement labels are defined only within the statement to which they apply (and within its substatements, of course). A statement may not have the same label as a statement that contains it, but two statements may have the same label as long as neither one is nested within the other. Labeled statements may themselves be labeled. Effectively, this means that any statement may have multiple labels.

> 用于标记语句的标识符可以是非保留字的任何合法 JavaScript 标识符。标签的命名空间与变量和函数的命名空间不同，因此可以将相同的标识符用作语句标签以及变量或函数名称。语句标签仅在它们适用的语句内定义（当然，在其子语句中也定义）。一条语句可能没有与包含该语句的语句相同的标签，但是两个语句都可以具有相同的标签，只要两个语句都不嵌套在另一个语句中即可。带标签的语句本身可以被标记。实际上，这意味着任何语句都可以具有多个标签。

### 5.5.2 break
The break statement, used alone, causes the innermost enclosing loop or switch statement to exit immediately. Its syntax is simple:

> 单独使用 break 语句会使最里面的循环或 switch 语句立即退出。它的语法很简单：

```js
break;
```
Because it causes a loop or switch to exit, this form of the break statement is legal only if it appears inside one of these statements.

> 因为它导致循环或开关退出，所以这种形式的break语句仅当出现在这些语句之一内时才是合法的。

You’ve already seen examples of the break statement within a switch statement. In loops, it is typically used to exit prematurely when, for whatever reason, there is no longer any need to complete the loop. When a loop has complex termination conditions, it is often easier to implement some of these conditions with break statements rather than trying to express them all in a single loop expression. The following code searches the elements of an array for a particular value. The loop terminates in the normal way when it reaches the end of the array; it terminates with a break statement if it finds what it is looking for in the array:

> 您已经在 switch 语句中看到了 break 语句的示例。在循环中，通常由于某种原因而不再需要完成循环时，它会过早退出。当循环具有复杂的终止条件时，通常使用 break 语句更容易实现其中一些条件，而不是尝试在单个循环表达式中全部表达它们。以下代码在数组的元素中搜索特定值。当循环到达数组末尾时，循环以通常的方式终止。如果在数组中找到要查找的内容，则以 break 语句终止：

```js
for(let i = 0; i < a.length; i++) {
    if (a[i] === target) break;
}
```
JavaScript also allows the break keyword to be followed by a statement label (just the identifier, with no colon):

> JavaScript 还允许 break 关键字后跟一个语句标签（只是标识符，没有冒号）：

```
break labelname;
```
When break is used with a label, it jumps to the end of, or terminates, the enclosing statement that has the specified label. It is a syntax error to use break in this form if there is no enclosing statement with the specified label. With this form of the break statement, the named statement need not be a loop or switch: break can “break out of” any enclosing statement. This statement can even be a statement block grouped within curly braces for the sole purpose of naming the block with a label.

> 当 break 与标签一起使用时，它跳转到具有指定标签的封闭语句的末尾或终止。如果没有带有指定标签的封闭语句，则使用这种形式的 break 是语法错误。 使用 break 语句的这种形式，命名的语句不必是循环或 switch：break 可以“跳出”任何封闭的语句。该语句甚至可以是用大括号括起来的语句块，其唯一目的是用标签命名该块。

A newline is not allowed between the break keyword and the label name. This is a result of JavaScript’s automatic insertion of omitted semicolons: if you put a line terminator between the break keyword and the label that follows, JavaScript assumes you meant to use the simple, unlabeled form of the statement and treats the line terminator as a semicolon. (See §2.6.)

> 在 break 关键字和标签名之间不允许使用换行符。 这是 JavaScript 自动插入省略的分号的结果：如果在 break 关键字和后面的标签之间放置了行终止符，则 JavaScript 会假定您打算使用语句的简单、无标签形式并将行终止符视为分号 。（请参见 §2.6）

You need the labeled form of the break statement when you want to break out of a statement that is not the nearest enclosing loop or a switch. The following code demonstrates:

> 当想脱离不是最近的封闭循环或 switch 的语句时，需要使用 break 语句的标签形式。以下代码演示：

```js
let matrix = getData();  // Get a 2D array of numbers from somewhere
// Now sum all the numbers in the matrix.
let sum = 0, success = false;
// Start with a labeled statement that we can break out of if errors occur
computeSum: if (matrix) {
    for(let x = 0; x < matrix.length; x++) {
        let row = matrix[x];
        if (!row) break computeSum;
        for(let y = 0; y < row.length; y++) {
            let cell = row[y];
            if (isNaN(cell)) break computeSum;
            sum += cell;
        }
    }
    success = true;
}
// The break statements jump here. If we arrive here with success == false
// then there was something wrong with the matrix we were given.
// Otherwise, sum contains the sum of all cells of the matrix.
```
Finally, note that a break statement, with or without a label, can not transfer control across function boundaries. You cannot label a function definition statement, for example, and then use that label inside the function.

> 最后，请注意，带有或不带有标签的 break 语句无法跨函数边界转移控制权。例如，不能标记函数定义语句，然后在函数内部使用该标记。

### 5.5.3 continue
The continue statement is similar to the break statement. Instead of exiting a loop, however, continue restarts a loop at the next iteration. The continue statement’s syntax is just as simple as the break statement’s:

> continue 语句类似于 break 语句。但是，continue 不是退出循环，而是在重新开始循环的下一次迭代。continue 语句的语法与 break 语句的语法一样简单：

```js
continue;
```

The continue statement can also be used with a label:

> continue 语句也可以与标签一起使用：

```js
continue labelname;
```

The continue statement, in both its labeled and unlabeled forms, can be used only within the body of a loop. Using it anywhere else causes a syntax error.

> 标记和未标记形式的 continue 语句只能在循环体内使用。在其他任何地方使用它都会导致语法错误。

When the continue statement is executed, the current iteration of the enclosing loop is terminated, and the next iteration begins. This means different things for different types of loops:

> 当执行 continue 语句时，封闭循环的当前迭代将终止，并且下一个迭代开始。对于不同类型的循环，这意味着不同的事情：

In a while loop, the specified expression at the beginning of the loop is tested again, and if it’s true, the loop body is executed starting from the top.

> 在 while 循环中，将再次测试循环开始处的指定表达式，如果该表达式为 true，则循环主体将从顶部开始执行。

In a do/while loop, execution skips to the bottom of the loop, where the loop condition is tested again before restarting the loop at the top.

> 在 do/while 循环中，执行跳到循环的底部，在重新测试顶部的循环之前，先对循环条件进行测试。

In a for loop, the increment expression is evaluated, and the test expression is tested again to determine if another iteration should be done.

> 在 for 循环中，对增量表达式进行求值，然后再次对测试表达式进行测试，以确定是否应执行另一次迭代。

In a for/of or for/in loop, the loop starts over with the next iterated value or next property name being assigned to the specified variable.

> 在 for/of 或 for/in 循环中，循环从下一个迭代值或下一个属性名称分配给指定变量开始。

Note the difference in behavior of the continue statement in the while and for loops: a while loop returns directly to its condition, but a for loop first evaluates its increment expression and then returns to its condition. Earlier, we considered the behavior of the for loop in terms of an “equivalent” while loop. Because the continue statement behaves differently for these two loops, however, it is not actually possible to perfectly simulate a for loop with a while loop alone.

> 注意 while 和 for 循环中 continue 语句的行为差异：while 循环直接返回其条件，但是 for 循环首先计算其增量表达式，然后返回其条件。之前，我们以“等效” while 循环的形式考虑了 for 循环的行为。但是，由于 continue 语句在这两个循环中的行为不同，因此实际上不可能仅使用 while 循环来完美地模拟 for 循环。

The following example shows an unlabeled continue statement being used to skip the rest of the current iteration of a loop when an error occurs:

> 以下示例显示了一个未标记的 continue 语句，该语句在发生错误时用于跳过循环的当前迭代的其余部分：

```js
for(let i = 0; i < data.length; i++) {
    if (!data[i]) continue;  // Can't proceed with undefined data
    total += data[i];
}
```
Like the break statement, the continue statement can be used in its labeled form within nested loops when the loop to be restarted is not the immediately enclosing loop. Also, as with the break statement, line breaks are not allowed between the continue statement and its label name.

> 像 break 语句一样，当要重新启动的循环不是立即封闭的循环时，可以在嵌套循环内以标记形式使用 continue 语句。同样，与 break 语句一样，在 continue 语句及其标签名之间不允许换行。

### 5.5.4 return
Recall that function invocations are expressions and that all expressions have values. A return statement within a function specifies the value of invocations of that function. Here’s the syntax of the return statement:

> 回想一下，函数调用是表达式，并且所有表达式都具有值。函数内的 return 语句指定该函数的调用值。这是 return 语句的语法：

```js
return expression;
```

A return statement may appear only within the body of a function. It is a syntax error for it to appear anywhere else. When the return statement is executed, the function that contains it returns the value of expression to its caller. For example:

> return 语句可能仅出现在函数体内。它出现在其他任何地方都是语法错误。当执行 return 语句时，包含它的函数会将 expression 的值返回给其调用者。例如：

```js
function square(x) { return x*x; } // A function that has a return statement
square(2)                          // => 4
```
With no return statement, a function invocation simply executes each of the statements in the function body in turn until it reaches the end of the function and then returns to its caller. In this case, the invocation expression evaluates to undefined. The return statement often appears as the last statement in a function, but it need not be last: a function returns to its caller when a return statement is executed, even if there are other statements remaining in the function body.

> 在没有 return 语句的情况下，函数调用只是依次依次执行函数体中的每个语句，直到到达函数末尾，然后返回到其调用者。在这种情况下，调用表达式的计算结果为 undefined。return 语句通常显示为函数中的最后一条语句，但不一定要最后一条：执行 return 语句时，函数返回到其调用者，即使函数体内还有其他语句。

The return statement can also be used without an expression to make the function return undefined to its caller. For example:

> 还可以在没有表达式的情况下使用 return 语句，以使函数返回未定义给调用者。例如：

```js
function displayObject(o) {
    // Return immediately if the argument is null or undefined.
    if (!o) return;
    // Rest of function goes here...
}
```
Because of JavaScript’s automatic semicolon insertion (§2.6), you cannot include a line break between the return keyword and the expression that follows it.

> 由于 JavaScript 自动插入了分号（§2.6），因此不能在 return 关键字和其后的表达式之间包含换行符。

### 5.5.5 yield
The yield statement is much like the return statement but is used only in ES6 generator functions (see §12.3) to produce the next value in the generated sequence of values without actually returning:

> yield 语句与 return 语句非常相似，但仅在 ES6 生成器函数（请参阅 §12.3）中使用，以在所生成的值序列中生成下一个值，而无需实际返回：

```js
// A generator function that yields a range of integers
function* range(from, to) {
    for(let i = from; i <= to; i++) {
        yield i;
    }
}
```
In order to understand yield, you must understand iterators and generators, which will not be covered until Chapter 12. yield is included here for completeness, however. (Technically, though, yield is an operator rather than a statement, as explained in §12.4.2.)

> 为了了解 yield，必须了解迭代器和生成器，但是为了完整起见，直到第 12 章都不会涉及。（但是，从技术上讲，yield 是运算符，而不是语句，如 §12.4.2 节中所述。）

### 5.5.6 throw
An exception is a signal that indicates that some sort of exceptional condition or error has occurred. To throw an exception is to signal such an error or exceptional condition. To catch an exception is to handle it—to take whatever actions are necessary or appropriate to recover from the exception. In JavaScript, exceptions are thrown whenever a runtime error occurs and whenever the program explicitly throws one using the throw statement. Exceptions are caught with the try/catch/finally statement, which is described in the next section.

> 异常是表示已发生某种异常情况或错误的信号。引发异常是表示这种错误或异常情况。捕获异常就是对它进行处理——采取必要措施或适当措施以从异常中恢复。在 JavaScript 中，只要发生运行时错误，并且只要程序使用 throw 语句显式抛出一个异常，就会引发异常。使用 try/catch/finally 语句捕获异常，这将在下一部分中进行描述。

The throw statement has the following syntax:

> throw语句具有以下语法：

```js
throw expression;
```

expression may evaluate to a value of any type. You might throw a number that represents an error code or a string that contains a human-readable error message. The Error class and its subclasses are used when the JavaScript interpreter itself throws an error, and you can use them as well. An Error object has a name property that specifies the type of error and a message property that holds the string passed to the constructor function. Here is an example function that throws an Error object when invoked with an invalid argument:

> 表达式可以计算为任何类型的值。可能会抛出代表错误代码的数字或包含人类可读错误消息的字符串。当 JavaScript 解释器本身抛出错误时，将使用 Error 类及其子类，并且您也可以使用它们。Error 对象具有用于指定错误类型的 name 属性和用于保存传递给构造函数的字符串的 message 属性。这是一个示例函数，当使用无效参数调用该函数时，将引发 Error 对象：

```js
function factorial(x) {
    // If the input argument is invalid, throw an exception!
    if (x < 0) throw new Error("x must not be negative");
    // Otherwise, compute a value and return normally
    let f;
    for(f = 1; x > 1; f *= x, x--) /* empty */ ;
    return f;
}
factorial(4)   // => 24
```
When an exception is thrown, the JavaScript interpreter immediately stops normal program execution and jumps to the nearest exception handler. Exception handlers are written using the catch clause of the try/catch/finally statement, which is described in the next section. If the block of code in which the exception was thrown does not have an associated catch clause, the interpreter checks the next-highest enclosing block of code to see if it has an exception handler associated with it. This continues until a handler is found. If an exception is thrown in a function that does not contain a try/catch/finally statement to handle it, the exception propagates up to the code that invoked the function. In this way, exceptions propagate up through the lexical structure of JavaScript methods and up the call stack. If no exception handler is ever found, the exception is treated as an error and is reported to the user.

> 引发异常时，JavaScript 解释器立即停止正常程序执行并跳转到最近的异常处理程序。异常处理程序使用 try/catch/finally 语句的 catch 子句编写，这将在下一部分中进行描述。如果在其中引发了异常的代码块中没有关联的 catch 子句，则解释器将检查下一个最顶层的代码块，以查看其是否具有与之关联的异常处理程序。这一直持续到找到处理程序为止。如果在不包含 try/catch/finally 语句来处理它的函数中引发异常，则该异常会传播到调用该函数的代码。这样，异常会通过 JavaScript 方法的词法结构向上传播，并向上扩展到调用堆栈。如果未找到异常处理程序，则将该异常视为错误并报告给用户。

### 5.5.7 try/catch/finally
The try/catch/finally statement is JavaScript’s exception handling mechanism. The try clause of this statement simply defines the block of code whose exceptions are to be handled. The try block is followed by a catch clause, which is a block of statements that are invoked when an exception occurs anywhere within the try block. The catch clause is followed by a finally block containing cleanup code that is guaranteed to be executed, regardless of what happens in the try block. Both the catch and finally blocks are optional, but a try block must be accompanied by at least one of these blocks. The try, catch, and finally blocks all begin and end with curly braces. These braces are a required part of the syntax and cannot be omitted, even if a clause contains only a single statement.

> try/catch/finally 语句是 JavaScript 的异常处理机制。该语句的 try 子句仅定义要处理其异常的代码块。在 try 块之后是 catch 子句，catch 子句是在 try 块内任何地方发生异常时调用的语句块。catch 子句后面是一个 finally 块，其中包含保证可以执行的清除代码，无论 try 块中发生了什么。catch 和 finally 块都是可选的，但是 try 块必须至少与这些块之一相伴。尝试，捕获和最终阻止都以花括号开头和结尾。这些花括号是语法的必需部分，即使子句仅包含一个语句，也不能忽略这些花括号。

The following code illustrates the syntax and purpose of the try/catch/finally statement:

> 以下代码说明了 try/catch/finally 语句的语法和用途：

```js
try {
    // Normally, this code runs from the top of the block to the bottom
    // without problems. But it can sometimes throw an exception,
    // either directly, with a throw statement, or indirectly, by calling
    // a method that throws an exception.
}
catch(e) {
    // The statements in this block are executed if, and only if, the try
    // block throws an exception. These statements can use the local variable
    // e to refer to the Error object or other value that was thrown.
    // This block may handle the exception somehow, may ignore the
    // exception by doing nothing, or may rethrow the exception with throw.
}
finally {
    // This block contains statements that are always executed, regardless of
    // what happens in the try block. They are executed whether the try
    // block terminates:
    //   1) normally, after reaching the bottom of the block
    //   2) because of a break, continue, or return statement
    //   3) with an exception that is handled by a catch clause above
    //   4) with an uncaught exception that is still propagating
}
```
Note that the catch keyword is generally followed by an identifier in parentheses. This identifier is like a function parameter. When an exception is caught, the value associated with the exception (an Error object, for example) is assigned to this parameter. The identifier associated with a catch clause has block scope—it is only defined within the catch block.

> 请注意，catch 关键字通常在括号后跟一个标识符。该标识符就像一个函数参数。捕获到异常后，与该异常关联的值（例如 Error 对象）将分配给该参数。与 catch 子句关联的标识符具有块作用域——仅在catch块内有定义。

Here is a realistic example of the try/catch statement. It uses the factorial() method defined in the previous section and the client-side JavaScript methods prompt() and alert() for input and output:

> 这是 try/catch 语句的实际示例。它使用上一节中定义的 factorial() 方法以及客户端 JavaScript 方法 hint() 和 alert() 进行输入和输出：

```js
try {
    // Ask the user to enter a number
    let n = Number(prompt("Please enter a positive integer", ""));
    // Compute the factorial of the number, assuming the input is valid
    let f = factorial(n);
    // Display the result
    alert(n + "! = " + f);
}
catch(ex) {     // If the user's input was not valid, we end up here
    alert(ex);  // Tell the user what the error is
}
```
This example is a try/catch statement with no finally clause. Although finally is not used as often as catch, it can be useful. However, its behavior requires additional explanation. The finally clause is guaranteed to be executed if any portion of the try block is executed, regardless of how the code in the try block completes. It is generally used to clean up after the code in the try clause.

> 这个例子是一个 try/catch 语句，没有 finally 子句。虽然 finally 不像 catch 那样经常使用，但它很有用。可是，其行为需要额外说明。如果 try 块的任何部分被执行，则必定执行 finally 子句，无论 try 块中的代码如何完成。通常用于在 try 子句中的代码之后进行清理。

In the normal case, the JavaScript interpreter reaches the end of the try block and then proceeds to the finally block, which performs any necessary cleanup. If the interpreter left the try block because of a return, continue, or break statement, the finally block is executed before the interpreter jumps to its new destination.

> 在正常情况下，JavaScript 解释器到达 try 块的末尾，然后进行到 finally 块，该块执行任何必要的清除。如果解释器由于返回，继续或中断语句而离开 try 块，则在解释器跳转到其新目的地之前执行 finally 块。

If an exception occurs in the try block and there is an associated catch block to handle the exception, the interpreter first executes the catch block and then the finally block. If there is no local catch block to handle the exception, the interpreter first executes the finally block and then jumps to the nearest containing catch clause.

> 如果 try 块中发生异常，并且有一个关联的 catch 块来处理该异常，则解释器将首先执行 catch 块，然后执行 finally 块。如果没有本地 catch 块来处理该异常，则解释器将首先执行 finally 块，然后跳转到最近的包含 catch 子句。

If a finally block itself causes a jump with a return, continue, break, or throw statement, or by calling a method that throws an exception, the interpreter abandons whatever jump was pending and performs the new jump. For example, if a finally clause throws an exception, that exception replaces any exception that was in the process of being thrown. If a finally clause issues a return statement, the method returns normally, even if an exception has been thrown and has not yet been handled.

> 如果 finally 块本身通过 return、continue、break 或 throw 语句导致跳转，或者通过调用引发异常的方法来调用，则解释器将放弃所有挂起的任何程序并执行新的跳转。例如，如果 finally 子句引发异常，则该异常将替换正在引发过程中的所有异常。如果 finally 子句发出 return 语句，则即使已引发异常且尚未处理异常，该方法也会正常返回。

try and finally can be used together without a catch clause. In this case, the finally block is simply cleanup code that is guaranteed to be executed, regardless of what happens in the try block. Recall that we can’t completely simulate a for loop with a while loop because the continue statement behaves differently for the two loops. If we add a try/finally statement, we can write a while loop that works like a for loop and that handles continue statements correctly:

> try 和 finally 可以一起使用，而无需使用 catch 子句。在这种情况下，无论 try 块发生什么情况，finally 块都是保证可以执行的清除代码。回想一下，我们无法完全通过 while 循环来模拟 for 循环，因为 continue 语句在两个循环中的行为有所不同。如果添加 try/finally 语句，则可以编写一个 while 循环，该循环类似于 for 循环，并且可以正确处理 continue 语句：

```js
// Simulate for(initialize ; test ;increment ) body;
initialize ;
while( test ) {
    try { body ; }
    finally { increment ; }
}
```
Note, however, that a body that contains a break statement behaves slightly differently (causing an extra increment before exiting) in the while loop than it does in the for loop, so even with the finally clause, it is not possible to completely simulate the for loop with while.

> 但是请注意，包含 break 语句的主体在 while 循环中的行为与 for 循环中的行为略有不同（在退出前会导致额外的增量计算），因此即使使用 finally 子句，也无法完全用 while 模拟 for 循环。

BARE CATCH CLAUSES
Occasionally you may find yourself using a catch clause solely to detect and stop the propagation of an exception, even though you do not care about the type or the value of the exception. In ES2019 and later, you can omit the parentheses and the identifier and use the catch keyword bare in this case. Here is an example:

> 有时，即使不关心异常的类型或值，您可能会发现自己仅使用 catch 子句来检测并停止异常的传播。在 ES2019 及更高版本中，可以省略括号和标识符，并在这种情况下裸露使用 catch 关键字。 这是一个例子：

```js
// Like JSON.parse(), but return undefined instead of throwing an error
function parseJSON(s) {
    try {
        return JSON.parse(s);
    } catch {
        // Something went wrong but we don't care what it was
        return undefined;
    }
}
```
## 5.6 Miscellaneous Statements
This section describes the remaining three JavaScript statements—with, debugger, and "use strict".

> 本节描述了其余三个 JavaScript 语句——with、debugger 和“ use strict”。

### 5.6.1 with
The with statement runs a block of code as if the properties of a specified object were variables in scope for that code. It has the following syntax:

> with 语句运行代码块，就像指定对象的属性是该代码范围内的变量一样。它具有以下语法：

```js
with (object)
    statement
```
This statement creates a temporary scope with the properties of object as variables and then executes statement within that scope.

> 该语句使用对象的属性作为变量创建一个临时作用域，然后在该作用域内执行语句。

The with statement is forbidden in strict mode (see §5.6.3) and should be considered deprecated in non-strict mode: avoid using it whenever possible. JavaScript code that uses with is difficult to optimize and is likely to run significantly more slowly than the equivalent code written without the with statement.

> 在严格模式下禁止 with 语句（请参见 §5.6.3），并且在非严格模式下应将其视为已弃用：请尽可能避免使用它。与 with 一起使用的 JavaScript 代码难以优化，并且与没有 with 语句编写的等效代码相比，运行速度可能慢得多。

The common use of the with statement is to make it easier to work with deeply nested object hierarchies. In client-side JavaScript, for example, you may have to type expressions like this one to access elements of an HTML form:

> with 语句的常用用法是使使用深度嵌套的对象层次结构更清晰。例如，在客户端 JavaScript 中，可能必须键入此类表达式才能访问 HTML 表单的元素：

```js
document.forms[0].address.value
```
If you need to write expressions like this a number of times, you can use the with statement to treat the properties of the form object like variables:

> 如果需要多次编写这样的表达式，则可以使用 with 语句将表单对象的属性像变量一样对待：

```js
with(document.forms[0]) {
    // Access form elements directly here. For example:
    name.value = "";
    address.value = "";
    email.value = "";
}
```
This reduces the amount of typing you have to do: you no longer need to prefix each form property name with document.forms[0]. It is just as simple, of course, to avoid the with statement and write the preceding code like this:

> 这减少了必须进行的键入操作的数量：不再需要为每个表单属性名称加上 document.forms[0] 前缀。当然，避免 with 语句并像这样编写前面的代码也很简单：

```js
let f = document.forms[0];
f.name.value = "";
f.address.value = "";
f.email.value = "";
```
Note that if you use const or let or var to declare a variable or constant within the body of a with statement, it creates an ordinary variable and does not define a new property within the specified object.

> 请注意，如果使用 const 或 let 或 var 在 with 语句的主体内声明变量或常量，则它将创建普通变量，并且不会在指定对象内定义新属性。

### 5.6.2 debugger
The debugger statement normally does nothing. If, however, a debugger program is available and is running, then an implementation may (but is not required to) perform some kind of debugging action. In practice, this statement acts like a breakpoint: execution of JavaScript code stops, and you can use the debugger to print variables’ values, examine the call stack, and so on. Suppose, for example, that you are getting an exception in your function f() because it is being called with an undefined argument, and you can’t figure out where this call is coming from. To help you in debugging this problem, you might alter f() so that it begins like this:

> debugger 语句通常不执行任何操作。但是，如果 debugger 程序可用并且正在运行，则这个实现可以（但不是必需）执行某种调试操作。实际上，该语句就像一个断点：停止执行 JavaScript 代码，并且可以使用调试器打印变量的值，检查调用堆栈等。例如，假设您在函数 f() 中遇到一个异常，因为该异常正在使用未定义的参数进行调用，而您无法弄清楚该调用的来源。为了帮助调试此问题，可以更改 f() 使其开始，如下所示：

```js
function f(o) {
  if (o === undefined) debugger;  // Temporary line for debugging purposes
  ...                             // The rest of the function goes here.
}
```
Now, when f() is called with no argument, execution will stop, and you can use the debugger to inspect the call stack and find out where this incorrect call is coming from.

> 现在，当不带任何参数调用 f() 时，执行将停止，并且可以使用调试器检查调用堆栈，并找出此错误调用的出处。

Note that it is not enough to have a debugger available: the debugger statement won’t start the debugger for you. If you’re using a web browser and have the developer tools console open, however, this statement will cause a breakpoint.

> 请注意，仅有 debugger 是不够的：debugger 语句不会为启动调试器。但是，如果您使用的是网络浏览器并打开了开发者工具控制台，则此语句将导致一个断点。

### 5.6.3 “use strict”
"use strict" is a directive introduced in ES5. Directives are not statements (but are close enough that "use strict" is documented here). There are two important differences between the "use strict" directive and regular statements:

> “use strict”是ES5中引入的指令。指令不是语句（但足够接近，因此此处记录了“use strict”）。“use strict”指令和常规语句之间有两个重要区别：

It does not include any language keywords: the directive is just an expression statement that consists of a special string literal (in single or double quotes).

> 它不包含任何语言关键字：指令只是由特殊字符串文字（单引号或双引号）组成的表达式语句。

It can appear only at the start of a script or at the start of a function body, before any real statements have appeared.

> 它只能出现在脚本的开始处或函数体的开始处，然后才出现任何实际的语句。

The purpose of a "use strict" directive is to indicate that the code that follows (in the script or function) is strict code. The top-level (nonfunction) code of a script is strict code if the script has a "use strict" directive. A function body is strict code if it is defined within strict code or if it has a "use strict" directive. Code passed to the eval() method is strict code if eval() is called from strict code or if the string of code includes a "use strict" directive. In addition to code explicitly declared to be strict, any code in a class body (Chapter 9) or in an ES6 module (§10.3) is automatically strict code. This means that if all of your JavaScript code is written as modules, then it is all automatically strict, and you will never need to use an explicit "use strict" directive.

> “use strict”指令的目的是指示（在脚本或函数中）后面的代码是严格代码。如果脚本具有“use strict”指令，则该脚本的顶级（非函数）代码为严格代码。如果函数体是在严格代码中定义的，或者具有“use strict”指令，则它是严格代码。如果从严格代码中调用 eval() 或代码字符串包含“use strict”指令，则传递给 eval() 方法的代码为严格代码。除了明确声明为严格的代码之外，类主体（第9章）或 ES6 模块（10.3）中的任何代码都是自动严格的代码。这意味着，如果所有的JavaScript代码都是作为模块编写的，那么它们都是自动严格的，并且将不需要使用显式的“use strict”指令。 

Strict code is executed in strict mode. Strict mode is a restricted subset of the language that fixes important language deficiencies and provides stronger error checking and increased security. Because strict mode is not the default, old JavaScript code that still uses the deficient legacy features of the language will continue to run correctly. The differences between strict mode and non-strict mode are the following (the first three are particularly important):

> 严格代码在严格模式下执行。严格模式是该语言的受限子集，可修复重要的语言缺陷并提供更强的错误检查和更高的安全性。由于严格模式不是默认模式，因此旧 JavaScript 代码使用不足传统特性将继续正确运行。严格模式和非严格模式之间的区别如下（前三个特别重要）：

The with statement is not allowed in strict mode.

> 在严格模式下，不允许使用 with 语句。

In strict mode, all variables must be declared: a ReferenceError is thrown if you assign a value to an identifier that is not a declared variable, function, function parameter, catch clause parameter, or property of the global object. (In non-strict mode, this implicitly declares a global variable by adding a new property to the global object.)

> 在严格模式下，必须声明所有变量：如果将值分配给未声明的变量、函数、函数参数、catch 子句参数或全局对象的属性的标识符，则会引发 ReferenceError。（在非严格模式下，通过向全局对象添加新属性来隐式声明全局变量。）

In strict mode, functions invoked as functions (rather than as methods) have a this value of undefined. (In non-strict mode, functions invoked as functions are always passed the global object as their this value.) Also, in strict mode, when a function is invoked with call() or apply() (§8.7.4), the this value is exactly the value passed as the first argument to call() or apply(). (In non-strict mode, null and undefined values are replaced with the global object and nonobject values are converted to objects.)

> 在严格模式下，作为函数（而不是方法）调用的函数的 this 值是 undefined。（在非严格模式下，作为函数调用的函数总是将全局对象作为其 this 值。）此外，在严格模式下，当使用 call() 或 apply() 调用函数时（§8.7.4），this 值作为第一个参数传递给 call() 或 apply() 的值。（在非严格模式下，将 null 和 undefined 值替换为全局对象，并将 nonobject 值转换为对象。）

In strict mode, assignments to nonwritable properties and attempts to create new properties on non-extensible objects throw a TypeError. (In non-strict mode, these attempts fail silently.)

> 在严格模式下，对不可写属性的分配以及在不可扩展对象上尝试创建新属性的尝试将引发 TypeError。（在非严格模式下，这些尝试将以静默方式失败。）

In strict mode, code passed to eval() cannot declare variables or define functions in the caller’s scope as it can in non-strict mode. Instead, variable and function definitions live in a new scope created for the eval(). This scope is discarded when the eval() returns.

> 在严格模式下，传递给 eval() 的代码无法像在非严格模式下那样在调用者的作用域中声明变量或定义函数。相反，变量和函数定义位于为 eval() 创建的新作用域中。当 eval() 返回时，将放弃此 this 用域。

In strict mode, the Arguments object (§8.3.3) in a function holds a static copy of the values passed to the function. In non-strict mode, the Arguments object has “magical” behavior in which elements of the array and named function parameters both refer to the same value.

In strict mode, a SyntaxError is thrown if the delete operator is followed by an unqualified identifier such as a variable, function, or function parameter. (In nonstrict mode, such a delete expression does nothing and evaluates to false.)

In strict mode, an attempt to delete a nonconfigurable property throws a TypeError. (In non-strict mode, the attempt fails and the delete expression evaluates to false.)

In strict mode, it is a syntax error for an object literal to define two or more properties by the same name. (In non-strict mode, no error occurs.)

In strict mode, it is a syntax error for a function declaration to have two or more parameters with the same name. (In non-strict mode, no error occurs.)

In strict mode, octal integer literals (beginning with a 0 that is not followed by an x) are not allowed. (In non-strict mode, some implementations allow octal literals.)

In strict mode, the identifiers eval and arguments are treated like keywords, and you are not allowed to change their value. You cannot assign a value to these identifiers, declare them as variables, use them as function names, use them as function parameter names, or use them as the identifier of a catch block.

In strict mode, the ability to examine the call stack is restricted. arguments.caller and arguments.callee both throw a TypeError within a strict mode function. Strict mode functions also have caller and arguments properties that throw TypeError when read. (Some implementations define these nonstandard properties on non-strict functions.)

## 5.7 Declarations
The keywords const, let, var, function, class, import, and export are not technically statements, but they look a lot like statements, and this book refers informally to them as statements, so they deserve a mention in this chapter.

> 从技术上讲，关键字 const、let、var、function、class、import 和 export 并不是语句，但它们看起来很像语句，并且本书将它们非正式地称为语句，因此在本章中应予提及。

These keywords are more accurately described as declarations rather than statements. We said at the start of this chapter that statements “make something happen.” Declarations serve to define new values and give them names that we can use to refer to those values. They don’t make much happen themselves, but by providing names for values they, in an important sense, define the meaning of the other statements in your program.

> 这些关键字被更准确地描述为声明而不是语句。我们在本章开始时说过，语句“使某事发生”。声明用于定义新值，并为它们提供可用来引用这些值的名称。它们本身并不会带来太大的变化，但是通过提供值的名称，它们在重要的意义上定义了程序中其他语句的含义。

When a program runs, it is the program’s expressions that are being evaluated and the program’s statements that are being executed. The declarations in a program don’t “run” in the same way: instead, they define the structure of the program itself. Loosely, you can think of declarations as the parts of the program that are processed before the code starts running.

> 程序运行时，将对程序的表达式进行评估，并执行程序的语句。程序中的声明不是以相同的方式“运行”：相反，它们定义了程序本身的结构。不确切地说，可以将声明视为代码开始运行之前已处理的部分程序。

JavaScript declarations are used to define constants, variables, functions, and classes and for importing and exporting values between modules. The next subsections give examples of all of these declarations. They are all covered in much more detail elsewhere in this book.

> JavaScript 声明用于定义常量、变量、函数和类，以及在模块之间导入和导出值。接下来的小节将给出所有这些声明的示例。在本书的其他地方，将对它们进行更详细的介绍。

### 5.7.1 const, let, and var
The const, let, and var declarations are covered in §3.10. In ES6 and later, const declares constants, and let declares variables. Prior to ES6, the var keyword was the only way to declare variables and there was no way to declare constants. Variables declared with var are scoped to the containing function rather than the containing block. This can be a source of bugs, and in modern JavaScript there is really no reason to use var instead of let.
```js
const TAU = 2*Math.PI;
let radius = 3;
var circumference = TAU * radius;
```
### 5.7.2 function
The function declaration is used to define functions, which are covered in detail in Chapter 8. (We also saw function in §4.3, where it was used as part of a function expression rather than a function declaration.) A function declaration looks like this:
```js
function area(radius) {
    return Math.PI * radius * radius;
}
```
A function declaration creates a function object and assigns it to the specified name—area in this example. Elsewhere in our program, we can refer to the function—and run the code inside it—by using this name. The function declarations in any block of JavaScript code are processed before that code runs, and the function names are bound to the function objects throughout the block. We say that function declarations are “hoisted” because it is as if they had all been moved up to the top of whatever scope they are defined within. The upshot is that code that invokes a function can exist in your program before the code that declares the function.

§12.3 describes a special kind of function known as a generator. Generator declarations use the function keyword but follow it with an asterisk. §13.3 describes asynchronous functions, which are also declared using the function keyword but are prefixed with the async keyword.

### 5.7.3 class
In ES6 and later, the class declaration creates a new class and gives it a name that we can use to refer to it. Classes are described in detail in Chapter 9. A simple class declaration might look like this:
```js
class Circle {
    constructor(radius) { this.r = radius; }
    area() { return Math.PI * this.r * this.r; }
    circumference() { return 2 * Math.PI * this.r; }
}
```
Unlike functions, class declarations are not hoisted, and you cannot use a class declared this way in code that appears before the declaration.

### 5.7.4 import and export
The import and export declarations are used together to make values defined in one module of JavaScript code available in another module. A module is a file of JavaScript code with its own global namespace, completely independent of all other modules. The only way that a value (such as function or class) defined in one module can be used in another module is if the defining module exports it with export and the using module imports it with import. Modules are the subject of Chapter 10, and import and export are covered in detail in §10.3.

import directives are used to import one or more values from another file of JavaScript code and give them names within the current module. import directives come in a few different forms. Here are some examples:
```js
import Circle from './geometry/circle.js';
import { PI, TAU } from './geometry/constants.js';
import { magnitude as hypotenuse } from './vectors/utils.js';
```
Values within a JavaScript module are private and cannot be imported into other modules unless they have been explicitly exported. The export directive does this: it declares that one or more values defined in the current module are exported and therefore available for import by other modules. The export directive has more variants than the import directive does. Here is one of them:
```js
// geometry/constants.js
const PI = Math.PI;
const TAU = 2 * PI;
export { PI, TAU };
```
The export keyword is sometimes used as a modifier on other declarations, resulting in a kind of compound declaration that defines a constant, variable, function, or class and exports it at the same time. And when a module exports only a single value, this is typically done with the special form export default:
```js
export const TAU = 2 * Math.PI;
export function magnitude(x,y) { return Math.sqrt(x*x + y*y); }
export default class Circle { /* class definition omitted here */ }
```
## 5.8 Summary of JavaScript Statements
This chapter introduced each of the JavaScript language’s statements, which are summarized in Table 5-1.

Table 5-1. JavaScript statement syntax
Statement	Purpose
break

Exit from the innermost loop or switch or from named enclosing statement

case

Label a statement within a switch

class

Declare a class

const

Declare and initialize one or more constants

continue

Begin next iteration of the innermost loop or the named loop

debugger

Debugger breakpoint

default

Label the default statement within a switch

do/while

An alternative to the while loop

export

Declare values that can be imported into other modules

for

An easy-to-use loop

for/await

Asynchronously iterate the values of an async iterator

for/in

Enumerate the property names of an object

for/of

Enumerate the values of an iterable object such as an array

function

Declare a function

if/else

Execute one statement or another depending on a condition

import

Declare names for values defined in other modules

label

Give statement a name for use with break and continue

let

Declare and initialize one or more block-scoped variables (new syntax)

return

Return a value from a function

switch

Multiway branch to case or default: labels

throw

Throw an exception

try/catch/finally

Handle exceptions and code cleanup

“use strict”

Apply strict mode restrictions to script or function

var

Declare and initialize one or more variables (old syntax)

while

A basic loop construct

with

Extend the scope chain (deprecated and forbidden in strict mode)

yield

Provide a value to be iterated; only used in generator functions

---

1. The fact that the case expressions are evaluated at runtime makes the JavaScript switch statement much different from (and less efficient than) the switch statement of C, C++, and Java. In those languages, the case expressions must be compile-time constants of the same type, and switch statements can often compile down to highly efficient jump tables.
2. When we consider the continue statement in §5.5.3, we’ll see that this while loop is not an exact equivalent of the for loop.