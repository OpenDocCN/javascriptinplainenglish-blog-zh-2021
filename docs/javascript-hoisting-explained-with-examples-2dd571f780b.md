# JavaScript 提升举例说明

> 原文：<https://javascript.plainenglish.io/javascript-hoisting-explained-with-examples-2dd571f780b?source=collection_archive---------16----------------------->

## JavaScript 中提升的概念比您想象的要简单。

![](img/209888ed9861b7e70462ad29fc16eaf5.png)

Photo by [Jexo](https://unsplash.com/@jexo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

提升是作为开发人员需要理解的基本 JavaScript 概念之一。许多初学者发现很难理解这个概念，即使它很简单。

有时候 JavaScript 很奇怪，提升是 JavaScript 中奇怪的事情之一。这就是为什么如果你想避免代码中的错误和 bug，你需要理解这个概念，特别是如果你正在使用`var`。

所以在这篇文章中，我们将通过例子来学习 JavaScript 提升。让我们开始吧。

# 什么是吊装？

在英语中，提升意味着把某物拉到顶部。但是在 JavaScript 中，这是一种在执行代码之前将变量声明和函数声明移动到其作用域*顶部的行为。*

当您使用关键字`var`声明一个变量或函数时，该声明会在执行之前被提升到代码的顶部。

让我们来看一个简单的例子，让事情变得更简单。我将向你们展示一段代码在提升前后的样子。

*吊装前:*

```
**var firstName = "John";**
console.log(firstName); //John**var lastName = "Doe";**
console.log(lastName); //Doe
```

*吊装后:*

```
**var firstName;
var lastName;**firstName = "John";
console.log(firstName); //JohnlastName = "Doe";
console.log(lastName); //Doe
```

这正是提升在代码执行之前在幕后所做的事情。它将所有变量声明提升到文件的顶部。然后对它们进行初始化，这样它们就可以取值了。

因为变量声明(带有关键字`var`)总是会被放在最前面。我们可以在声明变量之前初始化变量并给它们赋值。

这里有一个例子:

```
x = 20;
console.log(x); //prints 20**var x;**
```

正如你所看到的，上面我们在声明变量之前使用了变量`x`。因此，它仍然在控制台中打印 20。那是因为底部的声明提升后会在顶部。

像这样:

```
**var x;**x = 20;
console.log(x); //prints 20
```

同样的事情也适用于带有关键字`var`的函数声明。

# 让和 const

用关键字`let`或`const`声明的变量和函数不会被提升。所以如果你用的是`let`和`const`，你就不用关心吊装了。

如果我们使用关键字`let`或`const`尝试上面的相同示例，我们将得到一个引用错误。

下面是一个例子:

```
x = 25;
console.log(x); //reference error.**let** x;
```

如你所见，我们得到了一个引用错误，告诉我们不能在声明之前访问变量。那是因为带有关键字`let`的变量没有被提升。

如果你不使用`var`，你不必关心提升。

当使用`let`和`const`时，同样的事情也适用于函数声明。

这里有一个例子:

```
sayHi();**const** sayHi = ()=>{
  console.log("Hi"); //reference error.
}
```

正如你所看到的，我们试图在声明函数之前调用它，这就是为什么我们得到了错误，因为没有提升，因为我们使用了`const`。即使我们在这种情况下使用了`var`，我们仍然会得到一个错误，因为只有声明`var sayHi`会被挂起，而不是函数本身。

# 结论

如您所见，提升只是在执行之前将声明移动到代码顶部的一种行为。如果你没有使用`var`，你不必在意它，但是一定要确保在顶部声明你的变量，这样你就可以避免错误。如果你确实使用了关键字`var`，那么你需要时刻记住提升。

感谢您阅读这篇文章。希望你觉得有用。

**更多阅读:**

[](/7-awesome-css-tools-for-all-web-developers-390ceced6f83) [## 面向所有 Web 开发人员的 7 款出色的 CSS 工具

### 有用的 CSS 工具，让您的生活更轻松，提高您的生产力。

javascript.plainenglish.io](/7-awesome-css-tools-for-all-web-developers-390ceced6f83) [](/6-useful-tips-to-improve-your-websites-accessibility-d47dd446d82) [## 提高网站可访问性的 6 个有用技巧

### 可达性可能比你想象的更重要，尤其是在 2021 年。

javascript.plainenglish.io](/6-useful-tips-to-improve-your-websites-accessibility-d47dd446d82) 

*更多内容请看*[***plain English . io***](http://plainenglish.io)