# 第 8 章 函数

This chapter covers JavaScript functions. Functions are a fundamental building block for JavaScript programs and a common feature in almost all programming languages. You may already be familiar with the concept of a function under a name such as subroutine or procedure.

> 本章介绍了 JavaScript 函数。函数是 JavaScript 程序的基本构建块，也是几乎所有编程语言的共同特性。你可能已经了解函数的概念，如子例程或过程。

A function is a block of JavaScript code that is defined once but may be executed, or invoked, any number of times. JavaScript functions are parameterized: a function definition may include a list of identifiers, known as parameters, that work as local variables for the body of the function. Function invocations provide values, or arguments, for the function’s parameters. Functions often use their argument values to compute a return value that becomes the value of the function-invocation expression. In addition to the arguments, each invocation has another value—the invocation context—that is the value of the this keyword.

> 函数是一个 JavaScript 代码块，只定义一次，但可以执行或调用任意次数。JavaScript 函数是参数化的：一个函数定义可以包含一个标识符列表，称为参数，作为函数体的局部变量。函数调用为函数的参数提供值或实参。函数通常使用它们的实参值来计算一个返回值，该返回值成为函数调用表达式的值。除了参数之外，每次调用都有另一个值——调用上下文——即 this 关键字的值。

If a function is assigned to a property of an object, it is known as a method of that object. When a function is invoked on or through an object, that object is the invocation context or this value for the function. Functions designed to initialize a newly created object are called constructors. Constructors were described in §6.2 and will be covered again in Chapter 9.

> 如果函数挂载在一个对象上作为其属性，它就被称为方法。当该方法在对象中被调用或通过对象调用时，该对象就是该方法函数的调用上下文或 this 值。用于初始化新创建的对象的函数称为构造函数。构造函数在 §6.2 中有介绍，我们将在第 9 章中再次谈到它。

In JavaScript, functions are objects, and they can be manipulated by programs. JavaScript can assign functions to variables and pass them to other functions, for example. Since functions are objects, you can set properties on them and even invoke methods on them.

> 在 JavaScript 中，函数是对象，它们可以被程序操作。例如，JavaScript 可以将函数赋给变量，并将它们传递给其他函数。由于函数是对象，所以您可以给它们设置属性，甚至调用它们的方法。

JavaScript function definitions can be nested within other functions, and they have access to any variables that are in scope where they are defined. This means that JavaScript functions are closures, and it enables important and powerful programming techniques.

> JavaScript 函数可以嵌套在其他函数中定义，并且它们可以访问定义它们所处的作用域内任何变量。这意味着 JavaScript 函数是闭包，支持闭包是非常重要的，它是非常强大的编程技巧。

## 8.1 Defining Functions

The most straightforward way to define a JavaScript function is with the function keyword, which can be used as a declaration or as an expression. ES6 defines an important new way to define functions without the function keyword: “arrow functions” have a particularly compact syntax and are useful when passing one function as an argument to another function. The subsections that follow cover these three ways of defining functions. Note that some details of function definition syntax involving function parameters are deferred to §8.3.

> 定义 JavaScript 函数最直接的方法是使用 function 关键字，它既可以用作声明又可以用作表达式。ES6 定义了一种不使用 function 关键字的重要新方法来定义的函数：“箭头函数”，它具有特别简洁语法，并且在将一个函数作为参数传递给另一个函数的场景中非常实用。接下来的小节将介绍这三种定义函数的方法。注意，关于函数定义语法包含的函数参数相关内容将在 §8.3 中介绍。

In object literals and class definitions, there is a convenient shorthand syntax for defining methods. This shorthand syntax was covered in §6.10.5 and is equivalent to using a function definition expression and assigning it to an object property using the basic name:value object literal syntax. In another special case, you can use keywords get and set in object literals to define special property getter and setter methods. This function definition syntax was covered in §6.10.6.

> 在对象字面量和类定义中，有一种方便的快捷语法来定义方法。这种简写语法在 §6.10.5 中有介绍，相当于通过对象字面量语法将函数定义表达式用最基本的属性名：属性值的方式赋值给对象的属性。在另一种特殊情况下，可以在对象字面量中使用关键字 get 和 set 来定义特殊的属性 getter 和 setter 方法。这个函数定义语法在 §6.10.6 中介绍过。

Note that functions can also be defined with the Function() constructor, which is the subject of §8.7.7. Also, JavaScript defines some specialized kinds of functions. function* defines generator functions (see Chapter 12) and async function defines asynchronous functions (see Chapter 13).

> 注意，函数也可以用 Function() 构造函数来定义，这是 §8.7.7 的主题。此外，JavaScript 还定义了一些特殊类型的函数。function* 定义函数生成器（见第 12 章）和 async function 定义异步函数（见第 13 章）。

### 8.1.1 Function Declarations

Function declarations consist of the function keyword, followed by these components:
- An identifier that names the function. The name is a required part of function declarations: it is used as the name of a variable, and the newly defined function object is assigned to the variable.
- A pair of parentheses around a comma-separated list of zero or more identifiers. These identifiers are the parameter names for the function, and they behave like local variables within the body of the function.
- A pair of curly braces with zero or more JavaScript statements inside. These statements are the body of the function: they are executed whenever the function is invoked.

---

函数声明由 function 关键字组成，后面跟着这些组件:
- 函数名称标识符。名称是函数声明的必要部分:它用作变量的名称，并将新定义的函数对象赋值给该变量。
- 一对圆括号，其中包含由0个或者多个用逗号分隔的标识符组成的列表。这些标识符是函数的参数名，它们的行为类似于函数体中的局部变量。
- 一对花括号，其中包含由0条或者多条 JavaScript 语句。这些语句构成了函数体：每当函数调用时，就会执行这些语句。

Here are some example function declarations:

> 下面是一些函数声明的例子:

```js
// Print the name and value of each property of o.  Return undefined.
function printprops(o) {
    for(let p in o) {
        console.log(`${p}: ${o[p]}\n`);
    }
}

// Compute the distance between Cartesian points (x1,y1) and (x2,y2).
function distance(x1, y1, x2, y2) {
    let dx = x2 - x1;
    let dy = y2 - y1;
    return Math.sqrt(dx*dx + dy*dy);
}

// A recursive function (one that calls itself) that computes factorials
// Recall that x! is the product of x and all positive integers less than it.
function factorial(x) {
    if (x <= 1) return 1;
    return x * factorial(x-1);
}
```

One of the important things to understand about function declarations is that the name of the function becomes a variable whose value is the function itself. Function declaration statements are “hoisted” to the top of the enclosing script, function, or block so that functions defined in this way may be invoked from code that appears before the definition. Another way to say this is that all of the functions declared in a block of JavaScript code will be defined throughout that block, and they will be defined before the JavaScript interpreter begins to execute any of the code in that block.

> 重中之重要理解函数声明是函数名变成一个变量，这个变量的值是函数本身。函数声明语句“被提前”到脚本、函数、块之前，因此这种方式定义的函数可以在它定义之前被调用。另一种说法是所有声明在 Javascript 代码块中的函数，在块内始终是有定义的，它们定义在 JavaScript 解释器开始解释执行块内任何语句之前。

The distance() and factorial() functions we’ve described are designed to compute a value, and they use return to return that value to their caller. The return statement causes the function to stop executing and to return the value of its expression (if any) to the caller. If the return statement does not have an associated expression, the return value of the function is undefined.

> distance() 和 factorial() 函数计算一个值，它们用 retrun 来将这个值返回给调用者。return 语句导致函数停止执行，并返回它的表达式的值（如果有的话）给调用者。如果 return 语句没有一个与之相关的表达式，则函数返回 undefined 值。

The printprops() function is different: its job is to output the names and values of an object’s properties. No return value is necessary, and the function does not include a return statement. The value of an invocation of the printprops() function is always undefined. If a function does not contain a return statement, it simply executes each statement in the function body until it reaches the end, and returns the undefined value to the caller.

> printprops() 函数不同：它负责输出对象属性的名称和值。没有返回值的必要，并且该函数也不包含一个 return 语句。 调用 printprops() 函数的返回值永远是 undefined。如果一个函数不包含一个 return 语句，它仅仅执行函数体内每一条语句直到结束，并返回 undefined 给调用者。

Prior to ES6, function declarations were only allowed at the top level within a JavaScript file or within another function. While some implementations bent the rule, it was not technically legal to define functions inside the body of loops, conditionals, or other blocks. In the strict mode of ES6, however, function declarations are allowed within blocks. A function defined within a block only exists within that block, however, and is not visible outside the block.

> 在 ES6 之前，函数只允许在 JavaScript 文件顶层或者其他函数中声明。然而一些实现违反规约，在循环体条件体或者其他块中定义函数。在 ES6 的严格模式下，函数允许在块内进行声明。一个定义在块内的函数只存在于该块内，块外是不可见的。

### 8.1.2 Function Expressions
Function expressions look a lot like function declarations, but they appear within the context of a larger expression or statement, and the name is optional.

> 函数表达式看起来很像函数声明，但是它出现在一个它的上层表达式或语句的上下文中，并且函数名称是可选项。

 Here are some example function expressions:

> 下面是一些函数表达式的例子：

```js
// This function expression defines a function that squares its argument.
// Note that we assign it to a variable
const square = function(x) { return x*x; };

// Function expressions can include names, which is useful for recursion.
const f = function fact(x) { if (x <= 1) return 1; else return x*fact(x-1); };

// Function expressions can also be used as arguments to other functions:
[3,2,1].sort(function(a,b) { return a-b; });

// Function expressions are sometimes defined and immediately invoked:
let tensquared = (function(x) {return x*x;}(10));
```

Note that the function name is optional for functions defined as expressions, and most of the preceding function expressions we’ve shown omit it. A function declaration actually declares a variable and assigns a function object to it. A function expression, on the other hand, does not declare a variable: it is up to you to assign the newly defined function object to a constant or variable if you are going to need to refer to it multiple times. It is a good practice to use const with function expressions so you don’t accidentally overwrite your functions by assigning new values.

> 注意函数名称在函数表达式中是可选项，在大部分函数表达式中我们省略了它。函数声明实际上声明了一个变量并且将函数对象赋值给它。按照这个角度来看，函数表达式没有声明一个变量：可以根据它是否会多次调用由你自己决定是将新定义的函数对象赋值给一个常量还是变量。用 const 定义函数表达式是一个非常好的做法，你不会因为意外赋值而重写了你的函数。

A name is allowed for functions, like the factorial function, that need to refer to themselves. If a function expression includes a name, the local function scope for that function will include a binding of that name to the function object. In effect, the function name becomes a local variable within the function. Most functions defined as expressions do not need names, which makes their definition more compact (though not nearly as compact as arrow functions, described below).

> 可以给函数一个名称，就像 factorial 函数，它需要调用它自己。如果一个函数表达式包含一个名称，那这个函数的局部函数作用域内会包含一个属性名为该函数名的对象，其值绑定的是该函数。实际上，函数名变成这个函数的一个局部变量。大多数函数表达式不需要函数名称，这让它们的定义更简洁（但是并没有下面要讲的箭头函数简洁）。

There is an important difference between defining a function f() with a function declaration and assigning a function to the variable f after creating it as an expression. When you use the declaration form, the function objects are created before the code that contains them starts to run, and the definitions are hoisted so that you can call these functions from code that appears above the definition statement. This is not true for functions defined as expressions, however: these functions do not exist until the expression that defines them are actually evaluated. Furthermore, in order to invoke a function, you must be able to refer to it, and you can’t refer to a function defined as an expression until it is assigned to a variable, so functions defined with expressions cannot be invoked before they are defined.

> 在函数声明和函数表达式之间有一个非常重要的不同。当你用函数声明，该函数对象创建于该函数所在作用域的代码开始执行之前，也就是声明提前，所以你可以在函数定义之前调用他们。如果用函数表达式来定义一个函数，这样使用就是不对的：该函数不会存在，直到函数定义表达式真正被计算。因为，想要执行一个函数，你必须可以引用它，而一个函数表达式定义的函数一直到该函数赋值给一个变量后才能被引用，所以要使用函数表达式需要在函数被调用之前定义。

### 8.1.3 Arrow Functions
In ES6, you can define functions using a particularly compact syntax known as “arrow functions.” This syntax is reminiscent of mathematical notation and uses an => “arrow” to separate the function parameters from the function body. The function keyword is not used, and, since arrow functions are expressions instead of statements, there is no need for a function name, either. The general form of an arrow function is a comma-separated list of parameters in parentheses, followed by the => arrow, followed by the function body in curly braces:

> 在 ES6 之后，你可以用一个特别简洁的语法来定义函数，被称为“箭头函数”。这个语法联想到数学符号，用一个 => "箭头"来分隔函数的参数和函数体。function 关键字未使用，并且，由于箭头函数是表达式而不是声明语句，也不需要一个函数名称。一般箭头函数用圆括号包含一个逗号分隔的参数列表，接一个 => 箭头，后面是花括号包含的函数体。

```js
const sum = (x, y) => { return x + y; };
```

But arrow functions support an even more compact syntax. If the body of the function is a single return statement, you can omit the return keyword, the semicolon that goes with it, and the curly braces, and write the body of the function as the expression whose value is to be returned:

> 但是箭头函数支持更加简洁的语法。如果函数体只有一个简单的 return 语句，你可以省略 return 关键字，分号和花括号都一起省略，将函数体写成一个计算返回值的表达式。

```js
const sum = (x, y) => x + y;
```

Furthermore, if an arrow function has exactly one parameter, you can omit the parentheses around the parameter list:

> 而且，如果一个箭头函数只有一个参数，你可以省略参数列表的圆括号。

```js
const polynomial = x => x*x + 2*x + 3;
```

Note, however, that an arrow function with no arguments at all must be written with an empty pair of parentheses:

> 注意，如果箭头函数没有参数，必须写一对空圆括号。

```js
const constantFunc = () => 42;
```

Note that, when writing an arrow function, you must not put a new line between the function parameters and the => arrow. Otherwise, you could end up with a line like const polynomial = x, which is a syntactically valid assignment statement on its own.

> 注意，当写一个箭头函数时，函数参数和箭头之间不能换行。否则，可能会直接在赋值后中止，就像 const polynomial = x，因为它本身是一个语法上合法的赋值语句。

Also, if the body of your arrow function is a single return statement but the expression to be returned is an object literal, then you have to put the object literal inside parentheses to avoid syntactic ambiguity between the curly braces of a function body and the curly braces of an object literal:

> 此外，如果箭头函数体是一个单一的 return 语句，而且他返回的是一个对象字面量，那必须将对象字面量用圆括号包起来，避免将对象字面量的大括号误解成函数体的大括号。

