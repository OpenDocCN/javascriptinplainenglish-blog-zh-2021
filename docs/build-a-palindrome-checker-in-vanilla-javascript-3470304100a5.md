# 用普通 JavaScript 构建一个回文检查器

> 原文：<https://javascript.plainenglish.io/build-a-palindrome-checker-in-vanilla-javascript-3470304100a5?source=collection_archive---------13----------------------->

![](img/a55bf61a3cfa8a6c402d09c350826f8b.png)

Photo by [Avinash Murugappan](https://unsplash.com/@avinash27?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

构建一个回文检查器是我构建并添加到 GitHub 个人资料中的第一批项目之一，当时我正在寻找作为前端 web 开发人员的第一份工作。起初，这似乎令人生畏，但并不十分困难。在这篇文章中，我将向你展示我是如何做到的。

## 什么是回文？

一个单词、短语或序列向前和向后读起来一样，例如*夫人*或*护士跑*。

## 我们的要求或验收标准(AC)

```
**As a** USER,
**I want** to type a word, phrase or sequence into the input,
**So that** I can see if that word is a palindrome.**As a** USER,
**I want** to see the word, phrase or sequence I type into the input AS I type into the keyboard,
**So that** I can see if that word is a palindrome as I have typed it.
```

## 1.首先，让我们创建我们的项目

我喜欢在我的`desktop`中的一个名为`dev`的文件夹中创建我的项目，所以我将在那里创建它。

1.  打开终端和 cd 到你想创建你的项目的地方。对我来说是`cd desktop/dev`
2.  现在让我们创建我们的文件。希望它看起来像这样:

```
- dev
-- palindromeChecker
--- index.html
--- script.js 
```

## 2.现在我们已经建立了一个初始项目，让我们构建一个基本的 HTML 文件

打开`index.html`文件:

```
<html>
  <head>
    <title>Palindrome Checker</title>
  </head>
  <body> <h1>Enter a word to check if its a palindrome</h1>
    <div>
      <input type='text' id='input-text' onkeyup='' />
      <div id='output-text'></div>
    </div>
  </body>
</html>
```

我们有一个基本的 HTML 文件，它有一个带`id=’input-text’`的 input 元素，我们将使用它来键入一个单词，以检查它是否是一个回文，我们还有一个带`id='output-text'`的 div，它将在屏幕上显示我们输入的单词。

注意`input`元素有一个名为`onkeyup`的属性，目前没有值。在这里，我们将使用我们将创建的函数来检查我们在`script.js`文件中的输入。

## 我为什么选择`onkeyup`？

作为我们的需求/接受标准(AC)的一部分，我们希望能够实时看到我们的输入类型。使用`onkeyup`属性允许我们记录在键盘上按下的键。

## 3.现在让我们创建我们的函数

打开`script.js`文件:

首先，我们需要选择`input`和`output`，这样我们就可以使用和操作显示屏。我们将使用下面的`getElementbyId`来选择它们:

```
const input = document.getElementById('input-text');
const output = document.getElementById('output-text');
```

接下来，无论我们在`output-dispay` div 中得到什么值，我们都需要将它转换成一个字母数组，而不是一个完整的单词。我们将使用`split()`来完成这项工作。这样我们就可以使用`reverse()`将其反转。一旦反转，我们希望使用`join()`将它重新组合在一起。

```
const checkPalindrome = () => {
  output.innerHTML = input.value
    .split('')
    .reverse()
    .join('')
```

上面的代码将把我们的输入反向返回给我们。然而，这个单词不会被识别为回文，因为它还没有考虑空格。例如，*赛车*会正确返回，但*赛车*不会，因为它将作为 *rac ecar* 返回。

为了解决这个问题，我们将使用复杂的正则表达式来去除空白。

我们的**最终解**看起来是这样的:

```
const input = document.getElementById('input-text');
const output = document.getElementById('output-text');const checkPalindrome = () => {
  output.innerHTML = input.value
    .split('')
    .reverse()
    .join('')
    .replace(/[\W_]+/g,'');
}
```

## 4.让我们把它放在一起

回到我们的`index.html`文件，我们需要调用我们刚刚创建的函数。为此，我们需要添加它:

打开`index.html`文件:

```
<html>
  <head>
    <title>Palindrome Checker</title>
  </head>
  <body><h1>Enter a word to check if its a palindrome</h1>
    <div>
      <input type='text' id='input-text' onkeyup='**checkPalindrome()**' />
      <div id='output-text'></div>
    </div>
  </body>
  **<script src='./script.js'></script>**
</html>
```

应该就是这样了。它缺乏风格，但它的作品！

# 结论

感谢阅读。我希望它有帮助。如果是的话，请在评论中告诉我。

## TL；博士；医生

查看我的 [GitHub](https://github.com/mazaherm/palindrome) 配置文件来查看代码。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)