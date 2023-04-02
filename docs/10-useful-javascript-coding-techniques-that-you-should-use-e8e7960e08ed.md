# 您应该使用的 10 种有用的 JavaScript 编码技术

> 原文：<https://javascript.plainenglish.io/10-useful-javascript-coding-techniques-that-you-should-use-e8e7960e08ed?source=collection_archive---------0----------------------->

## 实现编程任务的有用 JavaScript 技术。

![](img/7524a3e8cf186414f258056aa960af7a.png)

Photo by [Jexo](https://unsplash.com/@jexo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如今 JavaScript 无处不在。作为一个使用 JavaScript 的开发者，我没有理由去学习一门新的编程语言，至少现在没有。我可以只用 JavaScript 做几乎所有的事情(web 开发、移动、桌面等等)。除此之外，我真的很喜欢这门语言，因为它既友好又强大。

JavaScript 生态系统非常庞大。有许多库和框架可以用来节省时间和加速开发。然而，如果你有时间，你最好自己动手，而不是仅仅使用图书馆。

幸运的是，JavaScript 有许多特性和技术，您可以使用它们轻松完成您的编码任务。因此，在本文中，我们将介绍一些开发人员可以使用的简单 JavaScript 编码技术。让我们开始吧。

# **1。获取数组的最后一个元素**

很多时候，当你用 JavaScript 编码时，你将不得不获取数组的最后一个元素。为此，您只需要在访问元素时使用 length 属性。

这里有一个例子:

```
let numbersArr = [4, 8, 9, 34, 100];numbersArr**[numbersArr.length - 1]**; //return 100
```

由于索引从 0 开始，我们可以使用数组长度减 1 作为索引来访问最后一个元素。

# 2.特定范围内的随机数

如你所知，我们使用方法`Math.random()`返回一个介于 0 和 1 之间的随机数。

但有时，你需要得到一个特定范围内的随机数。例如 0 和 100 之间的随机数等等。

看看下面的例子:

```
// Random number between 0 and 4.
**Math.floor(Math.random() * 5);**// Random number between 0 and 49.
**Math.floor(Math.random() * 50);**// Random number between 0 and 309.
**Math.floor(Math.random() * 310);**
```

# 3.扁平化多维数组

您可以使用 ES2017 中发布的方法`flat()`轻松展平多维数组。

方法`flat()`采用一个参数来定义我们想要展平数组的深度(展平的级别)。

这里有一个例子:

```
let arr = [5, [1, 2], [4, 8]];**arr.flat()**; //returns [5, 1, 2, 4, 8]let twoLevelArr = [4, ["John", 7, [5, 9]]]**twoLevelArr.flat(2)**; //returns [4, "John", 7, 5, 9]
```

# 4.检查多种情况

当我们想在一个 IF 语句中检查多个条件时，最好使用数组方法`includes()`来处理。

这里有一个例子:

```
let name = "John";//Bad way.
if(name === "John" || name === "Ben" || name === "Chris"){
  console.log("included")
}//Better way.
if(**["John", "Ben", "Chris"].includes(name)**){
  console.log("included")
}
```

如你所见，如果你想让你的代码更简洁，这种情况下的方法`includes()`只是一种速记。我真的建议这样做。

# 5.提取唯一值

有时，您会遇到必须从数组中删除重复项的情况。

为此，您可以在 JavaScript 中使用带有 spread 操作符的 set 对象。

看看下面的例子:

```
const languages = ['JavaScript', 'Python', 'Python', 'JavaScript', 'HTML', 'Python'];const uniqueLanguages = **[...new Set(languages)]**;
console.log(uniqueLanguages);
//prints: ["JavaScript", "Python", "HTML"]
```

# 6.仅运行一次事件

如果您有一个只想运行一次的事件，可以使用选项`once`作为`addEventListener()`的第三个参数。

下面是一个例子:

```
document.body.addEventListener('click', () => {
    console.log('Run only once');
  }, **{ once: true }**);
```

如您所见，您只需将选项设置为`true`，事件将只运行一次。

# 7.对数组中的所有数字求和

对数组中的所有数字求和最简单的方法是使用 JavaScript 中的 reduce 方法。

这里有一个例子:

```
let numbers = [6, 9 , 90, 120, 55];**numbers.reduce((a, b)=> a + b, 0);** //returns 280
```

如果你有兴趣了解更多，你也可以看看我关于 reduce 方法的文章。

[](/the-reduce-method-in-javascript-explained-with-examples-6232b85e47f6) [## 举例说明 JavaScript 中的 Reduce 方法

### 通过示例了解 JavaScript 中的 reduce 方法。

javascript.plainenglish.io](/the-reduce-method-in-javascript-explained-with-examples-6232b85e47f6) 

# 8.对对象数组中的数字求和

获取一个对象数组中所有数字的和与从普通数组中获取是不同的。

在这种情况下，您仍然可以使用方法`reduce()`，但是您必须在 reduce 回调中返回一个对象。

下面的例子是一个带有 name 和 age 属性的用户对象数组。我们希望所有年龄的总和得到总年龄数:

```
const users  = [
  {name: "John", age: 25},
  {name: "Chris", age: 20},
  {name: "James", age: 31},
  ]

  users.reduce(function(a, b){
    **return {age: a.age + b.age}**
  })**.age**;
//returns 76.
```

如您所见，我们访问返回对象中的年龄。然后我们在 reduce 方法之后再次访问它，因为它返回一个包含总年龄数的对象。

# 9.关键词“在”

例如，在 JavaScript 中使用关键字`in`来检查属性是否定义在一个对象中，或者元素是否包含在一个数组中。

你可以看看下面的代码:

```
const employee = {
  name: "Chris",
  age: 25
}**"name" in employee;** //returns true.
**"age" in employee;**  //returns true.
**"experience" in employee;** //retuens false.
```

# 10.从数字到数字数组

我们可以使用 spread 操作符、map 方法和方法`parseInt()`将一个数字转换成一个*数字数组*。

下面是代码示例:

```
const toArray = num => **[...`${num}`].map(elem=> parseInt(elem))**toArray(1234); //returns [1, 2, 3, 4]
toArray(758999); //returns [7, 5, 8, 9, 9, 9]
```

如你所见，我们将参数`num`分布在一个空数组中，并映射每个元素，使用`parseInt()`将其转换成一个数字。

# 结论

这些是我可以和你分享的一些简单的 JavaScript 编码技术。总有一些情况下你需要用到它们。

感谢您阅读这篇文章。希望你觉得有用。

**更多阅读**

[](/my-favorite-css-properties-as-a-front-end-web-developer-131b64ced5b2) [## 作为前端 Web 开发人员，我最喜欢的 CSS 属性

### 你可能不知道的 7 个有用的 CSS 属性。

javascript.plainenglish.io](/my-favorite-css-properties-as-a-front-end-web-developer-131b64ced5b2) [](/10-awesome-front-end-development-tools-to-boost-your-productivity-b1d2efc4c4ba) [## 10 个令人敬畏的前端开发工具来提高您的生产力

### 你可能需要用到的有用的前端开发工具。

javascript.plainenglish.io](/10-awesome-front-end-development-tools-to-boost-your-productivity-b1d2efc4c4ba) 

*更多内容请看*[***plain English . io***](http://plainenglish.io)