```js
const f = x => { return { value: x }; };  // Good: f() returns an object
const g = x => ({ value: x });            // Good: g() returns an object
const h = x => { value: x };              // Bad: h() returns nothing
const i = x => { v: x, w: x };            // Bad: Syntax Error
```

In the third line of this code, the function h() is truly ambiguous: the code you intended as an object literal can be parsed as a labeled statement, so a function that returns undefined is created. On the fourth line, however, the more complicated object literal is not a valid statement, and this illegal code causes a syntax error.

> 这段代码的第三行，函数 h() 就有歧义：这段代码原本返回对象字面量被转化为一个标签语句，所以一个返回 undefined 的函数被创建。第四行，结构更复杂的对象字面量不是一个合法的语句，这段代码会抛出一个语法异常。

The concise syntax of arrow functions makes them ideal when you need to pass one function to another function, which is a common thing to do with array methods like map(), filter(), and reduce() (see §7.8.1), for example:

> 简洁的箭头函数可以完美的传递一个函数给另外一个函数，比如一些数组的常规操作方法 map()，filter() 和 reduce()（见 §7.8.1），例如：

```js
// Make a copy of an array with null elements removed.
let filtered = [1,null,2,3].filter(x => x !== null); // filtered == [1,2,3]
// Square some numbers:
let squares = [1,2,3,4].map(x => x*x);               // squares == [1,4,9,16]
```

Arrow functions differ from functions defined in other ways in one critical way: they inherit the value of the this keyword from the environment in which they are defined rather than defining their own invocation context as functions defined in other ways do. This is an important and very useful feature of arrow functions, and we’ll return to it again later in this chapter. Arrow functions also differ from other functions in that they do not have a prototype property, which means that they cannot be used as constructor functions for new classes (see §9.2).

> 箭头函数不同于用关键字定义的函数：箭头函数从定义它们的环境继承 this 关键字，而不是像其他定义方式那样定义自己的调用上下文。这是箭头函数一个重要且特别实用的特性，我们会在这一章的后面再次提到它。箭头函数也不同于其他函数，它们没有有原型属性。这意味着它不能被当作一个构造函数去创建一个类（见 §9.2）。

### 8.1.4 Nested Functions
In JavaScript, functions may be nested within other functions. For example:

> 在 JavaScript 中，函数可以嵌套在其他函数内。例如：

```js
function hypotenuse(a, b) {
    function square(x) { return x*x; }
    return Math.sqrt(square(a) + square(b));
}
```

The interesting thing about nested functions is their variable scoping rules: they can access the parameters and variables of the function (or functions) they are nested within. In the code shown here, for example, the inner function square() can read and write the parameters a and b defined by the outer function hypotenuse(). These scope rules for nested functions are very important, and we will consider them again in §8.6.

> 嵌套函数的有趣之处在于它的变量作用域规则：它们可以访问嵌套它们（或多重嵌套）的函数的参数和变量。例如，在上面的代码里，内部函数 square() 可以读写外部函数 hypotenuse() 定义的参数 a 和 b。这些作用域规则对嵌套函数非常重要，我们会在 §8.6 再深入了解它们。

## 8.2 Invoking Functions
The JavaScript code that makes up the body of a function is not executed when the function is defined, but rather when it is invoked. JavaScript functions can be invoked in five ways:

> 构成函数主体的 JavaScript 代码在定义之时并不会执行，只有调用该函数时，它们才会执行。JavaScript 函数可以以五种方式被调用。

As functions

As methods

As constructors

Indirectly through their call() and apply() methods

Implicitly, via JavaScript language features that do not appear like normal function invocations

> 作为函数
>
> 作为方法
>
> 作为构造函数
>
> 通过它们的 call() 和 apply() 方法间接调用
>
> 隐式调用，不同于普通函数调，通过 JavaScript 语言特性调用函数。


### 8.2.1 Function Invocation
Functions are invoked as functions or as methods with an invocation expression (§4.5). An invocation expression consists of a function expression that evaluates to a function object followed by an open parenthesis, a comma-separated list of zero or more argument expressions, and a close parenthesis. If the function expression is a property-access expression—if the function is the property of an object or an element of an array—then it is a method invocation expression. That case will be explained in the following example. The following code includes a number of regular function invocation expressions:

> 函数或方法通过调用表达式（§4.5）被调用。调用表达式由以下部分组成，计算函数对象的函数表达式，一个开放圆括号，逗号分隔的零个或多个实参表达式列表，一个闭合圆括号。如果函数表达式是属性访问表达式（函数是一个对象的属性或者一个数组的元素）那么它是一个方法调用表达式。这种情况会通过下面的例子说明，接下来这个代码包含了一些常规的函数调用表达式：

```js
printprops({x: 1});
let total = distance(0,0,2,1) + distance(2,1,3,5);
let probability = factorial(5)/factorial(13);
```
In an invocation, each argument expression (the ones between the parentheses) is evaluated, and the resulting values become the arguments to the function. These values are assigned to the parameters named in the function definition. In the body of the function, a reference to a parameter evaluates to the corresponding argument value.

> 在调用中，每个实参表达式（圆括号内的）执行计算，返回值作为函数的实参。这些值传给函数定义的参数。在函数体内，参数的引用指向对应实参的值。

For regular function invocation, the return value of the function becomes the value of the invocation expression. If the function returns because the interpreter reaches the end, the return value is undefined. If the function returns because the interpreter executes a return statement, then the return value is the value of the expression that follows the return or is undefined if the return statement has no value.

> 对于常规的函数调用，函数返回值变成函数调用表达式的值。如果因解释器执行到函数结尾而返回，返回值就是 undefined。如果函数返回是因为解释器执行一个 return 语句，那么返回值是 return 后面的表达式的计算结果，如果 return 语句没有值也返回 undefined。

#### CONDITIONAL INVOCATION
In ES2020 you can insert ?. after the function expression and before the open parenthesis in a function invocation in order to invoke the function only if it is not null or undefined. That is, the expression f?.(x) is equivalent (assuming no side effects) to:

> 在 ES2020 中你可以通过在函数表达式和圆括号之间插入 ?. 符号，使函数只有在不为 null 和 undefined 时候再调用。表达式 f?.(x) 等价（假设没有副作用）于：

```js
(f !== null && f !== undefined) ? f(x) : undefined
```
Full details on this conditional invocation syntax are in §4.5.1.

> 详细的条件执行语法描述在 §4.5.1。

For function invocation in non-strict mode, the invocation context (the this value) is the global object. In strict mode, however, the invocation context is undefined. Note that functions defined using the arrow syntax behave differently: they always inherit the this value that is in effect where they are defined.

> 函数调用在非严格模式下，调用上下文（ this ）是全局对象。然而在严格模式下，调用上下文是 undefined。注意箭头语法定义的函数行为是不同的：实际上它们总是继承它们定义位置的 this 值。

Functions written to be invoked as functions (and not as methods) do not typically use the this keyword at all. The keyword can be used, however, to determine whether strict mode is in effect:

> 以函数形式调用的函数通常不使用 this 关键字。不过，this 关键字可以用来判断当前是否是严格模式。

```js
// Define and invoke a function to determine if we're in strict mode.
const strict = (function() { return !this; }());
```
#### RECURSIVE FUNCTIONS AND THE STACK
A recursive function is one, like the factorial() function at the start of this chapter, that calls itself. Some algorithms, such as those involving tree-based data structures, can be implemented particularly elegantly with recursive functions. When writing a recursive function, however, it is important to think about memory constraints. When a function A calls function B, and then function B calls function C, the JavaScript interpreter needs to keep track of the execution contexts for all three functions. When function C completes, the interpreter needs to know where to resume executing function B, and when function B completes, it needs to know where to resume executing function A. You can imagine these execution contexts as a stack. When a function calls another function, a new execution context is pushed onto the stack. When that function returns, its execution context object is popped off the stack. If a function calls itself recursively 100 times, the stack will have 100 objects pushed onto it, and then have those 100 objects popped off. This call stack takes memory. On modern hardware, it is typically fine to write recursive functions that call themselves hundreds of times. But if a function calls itself ten thousand times, it is likely to fail with an error such as “Maximum call-stack size exceeded.”

> 递归函数就像本章开始的 factorial() 函数，它调用它自己。某些算法（如涉及基于树的数据结构）可以使用递归函数特别优雅地实现。在写递归函数时，考虑内存分配是很重要的。当函数 A 调用函数 B，然后函数 B 又调用函数 C 时，Javascript 编译器需要知道在哪里重新执行函数 B，当函数 B 执行完成后它需要知道在哪里执行函数 A。你可以将执行上下文想象成一个栈。当一个函数调用另外一个函数时，一个新的执行上下文被压入栈中。当被调用函数返回，它的执行上下文对象从栈中弹出。如果一个函数递归调用100次，那么会有100个对象被压入栈中，然后这100个对象再依次从栈中弹出。这种调用非常耗内存。以现代的硬件递归调用100次通常没什么问题。但是如果一个函数递归上千次，它可能会失败并报错“Maximum call-stack size exceeded.”。

### 8.2.2 Method Invocation
A method is nothing more than a JavaScript function that is stored in a property of an object. If you have a function f and an object o, you can define a method named m of o with the following line:

> 方法只不过是对象属性函数。如果有一个函数 f 和一个对象 o，可以用下面的代码给对象 o 定义一个名为 m 的方法：

```js
o.m = f;
```
Having defined the method m() of the object o, invoke it like this:

> 给对象 o 定义了方法 m()，用这种方式调用它：

```js
o.m();
```
Or, if m() expects two arguments, you might invoke it like this:

> 或者 m() 需要两个实参，可以这样调用它：

```js
o.m(x, y);
```
The code in this example is an invocation expression: it includes a function expression o.m and two argument expressions, x and y. The function expression is itself a property access expression, and this means that the function is invoked as a method rather than as a regular function.

> 示例中的代码是一个调用表达式：它包含一个函数表达式 o.m 和两个实参表达式 x 和 y。函数表达式本身是一个属性访问表达式，这意味着该函数被当作一个方法调用，而不是一个普通的函数。

The arguments and return value of a method invocation are handled exactly as described for regular function invocation. Method invocations differ from function invocations in one important way, however: the invocation context. Property access expressions consist of two parts: an object (in this case o) and a property name (m). In a method-invocation expression like this, the object o becomes the invocation context, and the function body can refer to that object by using the keyword this. Here is a concrete example:

> 对方法调用的参数和返回值的处理，和上面所描述的普通函数调用完全一致。但是，方法调用和函数调用有一个重要的区别，即：调用上下文。属性访问表达式由两部分组成：一个对象（本例中的 o）和属性名称（m）。在像这样的方法调用表达式里，对象 o 成为调用上下文，函数体可以使用关键字this引用该对象。下面是一个具体的例子：

```js
let calculator = { // An object literal
    operand1: 1,
    operand2: 1,
    add() {        // We're using method shorthand syntax for this function
        // Note the use of the this keyword to refer to the containing object.
        this.result = this.operand1 + this.operand2;
    }
};
calculator.add();  // A method invocation to compute 1+1.
calculator.result  // => 2
```
Most method invocations use the dot notation for property access, but property access expressions that use square brackets also cause method invocation. The following are both method invocations, for example:

> 大多数方法调用使用点符号来访问属性，使用方括号（属性访问表达式）也可以进行属性访问操作。下面两个例子都是函数调用：

```js
o["m"](x,y);   // Another way to write o.m(x,y).
a[0](z)        // Also a method invocation (assuming a[0] is a function).
```
Method invocations may also involve more complex property access expressions:

> 方法调用可能包括更复杂的属性访问表达式：

```js
customer.surname.toUpperCase(); // Invoke method on customer.surname
f().m();                        // Invoke method m() on return value of f()
```
Methods and the this keyword are central to the object-oriented programming paradigm. Any function that is used as a method is effectively passed an implicit argument—the object through which it is invoked. Typically, a method performs some sort of operation on that object, and the method-invocation syntax is an elegant way to express the fact that a function is operating on an object. Compare the following two lines:

> 方法和 this 关键字是面向对象编程范式的核心。任何函数只要作为方法调用实际上都会传入一个隐式的实参对象，就是调用这个方法对象本身。通常来讲，方法执行就是对象的某种操作，方法调用的语法也清晰的表达了它是操作对象的函数，比较下面两行代码：

```js
rect.setSize(width, height);
setRectSize(rect, width, height);
```
The hypothetical functions invoked in these two lines of code may perform exactly the same operation on the (hypothetical) object rect, but the method-invocation syntax in the first line more clearly indicates the idea that it is the object rect that is the primary focus of the operation.

> 我们假设这两行代码的功能完全一样，它们都作用于一个假定的对象 rect。可以看出，第一行的方法调用语法非常清晰地表明这个函数执行的载体是 rect 对象，函数中的所有操作都将基于这个对象。

#### METHOD CHAINING
When methods return objects, you can use the return value of one method invocation as part of a subsequent invocation. This results in a series (or “chain”) of method invocations as a single expression. When working with Promise-based asynchronous operations (see Chapter 13), for example, it is common to write code structured like this:

> 当方法返回一个对象，这个对象还可以再调用它的方法。这种方法调用序列中（或“链”）每次的调用结果都是另外一个表达式的组成部分。比如，基于 Promise 的异步操作（参见第 13 章），我们常常会这样写代码：

```js
// Run three asynchronous operations in sequence, handling errors.
doStepOne().then(doStepTwo).then(doStepThree).catch(handleErrors);
```
When you write a method that does not have a return value of its own, consider having the method return this. If you do this consistently throughout your API, you will enable a style of programming known as method chaining1 in which an object can be named once and then multiple methods can be invoked on it:

> 当方法并不需要返回值时，最好直接返回 this。如果在设计的 API 中一直采用这种方式，使用 API 就可以用方法链 ^1 风格的编程，在这种编程风格中，只要指定一次要调用的对象即可，余下的方法都可以基于此进行调用：

```js
new Square().x(100).y(100).size(50).outline("red").fill("blue").draw();
```
Note that this is a keyword, not a variable or property name. JavaScript syntax does not allow you to assign a value to this.

> 需要注意的是，this 是一个关键字，不是变量，也不是属性名。JavaScript 的语法不允许给 this 赋值。

The this keyword is not scoped the way variables are, and, except for arrow functions, nested functions do not inherit the this value of the containing function. If a nested function is invoked as a method, its this value is the object it was invoked on. If a nested function (that is not an arrow function) is invoked as a function, then its this value will be either the global object (non-strict mode) or undefined (strict mode). It is a common mistake to assume that a nested function defined within a method and invoked as a function can use this to obtain the invocation context of the method. The following code demonstrates the problem:

> 关键字 this 没有变量作用域的限制，除了箭头函数，嵌套函数不会从包含它的函数中继承 this。如果嵌套函数作为方法调用，其 this 的值指向调用它的对象。如果嵌套的函数作为函数调用（不包含箭头函数），其 this 值不是全局对象（非严格模式下）就是 undefined（严格模式下）。很多人误以为在一个方法中的函数声明并以函数调用的方式去执行可以用 this 来获取方法的执行上下文。下面这个例子说明了这个问题：

```js
let o = {                 // An object o.
    m: function() {       // Method m of the object.
        let self = this;  // Save the "this" value in a variable.
        this === o        // => true: "this" is the object o.
        f();              // Now call the helper function f().

        function f() {    // A nested function f
            this === o    // => false: "this" is global or undefined
            self === o    // => true: self is the outer "this" value.
        }
    }
};
o.m();                    // Invoke the method m on the object o.
```
Inside the nested function f(), the this keyword is not equal to the object o. This is widely considered to be a flaw in the JavaScript language, and it is important to be aware of it. The code above demonstrates one common workaround. Within the method m, we assign the this value to a variable self, and within the nested function f, we can use self instead of this to refer to the containing object.

> 嵌套函数 f() 中，this 关键之不等于对象 o。这被广泛的认为是 JavaScript 的一个缺陷，了解这一点是很是很重要的。上面的代码演示了一种常用的解决方案。在方法 m 中，将 this 值赋值给一个变量 self，在签到函数 f 中，可以用 self 代替 this 来引用包含它的对象。

In ES6 and later, another workaround to this issue is to convert the nested function f into an arrow function, which will properly inherit the this value:

> 在 ES6 之后，有另外一种解决方案来解决这个问题，将嵌套函数 f 转换成箭头函数，它会正确的继承 this 值：

```js
const f = () => {
    this === o  // true, since arrow functions inherit this
};
```
Functions defined as expressions instead of statements are not hoisted, so in order to make this code work, the function definition for f will need to be moved within the method m so that it appears before it is invoked.

> 函数表达式不像函数声明，声明提前，所以为了让这种解决方案定义的函数可以被调用，需要将 f 函数定义表达式放在方法 m 中，这样它才可以在它被调用时存在。

Another workaround is to invoke the bind() method of the nested function to define a new function that is implicitly invoked on a specified object:

> 另外还可以用嵌套函数的 bind() 方法，在指定对象上隐式调用一个新的函数：

```js
const f = (function() {
    this === o  // true, since we bound this function to the outer this
}).bind(this);
```
We’ll talk more about bind() in §8.7.5.

> 关于 bind() 方法将在 §8.7.5 中讲解。

### 8.2.3 Constructor Invocation
If a function or method invocation is preceded by the keyword new, then it is a constructor invocation. (Constructor invocations were introduced in §4.6 and §6.2.2, and constructors will be covered in more detail in Chapter 9.) Constructor invocations differ from regular function and method invocations in their handling of arguments, invocation context, and return value.

> 如果函数或者方法调用之前带有关键字 new，它就构成构造函数调用（构造函数调用在 §4.6 和 §6.2.2 节有简单介绍，第 9 章会对构造函数做更详细的讨论）。构造函数调用和普通的函数调用以及方法调用在实参处理、调用上下文和返回值方面都有不同。

If a constructor invocation includes an argument list in parentheses, those argument expressions are evaluated and passed to the function in the same way they would be for function and method invocations. It is not common practice, but you can omit a pair of empty parentheses in a constructor invocation. The following two lines, for example, are equivalent:

> 如果构造函数调用在圆括号内包含一组实参列表，先计算这些实参表达式，然后传入函数内，这和函数调用和方法调用是一致的。但如果构造函数没有形参，JavaScript 构造函数调用的语法是允许省略实参列表和圆括号的。凡是没有形参的构造函数调用都可以省略圆括号，比如，下面这两行代码就是等价的：

```js
o = new Object();
o = new Object;
```
A constructor invocation creates a new, empty object that inherits from the object specified by the prototype property of the constructor. Constructor functions are intended to initialize objects, and this newly created object is used as the invocation context, so the constructor function can refer to it with the this keyword. Note that the new object is used as the invocation context even if the constructor invocation looks like a method invocation. That is, in the expression new o.m(), o is not used as the invocation context.

> 构造函数调用创建一个新的空对象，这个对象继承自构造函数的 prototype 属性。构造函数试图初始化这个新创建的对象，并将这个对象用做其调用上下文，因此构造函数内可以使用 this 关键字来引用这个新创建的对象。注意，尽管构造函数看起来像一个方法调用，它依然会使用这个新对象作为调用上下文。也就是说，在表达式 new o.m() 中，调用上下文并不是 o。

Constructor functions do not normally use the return keyword. They typically initialize the new object and then return implicitly when they reach the end of their body. In this case, the new object is the value of the constructor invocation expression. If, however, a constructor explicitly uses the return statement to return an object, then that object becomes the value of the invocation expression. If the constructor uses return with no value, or if it returns a primitive value, that return value is ignored and the new object is used as the value of the invocation.

> 构造函数通常不使用 return 关键字，它们通常初始化新对象，当构造函数的函数体执行完毕时，它会隐式返回。在这种情况下，构造函数调用表达式的计算结果就是这个新对象的值。然而如果构造函数显式地使用 return 语句返回一个对象，那么调用表达式的值就是这个对象。如果构造函数使用 return 语句但没有指定返回值，或者返回一个原始值，那么这时将忽略返回值，同时使用这个新对象作为调用结果。

### 8.2.4 Indirect Invocation
JavaScript functions are objects, and like all JavaScript objects, they have methods. Two of these methods, call() and apply(), invoke the function indirectly. Both methods allow you to explicitly specify the this value for the invocation, which means you can invoke any function as a method of any object, even if it is not actually a method of that object. Both methods also allow you to specify the arguments for the invocation. The call() method uses its own argument list as arguments to the function, and the apply() method expects an array of values to be used as arguments. The call() and apply() methods are described in detail in §8.7.4.

> JavaScript 中的函数也是对象，和其他 JavaScript 对象没什么两样，函数对象也可以包含方法。其中的两个方法 call() 和 apply() 可以用来间接地调用函数。两个方法都允许显式指定调用所需的 this 值，也就是说，任何函数可以作为任何对象的方法来调用，哪怕这个函数不是那个对象的方法。两个方法都可以指定调用的实参。call() 方法使用它自有的实参列表作为函数的实参，apply() 方法则要求以数组的形式传入实参。§8.7.4 节会有关于 call() 和apply () 方法的详细讨论。

### 8.2.5 Implicit Function Invocation
There are various JavaScript language features that do not look like function invocations but that cause functions to be invoked. Be extra careful when writing functions that may be implicitly invoked, because bugs, side effects, and performance issues in these functions are harder to diagnose and fix than in regular functions for the simple reason that it may not be obvious from a simple inspection of your code when they are being called.

> 有各种各样的 JavaScript 语言特性，它们看起来不像函数调用但是却能调用函数。额外小心编写函数时可能会隐式调用，因为在隐式函数调用中 bug、副作用和性能问题都比普通的函数更难诊断和修复。

The language features that can cause implicit function invocation include:

> 可能引起函数隐式调用的语言特性包括：

If an object has getters or setters defined, then querying or setting the value of its properties may invoke those methods. See §6.10.6 for more information.

> 如果一个对象定义了 getter 或者 setter 方法，获取或者设置它的属性值可能调用这些方法。见 §6.10.6 有更多相关描述。

When an object is used in a string context (such as when it is concatenated with a string), its toString() method is called. Similarly, when an object is used in a numeric context, its valueOf() method is invoked. See §3.9.3 for details.

> 当对象用作一个字符串文本时（例如对象和一个字符串连接），它的 toString() 方法会被调用。同样的，对象用作一个数值型文本时，它的 valueOf() 方法被调用。详见 §3.9.3。

When you loop over the elements of an iterable object, there are a number of method calls that occur. Chapter 12 explains how iterators work at the function call level and demonstrates how to write these methods so that you can define your own iterable types.

> 当循环可迭代对象的元素时会产生很多方法调用。第 12 章介绍了迭代器在函数调用级别如何工作，并演示如何编写方法来定义自己的可迭代类型。

A tagged template literal is a function invocation in disguise. §14.5 demonstrates how to write functions that can be used in conjunction with template literal strings.

> 可以伪装在模板字面量中 。在 §14.5 中演示如何在模板字符串中调用函数。

Proxy objects (described in §14.7) have their behavior completely controlled by functions. Just about any operation on one of these objects will cause a function to be invoked.

> Proxy 对象（在 §14.7 中描述）的行为完全由函数控制。它的任何一个操作都会导致函数调用。

## 8.3 Function Arguments and Parameters
JavaScript function definitions do not specify an expected type for the function parameters, and function invocations do not do any type checking on the argument values you pass. In fact, JavaScript function invocations do not even check the number of arguments being passed. The subsections that follow describe what happens when a function is invoked with fewer arguments than declared parameters or with more arguments than declared parameters. They also demonstrate how you can explicitly test the type of function arguments if you need to ensure that a function is not invoked with inappropriate arguments.

> JavaScript 中的函数定义并未指定函数形参的类型，函数调用也未对传入的实参值做任何类型检查。实际上，JavaScript 函数调用甚至不检查传入形参的个数。下面几节将会讨论当调用函数时的实参个数和声明的形参个数不匹配时出现的状况，同样介绍了如何显式测试函数实参的类型，以避免非法的实参传入函数。

### 8.3.1 Optional Parameters and Defaults
When a function is invoked with fewer arguments than declared parameters, the additional parameters are set to their default value, which is normally undefined. It is often useful to write functions so that some arguments are optional. Following is an example:

> 当调用函数的时候传入的实参比函数声明时指定的形参个数要少，剩下的形参都将设置为 undefined 值。所以一些参数设置成可选的是非常实用的。看下面这个例子：

```js
// Append the names of the enumerable properties of object o to the
// array a, and return a.  If a is omitted, create and return a new array.
function getPropertyNames(o, a) {
    if (a === undefined) a = [];  // If undefined, use a new array
    for(let property in o) a.push(property);
    return a;
}

// getPropertyNames() can be invoked with one or two arguments:
let o = {x: 1}, p = {y: 2, z: 3};  // Two objects for testing
let a = getPropertyNames(o); // a == ["x"]; get o's properties in a new array
getPropertyNames(p, a);      // a == ["x","y","z"]; add p's properties to it
```
Instead of using an if statement in the first line of this function, you can use the || operator in this idiomatic way:

> 第一行代码中可以使用 || 运算符来代替一个 if 语句，这是一种习惯用法：

```js
a = a || [];
```
Recall from §4.10.2 that the || operator returns its first argument if that argument is truthy and otherwise returns its second argument. In this case, if any object is passed as the second argument, the function will use that object. But if the second argument is omitted (or null or another falsy value is passed), a newly created empty array will be used instead.

> 回忆一下，§4.10.2 介绍了“||”运算符，如果第一个实参是真值的话就返回第一个实参；否则返回第二个实参。在这个场景下，如果作为第二个实参传入任意对象，那么函数就会使用这个对象。如果省略掉第二个实参（或者传递 null 以及其他任何假值），那么就新创建一个空数组，并赋值给 a。

Note that when designing functions with optional arguments, you should be sure to put the optional ones at the end of the argument list so that they can be omitted. The programmer who calls your function cannot omit the first argument and pass the second: they would have to explicitly pass undefined as the first argument.

> 需要注意的是，当用这种可选实参来实现函数时，需要将可选实参放在实参列表的最后。那些调用你的函数的程序员是没办法省略第一个实参并传入第二个实参，他们必须显地的将 undefined 传入作为第一个实参 。

In ES6 and later, you can define a default value for each of your function parameters directly in the parameter list of your function. Simply follow the parameter name with an equals sign and the default value to use when no argument is supplied for that parameter:

> 在 ES6 之后，可以直接在函数的参数列表中为每个函数参数定义默认值。直接在参数名后面接一个等号再接一个默认值（用于没有实参提供给参数时参数的值）：

```js
// Append the names of the enumerable properties of object o to the
// array a, and return a.  If a is omitted, create and return a new array.
function getPropertyNames(o, a = []) {
    for(let property in o) a.push(property);
    return a;
}
```
Parameter default expressions are evaluated when your function is called, not when it is defined, so each time this getPropertyNames() function is invoked with one argument, a new empty array is created and passed.2 It is probably easiest to reason about functions if the parameter defaults are constants (or literal expressions like [] and {}). But this is not required: you can use variables, or function invocations, for example, to compute the default value of a parameter. One interesting case is that, for functions with multiple parameters, you can use the value of a previous parameter to define the default value of the parameters that follow it:

> 默认参数表达式只有在函数调用时进行计算，而不是在它定义时，所以每一次 getPropertyNames() 函数只传一个实参调用时，一个新的空数组被创建并传给参数。2 最容易理解的就是参数默认值是常量（或者字面量表达式 [] 和 {}）。但这并不是必须的：举个例子，你可以用变量或者函数调用，计算一个默认参数的值。一个很有趣的情况是，对于有多个参数的函数，可以用前面的参数值来定义后面的参数默认值。

```js
// This function returns an object representing a rectangle's dimensions.
// If only width is supplied, make it twice as high as it is wide.
const rectangle = (width, height=width*2) => ({width, height});
rectangle(1)  // => { width: 1, height: 2 }
```
This code demonstrates that parameter defaults work with arrow functions. The same is true for method shorthand functions and all other forms of function definitions.

> 这段代码描述了箭头函数中的参数默认值。方法函数和其他形式的函数定义也是如此。

### 8.3.2 Rest Parameters and Variable-Length Argument Lists
Parameter defaults enable us to write functions that can be invoked with fewer arguments than parameters. Rest parameters enable the opposite case: they allow us to write functions that can be invoked with arbitrarily more arguments than parameters. Here is an example function that expects one or more numeric arguments and returns the largest one:

> 调用函数时允许传入的实参比函数声明时指定的形参个数少。剩余参数允许相反的情况：它允许我们在调用函数时，传入比型参多任意个数的实参。下面是一个可以传入一个或多个数值型实参的例子，并且返回其中最大的数：

