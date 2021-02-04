# 第 9 章 类

JavaScript objects were covered in Chapter 6. That chapter treated each object as a unique set of properties, different from every other object. It is often useful, however, to define a class of objects that share certain properties. Members, or instances, of the class have their own properties to hold or define their state, but they also have methods that define their behavior. These methods are defined by the class and shared by all instances. Imagine a class named Complex that represents and performs arithmetic on complex numbers, for example. A Complex instance would have properties to hold the real and imaginary parts (the state) of the complex number. And the Complex class would define methods to perform addition and multiplication (the behavior) of those numbers.

> 第 6 章详细介绍了 JavaScript 对象，每个 JavaScript 对象都是一个属性集合，相互之间没有任何联系。在 JavaScript 中也可以定义对象的类，让每个对象都共享某些属性，这种“共享”的特性是非常有用的。类的成员或实例都包含一些属性，用以存放或定义它们的状态，其中有些属性定义了它们的行为（通常称为方法）。这些行为通常是由类定义的，而且为所有实例所共享。例如，假设有一个名为 Complex 的类用来表示复数，同时还定义了一些复数运算。一个 Complex 实例应当包含复数的实部和虚部（状态），同样 Complex 类还会定义复数的加法和乘法操作（行为）。

In JavaScript, classes use prototype-based inheritance: if two objects inherit properties (generally function-valued properties, or methods) from the same prototype, then we say that those objects are instances of the same class. That, in a nutshell, is how JavaScript classes work. JavaScript prototypes and inheritance were covered in §6.2.3 and §6.3.2, and you will need to be familiar with the material in those sections to understand this chapter. This chapter covers prototypes in §9.1.

> 在 JavaScript 中，类的实现是基于其原型继承机制的。如果两个实例都从同一个原型对象上继承了属性，我们说它们是同一个类的实例。JavaScript 原型和继承在 §6.2.3 和 §6.3.2 节中有详细讨论，为了更好地理解本章的内容，请务必首先阅读这两个章节。本章将会在 §9.1 中对原型做进一步讨论。

If two objects inherit from the same prototype, this typically (but not necessarily) means that they were created and initialized by the same constructor function or factory function. Constructors have been covered in §4.6, §6.2.2, and §8.2.3, and this chapter has more in §9.2.

> 如果两个对象继承自同一个原型，往往意味着（但不是绝对）它们是由同一个构造函数创建并初始化的。我们已经在 §4.6、§6.2.2 和 §8.2.3 节中详细讲解了构造函数，§9.2 会有进一步讨论。

JavaScript has always allowed the definition of classes. ES6 introduced a brand-new syntax (including a class keyword) that makes it even easier to create classes. These new JavaScript classes work in the same way that old-style classes do, and this chapter starts by explaining the old way of creating classes because that demonstrates more clearly what is going on behind the scenes to make classes work. Once we’ve explained those fundamentals, we’ll shift and start using the new, simplified class definition syntax.

> JavaScript 一直允许定义类。ES6 引入了全新的语法（包括 class 关键字），使创建类更加容易。这些新的 JavaScript 类的工作方式与旧式类相同，本章首先解释创建类的旧方法，因为这更清楚地展示了类是如何工作的。一旦我们解释了这些基本原理，我们将改变并开始使用新的、简化的类定义语法。

If you’re familiar with strongly typed object-oriented programming languages like Java or C++, you’ll notice that JavaScript classes are quite different from classes in those languages. There are some syntactic similarities, and you can emulate many features of “classical” classes in JavaScript, but it is best to understand up front that JavaScript’s classes and prototype-based inheritance mechanism are substantially different from the classes and class-based inheritance mechanism of Java and similar languages.

> 如果你对诸如 Java 和 C++ 这种强类型的面向对象编程比较熟悉，你会发现 JavaScript 中的类和 Java 以及 C++ 中的类有很大不同。尽管在写法上类似，而且在 JavaScript 中也能“模拟”出很多经典的类的特性，但是最好要理解 JavaScript 的类和基于原型的继承机制，以及和传统的 Java（当然还有类似 Java 的语言）的类和基于类的继承机制的不同之处。

## 9.1 Classes and Prototypes

In JavaScript, a class is a set of objects that inherit properties from the same prototype object. The prototype object, therefore, is the central feature of a class. Chapter 6 covered the Object.create() function that returns a newly created object that inherits from a specified prototype object. If we define a prototype object and then use Object.create() to create objects that inherit from it, we have defined a JavaScript class. Usually, the instances of a class require further initialization, and it is common to define a function that creates and initializes the new object. Example 9-1 demonstrates this: it defines a prototype object for a class that represents a range of values and also defines a factory function that creates and initializes a new instance of the class.

> 在 JavaScript 中，类的所有实例对象都从同一个原型对象上继承属性。因此，原型对象是类的核心。在示例 6-1 中定义了 inherit() 函数，这个函数返回一个新创建的对象，后者继承自某个原型对象。如果定义一个原型对象，然后通过 inherit() 函数创建一个继承自它的对象，这样就定义了一个 JavaScript 类。通常，类的实例还需要进一步的初始化，通常是通过定义一个函数来创建并初始化这个新对象，参照示例 9-1。示例 9-1 给一个表示“值的范围”的类定义了原型对象，还定义了一个“工厂”函数用以创建并初始化类的实例。

Example 9-1. A simple JavaScript class

> 示例 9-1：一个简单的 JavaScript 类

```js
// This is a factory function that returns a new range object.
function range(from, to) {
    // Use Object.create() to create an object that inherits from the
    // prototype object defined below.  The prototype object is stored as
    // a property of this function, and defines the shared methods (behavior)
    // for all range objects.
    let r = Object.create(range.methods);

    // Store the start and end points (state) of this new range object.
    // These are noninherited properties that are unique to this object.
    r.from = from;
    r.to = to;

    // Finally return the new object
    return r;
}

// This prototype object defines methods inherited by all range objects.
range.methods = {
    // Return true if x is in the range, false otherwise
    // This method works for textual and Date ranges as well as numeric.
    includes(x) { return this.from <= x && x <= this.to; },

    // A generator function that makes instances of the class iterable.
    // Note that it only works for numeric ranges.
    *[Symbol.iterator]() {
        for(let x = Math.ceil(this.from); x <= this.to; x++) yield x;
    },

    // Return a string representation of the range
    toString() { return "(" + this.from + "..." + this.to + ")"; }
};

// Here are example uses of a range object.
let r = range(1,3);      // Create a range object
r.includes(2)            // => true: 2 is in the range
r.toString()             // => "(1...3)"
[...r]                   // => [1, 2, 3]; convert to an array via iterator
```
There are a few things worth noting in the code of Example 9-1:

> 在示例 9-1 的代码中有一下几点值得注意：

This code defines a factory function range() for creating new Range objects.

> 这段代码定义了一个工厂函数 range() 用来创建一个新的 Range 对象。

It uses the methods property of this range() function as a convenient place to store the prototype object that defines the class. There is nothing special or idiomatic about putting the prototype object here.

> 用 range() 函数的 methods 属性来存放定义类的原型对象。只是将原型对象随意的放在一个地方，并不是一个规约或者习惯。

The range() function defines from and to properties on each Range object. These are the unshared, noninherited properties that define the unique state of each individual Range object.

> range() 函数在每个 Range 对象中都定义 from 和 to 属性。它们是非共享、非继承属性，是每个独立的 Range 对象的独特自有状态。

The range.methods object uses the ES6 shorthand syntax for defining methods, which is why you don’t see the function keyword anywhere. (See §6.10.5 to review object literal shorthand method syntax.)

> range.methods 对象应用了 ES6 的速记语法来定义方法，这是为什么没有看到 function 关键字的原因。（参照 §6.10.5 来复习对象字面量速记方法语法。）

One of the methods in the prototype has the computed name (§6.10.2) Symbol.iterator, which means that it is defining an iterator for Range objects. The name of this method is prefixed with *, which indicates that it is a generator function instead of a regular function. Iterators and generators are covered in detail in Chapter 12. For now, the upshot is that instances of this Range class can be used with the for/of loop and with the ... spread operator.

> 原型中的一个方法 Symbol.iterator 使用了计算属性名（§6.10.2），表明它是为 Range 对象定义一个迭代器。方法名称带有一个前缀 *，标识它是一个生成器函数而不是普通的函数。迭代器和生成器在第 12 章会详细描述。现在，只需要知道 Range 类的实例可以用 for/of 循环和可以用 ... 展开运算符。

The shared, inherited methods defined in range.methods all use the from and to properties that were initialized in the range() factory function. In order to refer to them, they use the this keyword to refer to the object through which they were invoked. This use of this is a fundamental characteristic of the methods of any class.

> 定义在 range.methods 中的共享继承方法都使用在 range() 工厂函数初始化的 from 和 to 属性。在这些方法被调用时，为了引用 from 和 to 属性，都使用 this 关键字来获取对象的引用。this 这种用法是任何类中方法的基本特征。

## 9.2 Classes and Constructors
Example 9-1 demonstrates a simple way to define a JavaScript class. It is not the idiomatic way to do so, however, because it did not define a constructor. A constructor is a function designed for the initialization of newly created objects. Constructors are invoked using the new keyword as described in §8.2.3. Constructor invocations using new automatically create the new object, so the constructor itself only needs to initialize the state of that new object. The critical feature of constructor invocations is that the prototype property of the constructor is used as the prototype of the new object. §6.2.3 introduced prototypes and emphasized that while almost all objects have a prototype, only a few objects have a prototype property. Finally, we can clarify this: it is function objects that have a prototype property. This means that all objects created with the same constructor function inherit from the same object and are therefore members of the same class. Example 9-2 shows how we could alter the Range class of Example 9-1 to use a constructor function instead of a factory function. Example 9-2 demonstrates the idiomatic way to create a class in versions of JavaScript that do not support the ES6 class keyword. Even though class is well supported now, there is still lots of older JavaScript code around that defines classes like this, and you should be familiar with the idiom so that you can read old code and so that you understand what is going on “under the hood” when you use the class keyword.

