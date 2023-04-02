# 学习 React 之前应该了解的 JavaScript 特性

> 原文：<https://javascript.plainenglish.io/8-javascript-features-to-know-before-learning-reactjs-aac8b7748b30?source=collection_archive---------0----------------------->

## 在做出反应之前，先学习这些 JavaScript 特性

![](img/8e87af51478dad6e2218c692cde5bc3b.png)

Image created with ❤️️ By author.

React 是目前用于构建前端 web 应用程序的流行 JavaScript 库之一。许多前端开发人员的工作需要将 React 作为一项技能，而不是在前端框架发布之前更流行的 jQuery。

在学习 React 之前，你应该先对 JavaScript 有一个扎实的了解。我说的是所有的 JavaScript 基础和基本原理。除此之外，您还应该了解 ES6+的特性，因为您将在 React 中大量使用它们。

如果你对 JavaScript 及其特性有很好的理解，学习框架对你来说会变得容易得多。

在本文中，我们将发现在学习 React 之前需要了解的一些重要的 JavaScript 特性。所以让我们开始吧。

# 1.让和 Const

ES6 引入了用于声明变量的`let`和`const`来替代`var`。`let`和`const`相比`var`有很多优势。

一个优点是它们有一个*块范围*，这意味着它们在块范围之外是不可访问的。

这里有一个例子:

```
{
    **const** a = 5;
    **let** b = 6;
    var c = 7;
}console.log(a); //Error: a is not defined.
console.log(b); //Error: b is not defined.
console.log(c); // 7
```

如您所见，用`const`和`let`声明变量在花括号之间的范围之外是不可访问的。这就是为什么我们得到一个错误。所以这非常有用，因为有时候用关键字`var`你可以在没有注意到的情况下改变一个变量。

`let`和`const`的另一个优点是，它们不会像关键字`var`一样被吊到文件的顶部。因此，如果您使用`let`和`const`，就不必再关心提升问题。

你可能也想知道 let 和 const 有什么区别。嗯，他们几乎是相似的。只需将`let`用于您稍后要更改的变量，将`const`用于您不想更改的常量变量。

看看下面的例子:

```
**const** x = 5;
x = 6; //Error.**let** y = 1;
y = 2;console.log(x); // 5
console.log(y); // 2
```

如您所见，您不能重新分配用关键字`const`声明的变量。这就是`let`和`const`的巨大区别。

我个人已经不用`var`这个关键词了。我在 React 上用了很多`let`和`const`。

# 2.箭头功能

ES6 中引入了箭头函数，作为编写普通函数的简单方法。箭头语法要短得多，也更容易编写。许多开发人员在他们的 React 代码中使用它。这就是为什么你也应该在 React 上使用它。

让我们看看如何编写箭头函数:

```
// Normal function.
const greeting = function(){
    console.log("hello");
    console.log("world");
}// Arrow function.
const greeting = **() =>** {
    console.log("hello");
    console.log("world");
}
```

如您所见，您不需要在箭头函数中使用 function 关键字。

此外，如果您的 arrow 函数只有一行，并且只有一个参数，您可以编写不带括号、花括号和 return 关键字的 arrow 语法。

这里有一个例子:

```
// Normal function.
const greeting = function(name){
    return "Hello " + name;
}// Arrow function.
const greeting = name **=>** "Hello " + name;
```

现在箭头函数无处不在，在学习 React 的时候你会经常看到它们。

# 3.解构

析构是你需要知道的重要的 ES6 特性之一。它在 React 代码中使用了很多。所以你应该了解一下。

它允许你复制对象或数组的一部分，并把它们放入命名变量中。

看看下面的例子，我们没有使用析构:

```
const user = { name: 'Mehdi', age: 19};//Without destructuring.
const name = user.name; //name = 'Mehdi'
const age = user.age; //age = 19
console.log(name); //Mehdi
console.log(age); //19
```

下面是使用 ES6 析构的同一个示例:

