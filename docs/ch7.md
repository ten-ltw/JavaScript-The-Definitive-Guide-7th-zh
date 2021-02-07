# 第 7 章 数组

This chapter documents arrays, a fundamental datatype in JavaScript and in most other programming languages. An array is an ordered collection of values. Each value is called an element, and each element has a numeric position in the array, known as its index. JavaScript arrays are untyped: an array element may be of any type, and different elements of the same array may be of different types. Array elements may even be objects or other arrays, which allows you to create complex data structures, such as arrays of objects and arrays of arrays. JavaScript arrays are zero-based and use 32-bit indexes: the index of the first element is 0, and the highest possible index is 4294967294 (2<sup>32</sup>−2), for a maximum array size of 4,294,967,295 elements. JavaScript arrays are dynamic: they grow or shrink as needed, and there is no need to declare a fixed size for the array when you create it or to reallocate it when the size changes. JavaScript arrays may be sparse: the elements need not have contiguous indexes, and there may be gaps. Every JavaScript array has a length property. For nonsparse arrays, this property specifies the number of elements in the array. For sparse arrays, length is larger than the highest index of any element.
 
> 本章记录了数组、一个在 JavaScript 和大多数其他编程语言中的基本数据类型。数组是值的有序集合。每个值叫做一个元素，而每个元素在数组中有一个位置，以数字表示，称为索引。JavaScript 数组是无类型的：数组元素可以是任意类型，并且同一个数组中的不同元素也可能有不同的类型。数组的元素甚至也可能是对象或其他数组，这允许创建复杂的数据结构，如对象的数组和数组的数组。JavaScript 数组的索引是基于零的 32 位数值：第一个元素的索引为 0，最大可能的索引为 4,294,967,294（2<sup>32</sup>-2），数组最大能容纳 4,294,967,295 个元素。JavaScript 数组是动态的：根据需要它们会增长或缩减，并且在创建数组时无须声明一个固定的大小或者在数组大小变化时无须重新分配空间。JavaScript 数组可能是稀疏的：数组元素的索引不一定要连续的，它们之间可以有空缺。每个 JavaScript 数组都有一个 length 属性。针对非稀疏数组，该属性就是数组元素的个数。针对稀疏数组，length 大于任何元素的最高索引。

JavaScript arrays are a specialized form of JavaScript object, and array indexes are really little more than property names that happen to be integers. We’ll talk more about the specializations of arrays elsewhere in this chapter. Implementations typically optimize arrays so that access to numerically indexed array elements is generally significantly faster than access to regular object properties.

> JavaScript 数组是 JavaScript 对象的特殊形式，数组索引实际上和碰巧是整数的属性名差不多。我们将在本章的其他地方更多地讨论特殊化的数组。通常，数组的实现是经过优化的，用数字索引来访问数组元素一般来说比访问常规的对象属性要快很多。

Arrays inherit properties from Array.prototype, which defines a rich set of array manipulation methods, covered in §7.8. Most of these methods are generic, which means that they work correctly not only for true arrays, but for any “array-like object.” We’ll discuss array-like objects in §7.9. Finally, JavaScript strings behave like arrays of characters, and we’ll discuss this in §7.10.

> 数组继承自 Array.prototype 中的属性，它定义了一套丰富的数组操作方法，§7.8 涵盖这方面内容。大多数这些方法是通用的，这意味着它们不仅对真正的数组有效，而且对“类数组对象”同样有效。§7.9 讨论类数组对象。最后，JavaScript 字符串的行为与字符数组类似，我们将在 §7.10 讨论。

ES6 introduces a set of new array classes known collectively as “typed arrays.” Unlike regular JavaScript arrays, typed arrays have a fixed length and a fixed numeric element type. They offer high performance and byte-level access to binary data and are covered in §11.2.

> ES6 引入了一组新的数组类，这些类统称为“类型化数组”。与常规的 JavaScript 数组不同，类型化数组有固定的长度和固定的数值元素类型。它们提供高性能和对二进制数据的字节级访问，在 §11.2 中有介绍。

## 7.1 Creating Arrays

There are several ways to create arrays. The subsections that follow explain how to create arrays with:

> 有很多种创建数组的方法。以下小节将说明如何使用以下方式创建数组：

Array literals

> 数组字面量

The ... spread operator on an iterable object

> 可迭代数组 ... 展开运算符

The Array() constructor

> Array() 构造函数

The Array.of() and Array.from() factory methods

> Array.of() 和 Array.from() 工厂方法

### 7.1.1 Array Literals
By far the simplest way to create an array is with an array literal, which is simply a comma-separated list of array elements within square brackets. For example:

> 到目前为止使用数组字面量是创建数组最简单的方法，在方括号中将数组元素用逗号隔开即可。例如：

```js
let empty = [];                 // An array with no elements
let primes = [2, 3, 5, 7, 11];  // An array with 5 numeric elements
let misc = [ 1.1, true, "a", ]; // 3 elements of various types + trailing comma
```
The values in an array literal need not be constants; they may be arbitrary expressions:

> 数组字面量中的值不一定要是常量；它们可以是任意的表达式：

```js
let base = 1024;
let table = [base, base+1, base+2, base+3];
```
Array literals can contain object literals or other array literals:

> 数组字面量可以包含对象字面量或其他数组字面量：

```js
let b = [[1, {x: 1, y: 2}], [2, {x: 3, y: 4}]];
```
If an array literal contains multiple commas in a row, with no value between, the array is sparse (see §7.3). Array elements for which values are omitted do not exist but appear to be undefined if you query them:

> 如果数组字面量在一行中包含多个逗号，之间没有值，则数组是稀疏的（请参阅 §7.3）。省略值的数组元素不存在，但如果查询它们则返回 undefined：

```js
let count = [1,,3]; // Elements at indexes 0 and 2. No element at index 1
let undefs = [,,];  // An array with no elements but a length of 2
```
Array literal syntax allows an optional trailing comma, so [,,] has a length of 2, not 3.

> 数组字面量语法允许可选的尾部逗号，所以 [,,] 的长度是 2，不是3。

### 7.1.2 The Spread Operator
In ES6 and later, you can use the “spread operator,” ..., to include the elements of one array within an array literal:

> ES6 之后，可以使用展开操作符 ... 将一个数组中的元素展开在数组字面量中：

```js
let a = [1, 2, 3];
let b = [0, ...a, 4];  // b == [0, 1, 2, 3, 4]
```
The three dots “spread” the array a so that its elements become elements within the array literal that is being created. It is as if the ...a was replaced by the elements of the array a, listed literally as part of the enclosing array literal. (Note that, although we call these three dots a spread operator, this is not a true operator because it can only be used in array literals and, as we’ll see later in the book, function invocations.)

> 三个点展开数组 a，所以它的元素变成了数组字面量，并被创建在数组中。就像 ...a 被数组 a 的元素所替换，被列出作为未闭合的数组字面量的一部分。（注意，尽管我们称三点是展开运算符，但这并不是一个操作，因为它只能用于数组字面量和本书后面提到的函数调用。）

The spread operator is a convenient way to create a (shallow) copy of an array:

> 展开运算符可以方便的创建一个数组的拷贝（浅拷贝）：

```js
let original = [1,2,3];
let copy = [...original];
copy[0] = 0;  // Modifying the copy does not change the original
original[0]   // => 1
```
The spread operator works on any iterable object. (Iterable objects are what the for/of loop iterates over; we first saw them in §5.4.4, and we’ll see much more about them in Chapter 12.) Strings are iterable, so you can use a spread operator to turn any string into an array of single-character strings:

> 展开运算符可以作用于任何可迭代对象。（可迭代对象是可以用 for/of 进行循环的对象；第一次在 §5.4.4 中提到，在第 12 章会看到更多关于它们的描述。）字符串是可迭代对象，所以可以使用展开操作符将字符串转换成单个字符的数组。

```js
let digits = [..."0123456789ABCDEF"];
digits // => ["0","1","2","3","4","5","6","7","8","9","A","B","C","D","E","F"]
```
Set objects (§11.1.1) are iterable, so an easy way to remove duplicate elements from an array is to convert the array to a set and then immediately convert the set back to an array using the spread operator:

> Set 对象（§11.1.1）是可迭代对象，所以数组去重有一种简单的方法是用展开运算符将数组转换成 set 然后再转成数组：

```js
let letters = [..."hello world"];
[...new Set(letters)]  // => ["h","e","l","o"," ","w","r","d"]
```
### 7.1.3 The Array() Constructor
Another way to create an array is with the Array() constructor. You can invoke this constructor in three distinct ways:

> 另一种创建数组的方法是使用 Array() 构造函数。可以用三种不同的方式调用这个构造函数：

Call it with no arguments:

> 调用时没有实参：

```js
let a = new Array();
```
This method creates an empty array with no elements and is equivalent to the array literal [].

> 这个方法创建了一个没有元素的空数组，它等价于 [] 数组字面量。

Call it with a single numeric argument, which specifies a length:

> 调用时有一个数值实参，它指定了数组的长度：

```js
let a = new Array(10);
```
This technique creates an array with the specified length. This form of the Array() constructor can be used to preallocate an array when you know in advance how many elements will be required. Note that no values are stored in the array, and the array index properties “0”, “1”, and so on are not even defined for the array.

> 该技术创建指定长度的数组。当预先知道所需元素个数时，这种形式的 Array() 构造函数可以用来预分配一个数组空间。注意，数组中没有存储值，甚至数组的索引属性“0”、“1”等还未定义。

Explicitly specify two or more array elements or a single non-numeric element for the array:

> 为数组显式指定两个或多个数组元素或者非数值元素：

```js
let a = new Array(5, 4, 3, 2, 1, "testing, testing");
```
In this form, the constructor arguments become the elements of the new array. Using an array literal is almost always simpler than this usage of the Array() constructor.

> 以这种形式，构造函数的实参将会成为新数组的元素。使用数组字面量比这样使用 Array() 构造函数要简单多了。

### 7.1.4 Array.of()
When the Array() constructor function is invoked with one numeric argument, it uses that argument as an array length. But when invoked with more than one numeric argument, it treats those arguments as elements for the array to be created. This means that the Array() constructor cannot be used to create an array with a single numeric element.