> 示例 9-1 展示了一个简单方式来定义一个 JavaScript 类。但是这种方法并不常用，因为它没有定义一个构造函数。构造函数是用来初始化新建对象的。如 §8.2.3 中所述构造函数用 new 关键字来调用。使用 new 调用构造函数会自动创建一个新对象，因此构造函数本身只需初始化这个新对象的状态即可。§6.2.3 介绍并强调了虽然所有对象都有原型，但是只有一部分对象有一个 prototype 属性。最后，我们可以澄清这一点：是函数对象具有 prototype 属性。这意味着所有用同一构造函数创建的对象继承同一个对象，因此它们是同一类的成员。示例 9-2 说明了如何使用一个构造函数来替代示例 9-1 中的工厂函数来修改 Range 类。示例 9-2 演示了在不支持 ES6 class 关键字版本的 JavaScript 中创建一个类的通用方法。即使是 class 已经很好支持的今天，仍然有很多旧 JavaScript 代码用这种方式定义类，并且你必须熟悉这种习惯用法，以便于阅读旧代码，也能够在使用 class 关键字时明白在底层中发生了什么。

Example 9-2. A Range class using a constructor

> 示例 9-2：使用构造函数的 Range 类

```js
// This is a constructor function that initializes new Range objects.
// Note that it does not create or return the object. It just initializes this.
function Range(from, to) {
    // Store the start and end points (state) of this new range object.
    // These are noninherited properties that are unique to this object.
    this.from = from;
    this.to = to;
}

// All Range objects inherit from this object.
// Note that the property name must be "prototype" for this to work.
Range.prototype = {
    // Return true if x is in the range, false otherwise
    // This method works for textual and Date ranges as well as numeric.
    includes: function(x) { return this.from <= x && x <= this.to; },

    // A generator function that makes instances of the class iterable.
    // Note that it only works for numeric ranges.
    [Symbol.iterator]: function*() {
        for(let x = Math.ceil(this.from); x <= this.to; x++) yield x;
    },

    // Return a string representation of the range
    toString: function() { return "(" + this.from + "..." + this.to + ")"; }
};

// Here are example uses of this new Range class
let r = new Range(1,3);   // Create a Range object; note the use of new
r.includes(2)             // => true: 2 is in the range
r.toString()              // => "(1...3)"
[...r]                    // => [1, 2, 3]; convert to an array via iterator
```
It is worth comparing Examples 9-1 and 9-2 fairly carefully and noting the differences between these two techniques for defining classes. First, notice that we renamed the range() factory function to Range() when we converted it to a constructor. This is a very common coding convention: constructor functions define, in a sense, classes, and classes have names that (by convention) begin with capital letters. Regular functions and methods have names that begin with lowercase letters.

> 将示例 9-1 和示例 9-2 中的代码做一个仔细的对比，可以发现两种类定义技术的差别。首先，注意当工厂函数 range() 转化为构造函数时被重命名为 Range()。这里遵循了一个常见的编程约定：从某种意义上讲，定义构造函数即是定义类，并且类名首字母要大写。而普通的函数和方法都是首字母小写。

Next, notice that the Range() constructor is invoked (at the end of the example) with the new keyword while the range() factory function was invoked without it. Example 9-1 uses regular function invocation (§8.2.1) to create the new object, and Example 9-2 uses constructor invocation (§8.2.3). Because the Range() constructor is invoked with new, it does not have to call Object.create() or take any action to create a new object. The new object is automatically created before the constructor is called, and it is accessible as the this value. The Range() constructor merely has to initialize this. Constructors do not even have to return the newly created object. Constructor invocation automatically creates a new object, invokes the constructor as a method of that object, and returns the new object. The fact that constructor invocation is so different from regular function invocation is another reason that we give constructors names that start with capital letters. Constructors are written to be invoked as constructors, with the new keyword, and they usually won’t work properly if they are invoked as regular functions. A naming convention that keeps constructor functions distinct from regular functions helps programmers know when to use new.

> 再者，注意 Range() 构造函数是通过 new 关键字调用的（在示例代码的末尾）， 而 range() 工厂函数则不必使用 new。示例 9-1 通过调用普通函数（§8.2.1）来创建新对象，示例 9-2 则使用构造函数调用（§8.2.3）来创建新对象。由于 Range() 构造函数是通过 new 关键字调用的，因此不必调用 Object.create() 或其他什么逻辑来创建新对象。在调用构造函数之前就已经创建了新对象，并且通过 this 关键字可以获取这个新对象。Range() 构造函数只不过是初始化 this 而已。构造函数甚至不必返回这个新创建的对象，构造函数会自动创建对象，然后将构造函数作为这个对象的方法来调用一次，最后返回这个新对象。构造函数调用与常规函数调用如此不同，实际上，这是我们为构造函数命名以大写字母为名的另一个原因。构造函数就是用来“构造新对象”的，它必须通过关键字 new 调用，如果将构造函数用做普通函数的话，往往不会正常工作。开发者可以通过命名规约来（构造函数首字母大写，普通方法首字母小写）判断是否应当在函数之前冠以关键字 new。

**CONSTRUCTORS AND NEW.TARGET**
Within a function body, you can tell whether the function has been invoked as a constructor with the special expression new.target. If the value of that expression is defined, then you know that the function was invoked as a constructor, with the new keyword. When we discuss subclasses in §9.5, we’ll see that new.target is not always a reference to the constructor it is used in: it might also refer to the constructor function of a subclass.

> 在函数正文中，可以使用特殊的表达式 new.target 来判断函数是否以构造函数的方式调用。如果定义了该表达式的值，那么这个函数是通过 new 关键字调用的构造函数。当我们在 §9.5 中讨论子类时，我们会看到 new.target 不总是其所在的构造函数的引用：它可能还引用子类的构造函数。

If new.target is undefined, then the containing function was invoked as a function, without the new keyword. JavaScript’s various error constructors can be invoked without new, and if you want to emulate this feature in your own constructors, you can write them like this:

> 如果 new.target 是 undefined，那么包含它的函数是作为函数调用的，没有使用 new 关键字。JavaScript 很多异常构造函数可以不使用 new 来调用，如果想模仿这个特性可以这样写：

```js
function C() {
    if (!new.target) return new C();
    // initialization code goes here
}
```
This technique only works for constructors defined in this old-fashioned way. Classes created with the class keyword do not allow their constructors to be invoked without new.

> 这个老式技巧只在构造函数定义时生效。类使用 class 关键字创建，不允许不使用 new 调用它的构造函数。

Another critical difference between Examples 9-1 and 9-2 is the way the prototype object is named. In the first example, the prototype was range.methods. This was a convenient and descriptive name, but arbitrary. In the second example, the prototype is Range.prototype, and this name is mandatory. An invocation of the Range() constructor automatically uses Range.prototype as the prototype of the new Range object.

> 示例 9-1 和 9-2 之间的另一个关键区别是原型对象的命名方式。在第一个示例中，原型是 range.methods。这是一个方便和描述性的名称，但随意。在第二个示例中，原型为 Range.prototype，此名称是规定的。Range() 构造函数的调用自动使用 Range.prototype 作为新 Range 对象的原型。

Finally, also note the things that do not change between Examples 9-1 and 9-2 : the range methods are defined and invoked in the same way for both classes. Because Example 9-2 demonstrates the idiomatic way to create classes in versions of JavaScript before ES6, it does not use the ES6 shorthand method syntax in the prototype object and explicitly spells out the methods with the function keyword. But you can see that the implementation of the methods is the same in both examples.

> 最后，还要注意示例 9-1 和 9-2 之间不变的部分：对两个类来说，range 方法以相同的方式定义和调用。由于示例 9-2 演示了在 ES6 之前在 JavaScript 版本中创建类的惯用方法，因此它没原型对象中使用 ES6 速记方法语法，并且使用 function 关键字显式拼出方法名。但是，可以看到，在这两个示例中，方法的实现是相同的。

Importantly, note that neither of the two range examples uses arrow functions when defining constructors or methods. Recall from §8.1.3 that functions defined in this way do not have a prototype property and so cannot be used as constructors. Also, arrow functions inherit the this keyword from the context in which they are defined rather than setting it based on the object through which they are invoked, and this makes them useless for methods because the defining characteristic of methods is that they use this to refer to the instance on which they were invoked.

> 请注意，在定义构造函数或方法时，两个 range 示例都没使用箭头函数。回想一下，从 §8.1.3 中，用这种方式定义的函数没有原型属性，因此不能用作构造函数。此外，箭头函数从定义它们的上下文中继承 this 关键字，而不是基于调用它们的对象设置 this 值，这使得箭头函数对方法毫无用处，因为方法的定义特征是方法使用 this 关键字来引用调用方法的实例。

Fortunately, the new ES6 class syntax doesn’t allow the option of defining methods with arrow functions, so this is not a mistake that you can accidentally make when using that syntax. We will cover the ES6 class keyword soon, but first, there are more details to cover about constructors.

> 幸运的是，新的 ES6 类语法不允许使用 arrow 函数定义方法，因此这不是使用该语法时可能会意外犯的错误。我们将很快介绍 ES6 类关键字，但首先，有更多关于构造函数的详细信息。

### 9.2.1 Constructors, Class Identity, and instanceof
As we’ve seen, the prototype object is fundamental to the identity of a class: two objects are instances of the same class if and only if they inherit from the same prototype object. The constructor function that initializes the state of a new object is not fundamental: two constructor functions may have prototype properties that point to the same prototype object. Then, both constructors can be used to create instances of the same class.

> 正如我们所看到的，原型对象是类的基本标识：只有两个对象继承同一原型对象时，这两个对象是同一类实例。构造函数的关键点不是初始化新创建对象的状态：两个构造函数可能具有指向同一原型对象的原型属性。那么，两个构造函数都可用于创建同一类的实例。

Even though constructors are not as fundamental as prototypes, the constructor serves as the public face of a class. Most obviously, the name of the constructor function is usually adopted as the name of the class. We say, for example, that the Range() constructor creates Range objects. More fundamentally, however, constructors are used as the righthand operand of the instanceof operator when testing objects for membership in a class. If we have an object r and want to know if it is a Range object, we can write:

> 尽管构造函数不像原型那样重要，但是构造函数充当 class 的大众脸。最明显的是，构造函数的名称通常用作类的名称。例如，我们说 Range() 构造函数创建 Range 对象。然而，更重要的是测试类中对象的成员关系，构造函数在右边被用作 instanceof 运算符的操作数。如果有一个对象 r，并且想知道它是不是一个 Range 对象，可以这样写：

```js
r instanceof Range   // => true: r inherits from Range.prototype
```
The instanceof operator was described in §4.9.4. The lefthand operand should be the object that is being tested, and the righthand operand should be a constructor function that names a class. The expression o instanceof C evaluates to true if o inherits from C.prototype. The inheritance need not be direct: if o inherits from an object that inherits from an object that inherits from C.prototype, the expression will still evaluate to true.

> instanceof 运算符在 §4.9.4 中有描述。左边的操作数是想要测试的对象，右边的操作数是命名类的构造函数。表达式 `o instanceof C` 计算结果为 true 时，o 继承自 C.prototype。不需要直接继承：如果 o 继承于一个继承了 C.prototype 的对象，表达式的计算结果也仍会是 true。

Technically speaking, in the previous code example, the instanceof operator is not checking whether r was actually initialized by the Range constructor. Instead, it is checking whether r inherits from Range.prototype. If we define a function Strange() and set its prototype to be the same as Range.prototype, then objects created with new Strange() will count as Range objects as far as instanceof is concerned (they won’t actually work as Range objects, however, because their from and to properties have not been initialized):

> 从技术上讲，在上一个代码示例中，instanceof 运算符的实例没有检查 r 是否实际由 Range 构造函数初始化。相反，它是检查 r 是否继承 Range.prototype。如果我们定义一个函数 Strange() 并将其原型设置与 Range.prototype 相同，则使用新 Strange() 创建的对象用 instanceof 运算符将算作 Range 对象（但是，它们实际上不会作为 Range 对象工作，因为它们的 from 和 to 属性尚未初始化）：

```js
function Strange() {}
Strange.prototype = Range.prototype;
new Strange() instanceof Range   // => true
```
Even though instanceof cannot actually verify the use of a constructor, it still uses a constructor function as its righthand side because constructors are the public identity of a class.

> 实际上即使 instanceof 不能验证使用了构造函数，它仍然使用构造函数作为其右侧，因为构造函数是类的公共标识。

If you want to test the prototype chain of an object for a specific prototype and do not want to use the constructor function as an intermediary, you can use the isPrototypeOf() method. In Example 9-1, for example, we defined a class without a constructor function, so there is no way to use instanceof with that class. Instead, however, we could test whether an object r was a member of that constructor-less class with this code:

> 如果要为特定原型测试对象的原型链，并且不想将构造函数用作媒介，可以使用 isPrototypeOf() 方法。例如，在示例 9-1 中，我们定义了一个没有构造函数的类，因此无法将 instanceof 与该类一起使用。但是，我们可以测试对象 r 是否是具有此代码的无构造函数类的成员：

```js
range.methods.isPrototypeOf(r);  // range.methods is the prototype object.
```
### 9.2.2 The constructor Property
In Example 9-2, we set Range.prototype to a new object that contained the methods for our class. Although it was convenient to express those methods as properties of a single object literal, it was not actually necessary to create a new object. Any regular JavaScript function (excluding arrow functions, generator functions, and async functions) can be used as a constructor, and constructor invocations need a prototype property. Therefore, every regular JavaScript function1 automatically has a prototype property. The value of this property is an object that has a single, non-enumerable constructor property. The value of the constructor property is the function object:

> 在示例 9-2 中，将 Range.prototype 定义为一个新对象，这个对象包含类所需要的方法。其实没有必要新创建一个对象，用单个对象字面量的属性就可以方便地定义原型上的方法。任何普通 JavaScript 函数（除箭头函数、生成器函数和异步函数之外）都可以用做构造函数，并且调用构造函数是需要一个 prototype 属性的。因此，每个 JavaScript 函数都自动拥有一个 prototype 属性。这个属性的值是一个对象，这个对象包含唯一一个不可枚举属性 constructor。constructor 属性的值是一个函数对象：

```js
let F = function() {}; // This is a function object.
let p = F.prototype;   // This is the prototype object associated with F.
let c = p.constructor; // This is the function associated with the prototype.
c === F                // => true: F.prototype.constructor === F for any F
```
The existence of this predefined prototype object with its constructor property means that objects typically inherit a constructor property that refers to their constructor. Since constructors serve as the public identity of a class, this constructor property gives the class of an object:

> 可以看到构造函数的原型中存在预先定义好的 constructor 属性，这意味着对象通常继承的 constructor 是它们的构造函数的引用。由于构造函数是类的“公共标识”， 因此这个 constructor 属性为对象提供了类。

```js
let o = new F();      // Create an object o of class F
o.constructor === F   // => true: the constructor property specifies the class
```
Figure 9-1 illustrates this relationship between the constructor function, its prototype object, the back reference from the prototype to the constructor, and the instances created with the constructor.

> 如图 9-1 所示，图 9-1 展示了构造函数和原型对象之间的关系，包括原型到构造函数的反向引用以及构造函数创建的实例。

<Figures figure="9-1">A constructor function, its prototype, and instances</Figures>

Notice that Figure 9-1 uses our Range() constructor as an example. In fact, however, the Range class defined in Example 9-2 overwrites the predefined Range.prototype object with an object of its own. And the new prototype object it defines does not have a constructor property. So instances of the Range class, as defined, do not have a constructor property. We can remedy this problem by explicitly adding a constructor to the prototype:

> 需要注意的是，图 9-1 用 Range() 构造函数作为示例。但实际上，示例 9-2 中定义的 Range 类使用它自身的一个新对象重写了预定义的 Range.prototype 对象。这个新定义的原型对象不含有 constructor 属性。因此 Range 类的实例也不含有 constructor 属性。我们可以通过补救措施来修正这个问题，显式给原型添加一个构造函数：

```js
Range.prototype = {
    constructor: Range,  // Explicitly set the constructor back-reference

    /* method definitions go here */
};
```
Another common technique that you are likely to see in older JavaScript code is to use the predefined prototype object with its constructor property and add methods to it one at a time with code like this:

> 另一种常见的解决办法是使用预定义的原型对象，预定义的原型对象包含 constructor 属性，然后依次给原型对象添加方法：

```js
// Extend the predefined Range.prototype object so we don't overwrite
// the automatically created Range.prototype.constructor property.
Range.prototype.includes = function(x) {
    return this.from <= x && x <= this.to;
};
Range.prototype.toString = function() {
    return "(" + this.from + "..." + this.to + ")";
};
```
## 9.3 Classes with the class Keyword
Classes have been part of JavaScript since the very first version of the language, but in ES6, they finally got their own syntax with the introduction of the class keyword. Example 9-3 shows what our Range class looks like when written with this new syntax.

> 类自第一个版本以来一直是 JavaScript 的一部分，但在 ES6 中，它们最终引入 class 关键字得到了自己的语法。示例 9-3 显示了使用此新语法编写 Range 类的实现。

Example 9-3. The Range class rewritten using class

> 示例 9-3：使用 class 编写 Range 类

```js
class Range {
    constructor(from, to) {
        // Store the start and end points (state) of this new range object.
        // These are noninherited properties that are unique to this object.
        this.from = from;
        this.to = to;
    }

    // Return true if x is in the range, false otherwise
    // This method works for textual and Date ranges as well as numeric.
    includes(x) { return this.from <= x && x <= this.to; }

    // A generator function that makes instances of the class iterable.
    // Note that it only works for numeric ranges.
    *[Symbol.iterator]() {
        for(let x = Math.ceil(this.from); x <= this.to; x++) yield x;
    }

    // Return a string representation of the range
    toString() { return `(${this.from}...${this.to})`; }
}

// Here are example uses of this new Range class
let r = new Range(1,3);   // Create a Range object
r.includes(2)             // => true: 2 is in the range
r.toString()              // => "(1...3)"
[...r]                    // => [1, 2, 3]; convert to an array via iterator
```
It is important to understand that the classes defined in Examples 9-2 and 9-3 work in exactly the same way. The introduction of the class keyword to the language does not alter the fundamental nature of JavaScript’s prototype-based classes. And although Example 9-3 uses the class keyword, the resulting Range object is a constructor function, just like the version defined in Example 9-2. The new class syntax is clean and convenient but is best thought of as “syntactic sugar” for the more fundamental class definition mechanism shown in Example 9-2.

> 重要的是要了解，在示例 9-2 和 9-3 中定义的类的工作方式完全相同。将 class 关键字引入语言并不会改变 JavaScript 基于原型的类的基本性质。尽管示例 9-3 使用 class 关键字，但生成的 Range 对象是一个构造函数，就像示例 9-2 中定义的版本一样。新的 class 语法更清洁方便，但是最好将其看作示例 9-2 所示的基本类定义机制的语法糖。

Note the following things about the class syntax in Example 9-3:

> 注意在示例 9-3 中关于 class 语法的一下几点：

The class is declared with the class keyword, which is followed by the name of class and a class body in curly braces.

> 用 class 关键字声明类，后面接一个类名，最后是花括号包含类的正文。

The class body includes method definitions that use object literal method shorthand (which we also used in Example 9-1), where the function keyword is omitted. Unlike object literals, however, no commas are used to separate the methods from each other. (Although class bodies are superficially similar to object literals, they are not the same thing. In particular, they do not support the definition of properties with name/value pairs.)

> 类正文包括使用对象字面量方法速记定义的方法（我们在示例 9-1 中也使用了），其中省略了函数关键字。但是，与对象字面量不同，没有用逗号将方法彼此分开。（虽然类正文表面上与对象字面量相似，但它们不是一回事。与对象不同，类不支持具有名/值对的属性的定义。

The keyword constructor is used to define the constructor function for the class. The function defined is not actually named “constructor”, however. The class declaration statement defines a new variable Range and assigns the value of this special constructor function to that variable.

> 关键字 constructor 用于定义类的构造函数。但是，定义的函数实际上并不命名为 constructor。类声明语句定义一个新的变量 Range，并将此特殊构造函数的值分配给该变量。