```js
function max(first=-Infinity, ...rest) {
    let maxValue = first; // Start by assuming the first arg is biggest
    // Then loop through the rest of the arguments, looking for bigger
    for(let n of rest) {
        if (n > maxValue) {
            maxValue = n;
        }
    }
    // Return the biggest
    return maxValue;
}

max(1, 10, 100, 2, 3, 1000, 4, 5, 6)  // => 1000
```
A rest parameter is preceded by three periods, and it must be the last parameter in a function declaration. When you invoke a function with a rest parameter, the arguments you pass are first assigned to the non-rest parameters, and then any remaining arguments (i.e., the “rest” of the arguments) are stored in an array that becomes the value of the rest parameter. This last point is important: within the body of a function, the value of a rest parameter will always be an array. The array may be empty, but a rest parameter will never be undefined. (It follows from this that it is never useful—and not legal—to define a parameter default for a rest parameter.)

> 剩余参数由三个 . 开始，必须是函数声明的最后一个参数。调用有剩余参数的函数时，传递的实参先赋值给非剩余参数，然后其余所有的实参（也就是“剩余”实参）存储在一个数组中变成剩余参数的值，最后一点非常重要：在一个函数体中，剩余参数的值总是一个数组。这个数组可能是空的，但是剩余参数永远不会是 undefined。（因此，从不会给剩余参数设置默认值，并且这也是不合法的。）

Functions like the previous example that can accept any number of arguments are called variadic functions, variable arity functions, or vararg functions. This book uses the most colloquial term, varargs, which dates to the early days of the C programming language.

> 类似这种函数可以接收任意个数的实参，这种函数也称为“不定实参函数”，这个术语源自古老的C语言。

Don’t confuse the ... that defines a rest parameter in a function definition with the ... spread operator, described in §8.3.4, which can be used in function invocations.

> 不要混淆 ... 定义函数的剩余参数和 ... 展开运算符，将在 §8.3.4 描述展开运算符在函数调用中的应用。

### 8.3.3 The Arguments Object
Rest parameters were introduced into JavaScript in ES6. Before that version of the language, varargs functions were written using the Arguments object: within the body of any function, the identifier arguments refers to the Arguments object for that invocation. The Arguments object is an array-like object (see §7.9) that allows the argument values passed to the function to be retrieved by number, rather than by name. Here is the max() function from earlier, rewritten to use the Arguments object instead of a rest parameter:

> 剩余参数是在 ES6 中加入的概念。在这之前，不定实参函数是用 Arguments 对象实现的：在函数体中，标识符 Arguments 是指向实参对象的引用。Arguments 对象是一个类数组对象（参照 §7.9），这样可以通过数字下标就能访问传入函数的实参值，而不用非要通过名字来得到实参。下面的 max() 函数就是以前用 Arguments 对象代替剩余参数的例子：

```js
function max(x) {
    let maxValue = -Infinity;
    // Loop through the arguments, looking for, and remembering, the biggest.
    for(let i = 0; i < arguments.length; i++) {
        if (arguments[i] > maxValue) maxValue = arguments[i];
    }
    // Return the biggest
    return maxValue;
}

max(1, 10, 100, 2, 3, 1000, 4, 5, 6)  // => 1000
```
The Arguments object dates back to the earliest days of JavaScript and carries with it some strange historical baggage that makes it inefficient and hard to optimize, especially outside of strict mode. You may still encounter code that uses the Arguments object, but you should avoid using it in any new code you write. When refactoring old code, if you encounter a function that uses arguments, you can often replace it with a ...args rest parameter. Part of the unfortunate legacy of the Arguments object is that, in strict mode, arguments is treated as a reserved word, and you cannot declare a function parameter or a local variable with that name.

> Arguments 对象可追溯到 JavaScript 的最早时代，并带有一些奇怪的历史包袱，这使得它效率低下且难以优化，尤其是不在严格模式下。可能还会遇到一些代码使用 Arguments 对象，但是在编写新代码时要避免使用，可以用 ... 剩余函数来替代。Arguments 对象还有部分令人遗憾的遗产，在严格模式下，arguments 被视为保留字，不能声明具有该名称的局部变量来定义函数的参数。

### 8.3.4 The Spread Operator for Function Calls
The spread operator ... is used to unpack, or “spread out,” the elements of an array (or any other iterable object, such as strings) in a context where individual values are expected. We’ve seen the spread operator used with array literals in §7.1.2. The operator can be used, in the same way, in function invocations:

> 当需要单个值时，... 展开运算符用来拆包，或者说将元素从数组（或者其他的任何和迭代对象，例如字符串）中“展开”到上下文。我们已经在 §7.1.2 见到了展开运算符在数组字面量上的使用。展开运算符可以在函数调用中以同样方式使用：

```js
let numbers = [5, 2, 10, -1, 9, 100, 1];
Math.min(...numbers)  // => -1
```
Note that ... is not a true operator in the sense that it cannot be evaluated to produce a value. Instead, it is a special JavaScript syntax that can be used in array literals and function invocations.

> 注意 ... 不是一个真正的运算符，因为它不能通过计算来提供一个值。它是一个可以用在数组字面量和函数调用中的特殊的 JavaScript 语法。

When we use the same ... syntax in a function definition rather than a function invocation, it has the opposite effect to the spread operator. As we saw in §8.3.2, using ... in a function definition gathers multiple function arguments into an array. Rest parameters and the spread operator are often useful together, as in the following function, which takes a function argument and returns an instrumented version of the function for testing: 

> 在函数定义和函数调用中使用相同的 ... 语法时，和展开运算符有着相仿的效果。在 §8.3.2 中我们看到函数定义使用 ... 将复数个函数实参合并到一个数组中。剩余参数和展开运算符经常一同使用，就像下面这个函数：

```js
// This function takes a function and returns a wrapped version
function timed(f) {
    return function(...args) {  // Collect args into a rest parameter array
        console.log(`Entering function ${f.name}`);
        let startTime = Date.now();
        try {
            // Pass all of our arguments to the wrapped function
            return f(...args);  // Spread the args back out again
        }
        finally {
            // Before we return the wrapped return value, print elapsed time.
            console.log(`Exiting ${f.name} after ${Date.now()-startTime}ms`);
        }
    };
}

// Compute the sum of the numbers between 1 and n by brute force
function benchmark(n) {
    let sum = 0;
    for(let i = 1; i <= n; i++) sum += i;
    return sum;
}

// Now invoke the timed version of that test function
timed(benchmark)(1000000) // => 500000500000; this is the sum of the numbers
```
### 8.3.5 Destructuring Function Arguments into Parameters
When you invoke a function with a list of argument values, those values end up being assigned to the parameters declared in the function definition. This initial phase of function invocation is a lot like variable assignment. So it should not be surprising that we can use the techniques of destructuring assignment (see §3.10.3) with functions.

> 用实参列表调用函数时，实参的值最终赋值给函数定义的参数。函数调用初始化阶段非常像变量赋值。所以我们不必惊讶于可以将解构赋值（见 §3.10.3）用于函数。

If you define a function that has parameter names within square brackets, you are telling the function to expect an array value to be passed for each pair of square brackets. As part of the invocation process, the array arguments will be unpacked into the individually named parameters. As an example, suppose we are representing 2D vectors as arrays of two numbers, where the first element is the X coordinate and the second element is the Y coordinate. With this simple data structure, we could write the following function to add two vectors:

> 如果一个函数的参数带有方括号，就说明函数要给每一个方括号传一个数组。在一个调用进程中，数组实参会被拆包传递给对应的参数。例如，假设我们将 2D 矢量表示为两个数字的数组，其中第一个元素是 X 坐标，第二个元素是 Y 坐标。用这个简单的数据结构，编写下面这个函数计算两个矢量的和：

```js
function vectorAdd(v1, v2) {
    return [v1[0] + v2[0], v1[1] + v2[1]];
}
vectorAdd([1,2], [3,4])  // => [4,6]
```
The code would be easier to understand if we destructured the two vector arguments into more clearly named parameters:

> 如果下面这种方式解构这两个矢量实参，这段代码将更容易理解：

```js
function vectorAdd([x1,y1], [x2,y2]) { // Unpack 2 arguments into 4 parameters
    return [x1 + x2, y1 + y2];
}
vectorAdd([1,2], [3,4])  // => [4,6]
```
Similarly, if you are defining a function that expects an object argument, you can destructure parameters of that object. Let’s use a vector example again, except this time, let’s suppose that we represent vectors as objects with x and y parameters:

> 同样，如果定义一个函数时需要对象实参，你能对这个对象进行参数解构。再次实用矢量的例子，这一次，我们用 x 和 y 参数包装成对象来描述矢量：

```js
// Multiply the vector {x,y} by a scalar value
function vectorMultiply({x, y}, scalar) {
    return { x: x*scalar, y: y*scalar };
}
vectorMultiply({x: 1, y: 2}, 2)  // => {x: 2, y: 4}
```
This example of destructuring a single object argument into two parameters is a fairly clear one because the parameter names we use match the property names of the incoming object. The syntax is more verbose and more confusing when you need to destructure properties with one name into parameters with different names. Here’s the vector addition example, implemented for object-based vectors:

> 这个例子将一个简单的对象实参解构成两个参数是很简单的，因为参数的名字和我们在对象中使用的属性名是匹配的。当您需要将同一个名称的属性解构为具有不同名称的参数时，语法更加冗长和难懂。下面是一个矢量加法的例子，基于对象矢量的实现：

```js
function vectorAdd(
    {x: x1, y: y1}, // Unpack 1st object into x1 and y1 params
    {x: x2, y: y2}  // Unpack 2nd object into x2 and y2 params
)
{
    return { x: x1 + x2, y: y1 + y2 };
}
vectorAdd({x: 1, y: 2}, {x: 3, y: 4})  // => {x: 4, y: 6}
```
The tricky thing about destructuring syntax like {x:x1, y:y1} is remembering which are the property names and which are the parameter names. The rule to keep in mind for destructuring assignment and destructuring function calls is that the variables or parameters being declared go in the spots where you’d expect values to go in an object literal. So property names are always on the lefthand side of the colon, and the parameter (or variable) names are on the right.

> 像 {x:x1, y:y1} 的解构语法棘手的是记住哪一个是属性名哪一个是参数名。牢记解构赋值和解构函数调用的规则，声明的变量或参数在对象字面量中的位置固定。属性名总是在冒号的左边，参数（或变量）名在右边。

You can define parameter defaults with destructured parameters. Here’s vector multiplication that works with 2D or 3D vectors:

> 可以使用解构参数定义参数默认值。下面是适用于 2D 或 3D 矢量的矢量乘法：

```js
// Multiply the vector {x,y} or {x,y,z} by a scalar value
function vectorMultiply({x, y, z=0}, scalar) {
    return { x: x*scalar, y: y*scalar, z: z*scalar };
}
vectorMultiply({x: 1, y: 2}, 2)  // => {x: 2, y: 4, z: 0}
```
Some languages (like Python) allow the caller of a function to invoke a function with arguments specified in name=value form, which is convenient when there are many optional arguments or when the parameter list is long enough that it is hard to remember the correct order. JavaScript does not allow this directly, but you can approximate it by destructuring an object argument into your function parameters. Consider a function that copies a specified number of elements from one array into another array with optionally specified starting offsets for each array. Since there are five possible parameters, some of which have defaults, and it would be hard for a caller to remember which order to pass the arguments in, we can define and invoke the arraycopy() function like this:

> 一些语言（像 Python）允许函数的调用者以 name=value 型式指定实参，这在有很多可选实参或者参数列表长到难以记住正确的顺序时是非常方便的。JavaScript 不允许直接这样做，但可以通过解构对象实参到函数参数中。构思一个函数将指定数量的元素从一个数组复制到另一个数组中，可以随意地为每个数组指定起始偏移量。如下有五个可传入参数，其中一些有默认值，并且调用者很难记住参数的顺序来传递实参，可以像这样定义和调用 arraycopy() 方法：

```js
function arraycopy({from, to=from, n=from.length, fromIndex=0, toIndex=0}) {
    let valuesToCopy = from.slice(fromIndex, fromIndex + n);
    to.splice(toIndex, 0, ...valuesToCopy);
    return to;
}
let a = [1,2,3,4,5], b = [9,8,7,6,5];
arraycopy({from: a, n: 3, to: b, toIndex: 4}) // => [9,8,7,6,1,2,3,5]
```
When you destructure an array, you can define a rest parameter for extra values within the array that is being unpacked. That rest parameter within the square brackets is completely different than the true rest parameter for the function:

> 当解构一个数组，在其被拆包时，可以定义一个剩余参数将其余值放在数组中。 在方括号中的剩余参数和真正的函数中的剩余参数是完全不同的：

```js
// This function expects an array argument. The first two elements of that
// array are unpacked into the x and y parameters. Any remaining elements
// are stored in the coords array. And any arguments after the first array
// are packed into the rest array.
function f([x, y, ...coords], ...rest) {
    return [x+y, ...rest, ...coords];  // Note: spread operator here
}
f([1, 2, 3, 4], 5, 6)   // => [3, 5, 6, 3, 4]
```
In ES2018, you can also use a rest parameter when you destructure an object. The value of that rest parameter will be an object that has any properties that did not get destructured. Object rest parameters are often useful with the object spread operator, which is also a new feature of ES2018:

> 在 ES2018，也可以用剩余参数解构对象。剩余参数是一个没有解构的属性的对象。对象剩余参数经常与对象展开运算符连用，这是 ES2018 的新特性：

```js
// Multiply the vector {x,y} or {x,y,z} by a scalar value, retain other props
function vectorMultiply({x, y, z=0, ...props}, scalar) {
    return { x: x*scalar, y: y*scalar, z: z*scalar, ...props };
}
vectorMultiply({x: 1, y: 2, w: -1}, 2)  // => {x: 2, y: 4, z: 0, w: -1}
```
Finally, keep in mind that, in addition to destructuring argument objects and arrays, you can also destructure arrays of objects, objects that have array properties, and objects that have object properties, to essentially any depth. Consider graphics code that represents circles as objects with x, y, radius, and color properties, where the color property is an array of red, green, and blue color components. You might define a function that expects a single circle object to be passed to it but destructures that circle object into six separate parameters:

> 最后，请记住，除了可以解构实参对象和数组，也可以解构数组对象，对象有数组属性，并且对象还有对象的属性。构思一个将圆表示为具有 x、y、半径和颜色属性的对象的图形代码，颜色属性是一个数组由 RGB 组成。你可以定义一个函数，该函数希望将单个圆对象传递给它，但其解构为六个单独的参数：

```js
function drawCircle({x, y, radius, color: [r, g, b]}) {
    // Not yet implemented
}
```
If function argument destructuring is any more complicated than this, I find that the code becomes harder to read, rather than simpler. Sometimes, it is clearer to be explicit about your object property access and array indexing.

