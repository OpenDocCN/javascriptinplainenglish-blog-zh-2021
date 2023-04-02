# ES2021 中引入的 5 项 JavaScript 功能

> 原文：<https://javascript.plainenglish.io/5-javascript-features-that-are-introduced-in-es2021-58179a702451?source=collection_archive---------0----------------------->

![](img/0896b3f6a65f253d4e3aa9a6ae3d363c.png)

自从 EcmaScript 规范改为每年更新后，我们越来越喜欢每年更新的 JavaScript 新特性。我们在 2021 年看到的更新并不逊色，逻辑赋值操作符、Promise.any 和数字分隔符是亮点。

在本帖中，我们将看看一些新特性，并讨论它们如何帮助您编写更好、更易维护的 JavaScript。

# 1.字符串.原型. replaceAll

![](img/003383823f3c88b5f6379d154e582b05.png)

Photo by [Miguel Tomás](https://unsplash.com/@miguelavtomas?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/replace?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

我想介绍的第一个新特性是`String.prototype.replaceAll()`,它用另一个字符串值替换所有出现的字符串。

在 replaceAll()之前。replace()默认情况下，该方法只替换模式的第一个实例，多次替换需要使用正则表达式。现在，当我们使用 replaceAll()时，我们将看到所有出现的内容都被替换。

```
const catPhrase = 'A cat sat on the cat mat';
const dogPhrase = catPhrase.replaceAll('cat', 'dog');
console.log(dogPhrase); // A **dog** sat on the **dog** mat
```

# 2.承诺。任何

![](img/59106923fc280c25a96a65355d24fc39.png)

Photo by [Womanizer WOW Tech](https://unsplash.com/@womanizer?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/promise?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

`Promise.any`方法接受一组承诺，一旦第一个承诺得到满足，它就会返回。

这非常类似于`Promise.race`方法，然而，它有一个关键的区别。虽然`Promise.race`会在任何一个承诺达成时返回，但`Promise.any`只会在其中一个承诺实现时返回。

已结算和已履行之间的区别在于，对于要履行的承诺，它不应该出错，但是对于要结算的承诺，它只需要返回，而不管响应是成功还是错误。

使用`Promise.any`就像传递给它一个承诺数组一样简单，你希望等待一个承诺来解决，就像这里看到的。

```
const promise = (delay) => new Promise((resolve) => {
    setTimeout(() => resolve(`${delay} milliseconds`), delay);
});const promises = [promise(50), promise(40), promise(30)];
const resolved = await Promise.any(promises);console.log(resolved); // 30 milliseconds
```

在本例中，第三个承诺将首先解决，因为它只有 30 毫秒的超时。

# 3.逻辑赋值运算符

![](img/d545103d2ee18cee4b574a4daf716421.png)

Photo by [Ryan Quintal](https://unsplash.com/@ryanquintal?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/lego?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

逻辑赋值运算符提供了逻辑运算符和赋值表达式的组合。ES2021 引入了其中两种新运算符:

*   或或等于
*   和等于

## 或或等于

Or 或 Equals 为我们提供了一个很好的简写，如果初始值为空，我们可以提供一个替代值。解释这是如何工作的最简单的方法是提供几个例子。

在下面的第一个例子中，由于`a`是真的，`a`仍然等于“hello”。

```
let a = “hello”;a ||= 10;console.log(a); // hello
```

在下面的第二个例子中，当`b`为 falsey 时，该值被设置为“world”。

```
let b = “”;
b ||= “world”;
console.log(b); // world
```

## 和等于

And 和 Equals 为我们提供了一个很好的简写方法，如果定义了一个先前的值，就可以覆盖它。解释这是如何工作的最简单的方法是提供几个例子。

在下面的第一个例子中，由于`a`为真，因此`a`被设置为“hello”。

```
let a = true;
a &&= “hello”;
console.log(a); hello
```

在下面的第二个例子中，由于`b`为 false，`b`仍然等于 false。

```
let b = false;
b &&= “world”;
console.log(b); false
```

# 4.数字分隔符

![](img/0f264151a6f6338b535cc042438fa3d9.png)

Photo by [Volkan Olmez](https://unsplash.com/@volkanolmez?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/numbers?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

数字分隔符引入了数字文字的分隔符，目的是使它们更容易阅读。在 ES2021 之前，我们会将百万值写为:

```
const billion = 1000000000
```

这样做的问题是很容易增加一个额外的零或者漏掉一个。对于数字分隔符，我们可以通过引入下划线来使数字更容易阅读。

```
const billion = 1_000_000_000
```

# 5.私有方法和字段

![](img/cf146d22425827589abc94e264a9fc45.png)

Photo by [Dayne Topkin](https://unsplash.com/@dtopkin1?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/private?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

当 ES2015 将类引入 JavaScript 时，当我得知它们缺乏库作者定义私有方法的能力时，我很失望。作为一个 JavaScript 库的作者，我喜欢这样的想法:通过使用类，我将能够保持我的内部方法，内部的。

ES2021 通过引入私有方法和私有字段最终修复了这一遗漏。要表明一个方法或字段是私有的，你只需要在名称前使用一个散列(#)。下面的例子摘自 [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/Private_class_fields) 。

```
class ClassWithPrivateField {
  #privateField
}

class ClassWithPrivateMethod {
  #privateMethod() {
    return 'hello world'
  }
}

class ClassWithPrivateStaticField {
  static #PRIVATE_STATIC_FIELD
}
```

# 包扎

我今天介绍的功能是你每天最有可能使用的。

自 ES6 以来，我们看到的 JavaScript 的改进是惊人的，我喜欢看到所有这些新特性进入我们的浏览器。对于热爱 JavaScript 的人来说，这确实非常令人兴奋。

# 类似文章

[](https://medium.com/javascript-in-plain-english/5-javascript-features-that-you-might-not-know-about-but-will-improve-your-code-80f93d704b62) [## 5 个鲜为人知的 JavaScript 特性将改善您的代码

### 让我们来看看 5 个您以前可能没有使用过的 JavaScript 特性，它们将帮助您改进代码

medium.com](https://medium.com/javascript-in-plain-english/5-javascript-features-that-you-might-not-know-about-but-will-improve-your-code-80f93d704b62) [](https://medium.com/javascript-in-plain-english/5-tech-talks-that-impacted-how-i-approach-software-engineering-dc7ace4af94d) [## 影响我从事软件工程的 5 个技术讲座

### 让我们看一些最好的技术演讲，让听众思考接触软件的不同方法…

medium.com](https://medium.com/javascript-in-plain-english/5-tech-talks-that-impacted-how-i-approach-software-engineering-dc7ace4af94d) [](https://medium.com/javascript-in-plain-english/13-things-you-can-do-with-javascript-arrays-5b6cb4c16c47) [## 使用 JavaScript 数组可以做的 13 件事

### 你可以用数组做的所有不同的事情，每个都有例子

medium.com](https://medium.com/javascript-in-plain-english/13-things-you-can-do-with-javascript-arrays-5b6cb4c16c47) [](https://medium.com/swlh/getting-the-most-out-of-visual-studio-code-829463d7023d) [## 充分利用 Visual Studio 代码

### 无论您是 Visual Studio 代码的新手还是有经验的用户，我都会分享一些我学到的东西来帮助您制作…

medium.com](https://medium.com/swlh/getting-the-most-out-of-visual-studio-code-829463d7023d)