If your class does not need to do any initialization, you can omit the constructor keyword and its body, and an empty constructor function will be implicitly created for you.

> 如果类不需要执行任何初始化，可以省略构造函数关键字及其正文，并将隐式创建一个空构造函数。

If you want to define a class that subclasses—or inherits from—another class, you can use the extends keyword with the class keyword:

> 如果要定义子类（或继承来自另一个类的类），可以使用 extends 关键字与 class 关键字：

```js
// A Span is like a Range, but instead of initializing it with
// a start and an end, we initialize it with a start and a length
class Span extends Range {
    constructor(start, length) {
        if (length >= 0) {
            super(start, start + length);
        } else {
            super(start + length, start);
        }
    }
}
```
Creating subclasses is a whole topic of its own. We’ll return to it, and explain the extends and super keywords shown here, in §9.5.

> 创建子类是完整的一节。我们将在 §9.5 重新讲到它，并解释这里的 extends 和 super 关键字。

Like function declarations, class declarations have both statement and expression forms. Just as we can write:

> 与函数声明一样，类声明同时具有语句和表达式形式。正如我们可以写：

```js
let square = function(x) { return x * x; };
square(3)  // => 9
we can also write:

let Square = class { constructor(x) { this.area = x * x; } };
new Square(3).area  // => 9
```
As with function definition expressions, class definition expressions can include an optional class name. If you provide such a name, that name is only defined within the class body itself.

> 与函数定义表达式一样，类定义表达式可以包含可选类名。如果提供这样的名称，则该名称仅在类正文本身中有定义。

Although function expressions are quite common (particularly with the arrow function shorthand), in JavaScript programming, class definition expressions are not something that you are likely to use much unless you find yourself writing a function that takes a class as its argument and returns a subclass.

> 尽管函数表达式很常见（尤其是使用箭头函数），但 JavaScript 编程中，类定义表达式可能并不是经常使用，除非正在编写一个以类为实参并返回子类的函数。

We’ll conclude this introduction to the class keyword by mentioning a couple of important things you should know that are not apparent from class syntax:

> 结束对 class 关键字的介绍前，最后提几个重要但是不易注意的类语法：

All code within the body of a class declaration is implicitly in strict mode (§5.6.3), even if no "use strict" directive appears. This means, for example, that you can’t use octal integer literals or the with statement within class bodies and that you are more likely to get syntax errors if you forget to declare a variable before using it.

> 类声明正文中的所有代码都隐式采用严格模式（§5.6.3），即使未出现"use strict"指令。例如，这意味着不能在类正文中使用八进制整数字面量或 with 语句，并且如果在使用变量之前忘记声明变量，则更有可能出现语法错误。

Unlike function declarations, class declarations are not “hoisted.” Recall from §8.1.1 that function definitions behave as if they had been moved to the top of the enclosing file or enclosing function, meaning that you can invoke a function in code that comes before the actual definition of the function. Although class declarations are like function declarations in some ways, they do not share this hoisting behavior: you cannot instantiate a class before you declare it.

> 与函数声明不同，类声明不是"声明提前"的。回想一下 §8.1.1 中，函数定义的行为就像它们被移动到封闭文件的顶部或封闭函数的顶部一样，这意味着可以在函数实际定义之前的代码中调用函数。尽管类声明在某些方面与函数声明一样，但它们不共享这种提前行为：在声明类之前，不能实例化类。

### 9.3.1 Static Methods
You can define a static method within a class body by prefixing the method declaration with the static keyword. Static methods are defined as properties of the constructor function rather than properties of the prototype object.

> 可以通过使用 static 关键字作为方法声明前缀来定义类正文中的静态方法。静态方法定义为构造函数的属性，而不是原型对象的属性。

For example, suppose we added the following code to Example 9-3:

> 例如，假设我们将以下代码添加到示例 9-3 中：

```js
static parse(s) {
    let matches = s.match(/^\((\d+)\.\.\.(\d+)\)$/);
    if (!matches) {
        throw new TypeError(`Cannot parse Range from "${s}".`)
    }
    return new Range(parseInt(matches[1]), parseInt(matches[2]));
}
```
The method defined by this code is Range.parse(), not Range.prototype.parse(), and you must invoke it through the constructor, not through an instance:

> 此代码定义的方法是 Range.parse()， 而不是 Range.prototype.parse()， 必须通过构造函数而不是通过实例调用它：

```js
let r = Range.parse('(1...10)'); // Returns a new Range object
r.parse('(1...10)');             // TypeError: r.parse is not a function
```
You’ll sometimes see static methods called class methods because they are invoked using the name of the class/constructor. When this term is used, it is to contrast class methods with the regular instance methods that are invoked on instances of the class. Because static methods are invoked on the constructor rather than on any particular instance, it almost never makes sense to use the this keyword in a static method.

> 有时会看到静态方法称为类方法，因为它们是使用类/构造函数的名称调用的。使用此术语时，将类方法与在类实例上调用的常规实例方法进行对比，由于静态方法在构造函数上调用，而不是在任何特定实例上调用，因此在静态方法中使用 this 关键字几乎从来就没有意义。

We’ll see examples of static methods in Example 9-4.

> 我们将在示例 9-4 中看到静态方法的示例。

### 9.3.2 Getters, Setters, and other Method Forms
Within a class body, you can define getter and setter methods (§6.10.6) just as you can in object literals. The only difference is that in class bodies, you don’t put a comma after the getter or setter. Example 9-4 includes a practical example of a getter method in a class.

> 在类正文中，可以定义 getter 和 setter 方法（§6.10.6），就像在对象字面量中一样。唯一的区别是，在类正文中，不会将逗号放在 getter 或 setter 之后。示例 9-4 包括类中 getter 方法的实际示例。

In general, all of the shorthand method definition syntaxes allowed in object literals are also allowed in class bodies. This includes generator methods (marked with *) and methods whose names are the value of an expression in square brackets. In fact, you’ve already seen (in Example 9-3) a generator method with a computed name that makes the Range class iterable:

> 通常，对象字面量中允许的所有速记方法定义语法也允许在类正文中使用。这包括生成器方法（用 * 标记）和名称为方括号中表达式值的方法。事实上，已经看到了（在示例 9-3 中）具有计算名称的生成器方法，该方法使 Range 类可重复：

```js
*[Symbol.iterator]() {
    for(let x = Math.ceil(this.from); x <= this.to; x++) yield x;
}
```
### 9.3.3 Public, Private, and Static Fields
In the discussion here of classes defined with the class keyword, we have only described the definition of methods within the class body. The ES6 standard only allows the creation of methods (including getters, setters, and generators) and static methods; it does not include syntax for defining fields. If you want to define a field (which is just an object-oriented synonym for “property”) on a class instance, you must do that in the constructor function or in one of the methods. And if you want to define a static field for a class, you must do that outside the class body, after the class has been defined. Example 9-4 includes examples of both kinds of fields.

> 在此处对使用 class 关键字定义的类的讨论中，我们只描述了类正文中方法的定义。ES6 标准只允许创建方法（包括 getter、setter 和生成器）和静态方法；它不包括用于定义字段的语法。如果要在类实例上定义字段（这只是面向对象中"属性"的同义词），则必须在构造函数函数或其中一个方法中这样做。必须在类正文之外类定义后，才能为类定义静态字段。示例 9-4 包括这各种字段的示例。

Standardization is underway, however, for extended class syntax that allows the definition of instance and static fields, in both public and private forms. The code shown in the rest of this section is not yet standard JavaScript as of early 2020 but is already supported in Chrome and partially supported (public instance fields only) in Firefox. The syntax for public instance fields is in common use by JavaScript programmers using the React framework and the Babel transpiler.

> 但是，对于允许以公有和私有形式定义实例和静态字段的扩展类语法正在进行标准化。本节其余部分中显示的代码在 2020 年初还不是标准 JavaScript，但在 Chrome 中已经支持，并且 Firefox 中已部分支持（仅使公有实例字段）。使用 React 框架和 Babel 编译器的 JavaScript 程序员常用公有实例字段的语法。

Suppose you’re writing a class like this one, with a constructor that initializes three fields:

> 假设你正在编写一个这样的类，其中一个构造函数初始化了三个字段：

```js
class Buffer {
    constructor() {
        this.size = 0;
        this.capacity = 4096;
        this.buffer = new Uint8Array(this.capacity);
    }
}
```
With the new instance field syntax that is likely to be standardized, you could instead write:

> 使用可能标准化的新实例字段语法，可以这样编写：

```js
class Buffer {
    size = 0;
    capacity = 4096;
    buffer = new Uint8Array(this.capacity);
}
```
The field initialization code has moved out of the constructor and now appears directly in the class body. (That code is still run as part of the constructor, of course. If you do not define a constructor, the fields are initialized as part of the implicitly created constructor.) The this. prefixes that appeared on the lefthand side of the assignments are gone, but note that you still must use this. to refer to these fields, even on the righthand side of the initializer assignments. The advantage of initializing your instance fields in this way is that this syntax allows (but does not require) you to put the initializers up at the top of the class definition, making it clear to readers exactly what fields will hold the state of each instance. You can declare fields without an initializer by just writing the name of the field followed by a semicolon. If you do that, the initial value of the field will be undefined. It is better style to always make the initial value explicit for all of your class fields.

> 字段初始化代码已移出构造函数，现在直接显示在类正文中。（当然，该代码仍作为构造函数的一部分运行。如果不定义构造函数，则字段初始化为隐式创建的构造函数的一部分。赋值左侧的 this. 前缀消失，但请注意即使是在初始化赋值的右侧，仍必须使用 this. 前缀引用这些字段。这种方式初始化实例字段的优点是，此语法允许（但不需要）将初始化放在类定义的顶部，使读者清楚地了解字段在每个实例将保存的状态。可以通过字段名后面跟一个分号来只声明不初始化一个字段。如果这样做，字段的初始值将是 undefined。显式设定初始化字段的值是比较好的风格。

Before the addition of this field syntax, class bodies looked a lot like object literals using shortcut method syntax, except that the commas had been removed. This field syntax—with equals signs and semicolons instead of colons and commas—makes it clear that class bodies are not at all the same as object literals.