> 如果函数实参解构比这更复杂，代码会变得更难读，而不是更简单。有时，显示地对对象属性访问和数组索引会让代码更清晰。

### 8.3.6 Argument Types
JavaScript method parameters have no declared types, and no type checking is performed on the values you pass to a function. You can help make your code self-documenting by choosing descriptive names for function arguments and by documenting them carefully in the comments for each function. (Alternatively, see §17.8 for a language extension that allows you to layer type checking on top of regular JavaScript.)

> JavaScript 方法的形参并未声明类型，在形参传入函数体之前也未做任何类型检查。可以采用语义化的单词来给函数实参命名，并在函数注释给每一个实参详细描述，以此使代码自文本化。

As described in §3.9, JavaScript performs liberal type conversion as needed. So if you write a function that expects a string argument and then call that function with a value of some other type, the value you passed will simply be converted to a string when the function tries to use it as a string. All primitive types can be converted to strings, and all objects have toString() methods (if not necessarily useful ones), so an error never occurs in this case.

> §3.9 已经提到，JavaScript 在必要时会进行类型转换。因此如果函数期 望接收一个字符串实参，而调用函数时传入其他类型的值，所传入的值会在函数体内将其用做字符串的地方转换为字符串类型。所有的原始类型都可以转换为字符串，所有的对象都包含 toString() 方法（尽管不一定有用），所以这种场景下是不会有任何错误的。

This is not always true, however. Consider again the arraycopy() method shown earlier. It expects one or two array arguments and will fail if these arguments are of the wrong type. Unless you are writing a private function that will only be called from nearby parts of your code, it may be worth adding code to check the types of arguments like this. It is better for a function to fail immediately and predictably when passed bad values than to begin executing and fail later with an error message that is likely to be unclear. Here is an example function that performs type-checking:

> 然而事情不总是这样，回头看一下刚才提到的 arraycopy() 方法。这个方法期望获得一个或两个实参，并且这些实参的类型错误会导致函数执行失败。除非所写的私有函数只会被附近的代码调用，你应当添加类似的实参类型检查逻辑。因为宁愿程序在传入非法值时报错，也不愿非法值导致程序在执行时报错，相比而言，逻辑执行时的报错消息不甚清晰且更难处理。下面这个例子中的函数就做了这种类型检查：

```js
// Return the sum of the elements an iterable object a.
// The elements of a must all be numbers.
function sum(a) {
    let total = 0;
    for(let element of a) { // Throws TypeError if a is not iterable
        if (typeof element !== "number") {
            throw new TypeError("sum(): elements must be numbers");
        }
        total += element;
    }
    return total;
}
sum([1,2,3])    // => 6
sum(1, 2, 3);   // !TypeError: 1 is not iterable
sum([1,2,"3"]); // !TypeError: element 2 is not a number
```
## 8.4 Functions as Values
The most important features of functions are that they can be defined and invoked. Function definition and invocation are syntactic features of JavaScript and of most other programming languages. In JavaScript, however, functions are not only syntax but also values, which means they can be assigned to variables, stored in the properties of objects or the elements of arrays, passed as arguments to functions, and so on.3

> 函数可以定义，也可以调用，这是函数最重要的特性。函数定义和调用是  JavaScript 的词法特性，对于其他大多数编程语言来说亦是如此。然而在 JavaScript 中，函数不仅是一种语法，也是值，也就是说，可以将函数赋值给变量，存储在对象的属性或数组的元素中，作为参数传入另外一个函数等。3

To understand how functions can be JavaScript data as well as JavaScript syntax, consider this function definition:

> 为了便于理解 JavaScript 中的函数是如何用做 Javascript 数据以及 JavaScript 语法的，来看一下这样一个函数定义：

```js
function square(x) { return x*x; }
```
This definition creates a new function object and assigns it to the variable square. The name of a function is really immaterial; it is simply the name of a variable that refers to the function object. The function can be assigned to another variable and still work the same way:

> 这个定义创建一个新的函数对象，并将其赋值给变量 square。函数的名字实际上是无形的，它（square）仅仅是变量的名称，这个变量是函数对象的引用。函数还可以赋值给其他的变量，并且仍可以正常工作：

```js
let s = square;  // Now s refers to the same function that square does
square(4)        // => 16
s(4)             // => 16
```
Functions can also be assigned to object properties rather than variables. As we’ve already discussed, we call the functions “methods” when we do this:

> 除了可以将函数赋值给变量，同样可以将函数赋值给对象的属性。当函数作为对象的属性调用时，函数就称为“方法”：

```js
let o = {square: function(x) { return x*x; }}; // An object literal
let y = o.square(16);                          // y == 256
```
Functions don’t even require names at all, as when they’re assigned to array elements:

> 函数甚至不需要带名字，就像把它们赋值给数组元素：

```js
let a = [x => x*x, 20]; // An array literal
a[0](a[1])              // => 400
```
The syntax of this last example looks strange, but it is still a legal function invocation expression!

> 上面的例子看起来很奇怪，但的确是合法的函数调用表达式！

As an example of how useful it is to treat functions as values, consider the Array.sort() method. This method sorts the elements of an array. Because there are many possible orders to sort by (numerical order, alphabetical order, date order, ascending, descending, and so on), the sort() method optionally takes a function as an argument to tell it how to perform the sort. This function has a simple job: for any two values it is passed, it returns a value that specifies which element would come first in a sorted array. This function argument makes Array.sort() perfectly general and infinitely flexible; it can sort any type of data into any conceivable order. Examples are shown in §7.8.6.

> 举一个例子来说明将函数当作值来对待的益处，考虑下 Array.sort() 方法。这个方法用来对数组元素进行排序。因为排序的规则有很多（基于数值大小、字母表顺序、日期大小、从小到大、从大到小等），sort() 方法可以接收一个函数作为参数，用来处理具体的排序操作。这个函数的作用非常简单：对于任意两个值都返回一个值，以指定它们在排序后的数组中的先后顺序。这个函数参数使得 Array.sort() 具有更完美的通用性和无限可扩展性，它可以对任何类型的数据进行任意排序。§7.8.6 有示例代码。

Example 8-1 demonstrates the kinds of things that can be done when functions are used as values. This example may be a little tricky, but the comments explain what is going on.

> 示例 8-1 展示了将函数用做值时的一些例子，这段代码可能会难读一些，但注释解释了代码的具体含义：

Example 8-1. Using functions as data

> 示例 8-1：用函数做值

```js
// We define some simple functions here
function add(x,y) { return x + y; }
function subtract(x,y) { return x - y; }
function multiply(x,y) { return x * y; }
function divide(x,y) { return x / y; }

// Here's a function that takes one of the preceding functions
// as an argument and invokes it on two operands
function operate(operator, operand1, operand2) {
    return operator(operand1, operand2);
}

// We could invoke this function like this to compute the value (2+3) + (4*5):
let i = operate(add, operate(add, 2, 3), operate(multiply, 4, 5));

// For the sake of the example, we implement the simple functions again,
// this time within an object literal;
const operators = {
    add:      (x,y) => x+y,
    subtract: (x,y) => x-y,
    multiply: (x,y) => x*y,
    divide:   (x,y) => x/y,
    pow:      Math.pow  // This works for predefined functions too
};

// This function takes the name of an operator, looks up that operator
// in the object, and then invokes it on the supplied operands. Note
// the syntax used to invoke the operator function.
function operate2(operation, operand1, operand2) {
    if (typeof operators[operation] === "function") {
        return operators[operation](operand1, operand2);
    }
    else throw "unknown operator";
}

operate2("add", "hello", operate2("add", " ", "world")) // => "hello world"
operate2("pow", 10, 2)  // => 100
```
### 8.4.1 Defining Your Own Function Properties
Functions are not primitive values in JavaScript, but a specialized kind of object, which means that functions can have properties. When a function needs a “static” variable whose value persists across invocations, it is often convenient to use a property of the function itself. For example, suppose you want to write a function that returns a unique integer whenever it is invoked. The function must never return the same value twice. In order to manage this, the function needs to keep track of the values it has already returned, and this information must persist across function invocations. You could store this information in a global variable, but that is unnecessary, because the information is used only by the function itself. It is better to store the information in a property of the Function object. Here is an example that returns a unique integer whenever it is called:

> JavaScript 中的函数并不是原始值，而是一种特殊的对象，也就是说，函数可以拥有属性。当函数需要一个“静态”变量来在调用时保持某个值不变，最方便的方式就是给函数定义属性，而不是定义全局变量，显然定义全局变量会让命名空间变得更加杂乱无章。比如，假设你想写一个返回一个唯一整数的函数，不管在哪里调用函数都会返回这个整数。而函数不能两次返回同一个值，为了做到这一点，函数必须能够跟踪它每次返回的值，而且这些值的信息需要在不同的函数调过程中持久化。可以将这些信息存放到全局变量中，但这并不是必需的，因为这个信息仅仅是函数本身用到的。最好将这个信息保存到函数对象的一个属性中，下面这个例子就实现了这样一个函数，每次调用函数都会返回一个唯一的整数：

```js
// Initialize the counter property of the function object.
// Function declarations are hoisted so we really can
// do this assignment before the function declaration.
uniqueInteger.counter = 0;

// This function returns a different integer each time it is called.
// It uses a property of itself to remember the next value to be returned.
function uniqueInteger() {
    return uniqueInteger.counter++;  // Return and increment counter property
}
uniqueInteger()  // => 0
uniqueInteger()  // => 1
```
As another example, consider the following factorial() function that uses properties of itself (treating itself as an array) to cache previously computed results:

> 来看另外一个例子，下面这个函数 factorial() 使用了自身的属性（将自身当做数组来对待）来缓存上一次的计算结果：

```js
// Compute factorials and cache results as properties of the function itself.
function factorial(n) {
    if (Number.isInteger(n) && n > 0) {           // Positive integers only
        if (!(n in factorial)) {                  // If no cached result
            factorial[n] = n * factorial(n-1);    // Compute and cache it
        }
        return factorial[n];                      // Return the cached result
    } else {
        return NaN;                               // If input was bad
    }
}
factorial[1] = 1;  // Initialize the cache to hold this base case.
factorial(6)  // => 720
factorial[5]  // => 120; the call above caches this value
```
## 8.5 Functions as Namespaces
Variables declared within a function are not visible outside of the function. For this reason, it is sometimes useful to define a function simply to act as a temporary namespace in which you can define variables without cluttering the global namespace.

> 变量声明在函数内对于函数体外是不可见的。因此，有时定义函数作为临时命名空间非常有用，您可以在其中定义变量而不弄乱全局命名空间。

Suppose, for example, you have a chunk of JavaScript code that you want to use in a number of different JavaScript programs (or, for client-side JavaScript, on a number of different web pages). Assume that this code, like most code, defines variables to store the intermediate results of its computation. The problem is that since this chunk of code will be used in many different programs, you don’t know whether the variables it creates will conflict with variables created by the programs that use it. The solution is to put the chunk of code into a function and then invoke the function. This way, variables that would have been global become local to the function:

> 比如，假设你写了一段 JavaScript 模块代码，这段代码将要用在不同的 JavaScript 程序中（对于客户端 JavaScript 来讲通常是用在各种各样的网页中）。和大多数代码一样，假定这段代码定义了一个用以存储中间计算结果的变量。这样问题就来了，当模块代码放到不同的程序中运行时，你无法得知这个变量是否已经创建了，如果已经存在这个变量，那么将会和代码发生冲突。解决办法当然是将代码放入一个函数内，然后调用这个函数。这样全局变量就变成了函数内的局部变量：

```js
function chunkNamespace() {
    // Chunk of code goes here
    // Any variables defined in the chunk are local to this function
    // instead of cluttering up the global namespace.
}
chunkNamespace();  // But don't forget to invoke the function!
```
This code defines only a single global variable: the function name chunkNamespace. If defining even a single property is too much, you can define and invoke an anonymous function in a single expression:

> 这段代码仅仅定义了一个单独的全局变量：名为 chunkNamespace 的函数。如果还是太麻烦，可以用一个单独的表达式定义一个匿名函数并调用它：

```js
(function() {  // chunkNamespace() function rewritten as an unnamed expression.
    // Chunk of code goes here
}());          // End the function literal and invoke it now.
```
This technique of defining and invoking a function in a single expression is used frequently enough that it has become idiomatic and has been given the name “immediately invoked function expression.” Note the use of parentheses in the previous code example. The open parenthesis before function is required because without it, the JavaScript interpreter tries to parse the function keyword as a function declaration statement. With the parenthesis, the interpreter correctly recognizes this as a function definition expression. The leading parenthesis also helps human readers recognize when a function is being defined to be immediately invoked instead of defined for later use.

> 这种定义匿名函数并立即在单个表达式中调用它的写法非常常见，并给它起了个名字“匿名调用函数表达式”。注意上面代码的圆括号的用法，function 之前的左圆括号是必需的，因为如果不写这个左圆括号，JavaScript 解释器会试图将关键字 function 解析为函数声明语句。使用圆括号 JavaScript 解释器才会正确地将其解析为函数定义表达式。使用前导括号也有助于人类阅读时区分函数定义是立即执行还是供以后使用。

This use of functions as namespaces becomes really useful when we define one or more functions inside the namespace function using variables within that namesapce, but then pass them back out as the return value of the namespace function. Functions like this are known as closures, and they’re the topic of the next section.

> 函数用作命名空间很常用，在命名空间函数中定义一个或多个函数使用其中的变量，然后将他们作为函数命名空间的返回值。这样的函数称为闭包，它们是下一节的主题。

## 8.6 Closures
Like most modern programming languages, JavaScript uses lexical scoping. This means that functions are executed using the variable scope that was in effect when they were defined, not the variable scope that is in effect when they are invoked. In order to implement lexical scoping, the internal state of a JavaScript function object must include not only the code of the function but also a reference to the scope in which the function definition appears. This combination of a function object and a scope (a set of variable bindings) in which the function’s variables are resolved is called a closure in the computer science literature.

> 和其他大多数现代编程语言一样，JavaScript 也采用词法作用域。也就是说，函数的执行依赖于变量作用域，这个作用域是在函数定义时决定的，而不是函数调用时决定的。为了实现这种词法作用域，JavaScript 函数对象的内部状态不仅包含函数的代码逻辑，还必须包括对函数定义出现的作用域的引用。将函数对象可和作用域相互关联起来（一对变量的绑定），函数体内部的变量都可以保存在函数作用域内，这种特性在计算机科学文献中称为闭包。

