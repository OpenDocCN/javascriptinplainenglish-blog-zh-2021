# JavaScript 基础:对象和函数

> 原文：<https://javascript.plainenglish.io/javascript-basics-objects-and-functions-30726efc766d?source=collection_archive---------3----------------------->

## 剧透:函数是对象

![](img/18d2950415592062e240cdd6897f79f0.png)

在这篇文章中，我们将介绍 JavaScript 中对象和函数的概念。

# 目标

对象是键/值对(属性)的集合。

```
{
   "key": "value"
}
```

属性值可以是基元(字符串、整数、布尔值等。)、另一个对象或函数(如果在对象内部，则称为方法)。一个对象及其属性位于内存中，它可以引用内存中与之相连的其他对象，如另一个对象或函数。

## 创建对象

JavaScript 对象可以通过两种方式创建:

```
let person = new Object(); // object initializelet animal = {}; // object literal
```

创建对象的两种方式是相同的。简写为 object literal，是创建新对象的更简短的方法。当 JavaScript 引擎解析语法并遇到花括号时，它假设您正在创建一个对象。JavaScript 引擎将对象文字视为一行代码。

## 访问/设置对象属性

可以使用`bracket notation`访问或设置 JavaScript 对象的属性。使用这种方法，我们可以动态地决定我们试图访问/设置哪个属性。在括号内，我们输入试图在内存中定位的值的名称。例如:

```
let person = {}
person["name"] = "Pete"
person["age"] = 18
console.log(person["name"]) // "Pete"
```

当我们设置“name”和“age”属性时，这将在内存中为每个属性创建一个位置，给它这些名称，并且`person`对象将有一个对内存中该位置的地址的引用。

访问属性和方法的一个更常见、更容易的操作符是`dot operator`。使用这种方法，不需要用引号来表示值。例如:

```
let person = {};
person.name = "Luka"
person.age = "34"
console.log(person.name) // "Luka"
```

在引擎盖下，JavaScript 正在读取`person`是一个对象。当 JavaScript 注意到对象后面的点时，它会将点之后的任何内容作为属性读取。

对象本身及其属性都在内存中。`dots`和`brackets`是访问信息的一种方式。建议使用 dot，除非在特殊情况下，例如:

```
let person = {}
person["Voted-Most-Likely-To-Be-A-CEO-in-HighSchool"] = true
person.Voted-Most-Likely-To-Be-A-CEO-in-HighSchool // will not work
```

有可能拥有包含符号甚至空格的属性。对于`dot notation`，JavaScript 将无法正确解析它并抛出语法错误。在这种情况下，`dot notation`将不适用于`bracket notation`。

# 功能

JavaScript 中的函数是`first-class`函数。这意味着函数被视为任何其他数据类型。它们可以作为值赋给变量，作为参数传递给其他函数，也可以由另一个函数返回。

## 函数是对象

就像任何对象一样，它驻留在内存中。函数具有普通对象的特征和一些其他特殊属性。属性和方法可以附加到函数上。函数对象有一些隐藏的属性:

*   一个函数不需要有名字，它可以是我们所知的`anonymous`函数。《出埃及记》`function(){ console.log("noName")}`
*   一个函数有一个`code`属性，写在花括号内的代码行放在这里。该属性的与众不同之处在于它是可调用的，这意味着您可以运行代码。

让我们看一个例子:

```
function sayHello(){
  console.log("Bye")
}sayHello.test = "Test"
```

我们在内存中创建了一个函数，它有两个属性:`name`，即`sayHello`和`code`，即`console.log("Bye")`。函数本身可以被调用，导致内部代码运行。如前所述，函数是 JavaScript 中的对象。可以创建属性并为其赋值。

## 函数语句和函数表达式

一个`function statement`声明了一个函数。类似于用关键字`var`、`const`或`let`声明变量，用关键字`function`声明`function statement`。让我们看一个例子:

```
// function statement
function example(){
   return "sample"
}
```

函数`example`被声明并存放在内存中。直到函数本身被调用和执行，它才返回值。有了`function statements`，他们就是`hoisted`。

`function expression`是一个动态创建并存储在变量中的函数。让我们看一个例子:

```
// function expression
const example = function(){
   return "sample"
}// OR arrow functionconst example = () => {
   return "sample"
}
```

在这两种情况下，我们都在内存中创建了一个函数。变量被分配给内存中的地址。但是，使用`function expressions`，数值不是`hoisted`。

综上所述，两者的区别在于`function statements`可以在代码到达之前调用，而`function expressions`由于吊装必须首先到达。

```
// function statementsample(); // will execute
function sample(){
   console.log('hello!')
}// function expression
sample(); // sample will be undefined at this point. Error
const sample = function(){
   console.log('goodbye!')
}
```

使用`function expressions`比`function statements`有好处。它们可以用作`closures`、其他函数的参数以及`immediately invoked functions` (IIFEs)。

# 通过值和引用

JavaScript 中经常出现的一个话题涉及到`by-value`和`by-reference`。

## 按价值

在这两种情况下，都涉及到变量。假设我们有一个赋给原始值的变量:

```
let a = "hello"
```

变量`a`拥有原始值(在本例中是一个字符串)在内存中的地址位置。比方说我们的另一行代码:

```
let b = a;
```

在这种情况下，`a`被声明为字符串，`hello`。在 JavaScript 中，如果被赋值的值是一个原始值，`b`实际上是指向内存中一个新的地址位置。`hello`的值将存在于两个地址位置。

这种方法被称为`by-value`。我们通过复制值将一个值(`b`)赋给另一个值(`a`)。这两个变量变得相同，但是在内存中的两个不同的位置。让我们来看看，如果我们尝试更改重新赋值，会发生什么情况:

```
//by value
let a = 4;
let b;
b = a;a = 2;
console.log(a) // 2
console.log(b) // 4
```

由于是原始类型，设置`b = a`会在内存中为`b`创建一个新位置，从`a`复制值并设置为`b`的值。因此，如果我们后来重新分配`a`的值，它不会影响`b`，因为它们在内存中是两个不同的位置。

## 通过引用

至此，我们已经关注了原始值。如果我们给一个包含函数和数组的对象赋一个变量，我们在内存中仍然有一个地址位置，这个变量会知道这个对象在哪里。

但是当我们试图将`b`赋值给`a`时，会发生一些不同的事情。让我们看另一个例子，变量相同，但赋值不同。

```
let a = {
  "property1": "sample",
  "property2": "example"
}let b = a;
```

在这个例子中，我们将变量`a`分配给一个对象。类似于前面的例子，我们将`b`赋值给`a`，它指向一个包含值(对象)的地址位置。与原始值不同，`b`不是在内存中获取新的地址位置，而是简单地指向内存中`a`所指向的相同位置。不会创建新对象。这同样适用于函数和数组。

这样，`a`和`b`都有相同的值。这叫做`by-reference`。当将所有对象设置为彼此相等时，或者作为参数传递给函数时，所有对象都会相互作用`by-reference`。如果我们试图改变变量`b`的属性，最终也会影响变量`a`，因为它们指向相同的地址位置。让我们来看看:

```
// by reference (all objects including functions and arrays)
let c = {"favQuote": "hello"}
let d;d = c;
c.favQuote = "goodbye"console.log(c) // {"favQuote": "goodbye"}
console.log(d) // {"favQuote": "goodbye"}
```

当将`c`设置为对象时，在存储器中创建一个地址位置。当将`d`赋值给`c`时，等号运算符注意到它是一个对象，而不是设置一个新的地址位置，而是指向同一个地址。

如上所述，如果我们试图改变一个变量的属性，它会对另一个变量产生影响。如果多个变量指向同一个对象，那么所有的变量都会被改变。

同样的概念也适用于将对象作为参数传递给函数。如果对象在功能代码块中改变，它将改变所有变量。

```
// by reference (even as parameters)function changeGreeting(obj){    obj.favQuote = "hi"}changeGreeting(d) //all values change
console.log(c) // {"favQuote": "hi"}
console.log(d) // {"favQuote": "hi"}
```

如果这是一个问题，那么必须创建一个新的对象来确保在内存中有一个新的位置。

```
let c = {"favQuote": "hello"}
let d = {"favQuote": "hello"}d.favQuote = "goodbye"console.log(c) // {"favQuote": "hello"}
console.log(d) // {"favQuote": "goodbye"}
```

这样，等号运算符会看到开始的花括号，并意识到该对象不是内存中预先存在的地址位置。这是一个全新的物体创造了飞行。

# 对象、函数和` this '

在我的博客 [JavaScript 基础:执行上下文](https://medium.com/javascript-in-plain-english/javascript-basics-execution-context-bd79ede1ccdd)中，我讨论了`execution context`的概念，它是在 JavaScript 中调用函数时创建的。创建时，`execution context`被添加到所谓的`execution stack`之上，后者跟踪并管理多个`execution contexts`。

把`execution context`想象成关注特定函数对象的代码。每个`execution context`都有一个`variable environment`，其中在函数内部创建的变量有一个对`outer environment`的引用，这意味着它可以访问在其代码范围之外定义的变量。

每次创建一个`execution context`时，它都会给我们一个变量`this`，并且它会根据函数的调用方式指向不同的对象。这个概念往往是 JavaScript 中容易混淆的部分。一旦 JavaScript 代码开始运行，变量`this`立即可用。

一旦运行了 JavaScript 代码，我们就有了`global execution context`。在这一层，`this`变量指向`window`对象(用于浏览器，但`global`在节点上)。当一个函数在全局级别被调用时，代码块内部的`this`变量仍然指向`window`对象。让我们探索一个例子:

```
let a = 'filler';function callMe(){
   console.log(this); // window object
}console.log(this); // window object
callMe();
```

提醒一下，在对象文字中，作为函数的属性值被称为`methods`。在函数是附加到对象的方法的情况下，`this`关键字成为包含该方法的对象。让我们想象一下:

```
const obj = {
   name: "Bob"
   sample: function(){ 
      console.log(this) // {name: "Bob", sample: f()}  
   }
}obj.sample()
```

为了有所帮助，`this`指向调用函数的地方或者点符号左边的地方。在这种情况下，`obj`是调用函数的部分，并成为上下文中的`this`关键字。然而，如果这个方法中有另一个函数，事情就会变得棘手和混乱。

```
const obj = {
   name: "Bob",
   sample: function(){ 
      let setName = function(newName){
         console.log(this) // this actually points to the window
         this.name = newName; 
      } 
      setName("Jack");
   }
}obj.sample()
```

`setName`函数表达式中的`this`实际上引用了`window`对象，但我们期望`this`引用`obj`。这是一个关于对象方法中函数语法的小错误。为了解决这个问题，我们可以使用一个变量来存储引用。让我们添加一行额外的代码:

```
const obj = {
   name: "Bob",
   sample: function(){ 
      let self = this;
      let setName = function(newName){
         console.log(self) // self references the obj
         self.name = newName; 
      } 
      setName("Jack");
   }
}obj.sample();
```

在`setName`函数表达式内部，没有名为`self`的变量。所以它在上下文之外寻找变量。它发现`self`在上下文中引用的`this`恰好是`obj`。修复和`this`的概念可能需要一点时间来完全掌握和理解。

# 结论

我们已经讨论了 JavaScript 中对象和函数的一些基本概念。理解这些概念有助于更高级的主题，如类和继承。

感谢您的阅读和快乐编码！