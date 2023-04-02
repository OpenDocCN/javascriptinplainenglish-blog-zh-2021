# 优化代码的 7 个简单 JavaScript 技巧

> 原文：<https://javascript.plainenglish.io/7-simple-javascript-tips-for-optimizing-your-code-ba83d4d7da4e?source=collection_archive---------2----------------------->

## 你可能不知道这些提示

![](img/62fd255f51bbf367acd2e6e36cadb4ac.png)

Photo by [AltumCode](https://unsplash.com/@altumcode?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我知道你关心优化你的代码，但有时你不知道如何去做。

想象一下，你的每一段代码都得到了很好的优化，性能会非常好，如果有任何问题，你可以很容易地调查你的代码。

所以，没有任何进一步的麻烦，让我们直接进入下面的 7 个简单的 JavaScript 技巧。

# 1.动态性能

你认为一个对象的属性名是固定的吗？

我过去一直这样认为，直到我发现它们可以是动态的。

方法如下:

```
let dynamicProperty = ‘author’;let book = {
  title: ‘JavaScript Best Practices’,
  [dynamicProperty]: ‘Amy Andrews’
};console.log(book); // { title:”JavaScript Best Practices”, author:”Amy Andrews” }
```

# 2.舍入技巧

如何将一个数字四舍五入为最接近的整数？

最简单的答案是使用`math.floor()`或`math.round()`，对吗？

但是如何使用`~~`操作符呢？因为这样更短更有效率。

因此，与其说:

```
Math.floor(2021.21);
Math.round(2021.21);
```

您可以使用:

```
~~(2021.21)
```

# 3.使用快捷方式

对于相同的任务，快捷方式比普通方式更快。如果明智地使用它们，你可以节省很多时间。

例如，您可以只使用逻辑运算符来删除整个`if/else`语句。

不要这样做:

```
function checkName(name) {
  if (name) {
    return name;
  } else {
    return ‘Name is null’;
  }
}
```

我们可以这样做:

```
function checkName(name) {
  return name || ‘Name is null’;
}
```

如果您想了解更多关于 JavaScript 快捷方式的信息，请查看下面的文章:

[](https://medium.com/javascript-in-plain-english/15-simple-coding-techniques-to-get-your-tasks-done-with-shorter-code-in-javascript-59d46801db0) [## 15 种简单的编码技术，用更短的 JavaScript 代码完成任务

### 不要浪费时间写长代码，而你可以把它写得更短，更清晰，更易读。

medium.com](https://medium.com/javascript-in-plain-english/15-simple-coding-techniques-to-get-your-tasks-done-with-shorter-code-in-javascript-59d46801db0) 

# 4.使用常见片段

我敢打赌，您曾经反复编写相同的代码来完成特定的任务。这是样板代码，对你的学习没有任何价值。最佳实践是保存这些代码段，在需要时复制并粘贴。

你可以在下面的文章中找到一些常见的片段。

[](https://medium.com/javascript-in-plain-english/18-useful-javascript-snippets-for-common-tasks-you-can-use-from-today-96fa03ce3df6) [## 18 个有用的 JavaScript 代码片段，你可以从现在开始使用

### 生命是短暂的，不要浪费时间一遍又一遍地写同样的代码。

medium.com](https://medium.com/javascript-in-plain-english/18-useful-javascript-snippets-for-common-tasks-you-can-use-from-today-96fa03ce3df6) 

# 5.string.replace()函数的特殊用法

我们都知道`string.replace()`会在一个字符串中搜索一个指定的值，并返回一个新的字符串，其中指定的值被替换。

```
let src = ‘I am a JavaScript developer.’;
let dest = src.replace(‘JavaScript’, ‘React’);
console.log(dest); // I am a React developer.
```

但是，它只会替换第一个找到的值，然后停止。

```
let src = ‘I am a JavaScript developer. I love JavaScript.’;
let dest = src.replace(‘JavaScript’, ‘React’);
console.log(dest); // I am a React developer. I love JavaScript.
```

正如您在上面的例子中看到的，只有第一个`JavaScript`值被替换。那么我们能做什么来替换字符串中出现的所有`JavaScript`值呢？

幸运的是，我们可以传递正则表达式，而不是将指定的值作为`replace()`函数的第一个参数。

让我们修改上面的例子。这一次，我们将传递正则表达式`/JavaScript/g`，而不是普通字符串`‘JavaScript’`。

```
let src = ‘I am a JavaScript developer. I love JavaScript.’;
let dest = src.replace(/JavaScript/g, ‘React’);
console.log(dest); // I am a React developer. I love React.
```

# 6.调整数组大小

我们可以通过直接编辑`length`来调整数组的大小。像这样:

```
let animals = [‘dog’, ‘cat’, ‘rabbit’, ‘snake’];
console.log(animals.length); // 4
console.log(animals); // [‘dog’, ‘cat’, ‘rabbit’, ‘snake’]animals.length = 2;
console.log(animals.length); // 2
console.log(animals); // [‘dog’, ‘cat’]
```

特殊情况下，清空一个数组:

```
animals.length = 0;
console.log(animals.length); // 0
console.log(animals); // []
```

# 7.使用析构交换值

过去，我们通常定义一个临时变量来交换两个变量之间的值。

```
let temp;
temp = x;
x = y;
y = temp;
```

现在，我们不再需要那个临时变量了。为了完成这个任务，我们只需要使用一个有用的 ES6 特性——析构。

```
[x, y] = [y, x];
```

或者甚至多于两个变量:

```
let x = 3, y = 6, z = 9;
console.log(x, y, z); // 3 6 9[x, y, z] = [y, z, x];
console.log(x, y, z); // 6 9 3
```

要了解更多关于使用析构的好处，你可以阅读下面的文章:

[](https://medium.com/better-programming/5-ways-to-make-the-most-of-destructuring-in-javascript-to-write-cleaner-code-d674c00da9c7) [## 充分利用 JavaScript 中析构的 5 种方法来编写更简洁的代码

### 析构是 ES6 最激动人心的特性之一

medium.com](https://medium.com/better-programming/5-ways-to-make-the-most-of-destructuring-in-javascript-to-write-cleaner-code-d674c00da9c7) 

# 最终想法

多产的 JavaScript 开发人员总是试图润色他们的代码。考虑到这一点，以上建议是完成这一任务的最佳方式之一。

你觉得这些建议怎么样？你知道其他有用的提示吗？请在下面的评论中告诉我。

[***和我一起分享更多关于编程的有益见解。***](https://bracketshack.substack.com/)