> 在添加字段语法之前，类正文看起来很像使用快捷方法语法的对象字面量，只不过逗号被删除。字段语法（使用等号和分号代替冒号和逗号）清楚地表明类正文与对象字面量不完全相同。

The same proposal that seeks to standardize these instance fields also defines private instance fields. If you use the instance field initialization syntax shown in the previous example to define a field whose name begins with # (which is not normally a legal character in JavaScript identifiers), that field will be usable (with the # prefix) within the class body but will be invisible and inaccessible (and therefore immutable) to any code outside of the class body. If, for the preceding hypothetical Buffer class, you wanted to ensure that users of the class could not inadvertently modify the size field of an instance, you could use a private #size field instead, then define a getter function to provide read-only access to the value:

> 标准化中的实例字段同时也定义了私有实例字段。如果使用上例中所示的实例字段初始化语法来定义其名称以 # 开头的字段（在 JavaScript 标识符中通常不是合法字符），则该字段在类正文中可用（使用 # 前缀），但对类正文之外的任何代码不可见且不可访问（因此不可变）。如果对于前面的 Buffer 类，要确保类的用户不会无意中修改实例的 size 字段，可以改为使用私有 #size 字段，然后定义 getter 函数以提供对值的只读访问：

```js
class Buffer {
    #size = 0;
    get size() { return this.#size; }
}
```
Note that private fields must be declared using this new field syntax before they can be used. You can’t just write this.#size = 0; in the constructor of a class unless you include a “declaration” of the field directly in the class body.

> 请注意，必须先使用新字段语法声明私有字段，然后才能使用它们。你不能只在类的构造函数中写 `this.#size = 0;`，除非直接在类正文中包含字段的"声明"。

Finally, a related proposal seeks to standardize the use of the static keyword for fields. If you add static before a public or private field declaration, those fields will be created as properties of the constructor function instead of properties of instances. Consider the static Range.parse() method we’ve defined. It included a fairly complex regular expression that might be good to factor out into its own static field. With the proposed new static field syntax, we could do that like this:

> 最后，在标准化过程中相关建议字段使用 static 关键字。如果在公有或私有字段声明之前添加静态字段，这些字段将创建为构造函数的属性，而不是实例的属性。思考我们定义的静态 Range.parse() 方法。它包括一个相当复杂的正则表达式，将其拆分到它自有的静态字段中可能会更好。使用建议的新静态字段语法，我们可以这编写：

```js
static integerRangePattern = /^\((\d+)\.\.\.(\d+)\)$/;
static parse(s) {
    let matches = s.match(Range.integerRangePattern);
    if (!matches) {
        throw new TypeError(`Cannot parse Range from "${s}".`)
    }
    return new Range(parseInt(matches[1]), matches[2]);
}
```
If we wanted this static field to be accessible only within the class, we could make it private using a name like #pattern.

> 如果我们希望此静态字段只能在类中访问，我们可以使用像 #pattern 这样的名称将其私有化。

### 9.3.4 Example: A Complex Number Class
Example 9-4 defines a class to represent complex numbers. The class is a relatively simple one, but it includes instance methods (including getters), static methods, instance fields, and static fields. It includes some commented-out code demonstrating how we might use the not-yet-standard syntax for defining instance fields and static fields within the class body.

> 示例 9-4 定义了一个表示复数的类。该类相对简单，但它包括实例方法（包括 getters）、静态方法、实例字段和静态字段。它包括一些注释掉的代码，演示如何使用尚未加入标准的语法定义类正文中的实例字段和静态字段。

Example 9-4. Complex.js: a complex number class

> 示例 9-4：Complex.js：一个复数类

```js
/**
 * Instances of this Complex class represent complex numbers.
 * Recall that a complex number is the sum of a real number and an
 * imaginary number and that the imaginary number i is the square root of -1.
 */
class Complex {
    // Once class field declarations are standardized, we could declare
    // private fields to hold the real and imaginary parts of a complex number
    // here, with code like this:
    //
    // #r = 0;
    // #i = 0;

    // This constructor function defines the instance fields r and i on every
    // instance it creates. These fields hold the real and imaginary parts of
    // the complex number: they are the state of the object.
    constructor(real, imaginary) {
        this.r = real;       // This field holds the real part of the number.
        this.i = imaginary;  // This field holds the imaginary part.
    }

    // Here are two instance methods for addition and multiplication
    // of complex numbers. If c and d are instances of this class, we
    // might write c.plus(d) or d.times(c)
    plus(that) {
        return new Complex(this.r + that.r, this.i + that.i);
    }
    times(that) {
        return new Complex(this.r * that.r - this.i * that.i,
                           this.r * that.i + this.i * that.r);
    }

    // And here are static variants of the complex arithmetic methods.
    // We could write Complex.sum(c,d) and Complex.product(c,d)
    static sum(c, d) { return c.plus(d); }
    static product(c, d) { return c.times(d); }

    // These are some instance methods that are defined as getters
    // so they're used like fields. The real and imaginary getters would
    // be useful if we were using private fields this.#r and this.#i
    get real() { return this.r; }
    get imaginary() { return this.i; }
    get magnitude() { return Math.hypot(this.r, this.i); }

    // Classes should almost always have a toString() method
    toString() { return `{${this.r},${this.i}}`; }

    // It is often useful to define a method for testing whether
    // two instances of your class represent the same value
    equals(that) {
        return that instanceof Complex &&
            this.r === that.r &&
            this.i === that.i;
    }

    // Once static fields are supported inside class bodies, we could
    // define a useful Complex.ZERO constant like this:
    // static ZERO = new Complex(0,0);
}

// Here are some class fields that hold useful predefined complex numbers.
Complex.ZERO = new Complex(0,0);
Complex.ONE = new Complex(1,0);
Complex.I = new Complex(0,1);
```

With the Complex class of Example 9-4 defined, we can use the constructor, instance fields, instance methods, class fields, and class methods with code like this:

> 定义了示例 9-4 的 Complex 类后，我们可以将构造函数、实例字段、实例方法、类字段和类方法如下使用：

```js
let c = new Complex(2, 3);     // Create a new object with the constructor
let d = new Complex(c.i, c.r); // Use instance fields of c
c.plus(d).toString()           // => "{5,5}"; use instance methods
c.magnitude                    // => Math.hypot(2,3); use a getter function
Complex.product(c, d)          // => new Complex(0, 13); a static method
Complex.ZERO.toString()        // => "{0,0}"; a static property
```
## 9.4 Adding Methods to Existing Classes
JavaScript’s prototype-based inheritance mechanism is dynamic: an object inherits properties from its prototype, even if the properties of the prototype change after the object is created. This means that we can augment JavaScript classes simply by adding new methods to their prototype objects.

> JavaScript 基于原型的继承机制是动态的：对象从其原型继承属性，即使原型的属性在创建对象后发生更改。这意味着我们只需向原型对象添加新方法，即可扩展 JavaScript 类。

Here, for example, is code that adds a method for computing the complex conjugate to the Complex class of Example 9-4:

> 例如，下面是将计算共轭复数的方法添加到示例 9-4 的 Complex 类的代码：

```js
// Return a complex number that is the complex conjugate of this one.
Complex.prototype.conj = function() { return new Complex(this.r, -this.i); };
```

The prototype object of built-in JavaScript classes is also open like this, which means that we can add methods to numbers, strings, arrays, functions, and so on. This is useful for implementing new language features in older versions of the language:

> JavaScript 类内置的原型对象也是这样展现的，这意味着我们可以向数字、字符串、数组、函数等添加方法。这对于在旧版本的语言中实现新特性非常有用：

```js
// If the new String method startsWith() is not already defined...
if (!String.prototype.startsWith) {
    // ...then define it like this using the older indexOf() method.
    String.prototype.startsWith = function(s) {
        return this.indexOf(s) === 0;
    };
}
```

Here is another example:

> 这是另外一个例子：

```js
// Invoke the function f this many times, passing the iteration number
// For example, to print "hello" 3 times:
//     let n = 3;
//     n.times(i => { console.log(`hello ${i}`); });
Number.prototype.times = function(f, context) {
    let n = this.valueOf();
    for(let i = 0; i < n; i++) f.call(context, i);
};
```
Adding methods to the prototypes of built-in types like this is generally considered to be a bad idea because it will cause confusion and compatibility problems in the future if a new version of JavaScript defines a method with the same name. It is even possible to add methods to Object.prototype, making them available for all objects. But this is never a good thing to do because properties added to Object.prototype are visible to for/in loops (though you can avoid this by using Object.defineProperty() [§14.1] to make the new property non-enumerable).

> 向这样在内置类型的原型添加方法通常被认为是一个坏主意，因为如果新版本的 JavaScript 定义具有相同名称的方法，将来就会造成混淆和兼容性问题。甚至可以向 Object.prototype 添加方法，使它们可作用于所有对象。但这从来就不是一件好事，因为添加到 Object.prototype 的属性对 for/in 循环可见（尽管可以使用 Object.defineProperty()（§14.1）来使新属性不可枚举来避免这种情况）。

## 9.5 Subclasses
In object-oriented programming, a class B can extend or subclass another class A. We say that A is the superclass and B is the subclass. Instances of B inherit the methods of A. The class B can define its own methods, some of which may override methods of the same name defined by class A. If a method of B overrides a method of A, the overriding method in B often needs to invoke the overridden method in A. Similarly, the subclass constructor B() must typically invoke the superclass constructor A() in order to ensure that instances are completely initialized.

> 在面向对象的编程中，B 类可以扩展 A 类或成为 A 类子类。我们称 A 是父类，B 是子类。B 的实例继承 A 的方法。B 类可以定义自有方法，使用相同名称可以重写类 A 中的方法。如果 B 的方法重写 A 方法，则 B 中的重写方法通常需要调用 A 中的重写方法。同样，子类构造函数 B() 通常必须调用父类构造函数 A()，以确保实例完全初始化。