```
const user = { name: 'Mehdi', age: 19};//ES6 destructuring
**const { name , age } = user;** //name = 'Mehdi', age = 19
console.log(name); //Mehdi
console.log(age); //19
```

正如您在上面的例子中看到的，第二个例子看起来更简洁，也更容易编写。在析构的例子中，变量`name`和`age`被创建并被赋予来自用户对象的值。这就是对象解构的力量。

除此之外，您还可以对数组使用析构。变量的赋值依赖于数组中的元素索引，而不是对象键。

这里有一个例子:

```
//array destructuring
**const [a, b, c] = [1, 2, 3, 4];**console.log(a); //1
console.log(b); //2
console.log(c); //3
```

如您所见，变量`a`、`b`和`c`在 numbers 数组中获得了具有相同索引的赋值。这叫做数组析构，在 React 中使用钩子的时候你会经常用到它。

# 4.ES6 模块

ES6 模块`import`和`export`在 React 中无处不在。所以你需要很好的理解这些。它们允许您从一个文件向另一个文件共享、导出和导入代码。这是在 JavaScript 文件之间共享代码的好方法。

在普通的 JavaScript 中，你必须首先告诉浏览器你正在使用模块。您可以通过在 HTML 的 head 标签中放置一个带有`type="module"`的模块脚本来实现。

```
**<script type="module" src="fileName.js"></script>**
```

比方说，您想要将一个函数从一个名为`index.js`的 JavaScript 文件导入到另一个名为`app.js`的文件中。为此，您必须先导出函数，然后再导入它。

这里有一个例子:

*导出:*

```
**export** const multiply = (a, b) => {
  return x * y;
}
```

*导入:*

```
**import** { multiply } from './index.js';
```

就这样，现在你可以使用文件`app.js`中的函数`multiply`了。

关于 ES6 模块的更多信息，您也可以查看我下面的文章:

[](/understand-javascript-modules-import-and-export-syntax-f231c5e2fafd) [## 理解 JavaScript 模块:导入和导出语法

### 通过实际例子理解 JavaScript ES6 模块

javascript.plainenglish.io](/understand-javascript-modules-import-and-export-syntax-f231c5e2fafd) 

# 5.ES6 类

JavaScript 中的类是作为一种语法糖引入的，用于在 JavaScript 中编写构造函数。它们用于创建对象，并允许在 JavaScript 中进行面向对象的编程。

然而，现在有了 React 钩子，你就不会用到很多类了。但是知道它们总是好的，因为它们在 JavaScript 中非常重要。

下面是一个类语法:

```
class Person{
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}//create new object from the class using the new keyword
let myPerson = **new** Person("John", 25); //{ name: 'John', age: 25}
```

所以类只是用 JavaScript 编写面向对象代码的一种新的简单方法。你可以在我下面的文章中了解它们:

[](/javascript-classes-explained-with-examples-c10d0426834b) [## 用例子解释 JavaScript 类

### 通过实例了解 JavaScript 中的类语法。

javascript.plainenglish.io](/javascript-classes-explained-with-examples-c10d0426834b) 

# 6.高阶函数

高阶函数是任何以另一个函数作为自变量的函数。在 JavaScript 中，有很多有用的高阶函数可以使用。“贴图”、“过滤”和“减少”是 React 中经常用到的。所以你需要很好的理解他们。

map 方法允许您遍历每个数组元素，并返回一个包含映射元素的新数组。

这里有一个例子:

```
let numbers = [6, 7 , 8, 3, 2];
numbers.**map**(number => number * 2); //[12, 14, 16, 6, 4]
```

filter 方法允许您遍历每个数组元素，并在新数组中过滤您想要的元素。

这里有一个例子:

```
let numbers = [6, 7 , 8, 3, 2];
numbers.**filter**(number => number < 5); //[3, 2]
```

reduce 方法也用于数组，它将数组元素缩减为单个值。

下面是一个使用 reduce 方法返回数字数组总数的示例:

```
let numbers = [6, 7 , 8, 3, 2];
numbers.**reduce**((accumulator, num) => accumulator + num);
//returns 26
```