> 当 Array() 构造函数调用时有一个数值型实参，它会将实参作为数组的长度。但当调用时不止一个数值型实参时，它会将那些实参作为数组的元素创建。这意味着 Array() 构造函数不能创建只有一个数值型元素的数组。

In ES6, the Array.of() function addresses this problem: it is a factory method that creates and returns a new array, using its argument values (regardless of how many of them there are) as the array elements:

> 在 ES6 中，Array.of() 函数修复了这个问题：它是一个将其实参值（无论有多少个实参）作为数组元素创建并返回一个新数组的工厂方法：

```js
Array.of()        // => []; returns empty array with no arguments
Array.of(10)      // => [10]; can create arrays with a single numeric argument
Array.of(1,2,3)   // => [1, 2, 3]
```
### 7.1.5 Array.from()
Array.from is another array factory method introduced in ES6. It expects an iterable or array-like object as its first argument and returns a new array that contains the elements of that object. With an iterable argument, Array.from(iterable) works like the spread operator [...iterable] does. It is also a simple way to make a copy of an array:

> Array.from 是 ES6 中另外一个数组工厂方法。它期望一个可迭代或类数组对象作为它的第一个实参，并返回一个包含对象中元素的新数组。使用一个可迭代实参，Array.from(iterable) 工作方式类似于展开运算符 [...iterable]。它也可以简单的拷贝一个数组：

```js
let copy = Array.from(original);
```
Array.from() is also important because it defines a way to make a true-array copy of an array-like object. Array-like objects are non-array objects that have a numeric length property and have values stored with properties whose names happen to be integers. When working with client-side JavaScript, the return values of some web browser methods are array-like, and it can be easier to work with them if you first convert them to true arrays:

> Array.from() 也很重要，因为它定义了一个将类数组对象拷贝成数组的方法。类数组对象是一个不是数组的对象，它有一个数值型的 length 属性，并且它的值碰巧保存在属性名为整数的属性中。当使用客户端 JavaScript 时，一些浏览器方法的返回值是类数组的，并且当将其转化成真正的数组后会更容易操作它们：

```js
let truearray = Array.from(arraylike);
```
Array.from() also accepts an optional second argument. If you pass a function as the second argument, then as the new array is being built, each element from the source object will be passed to the function you specify, and the return value of the function will be stored in the array instead of the original value. (This is very much like the array map() method that will be introduced later in the chapter, but it is more efficient to perform the mapping while the array is being built than it is to build the array and then map it to another new array.)

> Array.from() 第二个实参为可选实参。如果传递一个函数作为第二个实参，那么当新数组被创建，每一个元素都会被作为实参传入这个指定函数中，并且这个函数的每个返回值保存在数组中代替原来的值。（这很像后面会介绍的数组 map() 方法，但是，它会更加高效的执行映射，因其为没有创建数组，而是直接进行映射到另外一个数组。）

## 7.2 Reading and Writing Array Elements
You access an element of an array using the [] operator. A reference to the array should appear to the left of the brackets. An arbitrary expression that has a non-negative integer value should be inside the brackets. You can use this syntax to both read and write the value of an element of an array. Thus, the following are all legal JavaScript statements:

> 使用 [] 运算符来访问数组中的一个元素。数组的引用位于方括号的左边。方括号中是一个返回非负整数值的任意表达式。使用该语法既可以读又可以写数组的一个元素。因此，如下代码都是合法的 JavaScript 语句：

```js
let a = ["world"];     // Start with a one-element array
let value = a[0];      // Read element 0
a[1] = 3.14;           // Write element 1
let i = 2;
a[i] = 3;              // Write element 2
a[i + 1] = "hello";    // Write element 3
a[a[i]] = a[0];        // Read elements 0 and 2, write element 3
```
What is special about arrays is that when you use property names that are non-negative integers less than 2<sup>32</sup>–1, the array automatically maintains the value of the length property for you. In the preceding, for example, we created an array a with a single element. We then assigned values at indexes 1, 2, and 3. The length property of the array changed as we did, so:

> 数组特殊的是，当使用小于 2<sup>32</sup>–1 的非负整数属性名时，数组会自动维护 length 属性。例如，上文中我们创建了只有一个元素的数组 a。然后我们为其序列为 1、2 和 3 的元素进行赋值。数组 length 属性会自动改变：

```js
a.length       // => 4
```

Remember that arrays are a specialized kind of object. The square brackets used to access array elements work just like the square brackets used to access object properties. JavaScript converts the numeric array index you specify to a string—the index 1 becomes the string "1"—then uses that string as a property name. There is nothing special about the conversion of the index from a number to a string: you can do that with regular objects, too:

> 请记住，数组是对象的特殊形式。使用方括号访问数组元素就像用方括号访问对象的属性一样。JavaScript 将指定的数字索引值转换成字符串（索引值 1 变成“1”）然后将其作为属性名来使用。关于索引值从数字转换为字符串没什么特别之处：对常规对象也可以这么做：

```js
let o = {};    // Create a plain object
o[1] = "one";  // Index it with an integer
o["1"]         // => "one"; numeric and string property names are the same
```
It is helpful to clearly distinguish an array index from an object property name. All indexes are property names, but only property names that are integers between 0 and 2<sup>32</sup>–2 are indexes. All arrays are objects, and you can create properties of any name on them. If you use properties that are array indexes, however, arrays have the special behavior of updating their length property as needed.

> 清晰地区分数组的索引和对象的属性名是非常有用的。所有的索引都是属性名，但只有在 0～2<sup>32</sup>-2 之间的整数属性名才是索引。所有的数组都是对象，可以为其创建任意名字的属性。但如果使用的属性是数组的索引，数组的特殊行为就是将根据需要更新它们的 length 属性值。

Note that you can index an array using numbers that are negative or that are not integers. When you do this, the number is converted to a string, and that string is used as the property name. Since the name is not a non-negative integer, it is treated as a regular object property, not an array index. Also, if you index an array with a string that happens to be a non-negative integer, it behaves as an array index, not an object property. The same is true if you use a floating-point number that is the same as an integer:

> 注意，可以使用负数或非整数来索引数组。这种情况下，数值转换为字符串，字符串作为属性名来用。既然名字不是非负整数，它就只能当做常规的对象属性，而非数组的索引。同样，如果凑巧使用了是非负整数的字符串，它就当做数组索引，而非对象属性。当使用的一个浮点数和一个整数相等时情况也是一样的：

```js
a[-1.23] = true;  // This creates a property named "-1.23"
a["1000"] = 0;    // This the 1001st element of the array
a[1.000] = 1;     // Array index 1. Same as a[1] = 1;
```
The fact that array indexes are simply a special type of object property name means that JavaScript arrays have no notion of an “out of bounds” error. When you try to query a nonexistent property of any object, you don’t get an error; you simply get undefined. This is just as true for arrays as it is for objects:

> 事实上数组索引仅仅是对象属性名的一种特殊类型，这意味着 JavaScript 数组没有“越界”错误的概念。当试图查询任何对象中不存在的属性时，都不会报错，只会得到 undefined 值。类似于对象，对于对象同样存在这种情况。

```js
let a = [true, false]; // This array has elements at indexes 0 and 1
a[2]                   // => undefined; no element at this index.
a[-1]                  // => undefined; no property with this name.
```
## 7.3 Sparse Arrays
A sparse array is one in which the elements do not have contiguous indexes starting at 0. Normally, the length property of an array specifies the number of elements in the array. If the array is sparse, the value of the length property is greater than the number of elements. Sparse arrays can be created with the Array() constructor or simply by assigning to an array index larger than the current array length.

> 稀疏数组就是包含从 0 开始的不连续索引的数组。通常，数组的 length 属性值代表数组中元素的个数。如果数组是稀疏的，length 属性值大于元素的个数。可以用 Array() 构造函数或简单地指定数组的索引值大于当前的数组长度来创建稀疏数组。

```js
let a = new Array(5); // No elements, but a.length is 5.
a = [];               // Create an array with no elements and length = 0.
a[1000] = 0;          // Assignment adds one element but sets length to 1001.
```
We’ll see later that you can also make an array sparse with the delete operator.

> 后面会看到你也可以用 delete 运算符来生产稀疏数组。

Arrays that are sufficiently sparse are typically implemented in a slower, more memory-efficient way than dense arrays are, and looking up elements in such an array will take about as much time as regular object property lookup.

> 足够稀疏的数组通常在实现上比稠密的数组更慢、内存利用率更高，在这样的数组中查找元素的时间与常规对象属性的查找时间一样长。

Note that when you omit a value in an array literal (using repeated commas as in [1,,3]), the resulting array is sparse, and the omitted elements simply do not exist:

> 注意，当在数组字面量中省略值时（像 [1,,3] 中使用重复的逗号）返回的是稀疏数组，省略掉的值是不存在的：

```js
let a1 = [,];           // This array has no elements and length 1
let a2 = [undefined];   // This array has one undefined element
0 in a1                 // => false: a1 has no element with index 0
0 in a2                 // => true: a2 has the undefined value at index 0
```
Understanding sparse arrays is an important part of understanding the true nature of JavaScript arrays. In practice, however, most JavaScript arrays you will work with will not be sparse. And, if you do have to work with a sparse array, your code will probably treat it just as it would treat a nonsparse array with undefined elements.

> 了解稀疏数组是了解 JavaScript 数组的真实本质的一部分。尽管如此，实际上你所碰到的绝大多数 JavaScript 数组不是稀疏数组。并且，如果你确实碰到了稀疏数组，你的代码很可能像对待非稀疏数组一样来对待它们，只不过它们包含一些 undefined 元素。

## 7.4 Array Length
Every array has a length property, and it is this property that makes arrays different from regular JavaScript objects. For arrays that are dense (i.e., not sparse), the length property specifies the number of elements in the array. Its value is one more than the highest index in the array:

> 每个数组有一个 length 属性，就是这个属性使其区别于常规的 JavaScript 对象。针对稠密（也就是非稀疏）数组，length 属性值代表数组中元素的个数。其值比数组中最大的索引大 1：

```js
[].length             // => 0: the array has no elements
["a","b","c"].length  // => 3: highest index is 2, length is 3
```
When an array is sparse, the length property is greater than the number of elements, and all we can say about it is that length is guaranteed to be larger than the index of every element in the array. Or, put another way, an array (sparse or not) will never have an element whose index is greater than or equal to its length. In order to maintain this invariant, arrays have two special behaviors. The first we described above: if you assign a value to an array element whose index i is greater than or equal to the array’s current length, the value of the length property is set to i+1.