This section starts by showing how to define subclasses the old, pre-ES6 way, and then quickly moves on to demonstrate subclassing using the class and extends keywords and superclass constructor method invocation with the super keyword. Next is a subsection about avoiding subclasses and relying on object composition instead of inheritance. The section ends with an extended example that defines a hierarchy of Set classes and demonstrates how abstract classes can be used to separate interface from implementation.

> 本节首先演示 ES6 之前如何定义子类，然后演示使用 class 和 extends 关键字的子类和使用 super 关键字调用父类构造函数。再接下来一节是关于避免使用子类而依靠对象组合代替继承。本章最后结束于一个扩展的示例，定义 Set 类的层次结构和演示如何使用抽象类将接口与实现分离。

### 9.5.1 Subclasses and Prototypes
Suppose we wanted to define a Span subclass of the Range class from Example 9-2. This subclass will work just like a Range, but instead of initializing it with a start and an end, we’ll instead specify a start and a distance, or span. An instance of this Span class is also an instance of the Range superclass. A span instance inherits a customized toString() method from Span.prototype, but in order to be a subclass of Range, it must also inherit methods (such as includes()) from Range.prototype.

> 假设我们想要给示例 9-2 中 Range 类定义 Span 子类。此子类的工作方式与 Range 一样，但我们初始化改为指定开始和范围，而不是制定开始和结束。Span 类的实例也是父类 Range 的实例。Span 实例从 Span.prototype 继承自定义的 toString() 方法，但为了成为 Range 的子类，它还必须从 Range.prototype 继承方法（如 includes()）。

Example 9-5. Span.js: a simple subclass of Range

> 实例 9-5：Span.js：Range 一个简单的子类

```js
// This is the constructor function for our subclass
function Span(start, span) {
    if (span >= 0) {
        this.from = start;
        this.to = start + span;
    } else {
        this.to = start;
        this.from = start + span;
    }
}

// Ensure that the Span prototype inherits from the Range prototype
Span.prototype = Object.create(Range.prototype);

// We don't want to inherit Range.prototype.constructor, so we
// define our own constructor property.
Span.prototype.constructor = Span;

// By defining its own toString() method, Span overrides the
// toString() method that it would otherwise inherit from Range.
Span.prototype.toString = function() {
    return `(${this.from}... +${this.to - this.from})`;
};
```
In order to make Span a subclass of Range, we need to arrange for Span.prototype to inherit from Range.prototype. The key line of code in the preceding example is this one, and if it makes sense to you, you understand how subclasses work in JavaScript:

> 为了使 Span 成为 Range 的子类，我们需要使 Span.prototype 从 Range.prototype 继承。前面示例中的关键代码行是此代码行，如果能理解子类使如何工作的，它是非常有意义的：

```js
Span.prototype = Object.create(Range.prototype);
```

Objects created with the Span() constructor will inherit from the Span.prototype object. But we created that object to inherit from Range.prototype, so Span objects will inherit from both Span.prototype and Range.prototype.

> 使用 Span() 构造函数创建的对象将从 Span.prototype 对象继承。但是，我们创建了该对象并继承 Range.prototype，因此 Span 对象将同时从 Span.prototype 和 Range.prototype 继承。

You may notice that our Span() constructor sets the same from and to properties that the Range() constructor does and so does not need to invoke the Range() constructor to initialize the new object. Similarly, Span’s toString() method completely re-implements the string conversion without needing to call Range’s version of toString(). This makes Span a special case, and we can only really get away with this kind of subclassing because we know the implementation details of the superclass. A robust subclassing mechanism needs to allow classes to invoke the methods and constructor of their superclass, but prior to ES6, JavaScript did not have a simple way to do these things.

> 可能会注意到，我们的 Span() 构造函数设置与 Range() 构造函数相同的 from 和 to 属性，因此不需要调用 Range() 构造函数来初始化新对象。同样，Span 的 toString() 方法完全重新实现字符串转换，而无需调用 Range 版本的 toString()。这使得 Span 成为特例，我们必须摆脱这种子类，因为这种情况是我们知道父类的实现细节。一个健壮的子类机制需要允许类调用其父类的方法和构造函数，但在 ES6 之前，JavaScript 没有一个简单的方法来执行这些操作。

Fortunately, ES6 solves these problems with the super keyword as part of the class syntax. The next section demonstrates how it works.

> 幸运的是，ES6 用 super 关键字作为类语法一部分解决了这些问题。下一节演示它是如何工作的。

### 9.5.2 Subclasses with extends and super
In ES6 and later, you can create a superclass simply by adding an extends clause to a class declaration, and you can do this even for built-in classes:

> 在 ES6 之后，可以简单的在类声明时接一个 extends 从句添加一个父类，即使对于内置类也可以这样做：

```js
// A trivial Array subclass that adds getters for the first and last elements.
class EZArray extends Array {
    get first() { return this[0]; }
    get last() { return this[this.length-1]; }
}

let a = new EZArray();
a instanceof EZArray  // => true: a is subclass instance
a instanceof Array    // => true: a is also a superclass instance.
a.push(1,2,3,4);      // a.length == 4; we can use inherited methods
a.pop()               // => 4: another inherited method
a.first               // => 1: first getter defined by subclass
a.last                // => 3: last getter defined by subclass
a[1]                  // => 2: regular array access syntax still works.
Array.isArray(a)      // => true: subclass instance really is an array
EZArray.isArray(a)    // => true: subclass inherits static methods, too!
```
This EZArray subclass defines two simple getter methods. Instances of EZArray behave like ordinary arrays, and we can use inherited methods and properties like push(), pop(), and length. But we can also use the first and last getters defined in the subclass. Not only are instance methods like pop() inherited, but static methods like Array.isArray are also inherited. This is a new feature enabled by ES6 class syntax: EZArray() is a function, but it inherits from Array():

> EZArray 子类定义了两个简单的 getter 方法。EZArray 实例的行为类似于普通数组，我们可以使用继承的方法和属性，如 push()、pop() 和 length。但是，我们也可以使用子类中定义的 first 和 last getter 方法。不仅继承实例方法如 pop() ，也继承 Array.isArray 等静态方法。这是 ES6 类语法启用的新特性：EZArray() 是一个函数，但它从 Array() 继承：

```js
// EZArray inherits instance methods because EZArray.prototype
// inherits from Array.prototype
Array.prototype.isPrototypeOf(EZArray.prototype) // => true

// And EZArray inherits static methods and properties because
// EZArray inherits from Array. This is a special feature of the
// extends keyword and is not possible before ES6.
Array.isPrototypeOf(EZArray) // => true
```
Our EZArray subclass is too simple to be very instructive. Example 9-6 is a more fully fleshed-out example. It defines a TypedMap subclass of the built-in Map class that adds type checking to ensure that the keys and values of the map are of the specified types (according to typeof). Importantly, this example demonstrates the use of the super keyword to invoke the constructor and methods of the superclass.

> EZArray 子类太简单了，没有教育意义。示例 9-6 是一个更充实的示例。它定义了内置 Map 类的 TypedMap 子类，该子类添加类型检查以确保映射的键和值是指定的类型（根据 typeof）。重要的是，此示例演示了使用 super 关键字来调用父类的构造函数和方法。

Example 9-6. TypedMap.js: a subclass of Map that checks key and value types

> 示例 9-6：TypedMap.js：一个检测 key 和 value 类型的 Map 子类

```js
class TypedMap extends Map {
    constructor(keyType, valueType, entries) {
        // If entries are specified, check their types
        if (entries) {
            for(let [k, v] of entries) {
                if (typeof k !== keyType || typeof v !== valueType) {
                    throw new TypeError(`Wrong type for entry [${k}, ${v}]`);
                }
            }
        }

        // Initialize the superclass with the (type-checked) initial entries
        super(entries);

        // And then initialize this subclass by storing the types
        this.keyType = keyType;
        this.valueType = valueType;
    }

    // Now redefine the set() method to add type checking for any
    // new entries added to the map.
    set(key, value) {
        // Throw an error if the key or value are of the wrong type
        if (this.keyType && typeof key !== this.keyType) {
            throw new TypeError(`${key} is not of type ${this.keyType}`);
        }
        if (this.valueType && typeof value !== this.valueType) {
            throw new TypeError(`${value} is not of type ${this.valueType}`);
        }

        // If the types are correct, we invoke the superclass's version of
        // the set() method, to actually add the entry to the map. And we
        // return whatever the superclass method returns.
        return super.set(key, value);
    }
}
```
The first two arguments to the TypedMap() constructor are the desired key and value types. These should be strings, such as “number” and “boolean”, that the typeof operator returns. You can also specify a third argument: an array (or any iterable object) of [key,value] arrays that specify the initial entries in the map. If you specify any initial entries, then the first thing the constructor does is verify that their types are correct. Next, the constructor invokes the superclass constructor, using the super keyword as if it was a function name. The Map() constructor takes one optional argument: an iterable object of [key,value] arrays. So the optional third argument of the TypedMap() constructor is the optional first argument to the Map() constructor, and we pass it to that superclass constructor with super(entries).

> TypedMap() 构造函数的前两个实参是所需的键和值类型。这些实参应该是字符串，如"number"和"boolean"，这些字符串应该是 typeof 运算符的返回值。还可以指定第三个实参：指定 map 中初始条目的 [key,value] 数组（或任何可迭代对象）。如果指定任何初始条目，则构造函数要做的第一件事是验证其类型是否正确。接下来，构造函数调用父类构造函数，使用 super 关键字，就像它是一个函数名称一样。Map() 构造函数采用一个可选实参：可迭代对象 [key,value] 的数组。因此，TypedMap() 构造函数的第三个可选实参是 Map() 构造函数的第一个可选实参，我们用 `super(entries)` 将它传递给父类的构造函数。

After invoking the superclass constructor to initialize superclass state, the TypedMap() constructor next initializes its own subclass state by setting this.keyType and this.valueType to the specified types. It needs to set these properties so that it can use them again in the set() method.

> 调用父类构造函数初始化父类状态后，接下来 TypedMap() 构造函数初始化其自己的子类状态 this.keyType 和 this.valueType。它需要设置这些属性，以便它可以在 set() 方法中再次使用它们。

There are a few important rules that you will need to know about using super() in constructors:

> 在构造函数中使用 super() 需要了解一些重要规则：