Technically, all JavaScript functions are closures, but because most functions are invoked from the same scope that they were defined in, it normally doesn’t really matter that there is a closure involved. Closures become interesting when they are invoked from a different scope than the one they were defined in. This happens most commonly when a nested function object is returned from the function within which it was defined. There are a number of powerful programming techniques that involve this kind of nested function closures, and their use has become relatively common in JavaScript programming. Closures may seem confusing when you first encounter them, but it is important that you understand them well enough to use them comfortably.

> 从技术的角度讲，所有的 JavaScript 函数都是闭包，但是大多数函数调用和定义在同一个作用域内，通常不会注意这里有涉及到闭包。当调用函数不和其定义处于同一作用域内时，事情就变得非常微妙。当一个函数嵌套了另外一个函数，外部函数将嵌套的函数对象作为返回值返回的时候往往会发生这种事情。有很多强大的编程技术都利用到了这类嵌套的函数闭包，以至于这种编程模式在 JavaScript 中非常常见。当你第一次碰到闭包时可能会觉得非常让人费解，一旦你理解掌握了闭包之后，就能非常自如地使用它了，了解这一点至关重要。

The first step to understanding closures is to review the lexical scoping rules for nested functions. Consider the following code:

> 理解闭包首先要了解嵌套函数的词法作用域规则。看一下这段代码：

```js
let scope = "global scope";          // A global variable
function checkscope() {
    let scope = "local scope";       // A local variable
    function f() { return scope; }   // Return the value in scope here
    return f();
}
checkscope()                         // => "local scope"
```
The checkscope() function declares a local variable and then defines and invokes a function that returns the value of that variable. It should be clear to you why the call to checkscope() returns “local scope”. Now, let’s change the code just slightly. Can you tell what this code will return?

> checkscope() 函数声明了一个局部变量，然后定义并执行了一个函数 f() ，函数 f() 返回了这个变量的值，最后将函数 f() 的执行结果返回。你应当非常清楚为什么调用 checkscope() 会返回 local scope。现在我们对这段代码做一点改动。你知道这段代码返回什么吗？

```js
let scope = "global scope";          // A global variable
function checkscope() {
    let scope = "local scope";       // A local variable
    function f() { return scope; }   // Return the value in scope here
    return f;
}
let s = checkscope()();              // What does this return?
```
In this code, a pair of parentheses has moved from inside checkscope() to outside of it. Instead of invoking the nested function and returning its result, checkscope() now just returns the nested function object itself. What happens when we invoke that nested function (with the second pair of parentheses in the last line of code) outside of the function in which it was defined?

> 在这段代码中，我们将函数内的一对圆括号移动到了 checkscope() 之后。checkscope() 现在仅仅返回函数内嵌套的一个函数对象，而不是直接返回结果。在定义函数的作用域外面，调用这个嵌套的函数（包含最后一行代码的最后一对圆括号）会发生什么事情呢？

Remember the fundamental rule of lexical scoping: JavaScript functions are executed using the scope they were defined in. The nested function f() was defined in a scope where the variable scope was bound to the value “local scope”. That binding is still in effect when f is executed, no matter where it is executed from. So the last line of the preceding code example returns “local scope”, not “global scope”. This, in a nutshell, is the surprising and powerful nature of closures: they capture the local variable (and parameter) bindings of the outer function within which they are defined.

> 回想一下词法作用域的基本规则：JavaScript 函数的执行用到了作用域，这个作用域是函数定义的时候创建的。嵌套的函数 f() 定义在变量 scope 绑定的值是“local scope”的作用域里，这个绑定无论 f 函数在何处调用都依然有效。因此最后一行代码返回“local scope”，而不是“global scope”。简言之，闭包的这个特性强大到让人吃惊：它们可以捕捉到它们的外部函数所绑定的局部变量（和参数）。

In §8.4.1, we defined a uniqueInteger() function that used a property of the function itself to keep track of the next value to be returned. A shortcoming of that approach is that buggy or malicious code could reset the counter or set it to a noninteger, causing the uniqueInteger() function to violate the “unique” or the “integer” part of its contract. Closures capture the local variables of a single function invocation and can use those variables as private state. Here is how we could rewrite the uniqueInteger() using an immediately invoked function expression to define a namespace and a closure that uses that namespace to keep its state private:

> 在 §8.4.1 中定义了 uniqueInteger() 函数，这个函数使用自身的一个属性来保存每次返回的值，以便每次调用都能跟踪上次的返回值。但这种做法有一个问题，就是恶意代码可能将计数器重置或者把一个非整数赋值给它，导致 uniquenterger() 函数不一定能产生“唯一”的“整数”。而闭包可以捕捉到单个函数调用的局部变量，并将这些局部变量用做私有状态。下面是如何用立即调用函数表达式重写 uniqueInteger() 来定义命名空间和闭包来保持其状态私有化：

```js
let uniqueInteger = (function() {  // Define and invoke
    let counter = 0;               // Private state of function below
    return function() { return counter++; };
}());
uniqueInteger()  // => 0
uniqueInteger()  // => 1
```
In order to understand this code, you have to read it carefully. At first glance, the first line of code looks like it is assigning a function to the variable uniqueInteger. In fact, the code is defining and invoking (as hinted by the open parenthesis on the first line) a function, so it is the return value of the function that is being assigned to uniqueInteger. Now, if we study the body of the function, we see that its return value is another function. It is this nested function object that gets assigned to uniqueInteger. The nested function has access to the variables in its scope and can use the counter variable defined in the outer function. Once that outer function returns, no other code can see the counter variable: the inner function has exclusive access to it.

> 你需要仔细阅读这段代码才能理解其含义。粗略来看，第一行代码看起来像将函数赋值给一个变量 uniqueInteger，实际上，这段代码定义了一个立即调用的函数（函数的开始带有左圆括号），因此是这个函数的返回值赋值给变量 uniqueInteger。现在，我们来看函数体，这个函数的返回值是另外一个函数。这是一个嵌套的函数，我们将它赋值给变量 uniqueInteger。嵌套的函数是可以访问作用域内的变量的，而且可以访问外部函数中定义的 counter 变量。当外部函数返回之后，其他任何代码都无法访问 counter 变量：只有内部的函数才能访问到它。

Private variables like counter need not be exclusive to a single closure: it is perfectly possible for two or more nested functions to be defined within the same outer function and share the same scope. Consider the following code:

> 像 counter 一样的私有变量不是只能用在一个单独的闭包内，在同一个外部函数内定义的多个嵌套函数也可以访问它，这多个嵌套函数都共享一个作用域，看一下这段代码：

```js
function counter() {
    let n = 0;
    return {
        count: function() { return n++; },
        reset: function() { n = 0; }
    };
}

let c = counter(), d = counter();   // Create two counters
c.count()                           // => 0
d.count()                           // => 0: they count independently
c.reset();                          // reset() and count() methods share state
c.count()                           // => 0: because we reset c
d.count()                           // => 1: d was not reset
```
The counter() function returns a “counter” object. This object has two methods: count() returns the next integer, and reset() resets the internal state. The first thing to understand is that the two methods share access to the private variable n. The second thing to understand is that each invocation of counter() creates a new scope—independent of the scopes used by previous invocations—and a new private variable within that scope. So if you call counter() twice, you get two counter objects with different private variables. Calling count() or reset() on one counter object has no effect on the other.

> counter() 函数返回了一个“计数器”对象，这个对象包含两个方法：count() 返回下一个整数，reset() 重置内部状态。首先要理解，这两个方法都可以访问私有变量n。再者，每次调用 counter() 都会创建一个新的作用域链和一个新的私有变量。因此，如果调用 counter() 两次，则会得到两个计数器对象，而且彼此包含不同的私有变量，调用其中一个计数器对象的 count() 或 reset() 不会影响到另外一个对象。

It is worth noting here that you can combine this closure technique with property getters and setters. The following version of the counter() function is a variation on code that appeared in §6.10.6, but it uses closures for private state rather than relying on a regular object property:

> 从技术角度看，其实可以将这个闭包合并为属性存取器方法 getter 和 setter。下面这段代码所示的 counter() 函数的版本是 §6.10.6 中代码的变种，所不同的是，这里私有状态的实现是利用了闭包，而不是利用普通的对象属性来实现：

```js
function counter(n) {  // Function argument n is the private variable
    return {
        // Property getter method returns and increments private counter var.
        get count() { return n++; },
        // Property setter doesn't allow the value of n to decrease
        set count(m) {
            if (m > n) n = m;
            else throw Error("count can only be set to a larger value");
        }
    };
}

let c = counter(1000);
c.count            // => 1000
c.count            // => 1001
c.count = 2000;
c.count            // => 2000
c.count = 2000;    // !Error: count can only be set to a larger value
```
Note that this version of the counter() function does not declare a local variable but just uses its parameter n to hold the private state shared by the property accessor methods. This allows the caller of counter() to specify the initial value of the private variable.

> 需要注意的是，这个版本的 counter() 函数并未声明局部变量，而只是使用参数 n 来保存私有状态并与属性存取器方法共享。这样的话，调用 counter() 的函数就可以指定私有变量的初始值了。

Example 8-2 is a generalization of the shared private state through the closures technique we’ve been demonstrating here. This example defines an addPrivateProperty() function that defines a private variable and two nested functions to get and set the value of that variable. It adds these nested functions as methods of the object you specify.

> 示例 8-2是这种使用闭包技术来共享的私有状态的通用做法。这个例子定义了 addPrivateProperty() 函数，这个函数定义了一个私有变量，以及两个嵌套的函数用来获取和设置这个私有变量的值。它将这些嵌套函数添加为所指定对象的方法：

Example 8-2. Private property accessor methods using closures

> 示例 8-2：利用闭包实现的私有属性存取器方法

```js
// This function adds property accessor methods for a property with
// the specified name to the object o. The methods are named get<name>
// and set<name>. If a predicate function is supplied, the setter
// method uses it to test its argument for validity before storing it.
// If the predicate returns false, the setter method throws an exception.
//
// The unusual thing about this function is that the property value
// that is manipulated by the getter and setter methods is not stored in
// the object o. Instead, the value is stored only in a local variable
// in this function. The getter and setter methods are also defined
// locally to this function and therefore have access to this local variable.
// This means that the value is private to the two accessor methods, and it
// cannot be set or modified except through the setter method.
function addPrivateProperty(o, name, predicate) {
    let value;  // This is the property value

    // The getter method simply returns the value.
    o[`get${name}`] = function() { return value; };

    // The setter method stores the value or throws an exception if
    // the predicate rejects the value.
    o[`set${name}`] = function(v) {
        if (predicate && !predicate(v)) {
            throw new TypeError(`set${name}: invalid value ${v}`);
        } else {
            value = v;
        }
    };
}

// The following code demonstrates the addPrivateProperty() method.
let o = {};  // Here is an empty object

// Add property accessor methods getName and setName()
// Ensure that only string values are allowed
addPrivateProperty(o, "Name", x => typeof x === "string");

o.setName("Frank");       // Set the property value
o.getName()               // => "Frank"
o.setName(0);             // !TypeError: try to set a value of the wrong type
```
We’ve now seen a number of examples in which two closures are defined in the same scope and share access to the same private variable or variables. This is an important technique, but it is just as important to recognize when closures inadvertently share access to a variable that they should not share. Consider the following code:

> 我们已经看到了很多例子，在同一个作用域中定义两个闭包，这两个闭包共享同样的私有变量或变量。这是一种非常重要的技术，但还是要特别小心那些不希望共享的变量往往不经意间共享给了其他的闭包，了解这一点也很重要。看一下下面这段代码：

```js
// This function returns a function that always returns v
function constfunc(v) { return () => v; }

// Create an array of constant functions:
let funcs = [];
for(var i = 0; i < 10; i++) funcs[i] = constfunc(i);

// The function at array element 5 returns the value 5.
funcs[5]()    // => 5
```
When working with code like this that creates multiple closures using a loop, it is a common error to try to move the loop within the function that defines the closures. Think about the following code, for example:

> 这段代码利用循环创建了很多个闭包，当写类似这种代码的时候往往会犯一个错误：那就是试图将循环代码移入定义这个闭包的函数之内，看一下这段代码：

```js
// Return an array of functions that return the values 0-9
function constfuncs() {
    let funcs = [];
    for(var i = 0; i < 10; i++) {
        funcs[i] = () => i;
    }
    return funcs;
}

let funcs = constfuncs();
funcs[5]()    // => 10; Why doesn't this return 5?
```
This code creates 10 closures and stores them in an array. The closures are all defined within the same invocation of the function, so they share access to the variable i. When constfuncs() returns, the value of the variable i is 10, and all 10 closures share this value. Therefore, all the functions in the returned array of functions return the same value, which is not what we wanted at all. It is important to remember that the scope associated with a closure is “live.” Nested functions do not make private copies of the scope or make static snapshots of the variable bindings. Fundamentally, the problem here is that variables declared with var are defined throughout the function. Our for loop declares the loop variable with var i, so the variable i is defined throughout the function rather than being more narrowly scoped to the body of the loop. The code demonstrates a common category of bugs in ES5 and before, but the introduction of block-scoped variables in ES6 addresses the issue. If we just replace the var with a let or a const, then the problem goes away. Because let and const are block scoped, each iteration of the loop defines a scope that is independent of the scopes for all other iterations, and each of these scopes has its own independent binding of i.

> 上面这段代码创建了10个闭包，并将它们存储到一个数组中。这些闭包都是在同一个函数调用中定义的，因此它们可以共享变量 i。当 constfuncs() 返回时，变量 i 的值是10，所有的闭包都共享这一个值，因此，数组中的函数的返回值都是同一个值，这不是我们想要的结果。关联到闭包的作用域都是“活动的”，记住这一点非常重要。嵌套的函数不会将作用域内的私有成员复制一份，也不会对所绑定的变量生成静态快照。从根本上讲，这里的问题是，使用 var 声明的变量，它的定义贯穿整个函数。我们的 for 循环使用 var i 声明循环变量，因此变量 i 在整个函数中都有定义，而不是更狭义地作用于循环的主体。该代码演示了 ES6 之前的常见 Bug 类别，但在 ES6 中引入块级变量作用域解决了这个问题。如果我们只是用 let 或 const 替换 var， 那么问题就消失了。由于 let 和 const 是块级作用域，因此循环的每个迭代都定义了一个独立于所有其他迭代的作用域，并且每个作用域都有其自己的独立绑定 i。

Another thing to remember when writing closures is that this is a JavaScript keyword, not a variable. As discussed earlier, arrow functions inherit the this value of the function that contains them, but functions defined with the function keyword do not. So if you’re writing a closure that needs to use the this value of its containing function, you should use an arrow function, or call bind(), on the closure before returning it, or assign the outer this value to a variable that your closure will inherit:

> 书写闭包的时候还需注意一件事情，this 是 JavaScript 的关键字，而不是变量。正如之前讨论的，箭头函数从包含它们的函数中继承 this 值，但是用 function 关键字定义的函数不是。所以如果写一个闭包需要使用包含它的函数的 this 值，要在闭包返回之前使用箭头函数或者用调用 bind()，或者将 this 值赋值给一个变量，这样你的闭包会继承它：

```js
const self = this;  // Make the this value available to nested functions
```
## 8.7 Function Properties, Methods, and Constructor
We’ve seen that functions are values in JavaScript programs. The typeof operator returns the string “function” when applied to a function, but functions are really a specialized kind of JavaScript object. Since functions are objects, they can have properties and methods, just like any other object. There is even a Function() constructor to create new function objects. The subsections that follow document the length, name, and prototype properties; the call(), apply(), bind(), and toString() methods; and the Function() constructor.

> 我们看到在 JavaScript 程序中，函数是值。对函数执行 typeof 运算会返回字符串“function”，但是函数是 JavaScript 中特殊的对象。因为函数也是对象，它们也可以拥有属性和方法，就像普通的对象可以拥有属性和方法一样。甚至可以用 Function() 构造函数来创建新的函数对象。接下来几节就会着重介绍函数 length、name 和 prototype 属性；call()、 apply()、 bind() 和 toString() 方法；以及 Function() 构造函数。

### 8.7.1 The length Property
The read-only length property of a function specifies the arity of the function—the number of parameters it declares in its parameter list, which is usually the number of arguments that the function expects. If a function has a rest parameter, that parameter is not counted for the purposes of this length property.

> 函数的只读属性 length 指定函数参数个数--声明在其参数列表中的参数个数，大多数函数期望的实参个数。如果一个函数有一个剩余函数，它的参数个数不被计算入 length 属性。（经测试，可选参数也不计算 length。）

### 8.7.2 The name Property
The read-only name property of a function specifies the name that was used when the function was defined, if it was defined with a name, or the name of the variable or property that an unnamed function expression was assigned to when it was first created. This property is primarily useful when writing debugging or error messages.

> 如果使用名称定义函数，只读属性 name 指定函数定义时用的名称，或未命名函数表达式在首次创建时分配给的变量或属性的名称。此属性在编写调试或错误消息时很有用。

### 8.7.3 The prototype Property
All functions, except arrow functions, have a prototype property that refers to an object known as the prototype object. Every function has a different prototype object. When a function is used as a constructor, the newly created object inherits properties from the prototype object. Prototypes and the prototype property were discussed in §6.2.3 and will be covered again in Chapter 9.

> 所有函数都包含一个 prototype 属性，这个属性是指向一个对象的引用，这个对象称做原型对象。每一个函数都包含不同的原型对象。当将函数用作构造函数的时候，新创建的对象会从原型对象上继承属性。§6.2.3 讨论了原型和 prototype 属性，在第 9 章里会有进一步讨论。

### 8.7.4 The call() and apply() Methods
call() and apply() allow you to indirectly invoke (§8.2.4) a function as if it were a method of some other object. The first argument to both call() and apply() is the object on which the function is to be invoked; this argument is the invocation context and becomes the value of the this keyword within the body of the function. To invoke the function f() as a method of the object o (passing no arguments), you could use either call() or apply():

> 我们可以将 call() 和 apply () 看做是某个对象的方法，通过调用方法的形式来间接调用（见 §8.2.4）函数。call() 和 apply() 的第一个实参是要调用函数的母对象，它是调用上下文，在函数体内变成 this 关键字的值。要想以对象 o 的方法来调用函数 f()（没有实参传递），可以这样使用 call() 和 apply()：

```js
f.call(o);
f.apply(o);
```
Either of these lines of code are similar to the following (which assume that o does not already have a property named m):

> 每行代码和下面代码的功能类似（假设对象 o 中预先不存在名为 m 的属性）:

```js
o.m = f;     // Make f a temporary method of o.
o.m();       // Invoke it, passing no arguments.
delete o.m;  // Remove the temporary method.
```
Remember that arrow functions inherit the this value of the context where they are defined. This cannot be overridden with the call() and apply() methods. If you call either of those methods on an arrow function, the first argument is effectively ignored.

> 不要忘了，箭头函数从它定义的位置的上下文继承 this 值。这不能被 call() 和 apply() 方法重写。如果通过箭头函数调用它俩任何一个方法，第一个实参实际上都被忽略。

Any arguments to call() after the first invocation context argument are the values that are passed to the function that is invoked (and these arguments are not ignored for arrow functions). For example, to pass two numbers to the function f() and invoke it as if it were a method of the object o, you could use code like this:

> 对于 call() 来说，除了第一个作为调用上下文实参，之后的所有实参就是要传入待调用函数的值（并且，这部分实参对于箭头函数来说不被忽略）。比如，以对象 o 的方法的形式调用函数 f()，并传入两个数，可以使用这样的代码：

```js
f.call(o, 1, 2);
```
The apply() method is like the call() method, except that the arguments to be passed to the function are specified as an array:

> apply() 方法和 call() 类似，但传入实参的形式和 call() 有所不同，它的实参都放入一个数组中：

```js
f.apply(o, [1,2]);
```
If a function is defined to accept an arbitrary number of arguments, the apply() method allows you to invoke that function on the contents of an array of arbitrary length. In ES6 and later, we can just use the spread operator, but you may see ES5 code that uses apply() instead. For example, to find the largest number in an array of numbers without using the spread operator, you could use the apply() method to pass the elements of the array to the Math.max() function:

> 如果一个函数的实参可以是任意数量，用 apply() 方法允许你传入的参数数组可以是任意长度的。在 ES6 之后，我们可以用展开运算符，但是在 ES5 的代码中你可以看到这种情况是用 apply() 来替代。比如，不用展开运算符找出数组中最大的数值元素，调用 Math.max() 方法的时候可以给  apply() 传入一个包含任意个元素的数组：

```js
let biggest = Math.max.apply(Math, arrayOfNumbers);
```
The trace() function defined in the following is similar to the timed() function defined in §8.3.4, but it works for methods instead of functions. It uses the apply() method instead of a spread operator, and by doing that, it is able to invoke the wrapped method with the same arguments and the same this value as the wrapper method:

> 下面定义的 trace() 与 §8.3.4 中定义的 timed() 函数类似，但是它对方法有效而不是函数。它使用 apply() 方法而不是展开运算符，通过这样做，它能够调用具有相同参数和与被包装方法相同的 this 值的包装方法。

```js
// Replace the method named m of the object o with a version that logs
// messages before and after invoking the original method.
function trace(o, m) {
    let original = o[m];         // Remember original method in the closure.
    o[m] = function(...args) {   // Now define the new method.
        console.log(new Date(), "Entering:", m);      // Log message.
        let result = original.apply(this, args);      // Invoke original.
        console.log(new Date(), "Exiting:", m);       // Log message.
        return result;                                // Return result.
    };
}
```
### 8.7.5 The bind() Method
The primary purpose of bind() is to bind a function to an object. When you invoke the bind() method on a function f and pass an object o, the method returns a new function. Invoking the new function (as a function) invokes the original function f as a method of o. Any arguments you pass to the new function are passed to the original function. For example:

> bind() 方法的主要作用就是将函数绑定至某个对象。当在函数 f() 上调用 bind() 方法并传入一个对象 o 作为参数，这个方法将返回一个新的函数。（以函数调用的方式）调用新的函数将会把原始的函数 f() 当做 o 的方法来调用。传入新函数的任何实参都将传入原始函数，比如：

```js
function f(y) { return this.x + y; } // This function needs to be bound
let o = { x: 1 };                    // An object we'll bind to
let g = f.bind(o);                   // Calling g(x) invokes f() on o
g(2)                                 // => 3
let p = { x: 10, g };                // Invoke g() as a method of this object
p.g(2)                               // => 3: g is still bound to o, not p.
```
Arrow functions inherit their this value from the environment in which they are defined, and that value cannot be overridden with bind(), so if the function f() in the preceding code was defined as an arrow function, the binding would not work. The most common use case for calling bind() is to make non-arrow functions behave like arrow functions, however, so this limitation on binding arrow functions is not a problem in practice.

> 箭头函数从它们定义的上下文中继承 this 值，并且其不可被 bind() 方法重写，所以如果上面的代码用箭头函数定义函数 f()，这个绑定不会生效。调用 bind() 方法的最常用场景是让不带箭头的函数的行为像箭头函数一样，所以实际上绑定箭头函数的 this 局限性并不是一个问题。

The bind() method does more than just bind a function to an object, however. It can also perform partial application: any arguments you pass to bind() after the first are bound along with the this value. This partial application feature of bind() does work with arrow functions. Partial application is a common technique in functional programming and is sometimes called currying. Here are some examples of the bind() method used for partial application:

> 但是 bind() 方法不仅仅是将函数绑定至一个对象。它还附带一些其他应用：除了第一个实参之外，传入 bind() 的实参也会绑定至 this 值。这个附带的应用在箭头函数上也同样生效。是一种常见的函数式编程技术，有时也被称为“柯里化”。参照下面这个例子中的 bind() 方法的实现：

```js
let sum = (x,y) => x + y;      // Return the sum of 2 args
let succ = sum.bind(null, 1);  // Bind the first argument to 1
succ(2)  // => 3: x is bound to 1, and we pass 2 for the y argument

function f(y,z) { return this.x + y + z; }
let g = f.bind({x: 1}, 2);     // Bind this and y
g(3)     // => 6: this.x is bound to 1, y is bound to 2 and z is 3
```
The name property of the function returned by bind() is the name property of the function that bind() was called on, prefixed with the word “bound”.

> bind() 返回函数的名称属性是调用 bind() 的函数的名称属性前面加上前缀为单词"bound"。

### 8.7.6 The toString() Method
Like all JavaScript objects, functions have a toString() method. The ECMAScript spec requires this method to return a string that follows the syntax of the function declaration statement. In practice, most (but not all) implementations of this toString() method return the complete source code for the function. Built-in functions typically return a string that includes something like “[native code]” as the function body.

> 和所有的 JavaScript 对象一样，函数也有 toString() 方法，ECMAScript 规范规定这个方法返回一个字符串，这个字符串和函数声明语句的语法相关。实际上，大多数（非全部）的 toString() 方法的实现都返回函数的完整源码。内置函数往往返回一个类似”[native code]”的字符串作为函数体。

### 8.7.7 The Function() Constructor
Because functions are objects, there is a Function() constructor that can be used to create new functions:

> 因为函数是对象，有一个 Function() 构造函数可以用来创建新的函数：

```js
const f = new Function("x", "y", "return x*y;");
```
This line of code creates a new function that is more or less equivalent to a function defined with the familiar syntax:

> 这一行代码创建一个新的函数，这个函数和通过下面代码定义的函数几乎等价：

```js
const f = function(x, y) { return x*y; };
```
The Function() constructor expects any number of string arguments. The last argument is the text of the function body; it can contain arbitrary JavaScript statements, separated from each other by semicolons. All other arguments to the constructor are strings that specify the parameter names for the function. If you are defining a function that takes no arguments, you would simply pass a single string—the function body—to the constructor.

> Function() 构造函数可以传入任意数量的字符串实参，最后一个实参所表示的文本就是函数体；它可以包含任意的 JavaScript 语句，每两条语句之间用分号分隔。传入构造函数的其他所有的实参字符串是指定函数的形参名字的字符串。如果定义的函数不包含任何参数，只须给构造函数简单地传入一个字符串——函数体——即可。

Notice that the Function() constructor is not passed any argument that specifies a name for the function it creates. Like function literals, the Function() constructor creates anonymous functions.

> 注意，Function() 构造函数并不需要通过传入实参以指定函数名。就像函数字面量一样，Function() 构造函数创建一个匿名函数。

There are a few points that are important to understand about the Function() constructor:

> 关于 Function() 构造函数有几点需要特别注意：

The Function() constructor allows JavaScript functions to be dynamically created and compiled at runtime.

> Function() 构造函数允许 JavaScript 在运行时动态地创建并编译函数。

The Function() constructor parses the function body and creates a new function object each time it is called. If the call to the constructor appears within a loop or within a frequently called function, this process can be inefficient. By contrast, nested functions and function expressions that appear within loops are not recompiled each time they are encountered.

> 每次调用 Function() 构造函数都会解析函数体，并创建新的函数对象。如果是在一个循环或者多次调用的函数中执行这个构造函数，执行效率会受影响。相比之下，循环中的嵌套函数和函数定义表达式则不会每次执行时都重新编译。

A last, very important point about the Function() constructor is that the functions it creates do not use lexical scoping; instead, they are always compiled as if they were top-level functions, as the following code demonstrates:

> 最后一点，也是关于 Function() 构造函数非常重要的一点，就是它所创建的函数并不是使用词法作用域，相反，函数体代码的编译类似顶层函数，如下面代码所示：

```js
let scope = "global";
function constructFunction() {
    let scope = "local";
    return new Function("return scope");  // Doesn't capture local scope!
}
// This line returns "global" because the function returned by the
// Function() constructor does not use the local scope.
constructFunction()()  // => "global"
```
The Function() constructor is best thought of as a globally scoped version of eval() (see §4.12.2) that defines new variables and functions in its own private scope. You will probably never need to use this constructor in your code.

> 我们可以将 Function() 构造函数认为是在全局作用域中执行的 eval()（见  §4.12.2），eval() 可以在自己的私有作用域内定义新变量和函数，Function() 构造函数在实际编程过程中很少会用到。

## 8.8 Functional Programming
JavaScript is not a functional programming language like Lisp or Haskell, but the fact that JavaScript can manipulate functions as objects means that we can use functional programming techniques in JavaScript. Array methods such as map() and reduce() lend themselves particularly well to a functional programming style. The sections that follow demonstrate techniques for functional programming in JavaScript. They are intended as a mind-expanding exploration of the power of JavaScript’s functions, not as a prescription for good programming style.

> 和 Lisp、Haskell 不同，JavaScript 并非函数式编程语言，但在 JavaScript 中可以像操控对象一样操控函数，也就是说可以在 JavaScript 中应用函数式编程技术。数组方法诸如 map() 和 reduce() 就可以非常适合用于函数式编程风格。接下来的几节将会着重介绍 JavaScript 中的函数式编程技术。函数式编程旨在扩展对 JavaScript 函数功能功能的探索，而不是为了良好的编程风格。