> 当数组是稀疏的时，length 属性值大于元素的个数。而且关于此我们可以说数组长度保证大于它每个元素的索引值。或者，换一种说法，在数组中（无论稀疏与否）肯定找不到一个元素的索引值大于或等于它的长度。为了维持此规则不变化，数组有两个特殊的行为。第一个如同上面的描述：如果为一个数组元素赋值，它的索引 i 大于或等于现有数组的长度时，length 属性的值将设置为 i+1。

The second special behavior that arrays implement in order to maintain the length invariant is that, if you set the length property to a non-negative integer n smaller than its current value, any array elements whose index is greater than or equal to n are deleted from the array:

> 第二个特殊的行为就是设置 length 属性为一个小于当前长度的非负整数n时，当前数组中那些索引值大于或等于 n 的元素将从中删除：

```js
a = [1,2,3,4,5];     // Start with a 5-element array.
a.length = 3;        // a is now [1,2,3].
a.length = 0;        // Delete all elements.  a is [].
a.length = 5;        // Length is 5, but no elements, like new Array(5)
```
You can also set the length property of an array to a value larger than its current value. Doing this does not actually add any new elements to the array; it simply creates a sparse area at the end of the array.

> 还可以将数组的 length 属性值设置为大于其当前的长度。实际上这不会向数组中添加新的元素，它只是在数组尾部创建一个稀疏区域。

## 7.5 Adding and Deleting Array Elements
We’ve already seen the simplest way to add elements to an array: just assign values to new indexes:

> 我们已经见过添加数组元素最简单的方法：为新索引赋值：

```js
let a = [];      // Start with an empty array.
a[0] = "zero";   // And add elements to it.
a[1] = "one";
```
You can also use the push() method to add one or more values to the end of an array:

> 也可以使用push()方法在数组末尾增加一个或多个元素：

```js
let a = [];           // Start with an empty array
a.push("zero");       // Add a value at the end.  a = ["zero"]
a.push("one", "two"); // Add two more values.  a = ["zero", "one", "two"]
```
Pushing a value onto an array a is the same as assigning the value to a[a.length]. You can use the unshift() method (described in §7.8) to insert a value at the beginning of an array, shifting the existing array elements to higher indexes. The pop() method is the opposite of push(): it removes the last element of the array and returns it, reducing the length of an array by 1. Similarly, the shift() method removes and returns the first element of the array, reducing the length by 1 and shifting all elements down to an index one lower than their current index. See §7.8 for more on these methods.

> 在数组尾部压入一个元素与给 a[a.length] 赋值是一样的。可以使用 unshift() 方法（§7.8 有描述）在数组的首部插入一个元素，并且将其他元素依次移到更高的索引处。pop() 方法与 push() 相反：它移除数组最后一个元素并返回这个元素，使数组 length 减 1。同样，shift() 方法移除并返回数组的第一个元素，使数组 length 减 1，并将其他元素依次移到低 1 的索引处。§7.8 有更多关于这些方法的描述。

You can delete array elements with the delete operator, just as you can delete object properties:

> 可以像删除对象属性一样使用 delete 运算符来删除数组元素：

```js
let a = [1,2,3];
delete a[2];   // a now has no element at index 2
2 in a         // => false: no array index 2 is defined
a.length       // => 3: delete does not affect array length
```
Deleting an array element is similar to (but subtly different than) assigning undefined to that element. Note that using delete on an array element does not alter the length property and does not shift elements with higher indexes down to fill in the gap that is left by the deleted property. If you delete an element from an array, the array becomes sparse.

> 删除数组元素与为其赋 undefined 值是类似的（但有一些微妙的区别）。注意，对一个数组元素使用 delete 不会修改数组的 length 属性，也不会将元素从高索引处移下来填充已删除属性留下的空白。如果从数组中删除一个元素，它就变成稀疏数组。

As we saw above, you can also remove elements from the end of an array simply by setting the length property to the new desired length.

> 正如上面所看到的，也可以通过设置新的所需长度，即可从数组尾部删除元素。

Finally, splice() is the general-purpose method for inserting, deleting, or replaci ng array elements. It alters the length property and shifts array elements to higher or lower indexes as needed. See §7.8 for details.

> 最后，splice() 是一个通用的方法来插入、删除或替换数组元素。它会根据需要修改 length 属性并移动元素到更高或较低的索引处。详细内容见 §7.8。

## 7.6 Iterating Arrays
As of ES6, the easiest way to loop through each of the elements of an array (or any iterable object) is with the for/of loop, which was covered in detail in §5.4.4:

> 在 ES6 中，最容易遍历数组元素（或可迭代对象）的方法是 for/of 循环，在 §5.4.4 中详细介绍：

```js
let letters = [..."Hello world"];  // An array of letters
let string = "";
for(let letter of letters) {
    string += letter;
}
string  // => "Hello world"; we reassembled the original text
```
The built-in array iterator that the for/of loop uses returns the elements of an array in ascending order. It has no special behavior for sparse arrays and simply returns undefined for any array elements that do not exist.

> 内置数组迭代器 for/of 循环按照升序返回数组元素。对于稀疏数组它没有特殊的行为，数组中不存在的元素只是单纯的返回 undefined。

If you want to use a for/of loop for an array and need to know the index of each array element, use the entries() method of the array, along with destructuring assignment, like this:

> 如果使用 for/of 循环一个数组时还需要知道每个元素的索引，可以像这样将数组的 entries() 方法和解构语句一同使用：

```js
let everyother = "";
for(let [index, letter] of letters.entries()) {
    if (index % 2 === 0) everyother += letter;  // letters at even indexes
}
everyother  // => "Hlowrd"
```
Another good way to iterate arrays is with forEach(). This is not a new form of the for loop, but an array method that offers a functional approach to array iteration. You pass a function to the forEach() method of an array, and forEach() invokes your function once on each element of the array:

> 另一种不错的遍历数组方法是用 forEach()。这不是 for 循环的新形式，而是提供数组遍历功能方法的数组方法。可以给数组的 forEach() 方法传递一个函数，forEach() 会对数组中每一个元素调用这个方法：

```js
let uppercase = "";
letters.forEach(letter => {  // Note arrow function syntax here
    uppercase += letter.toUpperCase();
});
uppercase  // => "HELLO WORLD"
```
As you would expect, forEach() iterates the array in order, and it actually passes the array index to your function as a second argument, which is occasionally useful. Unlike the for/of loop, the forEach() is aware of sparse arrays and does not invoke your function for elements that are not there.

> 正如期望的，forEach() 按顺序对数组进行计算，实际上它将数组索引作为第二个实参传递到函数，这有时很有用。与 for/of 循环不同，forEach() 能意识到稀疏数组，并且不会为不存在的元素调用函数。

§7.8.1 documents the forEach() method in more detail. That section also covers related methods such as map() and filter() that perform specialized kinds of array iteration.

> §7.8.1 更详细地记录了 forEach() 方法。该部分还介绍演示了特定类型的数组遍历方法，如 map() 和 filter()。

You can also loop through the elements of an array with a good old-fashioned for loop (§5.4.3):

> 也可以用一种非常老旧方式遍历数组的元素（§5.4.3）：

```js
let vowels = "";
for(let i = 0; i < letters.length; i++) { // For each index in the array
    let letter = letters[i];              // Get the element at that index
    if (/[aeiou]/.test(letter)) {         // Use a regular expression test
        vowels += letter;                 // If it is a vowel, remember it
    }
}
vowels  // => "eoo"
```
In nested loops, or other contexts where performance is critical, you may sometimes see this basic array iteration loop written so that the array length is only looked up once rather than on each iteration. Both of the following for loop forms are idiomatic, though not particularly common, and with modern JavaScript interpreters, it is not at all clear that they have any performance impact:

> 在嵌套循环或其他性能至关重要的上下文中，有时可能会看到这样的数组遍历，以便数组长度仅被查一次，而不是在每次循环都去查询。以下两种形式都是符合习惯的 for 循环，虽然不是特别常用，而且对于现代 JavaScript 解释器，它们是否对性能有任何影响尚不清楚：

```js
// Save the array length into a local variable
for(let i = 0, len = letters.length; i < len; i++) {
    // loop body remains the same
}

// Iterate backwards from the end of the array to the start
for(let i = letters.length-1; i >= 0; i--) {
    // loop body remains the same
}
```
These examples assume that the array is dense and that all elements contain valid data. If this is not the case, you should test the array elements before using them. If you want to skip undefined and nonexistent elements, you might write:

> 这些示例假定数组是稠密的，并且所有元素都包含有效的数据。如果不是这样，应该在使用数组元素之前测试它们。如果要跳过 undefined 和不存在的元素，可以编写：

```js
for(let i = 0; i < a.length; i++) {
    if (a[i] === undefined) continue; // Skip undefined + nonexistent elements
    // loop body here
}
```
## 7.7 Multidimensional Arrays
JavaScript does not support true multidimensional arrays, but you can approximate them with arrays of arrays. To access a value in an array of arrays, simply use the [] operator twice. For example, suppose the variable matrix is an array of arrays of numbers. Every element in matrix[x] is an array of numbers. To access a particular number within this array, you would write matrix[x][y]. Here is a concrete example that uses a two-dimensional array as a multiplication table:

> JavaScript 不支持真正的多维数组，但可以用数组的数组来近似。访问数组的数组中的元素，只要简单地使用两次 [] 操作符即可。例如，假设变量 matrix 是一个数组的数组，它的基本元素是数值，那么 matrix[x] 的每个元素是包含一个数值数组，访问数组中特定数值的代码为 matrix[x][y]。这里有一个具体的例子，它使用二维数组作为一个九九乘法表：

```js
// Create a multidimensional array
let table = new Array(10);               // 10 rows of the table
for(let i = 0; i < table.length; i++) {
    table[i] = new Array(10);            // Each row has 10 columns
}

// Initialize the array
for(let row = 0; row < table.length; row++) {
    for(let col = 0; col < table[row].length; col++) {
        table[row][col] = row*col;
    }
}

// Use the multidimensional array to compute 5*7
table[5][7]  // => 35
```
## 7.8 Array Methods
The preceding sections have focused on basic JavaScript syntax for working with arrays. In general, though, it is the methods defined by the Array class that are the most powerful. The next sections document these methods. While reading about these methods, keep in mind that some of them modify the array they are called on and some of them leave the array unchanged. A number of the methods return an array: sometimes, this is a new array, and the original is unchanged. Other times, a method will modify the array in place and will also return a reference to the modified array.