If you define a class with the extends keyword, then the constructor for your class must use super() to invoke the superclass constructor.

> 如果使用 extends 关键字定义类，则类的构造函数必须使用 super() 调用父类构造函数。

If you don’t define a constructor in your subclass, one will be defined automatically for you. This implicitly defined constructor simply takes whatever values are passed to it and passes those values to super().

> 如果未在子类中定义构造函数，将自动为你定义一个构造函数。此隐式定义的构造函数只将传递给它值传递给 super()。

You may not use the this keyword in your constructor until after you have invoked the superclass constructor with super(). This enforces a rule that superclasses get to initialize themselves before subclasses do.

> 在使用 super() 调用父类构造函数之前，不能在构造函数中使用 this 关键字。这个强制规则确保父类先于子类初始化。

The special expression new.target is undefined in functions that are invoked without the new keyword. In constructor functions, however, new.target is a reference to the constructor that was invoked. When a subclass constructor is invoked and uses super() to invoke the superclass constructor, that superclass constructor will see the subclass constructor as the value of new.target. A well-designed superclass should not need to know whether it has been subclassed, but it might be useful to be able to use new.target.name in logging messages, for example.

> 在未使用 new 关键字调用的函数中，new.target 表达式是 undefined。但是，在构造函数中，new.target 是引用调用的构造函数。当调用子类构造函数并使用 super() 调用父类构造函数时，该父类构造函数将看到子类构造函数作为 new.target 的值。虽然设计良好的父类不需要知道它是否有子类，但，在日志记录消息的场景中使用 new.target.name 会很有用。

After the constructor, the next part of Example 9-6 is a method named set(). The Map superclass defines a method named set() to add a new entry to the map. We say that this set() method in TypedMap overrides the set() method of its superclass. This simple TypedMap subclass doesn’t know anything about adding new entries to map, but it does know how to check types, so that is what it does first, verifying that the key and value to be added to the map have the correct types and throwing an error if they do not. This set() method doesn’t have any way to add the key and value to the map itself, but that is what the superclass set() method is for. So we use the super keyword again to invoke the superclass’s version of the method. In this context, super works much like the this keyword does: it refers to the current object but allows access to overridden methods defined in the superclass.

> 在构造函数之后，示例 9-6 的下一部分是名为 set() 的方法。Map 父类定义了名为 set() 的方法，以向 Map 添加新条目。TypedMap 中的 set() 方法将重写其父类的 set() 方法。这个简单的 TypedMap 子类对向 Map 添加新条目一无所知，但它知道如何检查类型，因此它首先会这样做，验证要添加到地图中的键和值的类型是否正确，如果它们不正确则抛出异常。此 set() 方法无法将键和值添加到 Map 本身，但这就是父类 set() 方法的用途。因此，我们再次使用 super 关键字来调用父类版本的 set() 方法。在此上下文中，super 的工作方式与 this 关键字的工作方式非常相似：它引用当前对象，但允许访问在父级类中定义的被重写方法。

In constructors, you are required to invoke the superclass constructor before you can access this and initialize the new object yourself. There are no such rules when you override a method. A method that overrides a superclass method is not required to invoke the superclass method. If it does use super to invoke the overridden method (or any method) in the superclass, it can do that at the beginning or the middle or the end of the overriding method.

> 在构造函数中，需要先调用父类构造函数，然后才能访问 this 和初始化新对象。但重写方法时没有此类规则。调用重写父类方法时不需要调用父类方法。如果它确实使用 super 来调用父类中的重写方法（或任何方法），它可以在重写方法的开头、中间或末尾调用。

Finally, before we leave the TypedMap example behind, it is worth noting that this class is an ideal candidate for the use of private fields. As the class is written now, a user could change the keyType or valueType properties to subvert the type checking. Once private fields are supported, we could change these properties to #keyType and #valueType so that they could not be altered from the outside.

> 最后，在将 TypedMap 示例抛在脑后之前，值得注意的是，此类是使用私有字段的理想场景。现在编写类时，用户可以更改 keyType 或 valueType 属性以破坏类型检查。一旦支持私有字段，我们可以将这些属性改为 #keyType 和 #valueType，以便它们不能从外部更改。

### 9.5.3 Delegation Instead of Inheritance
The extends keyword makes it easy to create subclasses. But that does not mean that you should create lots of subclasses. If you want to write a class that shares the behavior of some other class, you can try to inherit that behavior by creating a subclass. But it is often easier and more flexible to get that desired behavior into your class by having your class create an instance of the other class and simply delegating to that instance as needed. You create a new class not by subclassing, but instead by wrapping or “composing” other classes. This delegation approach is often called “composition”, and it is an oft-quoted maxim of object-oriented programming that one should “favor composition over inheritance.”2

> extends 关键字便于创建子类。但这并不意味着应该创建大量的子类。如果要编写某些其他类共享的行为的类，可以尝试通过创建子类来继承该行为。但是，通常将期望的行为编写在类中比用类创建其他类的实例并根据需要委托给该实例更简单也更灵活。创建新类不将其作为子类，而是通过包装或"组合"其他类。这种委托方法通常称为"组合"，它是一种面向对象编程经常被引用的座右铭"倾向于组合而不是继承"。^2

Suppose, for example, we wanted a Histogram class that behaves something like JavaScript’s Set class, except that instead of just keeping track of whether a value has been added to set or not, it instead maintains a count of the number of times the value has been added. Because the API for this Histogram class is similar to Set, we might consider subclassing Set and adding a count() method. On the other hand, once we start thinking about how we might implement this count() method, we might realize that the Histogram class is more like a Map than a Set because it needs to maintain a mapping between values and the number of times they have been added. So instead of subclassing Set, we can create a class that defines a Set-like API but implements those methods by delegating to an internal Map object. Example 9-7 shows how we could do this.

> 例如，假设我们想要一个行为类似于 JavaScript 的 Set 类的 Histogram 类，只不过，它不只是跟踪是否给集合添加了值，还维护该值添加次数的计数。由于 Histogram 类的 API 与 Set 类似，因此我们可以考虑 Set 子类并添加 count() 方法。另一方面，一旦我们开始考虑如何实现 count() 方法，我们可能会意识到 Histogram 类更像是一个 Map 而不是一个 Set，因为它需要维护值与添加它们次数之间的映射。因此，我们可以创建一个类，该类定义一个类似 Set 的 API，但委托内部 Map 对象来实现这些方法，而不是创建 Set 的子类。示例 9-7 显示了我们如何做到这一点。

Example 9-7. Histogram.js: a Set-like class implemented with delegation

> 示例 9-7：Histogram.js：使用委托实现一个类似 Set 的类

```js
/**
 * A Set-like class that keeps track of how many times a value has
 * been added. Call add() and remove() like you would for a Set, and
 * call count() to find out how many times a given value has been added.
 * The default iterator yields the values that have been added at least
 * once. Use entries() if you want to iterate [value, count] pairs.
 */
class Histogram {
    // To initialize, we just create a Map object to delegate to
    constructor() { this.map = new Map(); }

    // For any given key, the count is the value in the Map, or zero
    // if the key does not appear in the Map.
    count(key) { return this.map.get(key) || 0; }

    // The Set-like method has() returns true if the count is non-zero
    has(key) { return this.count(key) > 0; }

    // The size of the histogram is just the number of entries in the Map.
    get size() { return this.map.size; }

    // To add a key, just increment its count in the Map.
    add(key) { this.map.set(key, this.count(key) + 1); }

    // Deleting a key is a little trickier because we have to delete
    // the key from the Map if the count goes back down to zero.
    delete(key) {
        let count = this.count(key);
        if (count === 1) {
            this.map.delete(key);
        } else if (count > 1) {
            this.map.set(key, count - 1);
        }
    }

    // Iterating a Histogram just returns the keys stored in it
    [Symbol.iterator]() { return this.map.keys(); }

    // These other iterator methods just delegate to the Map object
    keys() { return this.map.keys(); }
    values() { return this.map.values(); }
    entries() { return this.map.entries(); }
}
```
All the Histogram() constructor does in Example 9-7 is create a Map object. And most of the methods are one-liners that just delegate to a method of the map, making the implementation quite simple. Because we used delegation rather than inheritance, a Histogram object is not an instance of Set or Map. But Histogram implements a number of commonly used Set methods, and in an untyped language like JavaScript, that is often good enough: a formal inheritance relationship is sometimes nice, but often optional.

> 在示例 9-7 中，Histogram() 构造函数创建一个 Map 对象。大多数方法都是单行，它们只是委托给 Map 的方法，使得实现变得非常简单。因为我们使用委托而不是继承，所以 Histogram 对象不是 Set 或 Map 的实例。但是，Histogram 实现了许多常用的 Set 方法，并没有过多的使用额外的 JavaScript，这通常足够好：有条理的继承关系有时是不错，但通常是可选的。

### 9.5.4 Class Hierarchies and Abstract Classes
Example 9-6 demonstrated how we can subclass Map. Example 9-7 demonstrated how we can instead delegate to a Map object without actually subclassing anything. Using JavaScript classes to encapsulate data and modularize your code is often a great technique, and you may find yourself using the class keyword frequently. But you may find that you prefer composition to inheritance and that you rarely need to use extends (except when you’re using a library or framework that requires you to extend its base classes).

> 示例 9-6 演示了如创建 Map 的子类。示例 9-7 演示了如何在不创建子类的情况下将委托给 Map 对象。使用 JavaScript 类封装数据和模块化代码通常是一种很好的技术，你可能会发现自己经常使用类关键字。但是，你可能会发现，你更喜欢组合而不是继承，而且很少需要使用 extends（除非使用需要扩展的库或框架）。

There are some circumstances when multiple levels of subclassing are appropriate, however, and we’ll end this chapter with an extended example that demonstrates a hierarchy of classes representing different kinds of sets. (The set classes defined in Example 9-8 are similar to, but not completely compatible with, JavaScript’s built-in Set class.)

> 但是，在某些情况下，多个级别的子类是合适的，我们将举一个扩展示例来结束本章，通过描述不同种类的集合来演示类的层次结构。（示例 9-8 中定义的类跟 JavaScript 中的内置 Set 类很相似，但不完全兼容。）