如果你感兴趣，也可以看看我下面这篇关于 JavaScript 中 reduce 方法的文章:

[](/the-reduce-method-in-javascript-explained-with-examples-6232b85e47f6) [## 举例说明 JavaScript 中的 Reduce 方法

### 通过示例了解 JavaScript 中的 reduce 方法。

javascript.plainenglish.io](/the-reduce-method-in-javascript-explained-with-examples-6232b85e47f6) 

# 7.扩展运算符

扩展操作符`…`也是我在 React 中经常使用的特性之一。它允许在 JavaScript 中传播可迭代对象的值。

你可以用它来复制对象和数组。也可以组合复制的对象和数组。

下面是我的一篇文章，讲述了使用 spread operator `{…}`可以做的一些事情:

[](/5-useful-things-the-spread-operator-can-do-in-javascript-f0306358bc9c) [## JavaScript 中 Spread 操作符可以做的 5 件有用的事情

### 用 Spread 操作符编写一个更好更干净的 JavaScript 代码

javascript.plainenglish.io](/5-useful-things-the-spread-operator-can-do-in-javascript-f0306358bc9c) 

让我们来看一个在 JavaScript 中使用 spread 运算符的简单示例:

```
//copy and combine two objectslet obj1 = {name: "Mehdi", age: 19};let obj2 = {eyeColor: "Black", hairColor: "Black"};//using the spread operator.
let combination = **{...obj1, ...obj2}**;console.log(combination);
//output: {name: "Mehdi", age: 19, eyeColor: "Black", hairColor: "Black"}
```

下面是数组的另一个示例:

```
//copy and combine two arrayslet arr1 = [1, 2, 3];
let arr2 = [5, 6, 7, 8];let combination = **[...arr1, ...arr2]**;console.log(combination);
//output: [1, 2, 3, 5, 6, 7, 8]
```

正如您在上面的例子中看到的，spread 操作符允许我们轻松地复制和组合数组和对象。所以它非常有用，你应该学习它。

# 8.三元运算符

三元运算符`?` `:`是一种在 JavaScript 中编写条件语句的简单方法。

我注意到，在 React 中，大多数时候我使用三元运算符来有条件地呈现事物。这就是为什么我认为在 React 中使用它之前，您也应该在 JavaScript 中了解它。

看看下面的例子:

```
let isOnline = true;// if else statement.
if(isOnline){
    console.log("He is Online.");
}else{
    console.log("He is Offline.");
}
//He is Online //Same example using the ternary operator[condition] ? [if] : [else]**isOnline ? console.log("He is Online.") : console.log("He is Offline.");** //He is Online
```

正如您所看到的，三元运算符允许我们仅用一行代码轻松编写条件语句。它对小环境非常有用，我更喜欢用它来有条件地渲染 React 中的东西。

如果您想了解 JavaScript 中三元运算符的更多信息，也可以再次查看我下面的文章:

[](/better-javascript-the-ternary-operator-d181338c4c20) [## 更好的 JavaScript——三元运算符

### 理解 JavaScript 中的三元运算符以及如何使用它

javascript.plainenglish.io](/better-javascript-the-ternary-operator-d181338c4c20) 

# 结论

如果你想学习 React 或任何其他 JavaScript 框架，我上面列出的所有这些 JavaScript 特性都非常重要。如果你理解了这些，学习框架就会变得像小菜一碟。除此之外，我还建议在转向 React 之前学习 Async/Await 和 fetch API。

感谢您阅读这篇文章。希望你觉得有用。

**更多阅读**

[](/5-useful-javascript-features-that-nobody-is-talking-about-b630838dedba) [## 没有人谈论的 5 个有用的 JavaScript 特性

### 你应该知道的冷门 JavaScript 特性。

javascript.plainenglish.io](/5-useful-javascript-features-that-nobody-is-talking-about-b630838dedba) 

*更多内容尽在*[***plain English . io***](https://plainenglish.io/)