> 前面几节重点介绍了用于处理数组的基本 JavaScript 语法。但通常，由 Array 类定义的方法是最强大的。下一节将记录这些方法。在阅读有关这些方法时，请记住，其中一些方法修改了调用的数组，而其中一些方法使数组保持不变。许多方法返回数组：有时，这是一个新数组，原始数组保持不变。其他时候，方法将修改数组，并且返回对修改后数组的引用。

Each of the subsections that follows covers a group of related array methods:

> 以下每个小节都涵盖一组相关的数组方法：

Iterator methods loop over the elements of an array, typically invoking a function that you specify on each of those elements.

> 迭代器方法循环遍历数组的元素，通常调用在每个元素上指定的函数。

Stack and queue methods add and remove array elements to and from the beginning and the end of an array.

> 堆栈和队列方法在数组的开头和结尾添加和删除数组元素。

Subarray methods are for extracting, deleting, inserting, filling, and copying contiguous regions of a larger array.

> 子数组方法用于提取、删除、插入、填充和复制一个更大数组中相邻的区域。

Searching and sorting methods are for locating elements within an array and for sorting the elements of an array.

> 搜索和排序方法用于查找数组中的元素和排序数组的元素。

The following subsections also cover the static methods of the Array class and a few miscellaneous methods for concatenating arrays and converting arrays to strings.

> 以下小节还介绍 Array 类的静态方法和一些用于连接数组和将数组转换为字符串的各种方法。

### 7.8.1 Array Iterator Methods
The methods described in this section iterate over arrays by passing array elements, in order, to a function you supply, and they provide convenient ways to iterate, map, filter, test, and reduce arrays.

> 本节中介绍的方法通过将数组元素按顺序传递到所指定的函数来遍历数组，它们提供了迭代、映射、筛选、测试和减少数组的便捷方法。

Before we explain the methods in detail, however, it is worth making some generalizations about them. First, all of these methods accept a function as their first argument and invoke that function once for each element (or some elements) of the array. If the array is sparse, the function you pass is not invoked for nonexistent elements. In most cases, the function you supply is invoked with three arguments: the value of the array element, the index of the array element, and the array itself. Often, you only need the first of these argument values and can ignore the second and third values.

> 然而，在详细解释这些方法之前，值得对它们进行一些概括。首先，所有这些方法都接受函数作为其第一个实参，并使用调用数组的每个元素（或某些元素）作为实参调用该函数。如果数组是稀疏的，则不会为不存在的元素调用传递的函数。在大多数情况下，提供的函数被调用时有三个实参：数组元素的值、数组元素的索引和数组本身。通常，只需要这些实参值中的第一个，并且可以忽略第二个和第三个值。

Most of the iterator methods described in the following subsections accept an optional second argument. If specified, the function is invoked as if it is a method of this second argument. That is, the second argument you pass becomes the value of the this keyword inside of the function you pass as the first argument. The return value of the function you pass is usually important, but different methods handle the return value in different ways. None of the methods described here modify the array on which they are invoked (though the function you pass can modify the array, of course).

> 以下小节中描述的大多数迭代器方法都接受可选的第二个实参。如果指定，则调用函数就像它是第二个实参的方法一样。也就是说，传递的第二个实参将成为第一个函数实参内部的 this 值。传递的函数的返回值通常很重要，但不同的方法以不同的方式处理返回值。此处描述的方法都没有修改调用它们的数组（当然，传递的函数可以修改这个数组）。

Each of these functions is invoked with a function as its first argument, and it is very common to define that function inline as part of the method invocation expression instead of using an existing function that is defined elsewhere. Arrow function syntax (see §8.1.3) works particularly well with these methods, and we will use it in the examples that follow.

> 这节的每个函数都调用它的第一个函数实参，并且通常将该函数内联定义为方法调用表达式的一部分，而不是使用在其他地方显示定义的函数。箭头函数语法（参见 §8.1.3）在这些方法中特别有效，我们将在下面的示例中使用它。

#### FOREACH()
The forEach() method iterates through an array, invoking a function you specify for each element. As we’ve described, you pass the function as the first argument to forEach(). forEach() then invokes your function with three arguments: the value of the array element, the index of the array element, and the array itself. If you only care about the value of the array element, you can write a function with only one parameter—the additional arguments will be ignored:

> forEach() 方法遍历数组，调用为每个元素指定的函数。正如我们已经描述的那样，将函数作为第一个实参传递给 forEach()。forEach() 然后使用三个实参调用函数：数组元素的值、数组元素的索引和数组本身。如果只关心数组元素的值，则编写一个只有一个实参的函数（将忽略其他实参）：

```js
let data = [1,2,3,4,5], sum = 0;
// Compute the sum of the elements of the array
data.forEach(value => { sum += value; });          // sum == 15

// Now increment each array element
data.forEach(function(v, i, a) { a[i] = v + 1; }); // data == [2,3,4,5,6]
```
Note that forEach() does not provide a way to terminate iteration before all elements have been passed to the function. That is, there is no equivalent of the break statement you can use with a regular for loop.

> 请注意，forEach() 不提供在所有元素传递给函数之前终止迭代的方法。也就是说，没有等效于常规 for 循环的 break 语句可以使用。

#### MAP()
The map() method passes each element of the array on which it is invoked to the function you specify and returns an array containing the values returned by your function. For example:

> map() 方法将调用数组的每个元素传递到指定的函数，并返回一个包含函数返回的值的数组。例如：

```js
let a = [1, 2, 3];
a.map(x => x*x)   // => [1, 4, 9]: the function takes input x and returns x*x
```
The function you pass to map() is invoked in the same way as a function passed to forEach(). For the map() method, however, the function you pass should return a value. Note that map() returns a new array: it does not modify the array it is invoked on. If that array is sparse, your function will not be called for the missing elements, but the returned array will be sparse in the same way as the original array: it will have the same length and the same missing elements.

> 传递到 map() 的函数的调用方式与传递给 forEach() 的函数相同。但是，对于 map() 方法，传递的函数应返回一个值。请注意，map() 返回一个新数组：它不会修改调用它的数组。如果该数组是稀疏的，则不会为缺失的元素调用函数，但返回的数组将稀疏，其确实元素与原始数组的位置相同：它将具有相同的长度和相同的缺失元素。

#### FILTER()
The filter() method returns an array containing a subset of the elements of the array on which it is invoked. The function you pass to it should be predicate: a function that returns true or false. The predicate is invoked just as for forEach() and map(). If the return value is true, or a value that converts to true, then the element passed to the predicate is a member of the subset and is added to the array that will become the return value. Examples:

> filter() 方法返回一个数组，其中包含调用该数组的数组元素的子集。传递给它的函数应该是断言：返回真或假的函数。断言函数的调用就像 forEach() 和 map() 调用一样。如果返回值为 true，或者能转换为 true 的值，则传递给断言的元素是子集的成员，并将添加到将成为返回值的数组中。例子：

```js
let a = [5, 4, 3, 2, 1];
a.filter(x => x < 3)         // => [2, 1]; values less than 3
a.filter((x,i) => i%2 === 0) // => [5, 3, 1]; every other value
```
Note that filter() skips missing elements in sparse arrays and that its return value is always dense. To close the gaps in a sparse array, you can do this:

> 注意 filter() 跳过稀疏数组中的丢失元素并且返回值也总是稠密的。要缩小稀疏数组的间距，可以这样做：

```js
let dense = sparse.filter(() => true);
```
And to close gaps and remove undefined and null elements, you can use filter, like this:

> 要缩小间隙并移除 undefined 和 null 元素，可以用 filter 这样做：

```js
a = a.filter(x => x !== undefined && x !== null);
```
#### FIND() AND FINDINDEX()
The find() and findIndex() methods are like filter() in that they iterate through your array looking for elements for which your predicate function returns a truthy value. Unlike filter(), however, these two methods stop iterating the first time the predicate finds an element. When that happens, find() returns the matching element, and findIndex() returns the index of the matching element. If no matching element is found, find() returns undefined and findIndex() returns -1:

> find() 和 findIndex() 方法就像 filter()，因为它们在数组中迭代，查找断言函数返回真实值的元素。但是，与 filter()不同，这两种方法在断言首次查找元素到时停止遍历。发生这种情况时，find() 返回匹配元素，而 findIndex() 返回匹配元素的索引。如果未找到匹配元素，find() 返回 undefined，findIndex() 返回 -1：

```js
let a = [1,2,3,4,5];
a.findIndex(x => x === 3)  // => 2; the value 3 appears at index 2
a.findIndex(x => x < 0)    // => -1; no negative numbers in the array
a.find(x => x % 5 === 0)   // => 5: this is a multiple of 5
a.find(x => x % 7 === 0)   // => undefined: no multiples of 7 in the array
```
#### EVERY() AND SOME()
The every() and some() methods are array predicates: they apply a predicate function you specify to the elements of the array, then return true or false.

> every() 和 some() 方法是数组断言：它们将指定的断言函数应用于数组的元素，然后返回 true 或 false。

The every() method is like the mathematical “for all” quantifier ∀: it returns true if and only if your predicate function returns true for all elements in the array:

> every() 方法与数学全称量化符号 ∀ 相似：如果数组中所有元素执行断言函数返回值都为 true，则返回 true：

```js
let a = [1,2,3,4,5];
a.every(x => x < 10)      // => true: all values are < 10.
a.every(x => x % 2 === 0) // => false: not all values are even.
```
The some() method is like the mathematical “there exists” quantifier ∃: it returns true if there exists at least one element in the array for which the predicate returns true and returns false if and only if the predicate returns false for all elements of the array:

> some() 方法与数学存在限定符 ∃ 相同：如果数组中存在至少有一个元素调用断言函数返回 true 的返回 true，仅在断言全部返回 false 时返回 false：