### 8.8.1 Processing Arrays with Functions
Suppose we have an array of numbers and we want to compute the mean and standard deviation of those values. We might do that in nonfunctional style like this:

> 假设有一个数组，数组元素都是数字，我们想要计算这些元素的平均值和标准差。若使用非函数式编程风格的话，代码会是这样：

```js
let data = [1,1,3,5,5];  // This is our array of numbers

// The mean is the sum of the elements divided by the number of elements
let total = 0;
for(let i = 0; i < data.length; i++) total += data[i];
let mean = total/data.length;  // mean == 3; The mean of our data is 3

// To compute the standard deviation, we first sum the squares of
// the deviation of each element from the mean.
total = 0;
for(let i = 0; i < data.length; i++) {
    let deviation = data[i] - mean;
    total += deviation * deviation;
}
let stddev = Math.sqrt(total/(data.length-1));  // stddev == 2
```
We can perform these same computations in concise functional style using the array methods map() and reduce() like this (see §7.8.1 to review these methods):

> 可以使用数组方法 map() 和 reduce() 来实现同样的计算，这种实现极其简洁（参照 §7.8.1 来查看这些方法）：

```js
// First, define two simple functions
const sum = (x,y) => x+y;
const square = x => x*x;

// Then use those functions with Array methods to compute mean and stddev
let data = [1,1,3,5,5];
let mean = data.reduce(sum)/data.length;  // mean == 3
let deviations = data.map(x => x-mean);
let stddev = Math.sqrt(deviations.map(square).reduce(sum)/(data.length-1));
stddev  // => 2
```
This new version of the code looks quite different than the first one, but it is still invoking methods on objects, so it has some object-oriented conventions remaining. Let’s write functional versions of the map() and reduce() methods:

> 这个新版本的代码看起来跟第一版有很大不同，但是它仍然调用对象的方法，所以它还是面向对象编程。接下来用函数版本的 map() 和 reduce() 方法：

```js
const map = function(a, ...args) { return a.map(...args); };
const reduce = function(a, ...args) { return a.reduce(...args); };
```
With these map() and reduce() functions defined, our code to compute the mean and standard deviation now looks like this:

> 用这两个函数定义了 map() 和 reduce()，我们计算平均值和标准差变成这样：

```js
const sum = (x,y) => x+y;
const square = x => x*x;

let data = [1,1,3,5,5];
let mean = reduce(data, sum)/data.length;
let deviations = map(data, x => x-mean);
let stddev = Math.sqrt(reduce(map(deviations, square), sum)/(data.length-1));
stddev  // => 2
```
### 8.8.2 Higher-Order Functions
A higher-order function is a function that operates on functions, taking one or more functions as arguments and returning a new function. Here is an example:

> 所谓高阶函数就是操作函数的函数，它接收一个或多个函数作为参数，并返回一个新函数。来看这个例子：

```js
// This higher-order function returns a new function that passes its
// arguments to f and returns the logical negation of f's return value;
function not(f) {
    return function(...args) {             // Return a new function
        let result = f.apply(this, args);  // that calls f
        return !result;                    // and negates its result.
    };
}

const even = x => x % 2 === 0; // A function to determine if a number is even
const odd = not(even);         // A new function that does the opposite
[1,1,3,5,5].every(odd)         // => true: every element of the array is odd
```
This not() function is a higher-order function because it takes a function argument and returns a new function. As another example, consider the mapper() function that follows. It takes a function argument and returns a new function that maps one array to another using that function. This function uses the map() function defined earlier, and it is important that you understand how the two functions are different:

> 上面的 not() 函数就是一个高阶函数，因为它接收一个函数作为参数，并返回一个新函数。另外一个例子，来看下面的 mapper() 函数，它也是接收一个函数作为实参，并返回一个新函数，这个新函数将一个数组映射到另一个使用这个函数的数组上。这个函数使用了之前定义的 map() 函数，但要首先理解这两个函数有哪里不 同，理解这一点至关重要：

```js
// Return a function that expects an array argument and applies f to
// each element, returning the array of return values.
// Contrast this with the map() function from earlier.
function mapper(f) {
    return a => map(a, f);
}

const increment = x => x+1;
const incrementAll = mapper(increment);
incrementAll([1,2,3])  // => [2,3,4]
```
Here is another, more general, example that takes two functions, f and g, and returns a new function that computes f(g()):

> 这里是一个更常见的例子，它接收两个函数 f() 和 g()，并返回一个新的函数用以计算 f(g())：

```js
// Return a new function that computes f(g(...)).
// The returned function h passes all of its arguments to g, then passes
// the return value of g to f, then returns the return value of f.
// Both f and g are invoked with the same this value as h was invoked with.
function compose(f, g) {
    return function(...args) {
        // We use call for f because we're passing a single value and
        // apply for g because we're passing an array of values.
        return f.call(this, g.apply(this, args));
    };
}

const sum = (x,y) => x+y;
const square = x => x*x;
compose(square, sum)(2,3)  // => 25; the square of the sum
```
The partial() and memoize() functions defined in the sections that follow are two more important higher-order functions.

> 本章后续几节中定义了 partial() 和 memoize() 函数，这两个函数是非常重要的高阶函数。

### 8.8.3 Partial Application of Functions
The bind() method of a function f (see §8.7.5) returns a new function that invokes f in a specified context and with a specified set of arguments. We say that it binds the function to an object and partially applies the arguments. The bind() method partially applies arguments on the left—that is, the arguments you pass to bind() are placed at the start of the argument list that is passed to the original function. But it is also possible to partially apply arguments on the right:

> 函数 f()（见 §8.7.5）的 bind() 方法返回一个新函数，给新函数传入特定的上下文和一组指定的参数，然后调用函数 f()。我们说它把函数“绑定至”对象并传入一部分参数。bind() 方法只是将实参放在（完整实参列表的）左侧，也就是说传入 bind() 的实参都是放在传入原始函数的实参列表开始的位置，但有时我们期望将传入 bind() 的实参放在（完整实参列表的）右侧：

```js
// The arguments to this function are passed on the left
function partialLeft(f, ...outerArgs) {
    return function(...innerArgs) { // Return this function
        let args = [...outerArgs, ...innerArgs]; // Build the argument list
        return f.apply(this, args);              // Then invoke f with it
    };
}

// The arguments to this function are passed on the right
function partialRight(f, ...outerArgs) {
    return function(...innerArgs) {  // Return this function
        let args = [...innerArgs, ...outerArgs]; // Build the argument list
        return f.apply(this, args);              // Then invoke f with it
    };
}

// The arguments to this function serve as a template. Undefined values
// in the argument list are filled in with values from the inner set.
function partial(f, ...outerArgs) {
    return function(...innerArgs) {
        let args = [...outerArgs]; // local copy of outer args template
        let innerIndex=0;          // which inner arg is next
        // Loop through the args, filling in undefined values from inner args
        for(let i = 0; i < args.length; i++) {
            if (args[i] === undefined) args[i] = innerArgs[innerIndex++];
        }
        // Now append any remaining inner arguments
        args.push(...innerArgs.slice(innerIndex));
        return f.apply(this, args);
    };
}

// Here is a function with three arguments
const f = function(x,y,z) { return x * (y - z); };
// Notice how these three partial applications differ
partialLeft(f, 2)(3,4)         // => -2: Bind first argument: 2 * (3 - 4)
partialRight(f, 2)(3,4)        // =>  6: Bind last argument: 3 * (4 - 2)
partial(f, undefined, 2)(3,4)  // => -6: Bind middle argument: 3 * (2 - 4)
```
These partial application functions allow us to easily define interesting functions out of functions we already have defined. Here are some examples:

> 利用这种不完全函数的编程技巧，可以编写一些有意思的代码，利用已有的函数来定义新的函数，参照下面这个例子：

```js
const increment = partialLeft(sum, 1);
const cuberoot = partialRight(Math.pow, 1/3);
cuberoot(increment(26))  // => 3
```
Partial application becomes even more interesting when we combine it with other higher-order functions. Here, for example, is a way to define the preceding not() function just shown using composition and partial application:

> 当将不完全调用和其他高阶函数整合在一起的时候，事情就变得格外有趣了。比如，这里的例子定义了 not() 函数，它用到了刚才提到的不完全调用：

```js
const not = partialLeft(compose, x => !x);
const even = x => x % 2 === 0;
const odd = not(even);
const isNumber = not(isNaN);
odd(3) && isNumber(2)  // => true
```
We can also use composition and partial application to redo our mean and standard deviation calculations in extreme functional style:

> 我们也可以使用不完全调用的组合来重新组织求平均数和标准差的代码，这种编码风格是非常纯粹的函数式编程：

```js
// sum() and square() functions are defined above. Here are some more:
const product = (x,y) => x*y;
const neg = partial(product, -1);
const sqrt = partial(Math.pow, undefined, .5);
const reciprocal = partial(Math.pow, undefined, neg(1));

// Now compute the mean and standard deviation.
let data = [1,1,3,5,5];   // Our data
let mean = product(reduce(data, sum), reciprocal(data.length));
let stddev = sqrt(product(reduce(map(data,
                                     compose(square,
                                             partial(sum, neg(mean)))),
                                 sum),
                          reciprocal(sum(data.length,neg(1)))));
[mean, stddev]  // => [3, 2]
```
Notice that this code to compute mean and standard deviation is entirely function invocations; there are no operators involved, and the number of parentheses has grown so large that this JavaScript is beginning to look like Lisp code. Again, this is not a style that I advocate for JavaScript programming, but it is an interesting exercise to see how deeply functional JavaScript code can be.

> 注意，这段代码计算平均值和标准差完全是函数调用;没有涉及运算符，并且括号的数量增长如此之大让 JavaScript 开始看起来像 Lisp 代码。同样，这不是我提倡的 JavaScript 编程风格，但它是一个有趣的练习，看看 JavaScript 代码的功能有多深。

### 8.8.4 Memoization
In §8.4.1, we defined a factorial function that cached its previously computed results. In functional programming, this kind of caching is called memoization. The code that follows shows a higher-order function, memoize(), that accepts a function as its argument and returns a memoized version of the function:

> 在 §8.4.1 中定义了一个阶乘函数，它可以将上次的计算结果缓存起来。在函数式编程当中，这种缓存技巧叫做“记忆”（memorization）。下面的代码展示了一个高阶函数，memorize() 接收一个函数作为实参，并返回带有记忆能力的函数:

```js
// Return a memoized version of f.
// It only works if arguments to f all have distinct string representations.
function memoize(f) {
    const cache = new Map();  // Value cache stored in the closure.

    return function(...args) {
        // Create a string version of the arguments to use as a cache key.
        let key = args.length + args.join("+");
        if (cache.has(key)) {
            return cache.get(key);
        } else {
            let result = f.apply(this, args);
            cache.set(key, result);
            return result;
        }
    };
}
```
The memoize() function creates a new object to use as the cache and assigns this object to a local variable so that it is private to (in the closure of) the returned function. The returned function converts its arguments array to a string and uses that string as a property name for the cache object. If a value exists in the cache, it returns it directly. Otherwise, it calls the specified function to compute the value for these arguments, caches that value, and returns it. Here is how we might use memoize():

> memorize() 函数创建一个新的对象，这个对象被当做缓存（的宿主）并赋值给一个局部变量，因此对于返回的函数来说它是私有的（在闭包中）。所返回的函数将它的实参数组转换成字符串，并将字符串用做缓存对象的属性名。如果在缓存中存在这个值，则直接返回它。否则，就调用既定的函数对实参进行计算，将计算结果缓存起来并返回，下面的代码展示了如何使用 memorize()：

```js
// Return the Greatest Common Divisor of two integers using the Euclidian
// algorithm: http://en.wikipedia.org/wiki/Euclidean_algorithm
function gcd(a,b) {  // Type checking for a and b has been omitted
    if (a < b) {           // Ensure that a >= b when we start
        [a, b] = [b, a];   // Destructuring assignment to swap variables
    }
    while(b !== 0) {       // This is Euclid's algorithm for GCD
        [a, b] = [b, a%b];
    }
    return a;
}

const gcdmemo = memoize(gcd);
gcdmemo(85, 187)  // => 17

// Note that when we write a recursive function that we will be memoizing,
// we typically want to recurse to the memoized version, not the original.
const factorial = memoize(function(n) {
    return (n <= 1) ? 1 : n * factorial(n-1);
});
factorial(5)      // => 120: also caches values for 4, 3, 2 and 1.
```
## 8.9 Summary
Some key points to remember about this chapter are as follows:

You can define functions with the function keyword and with the ES6 => arrow syntax.

You can invoke functions, which can be used as methods and constructors.

Some ES6 features allow you to define default values for optional function parameters, to gather multiple arguments into an array using a rest parameter, and to destructure object and array arguments into function parameters.

You can use the ... spread operator to pass the elements of an array or other iterable object as arguments in a function invocation.

A function defined inside of and returned by an enclosing function retains access to its lexical scope and can therefore read and write the variables defined inside the outer function. Functions used in this way are called closures, and this is a technique that is worth understanding.

Functions are objects that can be manipulated by JavaScript, and this enables a functional style of programming.

> 本章关键点总结如下：
> 
> 可以用函数关键字和 ES6 => 箭头函数来定义函数。
> 
> 可以以方法和构造函数的方式调用函数。
> 
> 一些 ES6 特性，允许参数设定默认值，可以用剩余参数将多个参数搜集到一个数组中，可以解构对象和数组实参到函数参数中。
> 
> 可以用 ... 展开运算符传递数组元素或者其他可迭代对象到函数调用。
> 
> 封闭函数内部定义并返回的函数保留对其词法作用域的访问，因此可以读取和写入外部函数内定义的变量。用这种方式使用的函数称为闭包，这是一种值得理解的技术。
> 
> 函数是可由 JavaScript 操作的对象，这使 JavaScript 支持函数式编程。

---

1. The term was coined by Martin Fowler. See http://martinfowler.com/dslCatalog/methodChaining.html.
2. If you are familiar with Python, note that this is different than Python, in which every invocation shares the same default value.
3. This may not seem like a particularly interesting point unless you are familiar with more static languages, in which functions are part of a program but cannot be manipulated by the program.

> 1. 这个术语最初是由 Martin Fowler 提出的，参见http://martinfowler.com/dslwip/MethodChaining.html。
> 2. 这看起来不足为奇，但如果你对 Python 很熟悉，你会发现 Python 中的函数是程序的一 部分，但无法被程序操作。
> 3. 这似乎并不是一个特别有趣的点，除非你熟悉更多的静态语言，其中函数是程序的一部分，但不能由程序操作。