Example 9-8 defines lots of subclasses, but it also demonstrates how you can define abstract classes—classes that do not include a complete implementation—to serve as a common superclass for a group of related subclasses. An abstract superclass can define a partial implementation that all subclasses inherit and share. The subclasses, then, only need to define their own unique behavior by implementing the abstract methods defined—but not implemented—by the superclass. Note that JavaScript does not have any formal definition of abstract methods or abstract classes; I’m simply using that name here for unimplemented methods and incompletely implemented classes.

> 示例 9-8 定义了大量子类，但它也演示了如何定义抽象类（不包括完整实现的类）作为一组相关子类的通用父类。抽象父类可以定义所有子类继承和共享的部分实现。因此，子类只需要通过实现父类定义的抽象方法（没有实现）来定义它们自己的独特行为。请注意，JavaScript 对抽象方法或抽象类没有任何正式定义；我只是将这个名字用于未实现的方法和不完全实现的类。

Example 9-8 is well commented and stands on its own. I encourage you to read it as a capstone example for this chapter on classes. The final class in Example 9-8 does a lot of bit manipulation with the &, |, and ~ operators, which you can review in §4.8.3.

> 示例 9-8 评论良好，并且独立。我鼓励你把它作为本章关于类的顶级示例。示例 9-8 用 &、| 和 ~ 运算符执行大量位操作，可以在 §4.8.3 中查看这些运算符。

Example 9-8. Sets.js: a hierarchy of abstract and concrete set classes

> 示例 9-8：Sets.js：抽象类和实体类的层次

```js
/**
 * The AbstractSet class defines a single abstract method, has().
 */
class AbstractSet {
    // Throw an error here so that subclasses are forced
    // to define their own working version of this method.
    has(x) { throw new Error("Abstract method"); }
}

/**
 * NotSet is a concrete subclass of AbstractSet.
 * The members of this set are all values that are not members of some
 * other set. Because it is defined in terms of another set it is not
 * writable, and because it has infinite members, it is not enumerable.
 * All we can do with it is test for membership and convert it to a
 * string using mathematical notation.
 */
class NotSet extends AbstractSet {
    constructor(set) {
        super();
        this.set = set;
    }

    // Our implementation of the abstract method we inherited
    has(x) { return !this.set.has(x); }
    // And we also override this Object method
    toString() { return `{ x| x ∉ ${this.set.toString()} }`; }
}

/**
 * Range set is a concrete subclass of AbstractSet. Its members are
 * all values that are between the from and to bounds, inclusive.
 * Since its members can be floating point numbers, it is not
 * enumerable and does not have a meaningful size.
 */
class RangeSet extends AbstractSet {
    constructor(from, to) {
        super();
        this.from = from;
        this.to = to;
    }

    has(x) { return x >= this.from && x <= this.to; }
    toString() { return `{ x| ${this.from} ≤ x ≤ ${this.to} }`; }
}

/*
 * AbstractEnumerableSet is an abstract subclass of AbstractSet.  It defines
 * an abstract getter that returns the size of the set and also defines an
 * abstract iterator. And it then implements concrete isEmpty(), toString(),
 * and equals() methods on top of those. Subclasses that implement the
 * iterator, the size getter, and the has() method get these concrete
 * methods for free.
 */
class AbstractEnumerableSet extends AbstractSet {
    get size() { throw new Error("Abstract method"); }
    [Symbol.iterator]() { throw new Error("Abstract method"); }

    isEmpty() { return this.size === 0; }
    toString() { return `{${Array.from(this).join(", ")}}`; }
    equals(set) {
        // If the other set is not also Enumerable, it isn't equal to this one
        if (!(set instanceof AbstractEnumerableSet)) return false;

        // If they don't have the same size, they're not equal
        if (this.size !== set.size) return false;

        // Loop through the elements of this set
        for(let element of this) {
            // If an element isn't in the other set, they aren't equal
            if (!set.has(element)) return false;
        }

        // The elements matched, so the sets are equal
        return true;
    }
}

/*
 * SingletonSet is a concrete subclass of AbstractEnumerableSet.
 * A singleton set is a read-only set with a single member.
 */
class SingletonSet extends AbstractEnumerableSet {
    constructor(member) {
        super();
        this.member = member;
    }

    // We implement these three methods, and inherit isEmpty, equals()
    // and toString() implementations based on these methods.
    has(x) { return x === this.member; }
    get size() { return 1; }
    *[Symbol.iterator]() { yield this.member; }
}

/*
 * AbstractWritableSet is an abstract subclass of AbstractEnumerableSet.
 * It defines the abstract methods insert() and remove() that insert and
 * remove individual elements from the set, and then implements concrete
 * add(), subtract(), and intersect() methods on top of those. Note that
 * our API diverges here from the standard JavaScript Set class.
 */
class AbstractWritableSet extends  AbstractEnumerableSet {
    insert(x) { throw new Error("Abstract method"); }
    remove(x) { throw new Error("Abstract method"); }

    add(set) {
        for(let element of set) {
            this.insert(element);
        }
    }

    subtract(set) {
        for(let element of set) {
            this.remove(element);
        }
    }

    intersect(set) {
        for(let element of this) {
            if (!set.has(element)) {
                this.remove(element);
            }
        }
    }
}

/**
 * A BitSet is a concrete subclass of AbstractWritableSet with a
 * very efficient fixed-size set implementation for sets whose
 * elements are non-negative integers less than some maximum size.
 */
class BitSet extends AbstractWritableSet {
    constructor(max) {
        super();
        this.max = max;  // The maximum integer we can store.
        this.n = 0;      // How many integers are in the set
        this.numBytes = Math.floor(max / 8) + 1;   // How many bytes we need
        this.data = new Uint8Array(this.numBytes); // The bytes
    }

    // Internal method to check if a value is a legal member of this set
    _valid(x) { return Number.isInteger(x) && x >= 0 && x <= this.max; }

    // Tests whether the specified bit of the specified byte of our
    // data array is set or not. Returns true or false.
    _has(byte, bit) { return (this.data[byte] & BitSet.bits[bit]) !== 0; }

    // Is the value x in this BitSet?
    has(x) {
        if (this._valid(x)) {
            let byte = Math.floor(x / 8);
            let bit = x % 8;
            return this._has(byte, bit);
        } else {
            return false;
        }
    }

    // Insert the value x into the BitSet
    insert(x) {
        if (this._valid(x)) {               // If the value is valid
            let byte = Math.floor(x / 8);   // convert to byte and bit
            let bit = x % 8;
            if (!this._has(byte, bit)) {    // If that bit is not set yet
                this.data[byte] |= BitSet.bits[bit]; // then set it
                this.n++;                            // and increment set size
            }
        } else {
            throw new TypeError("Invalid set element: " + x );
        }
    }

    remove(x) {
        if (this._valid(x)) {              // If the value is valid
            let byte = Math.floor(x / 8);  // compute the byte and bit
            let bit = x % 8;
            if (this._has(byte, bit)) {    // If that bit is already set
                this.data[byte] &= BitSet.masks[bit];  // then unset it
                this.n--;                              // and decrement size
            }
        } else {
            throw new TypeError("Invalid set element: " + x );
        }
    }

    // A getter to return the size of the set
    get size() { return this.n; }

    // Iterate the set by just checking each bit in turn.
    // (We could be a lot more clever and optimize this substantially)
    *[Symbol.iterator]() {
        for(let i = 0; i <= this.max; i++) {
            if (this.has(i)) {
                yield i;
            }
        }
    }
}

// Some pre-computed values used by the has(), insert() and remove() methods
BitSet.bits = new Uint8Array([1, 2, 4, 8, 16, 32, 64, 128]);
BitSet.masks = new Uint8Array([~1, ~2, ~4, ~8, ~16, ~32, ~64, ~128]);
```
## 9.6 Summary
This chapter has explained the key features of JavaScript classes:

> 本章说明了 JavaScript 类的主要功能：

Objects that are members of the same class inherit properties from the same prototype object. The prototype object is the key feature of JavaScript classes, and it is possible to define classes with nothing more than the Object.create() method.

> 同一类的成员对象从同一原型对象继承属性。原型对象是 JavaScript 类的关键特性，只有 Object.create() 方法可以定义类。

Prior to ES6, classes were more typically defined by first defining a constructor function. Functions created with the function keyword have a prototype property, and the value of this property is an object that is used as the prototype of all objects created when the function is invoked with new as a constructor. By initializing this prototype object, you can define the shared methods of your class. Although the prototype object is the key feature of the class, the constructor function is the public identity of the class.

> 在 ES6 之前，典型的类定义先定义构造函数。使用 function 关键字创建的函数具有原型属性，this 属性的值是使用 new 将函数用作构造函数调用时创建的对象的原型对象。通过初始化此原型对象，可以定义类的共享方法。虽然原型对象是类的关键特性，但构造函数是类的公共标识。

ES6 introduces a class keyword that makes it easier to define classes, but under the hood, constructor and prototype mechanism remains the same.

> ES6 引入了一个 class 关键字，它使定义类更加容易，但它只是个语法糖，构造函数和原型机制保持不变。

Subclasses are defined using the extends keyword in a class declaration.

> 子类使用类声明中的 extends 关键字定义。

Subclasses can invoke the constructor of their superclass or overridden methods of their superclass with the super keyword.

> 子类可以使用 super 关键字调用其父类的构造函数或父类的重写方法。

---

1. Except functions returned by the ES5 Function.bind() method. Bound functions have no prototype property of their own, but they use the prototype of the underlying function if they are invoked as constructors.

2. See Design Patterns (Addison-Wesley Professional) by Erich Gamma et al. or Effective Java (Addison-Wesley Professional) by Joshua Bloch, for example.

> 1. 除了 ES5 Function.bind() 方法返回的函数。绑定函数没有自己的原型属性，但如果它们作为构造函数调用，则它们使用基础函数的原型。

> 2. 例如，见《Design Patterns (Addison-Wesley Professional)》作者 Erich Gamma 等，或者《Effective Java (Addison-Wesley Professional)》作者 Joshua Bloch。