```js
let a = [1,2,3,4,5];
a.some(x => x%2===0)  // => true; a has some even numbers.
a.some(isNaN)         // => false; a has no non-numbers.
```
Note that both every() and some() stop iterating array elements as soon as they know what value to return. some() returns true the first time your predicate returns true and only iterates through the entire array if your predicate always returns false. every() is the opposite: it returns false the first time your predicate returns false and only iterates all elements if your predicate always returns true. Note also that, by mathematical convention, every() returns true and some returns false when invoked on an empty array.

> 请注意，every() 和 some() 只要它们知道要返回的值，都停止对数组元素的遍历。some() 在断言函数第一次返回 true 时返回 true，并且只有在每个元素调用断言函数都返回 false 时，才会遍历整个数组 。every() 正好相反：它返回 false 时，您的谓词返回 false，并且仅在谓词始终返回 true 时，才会回注所有元素。另请注意，根据数学约定，every() 返回 true，有些返回 false，当在空数组上调用时，某些返回 false。

#### REDUCE() AND REDUCERIGHT()
The reduce() and reduceRight() methods combine the elements of an array, using the function you specify, to produce a single value. This is a common operation in functional programming and also goes by the names “inject” and “fold.” Examples help illustrate how it works:

> reduce() 和 reduceRight() 方法使用指定的函数将数组元素进行组合，生成单个值。这在函数式编程中是常见的操作，也可以称为“注入”和“折叠”。举例说明它是如何工作的：

```js
let a = [1,2,3,4,5];
a.reduce((x,y) => x+y, 0)          // => 15; the sum of the values
a.reduce((x,y) => x*y, 1)          // => 120; the product of the values
a.reduce((x,y) => (x > y) ? x : y) // => 5; the largest of the values
```
reduce() takes two arguments. The first is the function that performs the reduction operation. The task of this reduction function is to somehow combine or reduce two values into a single value and to return that reduced value. In the examples we’ve shown here, the functions combine two values by adding them, multiplying them, and choosing the largest. The second (optional) argument is an initial value to pass to the function.

> reduce() 需要两个实参。第一个是执行化简操作的函数。化简函数的任务就是用某种方法把两个值组合或化简为一个值，并返回化简后的值。在上述例子中，函数通过加法、乘法或取最大值的方法组合两个值。第二个（可选）的实参是一个传递给函数的初始值。

Functions used with reduce() are different than the functions used with forEach() and map(). The familiar value, index, and array values are passed as the second, third, and fourth arguments. The first argument is the accumulated result of the reduction so far. On the first call to the function, this first argument is the initial value you passed as the second argument to reduce(). On subsequent calls, it is the value returned by the previous invocation of the function. In the first example, the reduction function is first called with arguments 0 and 1. It adds these and returns 1. It is then called again with arguments 1 and 2 and returns 3. Next, it computes 3+3=6, then 6+4=10, and finally 10+5=15. This final value, 15, becomes the return value of reduce().

> reduce() 使用的函数与 forEach() 和 map() 使用的函数不同。比较熟悉的是，数组元素、元素的索引和数组本身将作为第 2～4 个实参传递给函数。第一个实参是到目前为止的化简操作累积的结果。第一次调用函数时，第一个实参是一个初始值，它就是传递给 reduce() 的第二个实参。在接下来的调用中，这个值就是上一次化简函数的返回值。在上面的第一个例子中，第一次调用化简函数时的实参是 0 和 1。将两者相加并返回 1。再次调用时的实参是 1 和 2，它返回 3。然后它计算 3+3=6、6+4=10， 最后计算 10+5=15。最后的值是 15，reduce() 返回这个值。

You may have noticed that the third call to reduce() in this example has only a single argument: there is no initial value specified. When you invoke reduce() like this with no initial value, it uses the first element of the array as the initial value. This means that the first call to the reduction function will have the first and second array elements as its first and second arguments. In the sum and product examples, we could have omitted the initial value argument.

> 可能已经注意到了，上面第三次调用 reduce() 时只有一个实参：没有指定初始值。当不指定初始值调用 reduce() 时，它将使用数组的第一个元素作为其初始值。这意味着第一次调用化简函数就使用了第一个和第二个数组元素作为其第一个和第二个实参。在上面求和与求积的例子中，可以省略初始值实参。

Calling reduce() on an empty array with no initial value argument causes a TypeError. If you call it with only one value—either an array with one element and no initial value or an empty array and an initial value—it simply returns that one value without ever calling the reduction function.

> 在空数组上，不带初始值实参调用 reduce() 将导致类型错误异常。如果调用它的时候只有一个值（数组只有一个元素并且没有指定初始值，或者有一个空数组并且指定一个初始值）reduce() 只是简单地返回那个值而不会调用化简函数。

reduceRight() works just like reduce(), except that it processes the array from highest index to lowest (right-to-left), rather than from lowest to highest. You might want to do this if the reduction operation has right-to-left associativity, for example:

> reduceRight() 的工作原理和 reduce() 一样，不同的是它按照数组索引从高到低（从右到左）处理数组，而不是从低到高。如果 reduction 操作的优先顺序是从右到左，你可能想使用它，例如：

```js
// Compute 2^(3^4).  Exponentiation has right-to-left precedence
let a = [2, 3, 4];
a.reduceRight((acc,val) => Math.pow(val,acc)) // => 2.4178516392292583e+24
```
Note that neither reduce() nor reduceRight() accepts an optional argument that specifies the this value on which the reduction function is to be invoked. The optional initial value argument takes its place. See the Function.bind() method (§8.7.5) if you need your reduction function invoked as a method of a particular object.

> 注意，reduce() 和 reduceRight() 都能接收一个可选的实参，它指定了化简函数调用时的 this 关键字的值。可选的初始值实参仍然需要占一个位置。如果想让化简函数作为一个特殊对象的方法调用，请参看 Function.bind() 方法（§8.7.5）。

The examples shown so far have been numeric for simplicity, but reduce() and reduceRight() are not intended solely for mathematical computations. Any function that can combine two values (such as two objects) into one value of the same type can be used as a reduction function. On the other hand, algorithms expressed using array reductions can quickly become complex and hard to understand, and you may find that it is easier to read, write, and reason about your code if you use regular looping constructs to process your arrays.

> 为了简单起见，到目前位置所展示的例子都是数值的，但数学计算不是 reduce() 和 reduceRight() 的唯一意图。任何想要将两个相同类型的值（例如两个对象）合并到一个值的函数都可以用化简函数。另一方面，使用数组化简的算法可能很快变得复杂且难以理解，可能会发现，如果使用常规循环构造来处理数组则更容易读、写和推理。

### 7.8.2 Flattening arrays with flat() and flatMap()
In ES2019, the flat() method creates and returns a new array that contains the same elements as the array it is called on, except that any elements that are themselves arrays are “flattened” into the returned array. For example:

> 在 ES2019 中，flat() 方法创建并返回一个新的数组，该数组包含与调用的数组相同的元素，只不过作为数组的任何元素都"展平"到返回的数组中。例如：

```js
[1, [2, 3]].flat()    // => [1, 2, 3]
[1, [2, [3]]].flat()  // => [1, 2, [3]]
```
When called with no arguments, flat() flattens one level of nesting. Elements of the original array that are themselves arrays are flattened, but array elements of those arrays are not flattened. If you want to flatten more levels, pass a number to flat():

> 当调用时没有实参，flat() 将平展一个级别的嵌套。作为数组的原始数组的元素被展平，但这些数组的数组元素不会展平。如果要展平更多级别，需要传递数字给 flat()：

```js
let a = [1, [2, [3, [4]]]];
a.flat(1)   // => [1, 2, [3, [4]]]
a.flat(2)   // => [1, 2, 3, [4]]
a.flat(3)   // => [1, 2, 3, 4]
a.flat(4)   // => [1, 2, 3, 4]
```
The flatMap() method works just like the map() method (see “map()”) except that the returned array is automatically flattened as if passed to flat(). That is, calling a.flatMap(f) is the same as (but more efficient than) a.map(f).flat():

> flatMap() 方法的工作方式与 map() 方法（见“map()”）类似，只不过返回的数组会自动展平，就像传递到 flat()。也就是说，调用 a.flatMap(f) 与 a.map(f).flat()（但更高效）相同：

```js
let phrases = ["hello world", "the definitive guide"];
let words = phrases.flatMap(phrase => phrase.split(" "));
words // => ["hello", "world", "the", "definitive", "guide"];
```
You can think of flatMap() as a generalization of map() that allows each element of the input array to map to any number of elements of the output array. In particular, flatMap() allows you to map input elements to an empty array, which flattens to nothing in the output array:

> 可以将 flatMap() 视为 map() 的泛化，它允许输入数组的每个元素映射到输出数组的多个元素。特别的是，flatMap() 允许将输入元素映射到空数组，该数组在平展后不输出到数组中：

```js
// Map non-negative numbers to their square roots
[-2, -1, 1, 2].flatMap(x => x < 0 ? [] : Math.sqrt(x)) // => [1, 2**0.5]
```
### 7.8.3 Adding arrays with concat()
The concat() method creates and returns a new array that contains the elements of the original array on which concat() was invoked, followed by each of the arguments to concat(). If any of these arguments is itself an array, then it is the array elements that are concatenated, not the array itself. Note, however, that concat() does not recursively flatten arrays of arrays. concat() does not modify the array on which it is invoked:

> concat() 方法创建并返回一个新数组，它的元素包括调用 concat() 的原始数组的元素和 concat() 的每个实参。如果这些实参中的任何一个自身是数组，则连接的是数组的元素，而非数组本身。但要注意，concat() 不会递归扁平化数组的数组。concat() 也不会修改调用的数组：

```js
let a = [1,2,3];
a.concat(4, 5)          // => [1,2,3,4,5]
a.concat([4,5],[6,7])   // => [1,2,3,4,5,6,7]; arrays are flattened
a.concat(4, [5,[6,7]])  // => [1,2,3,4,5,[6,7]]; but not nested arrays
a                       // => [1,2,3]; the original array is unmodified
```
Note that concat() makes a new copy of the array it is called on. In many cases, this is the right thing to do, but it is an expensive operation. If you find yourself writing code like `a = a.concat(x)`, then you should think about modifying your array in place with push() or splice() instead of creating a new one.

> 请注意，concat() 创建调用数组的新副本。在许多情况下，这是正确的做法，但它是一个昂贵的操作。如果您发现自己编写代码像 `a = a.concat(x)`，那么您应该考虑使用 push() 或 splice() 修改数组，而不是创建新的数组。

### 7.8.4 Stacks and Queues with push(), pop(), shift(), and unshift()
The push() and pop() methods allow you to work with arrays as if they were stacks. The push() method appends one or more new elements to the end of an array and returns the new length of the array. Unlike concat(), push() does not flatten array arguments. The pop() method does the reverse: it deletes the last element of an array, decrements the array length, and returns the value that it removed. Note that both methods modify the array in place. The combination of push() and pop() allows you to use a JavaScript array to implement a first-in, last-out stack. For example:

> push() 和 pop() 方法允许将数组当做栈来使用。push() 方法在数组的尾部添加一个或多个元素，并返回数组新的长度。pop() 方法则相反：它删除数组的最后一个元素，减小数组长度并返回它删除的值。注意，两个方法都修改并替换原始数组而非生成一个修改版的新数组。组合使用 push() 和 pop() 能够用 JavaScript 数组实现先进后出的栈。例如：

```js
let stack = [];       // stack == []
stack.push(1,2);      // stack == [1,2];
stack.pop();          // stack == [1]; returns 2
stack.push(3);        // stack == [1,3]
stack.pop();          // stack == [1]; returns 3
stack.push([4,5]);    // stack == [1,[4,5]]
stack.pop()           // stack == [1]; returns [4,5]
stack.pop();          // stack == []; returns 1
```
The push() method does not flatten an array you pass to it, but if you want to push all of the elements from one array onto another array, you can use the spread operator (§8.3.4) to flatten it explicitly:

> push() 方法不展平传入的数组，但如果想要将数组的元素全部压入另外一个数组，可以使用展开运算符（§8.3.4）来显示展开：

```js
a.push(...values);
```
The unshift() and shift() methods behave much like push() and pop(), except that they insert and remove elements from the beginning of an array rather than from the end. unshift() adds an element or elements to the beginning of the array, shifts the existing array elements up to higher indexes to make room, and returns the new length of the array. shift() removes and returns the first element of the array, shifting all subsequent elements down one place to occupy the newly vacant space at the start of the array. You could use unshift() and shift() to implement a stack, but it would be less efficient than using push() and pop() because the array elements need to be shifted up or down every time an element is added or removed at the start of the array. Instead, though, you can implement a queue data structure by using push() to add elements at the end of an array and shift() to remove them from the start of the array:

> unshift() 和 shift() 方法的行为非常类似于 push() 和 pop()，不一样的是前者是在数组的头部而非尾部进行元素的插入和删除操作。unshift() 在数组的头部添加一个或多个元素，并将已存在的元素移动到更高索引的位置来获得足够的空间，最后返回数组新的长度。shift() 删除数组的第一个元素并将其返回，然后把所有随后的元素下移一个位置来填补数组头部的空缺。可以使用 unshift() 和 shift() 实现栈，但它比使用 push() 和 pop() 的效率低，因为每次在数组头部添加或删除元素时，都需要向上或向下移动数组元素。但是，您可以使用 push() 在数组末尾添加元素并 shift() 从数组的头部删除它们来实现队列数据解构：

```js
let q = [];            // q == []
q.push(1,2);           // q == [1,2]
q.shift();             // q == [2]; returns 1
q.push(3)              // q == [2, 3]
q.shift()              // q == [3]; returns 2
q.shift()              // q == []; returns 3
```
There is one feature of unshift() that is worth calling out because you may find it surprising. When passing multiple arguments to unshift(), they are inserted all at once, which means that they end up in the array in a different order than they would be if you inserted them one at a time:

> unshift() 有一个特性是值得一提的，你可能会觉得它令人惊讶。将多个实参传入 unshift() 时，它们将一次全部插入，这意味着它们最终在数组中的顺序与一次插入一个实参的顺序时不同的：

```js
let a = [];            // a == []
a.unshift(1)           // a == [1]
a.unshift(2)           // a == [2, 1]
a = [];                // a == []
a.unshift(1,2)         // a == [1, 2]
```
### 7.8.5 Subarrays with slice(), splice(), fill(), and copyWithin()
Arrays define a number of methods that work on contiguous regions, or subarrays or “slices” of an array. The following sections describe methods for extracting, replacing, filling, and copying slices.

> 数组定义了许多在连续区域，子数组或数组的“片段”上工作的方法。 以下各节描述了提取，替换，填充和复制片段的方法。

#### SLICE()
The slice() method returns a slice, or subarray, of the specified array. Its two arguments specify the start and end of the slice to be returned. The returned array contains the element specified by the first argument and all subsequent elements up to, but not including, the element specified by the second argument. If only one argument is specified, the returned array contains all elements from the start position to the end of the array. If either argument is negative, it specifies an array element relative to the length of the array. An argument of –1, for example, specifies the last element in the array, and an argument of –2 specifies the element before that one. Note that slice() does not modify the array on which it is invoked. Here are some examples:

> slice() 方法返回指定数组的一个片段或子数组。它的两个实参分别指定了片段的开始和结束的位置。返回的数组包含第一个实参指定的位置到（但不包含）第二个实参指定的位置之间的所有数组元素。如果只指定一个实参，返回的数组将包含从开始位置到数组结尾的所有元素。如实参中出现负数，它表示相对于数组 length 的位置。例如，实参 -1 指定了最后一个元素，而 -2 指定了它前面的元素。注意，slice() 不会修改调用的数组。下面有一些示例：

```js
let a = [1,2,3,4,5];
a.slice(0,3);    // Returns [1,2,3]
a.slice(3);      // Returns [4,5]
a.slice(1,-1);   // Returns [2,3,4]
a.slice(-3,-2);  // Returns [3]
```
#### SPLICE()
splice() is a general-purpose method for inserting or removing elements from an array. Unlike slice() and concat(), splice() modifies the array on which it is invoked. Note that splice() and slice() have very similar names but perform substantially different operations.

> splice() 方法是在数组中插入或删除元素的通用方法。不同于 slice() 和 concat()，splice() 会修改调用的数组。注意，splice() 和 slice() 拥有非常相似的名字， 但它们的功能却有本质的区别。

splice() can delete elements from an array, insert new elements into an array, or perform both operations at the same time. Elements of the array that come after the insertion or deletion point have their indexes increased or decreased as necessary so that they remain contiguous with the rest of the array. The first argument to splice() specifies the array position at which the insertion and/or deletion is to begin. The second argument specifies the number of elements that should be deleted from (spliced out of) the array. (Note that this is another difference between these two methods. The second argument to slice() is an end position. The second argument to splice() is a length.) If this second argument is omitted, all array elements from the start element to the end of the array are removed. splice() returns an array of the deleted elements, or an empty array if no elements were deleted. For example:

> splice() 能够从数组中删除元素、插入元素到数组中或者同时完成这两种操作。在插入或删除点之后的数组元素会根据需要增加或减小它们的索引值，因此数组的其他部分仍然保持连续的。splice() 的第一个实参指定了插入和（或）删除的起始位置。第二个实参指定了应该从数组中删除的元素的个数。（注意这里是这两个方法的另外一个不同。slice() 的第二个实参是结束的位置。splice() 的第二个实参是长度。）如果省略第二个实参，从起始点开始到数组结尾的所有元素都将被删除。splice() 返回一个由删除元素组成的数组，或者如果没有删除元素就返回一个空数组。例如：

```js
let a = [1,2,3,4,5,6,7,8];
a.splice(4)    // => [5,6,7,8]; a is now [1,2,3,4]
a.splice(1,2)  // => [2,3]; a is now [1,4]
a.splice(1,1)  // => [4]; a is now [1]
```
The first two arguments to splice() specify which array elements are to be deleted. These arguments may be followed by any number of additional arguments that specify elements to be inserted into the array, starting at the position specified by the first argument. For example:

> splice() 的前两个实参指定了需要删除的数组元素。紧随其后的任意个数的实参指定了需要插入到数组中的元素，从第一个实参指定的位置开始插入。例如：

```js
let a = [1,2,3,4,5];
a.splice(2,0,"a","b")  // => []; a is now [1,2,"a","b",3,4,5]
a.splice(2,2,[1,2],3)  // => ["a","b"]; a is now [1,2,[1,2],3,3,4,5]
```
Note that, unlike concat(), splice() inserts arrays themselves, not the elements of those arrays.

> 注意，不同于 concat()，splice() 插入数组本身，不是数组的元素。

#### FILL()
The fill() method sets the elements of an array, or a slice of an array, to a specified value. It mutates the array it is called on, and also returns the modified array:

> fill() 方法将数组或数组片段的元素填充为指定值。它将对调用它的数组进行突变，并返回修改后的数组：

```js
let a = new Array(5);   // Start with no elements and length 5
a.fill(0)               // => [0,0,0,0,0]; fill the array with zeros
a.fill(9, 1)            // => [0,9,9,9,9]; fill with 9 starting at index 1
a.fill(8, 2, -1)        // => [0,9,8,8,9]; fill with 8 at indexes 2, 3
```
The first argument to fill() is the value to set array elements to. The optional second argument specifies the starting index. If omitted, filling starts at index 0. The optional third argument specifies the ending index—array elements up to, but not including, this index will be filled. If this argument is omitted, then the array is filled from the start index to the end. You can specify indexes relative to the end of the array by passing negative numbers, just as you can for slice().

> fill() 的第一个实参是将数组元素填充的值。可选的第二个实参指定起始索引。如果省略，则填充将从索引 0 开始。可选的第三个实参指定结束索引，将填充到（但不包括）该索引的数组元素。 如果省略此实参，则从起始索引到末尾填充数组。可以通过传递负数来指定相对于数组末尾的索引，就像 slice() 一样。

#### COPYWITHIN()
copyWithin() copies a slice of an array to a new position within the array. It modifies the array in place and returns the modified array, but it will not change the length of the array. The first argument specifies the destination index to which the first element will be copied. The second argument specifies the index of the first element to be copied. If this second argument is omitted, 0 is used. The third argument specifies the end of the slice of elements to be copied. If omitted, the length of the array is used. Elements from the start index up to, but not including, the end index will be copied. You can specify indexes relative to the end of the array by passing negative numbers, just as you can for slice():

> copyWithin() 将数组的一个片段复制到数组中的新位置。它在适当的位置修改数组并返回修改后的数组，但不会更改数组的长度。第一个实参指定将第一个元素复制到的目标索引。第二个实参指定被复制的第一个元素的索引。如果省略此第二个实参，则使用 0。第三个实参指定被复制的元素片段的结尾。如果省略，则使用数组的长度。从开始索引到结束索引（但不包括结束索引）的元素将被复制。可以通过传递负数来指定相对于数组末尾的索引，就像 slice() 一样：

```js
let a = [1,2,3,4,5];
a.copyWithin(1)       // => [1,1,2,3,4]: copy array elements up one
a.copyWithin(2, 3, 5) // => [1,2,3,4,4]: copy last 2 elements to index 2
a.copyWithin(0, -2)   // => [4,4,3,4,4]: negative offsets work, too
```
copyWithin() is intended as a high-performance method that is particularly useful with typed arrays (see §11.2). It is modeled after the memmove() function from the C standard library. Note that the copy will work correctly even if there is overlap between the source and destination regions.

> copyWithin() 旨在作为一种高性能方法，对类型化数组特别有用（请参见 §11.2）。它模仿的 C 标准库中 memmove() 函数。 请注意，即使源区域和目标区域之间存在重叠，该拷贝也可以正常工作。

### 7.8.6 Array Searching and Sorting Methods
Arrays implement indexOf(), lastIndexOf(), and includes() methods that are similar to the same-named methods of strings. There are also sort() and reverse() methods for reordering the elements of an array. These methods are described in the subsections that follow.

> 数组实现 indexOf()、lastIndexOf() 和 include() 方法，这些方法类似于名称相同的字符串方法。还有 sort() 和 reverse() 方法，用于对数组元素进行重新排序。这些方法在下面的小节中介绍。

#### INDEXOF() AND LASTINDEXOF()
indexOf() and lastIndexOf() search an array for an element with a specified value and return the index of the first such element found, or -1 if none is found. indexOf() searches the array from beginning to end, and lastIndexOf() searches from end to beginning:

> indexOf() 和 lastIndexOf() 在数组中搜索具有指定值的元素，并返回找到的第一个元素的索引，如果未找到，则返回 -1。indexOf() 从头到尾搜索数组，lastIndexOf() 从尾到头搜索：

```js
let a = [0,1,2,1,0];
a.indexOf(1)       // => 1: a[1] is 1
a.lastIndexOf(1)   // => 3: a[3] is 1
a.indexOf(3)       // => -1: no element has value 3
```
indexOf() and lastIndexOf() compare their argument to the array elements using the equivalent of the === operator. If your array contains objects instead of primitive values, these methods check to see if two references both refer to exactly the same object. If you want to actually look at the content of an object, try using the find() method with your own custom predicate function instead.

> indexOf() 和 lastIndexOf() 使用 === 运算符将其实参与数组元素进行比较。如果数组包含对象而不是原始值，则这些方法将检查两个引用是否都指向完全相同的对象。如果要实际查看对象的内容，尝试将 find() 方法代替自定义的断言函数。

indexOf() and lastIndexOf() take an optional second argument that specifies the array index at which to begin the search. If this argument is omitted, indexOf() starts at the beginning and lastIndexOf() starts at the end. Negative values are allowed for the second argument and are treated as an offset from the end of the array, as they are for the slice() method: a value of –1, for example, specifies the last element of the array.

> indexOf() 和 lastIndexOf() 采用可选的第二个实参，该实参指定开始搜索的数组索引。如果省略此参数，则 indexOf() 从开头开始，lastIndexOf() 从结尾开始。第二个参数允许使用负值，并将其视为距数组末端的偏移量，就像 slice() 方法一样：例如，值 –1 指定数组的最后一个元素。

The following function searches an array for a specified value and returns an array of all matching indexes. This demonstrates how the second argument to indexOf() can be used to find matches beyond the first.

> 以下函数在数组中搜索指定的值，并返回所有匹配索引的数组。这演示了如何使用 indexOf() 的第二个参数来查找第一个参数之外的匹配项。

```js
// Find all occurrences of a value x in an array a and return an array
// of matching indexes
function findall(a, x) {
    let results = [],            // The array of indexes we'll return
        len = a.length,          // The length of the array to be searched
        pos = 0;                 // The position to search from
    while(pos < len) {           // While more elements to search...
        pos = a.indexOf(x, pos); // Search
        if (pos === -1) break;   // If nothing found, we're done.
        results.push(pos);       // Otherwise, store index in array
        pos = pos + 1;           // And start next search at next element
    }
    return results;              // Return array of indexes
}
```
Note that strings have indexOf() and lastIndexOf() methods that work like these array methods, except that a negative second argument is treated as zero.

> 请注意，字符串具有 indexOf() 和 lastIndexOf() 方法，它们与这些数组方法一样工作，不同之处在于第二个实参是负数时被视为零。

#### INCLUDES()
The ES2016 includes() method takes a single argument and returns true if the array contains that value or false otherwise. It does not tell you the index of the value, only whether it exists. The includes() method is effectively a set membership test for arrays. Note, however, that arrays are not an efficient representation for sets, and if you are working with more than a few elements, you should use a real Set object (§11.1.1).

> ES2016 的 includes() 方法采用单个实参，如果数组包含该值返回 true 否则 false。它不会告诉你值的索引，只告诉你该值是否存在。includes() 方法实际上是数组集的成员身份测试。但是请注意，数组不是 Set 的高效表示形式，如果使用多个元素，则应使用真正的 Set 对象（§11.1.1）。

The includes() method is slightly different than the indexOf() method in one important way. indexOf() tests equality using the same algorithm that the === operator does, and that equality algorithm considers the not-a-number value to be different from every other value, including itself. includes() uses a slightly different version of equality that does consider NaN to be equal to itself. This means that indexOf() will not detect the NaN value in an array, but includes() will:

> includes() 方法在一个重要方面与 indexOf() 方法略有不同。indexOf() 与 === 运算符使用相同的算法测试相等性，并且这个相等算法认为非数字值与所有其他值（包括自身）不同。includes() 使用略有不同的相等算法，它认为 NaN 等于自身。这意味着 indexOf() 不会检测数组中的 NaN 值，但 includes() 可以：

```js
let a = [1,true,3,NaN];
a.includes(true)            // => true
a.includes(2)               // => false
a.includes(NaN)             // => true
a.indexOf(NaN)              // => -1; indexOf can't find NaN
```
#### SORT()
sort() sorts the elements of an array in place and returns the sorted array. When sort() is called with no arguments, it sorts the array elements in alphabetical order (temporarily converting them to strings to perform the comparison, if necessary):

> sort() 对数组的元素直接进行排序，并返回排序后的数组。当调用 sort() 时，它会按字母顺序对数组元素进行排序（如有必要，暂时将它们转换为字符串以执行比较）：

```js
let a = ["banana", "cherry", "apple"];
a.sort(); // a == ["apple", "banana", "cherry"]
```
If an array contains undefined elements, they are sorted to the end of the array.

> 如果数组中包含 undefined 元素，它们会被放在数组的结尾。

To sort an array into some order other than alphabetical, you must pass a comparison function as an argument to sort(). This function decides which of its two arguments should appear first in the sorted array. If the first argument should appear before the second, the comparison function should return a number less than zero. If the first argument should appear after the second in the sorted array, the function should return a number greater than zero. And if the two values are equivalent (i.e., if their order is irrelevant), the comparison function should return 0. So, for example, to sort array elements into numerical rather than alphabetical order, you might do this:

> 若要将数组按字母顺序以外的顺序排序，必须将比较函数作为实参传递给 sort()。该函数决定了它的两个实参在排好序的数组中的先后顺序。假设第一个实参应该在前，比较函数应该返回一个小于 0 的数值。反之，假设第一个参数应该在后，函数应该返回一个大于 0 的数值。并且，假设两个值相等（也就是说，它们的顺序无关紧要），函数应该返回 0。例如，用数值大小而非字母表顺序进行数组排序，代码如下：

```js
let a = [33, 4, 1111, 222];
a.sort();               // a == [1111, 222, 33, 4]; alphabetical order
a.sort(function(a,b) {  // Pass a comparator function
    return a-b;         // Returns < 0, 0, or > 0, depending on order
});                     // a == [4, 33, 222, 1111]; numerical order
a.sort((a,b) => b-a);   // a == [1111, 222, 33, 4]; reverse numerical order
```
As another example of sorting array items, you might perform a case-insensitive alphabetical sort on an array of strings by passing a comparison function that converts both of its arguments to lowercase (with the toLowerCase() method) before comparing them:

> 另外一个数组元素排序的例子，也许需要对一个字符串数组执行不区分大小写的字母表排序，比较函数首先将实参都转化为小写字符串（使用 toLowerCase() 方法），再开始比较：

```js
let a = ["ant", "Bug", "cat", "Dog"];
a.sort();    // a == ["Bug","Dog","ant","cat"]; case-sensitive sort
a.sort(function(s,t) {
    let a = s.toLowerCase();
    let b = t.toLowerCase();
    if (a < b) return -1;
    if (a > b) return 1;
    return 0;
});   // a == ["ant","Bug","cat","Dog"]; case-insensitive sort
```
#### REVERSE()
The reverse() method reverses the order of the elements of an array and returns the reversed array. It does this in place; in other words, it doesn’t create a new array with the elements rearranged but instead rearranges them in the already existing array:

> reverse() 方法反转数组中元素的顺序并返回反转后的数组。它直接在数组中操作，换一种说法，它不创建一个新的数组，它不创建一个新的带有排序后的元素的数组，而是直接在已存在的数组中进行排序。

```js
let a = [1,2,3];
a.reverse();   // a == [3,2,1]
```
### 7.8.7 Array to String Conversions
The Array class defines three methods that can convert arrays to strings, which is generally something you might do when creating log and error messages. (If you want to save the contents of an array in textual form for later reuse, serialize the array with JSON.stringify() [§6.8] instead of using the methods described here.)

> Array 类定义了三个方法来将数组转化为字符串，通常在创建日志和错误信息时会用到。（如果要以文本形式保存数组的内容供以后重用，请使用 JSON.stringify()（§6.8）序列化数组，而不是使用此处描述的方法。）

The join() method converts all the elements of an array to strings and concatenates them, returning the resulting string. You can specify an optional string that separates the elements in the resulting string. If no separator string is specified, a comma is used:

> join() 方法将数组的所有元素转换为字符串并连接它们，返回生成的字符串。可以指定一个可选字符串来分隔生成的字符串中的元素。如果未指定分隔符字符串，则使用逗号：

```js
let a = [1, 2, 3];
a.join()               // => "1,2,3"
a.join(" ")            // => "1 2 3"
a.join("")             // => "123"
let b = new Array(10); // An array of length 10 with no elements
b.join("-")            // => "---------": a string of 9 hyphens
```
The join() method is the inverse of the String.split() method, which creates an array by breaking a string into pieces.

> join() 方法是 String.split() 方法的反向方法，该方法通过将字符串拆分为多个片段来创建数组。

Arrays, like all JavaScript objects, have a toString() method. For an array, this method works just like the join() method with no arguments:

> 数组与所有 JavaScript 对象一样，具有 toString() 方法。对于数组，此方法的工作方式与没有参数的 join() 方法相同：

```js
[1,2,3].toString()          // => "1,2,3"
["a", "b", "c"].toString()  // => "a,b,c"
[1, [2,"c"]].toString()     // => "1,2,c"
```
Note that the output does not include square brackets or any other sort of delimiter around the array value.

> 请注意，输出不包括方括号或数组值周围的任何其他分隔符。

toLocaleString() is the localized version of toString(). It converts each array element to a string by calling the toLocaleString() method of the element, and then it concatenates the resulting strings using a locale-specific (and implementation-defined) separator string.

> toLocaleString() 是 toString() 的本地化版本。它通过调用元素的 toLocaleString() 方法将每个数组元素转换为字符串，然后使用特定于区域设置（和实现定义）分隔符字符串连接生成的字符串。

### 7.8.8 Static Array Functions
In addition to the array methods we’ve already documented, the Array class also defines three static functions that you can invoke through the Array constructor rather than on arrays. Array.of() and Array.from() are factory methods for creating new arrays. They were documented in §7.1.4 and §7.1.5.

> 除了我们已经记录的数组方法之外，Array 类还定义了三个静态函数，可以通过 Array 构造函数而不是数组调用。Array.of() 和 Array.from() 是用于创建新数组的工厂方法。它们记录在 §7.1.4 和 §7.1.5 中。

The one other static array function is Array.isArray(), which is useful for determining whether an unknown value is an array or not:

> 另外一个静态数组方法是 Array.isArray()，用来判断一个未知值是否是数组：

```js
Array.isArray([])     // => true
Array.isArray({})     // => false
```
## 7.9 Array-Like Objects
As we’ve seen, JavaScript arrays have some special features that other objects do not have:

> 我们已经看到，JavaScript 数组的有一些特性是其他对象所没有的：

The length property is automatically updated as new elements are added to the list.

> 当有新的元素添加到列表中时，自动更新 length 属性。

Setting length to a smaller value truncates the array.

> length 设置为一个较小值将截断数组。

Arrays inherit useful methods from Array.prototype.

> 从 Array.prototype 中继承一些有用的方法。

Array.isArray() returns true for arrays.

> 数组传入 Array.isArray() 方法返回 true。

These are the features that make JavaScript arrays distinct from regular objects. But they are not the essential features that define an array. It is often perfectly reasonable to treat any object with a numeric length property and corresponding non-negative integer properties as a kind of array.

> 这些特性让 JavaScript 数组和常规的对象有明显的区别。但是它们不是定义数组的本质特性。一种常常完全合理的看法是把拥有一个数值型 length 属性和对应非负整数属性的对象看作数组的同类。

These “array-like” objects actually do occasionally appear in practice, and although you cannot directly invoke array methods on them or expect special behavior from the length property, you can still iterate through them with the same code you’d use for a true array. It turns out that many array algorithms work just as well with array-like objects as they do with real arrays. This is especially true if your algorithms treat the array as read-only or if they at least leave the array length unchanged.

> 实际上这些“类数组”对象在实践中偶尔出现，虽然不能通过它们直接调用数组方法或者期望 length 属性有什么特殊的行为，但是仍然可以用针对真正数组遍历代码来遍历它们。结论就是很多数组算法针对类数组对象同样奏效，就像针对真正的数组一样。尤其是这种情况，算法把数组看成只读的或者如果保持数组长度不变。

The following code takes a regular object, adds properties to make it an array-like object, and then iterates through the “elements” of the resulting pseudo-array:

> 以下代码为一个常规对象增加了一些属性使其变成类数组对象，然后遍历生成的伪数组的“元素”：

```js
let a = {};  // Start with a regular empty object

// Add properties to make it "array-like"
let i = 0;
while(i < 10) {
    a[i] = i * i;
    i++;
}
a.length = i;

// Now iterate through it as if it were a real array
let total = 0;
for(let j = 0; j < a.length; j++) {
    total += a[j];
}
```
In client-side JavaScript, a number of methods for working with HTML documents (such as document.querySelectorAll(), for example) return array-like objects. Here’s a function you might use to test for objects that work like arrays:

> 在客户端 JavaScript 中，很多作用于 HTML documents 的方法（例如 document.querySelectorAll()）返回类数组对象。下面这个函数可能会用于测试对象是否可以用作类数组：

```js
// Determine if o is an array-like object.
// Strings and functions have numeric length properties, but are
// excluded by the typeof test. In client-side JavaScript, DOM text
// nodes have a numeric length property, and may need to be excluded
// with an additional o.nodeType !== 3 test.
function isArrayLike(o) {
    if (o &&                            // o is not null, undefined, etc.
        typeof o === "object" &&        // o is an object
        Number.isFinite(o.length) &&    // o.length is a finite number
        o.length >= 0 &&                // o.length is non-negative
        Number.isInteger(o.length) &&   // o.length is an integer
        o.length < 4294967295) {        // o.length < 2^32 - 1
        return true;                    // Then o is array-like.
    } else {
        return false;                   // Otherwise it is not.
    }
}
```
We’ll see in a later section that strings behave like arrays. Nevertheless, tests like this one for array-like objects typically return false for strings—they are usually best handled as strings, not as arrays.

> 我们会在下一节看到字符串的行为像数组一样。尽管如此，对于数组这种测试（对字符串通常返回 false ）它们通常最好作为字符串处理，而不是作为数组处理。

Most JavaScript array methods are purposely defined to be generic so that they work correctly when applied to array-like objects in addition to true arrays. Since array-like objects do not inherit from Array.prototype, you cannot invoke array methods on them directly. You can invoke them indirectly using the Function.call method, however (see §8.7.4 for details):

> 大多数 JavaScript 数组方法都特意定义为泛型，以便它们在应用于除数组之外的类数组可以正常工作。由于类数组对象不会从 Array.prototype 继承，因此不能直接在它们上调用数组方法。但是，可以使用 Function.call 方法间接调用它们（详情请参阅 §8.7.4）：

```js
let a = {"0": "a", "1": "b", "2": "c", length: 3}; // An array-like object
Array.prototype.join.call(a, "+")                  // => "a+b+c"
Array.prototype.map.call(a, x => x.toUpperCase())  // => ["A","B","C"]
Array.prototype.slice.call(a, 0)   // => ["a","b","c"]: true array copy
Array.from(a)                      // => ["a","b","c"]: easier array copy
```
The second-to-last line of this code invokes the Array slice() method on an array-like object in order to copy the elements of that object into a true array object. This is an idiomatic trick that exists in much legacy code, but is now much easier to do with Array.from().

> 此代码倒数第二行调用数组类对象上的 Array slice() 方法，以便将该对象的元素复制到真正的数组对象中。这是一个惯用的技巧，存在于许多旧代码中，但现在使用 Array.from() 要容易得多。

## 7.10 Strings as Arrays
JavaScript strings behave like read-only arrays of UTF-16 Unicode characters. Instead of accessing individual characters with the charAt() method, you can use square brackets:

> JavaScript 字符串的行为类似于 UTF-16 Unicode 字符的只读数组。可以使用方括号替代 charAt() 方法访问单个字符：

```js
let s = "test";
s.charAt(0)    // => "t"
s[1]           // => "e"
```
The typeof operator still returns “string” for strings, of course, and the Array.isArray() method returns false if you pass it a string.

> 当然，字符串使用 typeof 运算符仍然返回 "string"，如果将字符串传递给 Array.isArray() 方法，则返回 false。

The primary benefit of indexable strings is simply that we can replace calls to charAt() with square brackets, which are more concise and readable, and potentially more efficient. The fact that strings behave like arrays also means, however, that we can apply generic array methods to them. For example:

> 可索引字符串的主要好处是，我们可以用方括号替换对 charAt() 的调用，方括号更简洁、更可读，而且可能更高效。但是，字符串的行为类似于数组，也意味着我们可以对它们应用泛型数组方法。例如：

```js
Array.prototype.join.call("JavaScript", " ")  // => "J a v a S c r i p t"
```
Keep in mind that strings are immutable values, so when they are treated as arrays, they are read-only arrays. Array methods like push(), sort(), reverse(), and splice() modify an array in place and do not work on strings. Attempting to modify a string using an array method does not, however, cause an error: it simply fails silently.

> 请记住，字符串是不可变值，因此当字符串被视为数组时，它们是只读数组。数组方法 push()、sort()、reverse() 和 splice() 直接修改数组，它们不能处理字符串。但是，尝试使用数组方法修改字符串不会引发异常：它只是静默失败。

## 7.11 Summary
This chapter has covered JavaScript arrays in depth, including esoteric details about sparse arrays and array-like objects. The main points to take from this chapter are:

> 本章深入介绍了 JavaScript 数组，包括有关稀疏数组和类数组对象的深奥细节。本章要点包括：

Array literals are written as comma-separated lists of values within square brackets.

> 数组字面量编写：方括号内逗号分隔值列表。

Individual array elements are accessed by specifying the desired array index within square brackets.

> 通过在方括号内指定所需的数组索引来访问单个数组元素。

The for/of loop and ... spread operator introduced in ES6 are particularly useful ways to iterate arrays.

> for/of 循环和 ES6 中引入的 ... 展开运算符是遍历数组的特别有用的方法。

The Array class defines a rich set of methods for manipulating arrays, and you should be sure to familiarize yourself with the Array API.

> Array 类定义了一组用于操作数组的丰富方法，应该确保熟悉 Array API。