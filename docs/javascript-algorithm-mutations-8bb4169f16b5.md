# JavaScript 算法:突变

> 原文：<https://javascript.plainenglish.io/javascript-algorithm-mutations-8bb4169f16b5?source=collection_archive---------14----------------------->

## 让我们使用 JavaScript 来检查突变

![](img/95e4a0d7525d3f8b0becd403aeb2dd3e.png)

Photo by [Fotis Fotopoulos](https://unsplash.com/@ffstop?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 介绍

作为一名 JavaScript 开发人员，您需要掌握一些解决问题的技能，以便找到编码问题的解决方案。实现这一目标的最佳方式是解决算法和编码挑战。

在本文中，我们将尝试解决一个简单的算法，检查两个单词之间的突变。让我们开始吧。

# 说明

您有一个名为`mutation`的函数，它接受一个数组作为它的参数。数组本身包含两个单词作为字符串:`["word1", "word2"]`。你需要检查这两个词之间的变异。

如果数组中的第一个单词包含了第二个单词中的所有字母，你将返回`true`。如果不是，函数应该返回`false`。

看看下面的例子:

```
function **mutation**(arr) {
 // Your code here.}mutation(["Brad", "rabd"]) should return **true.** mutation(["hello", "abc"]) should return **false.** mutation(["Noela", "Olea"]) should return **true**.
mutation(["ate", "date"]) should return **false**.
```

正如你所看到的，如果第二个单词的所有字母在第一个单词中都可用，你必须返回`true`,并注意字母的大小写。否则就要返回`false`。

# 求解算法

有许多方法可以解决算法或编码挑战。我解决这个问题的方法是首先将数组中的两个单词转换成两个字母数组。为了避免字母大小写的差异，我将把所有内容都转换成小写。

这里有一个例子:

```
function mutation(arr) {
 const firstWord = **arr[0].toLowerCase().split("")**;
 const secondWord = **arr[1].toLowerCase().split("")**; console.log(firstWord); // ['h', 'e', 'l', 'l', 'o']
 console.log(secondWord); // ['a', 'b', 'c']}
mutation(["hello", "abc"]);
```

如您所见，我们将这两个单词转换成了两个字母数组。现在我们需要检查数组第二个字`secondWord`的所有字母是否在数组第一个字`firstWord`中可用。

为此，我们需要使用方法`every()`和`includes()`来检查可用性。如果你不熟悉方法`every()`，你可以查看我下面的文章:

[](/the-methods-some-and-every-in-javascript-8b303a36eaae) [## JavaScript 中的一些和所有方法

### 了解一些高阶函数。

javascript.plainenglish.io](/the-methods-some-and-every-in-javascript-8b303a36eaae) 

方法`every`根据一个数组中的所有元素是否通过某个测试返回`true`或`false`。

我们将使用`every()`来检查数组`secondWord`中的所有字母是否在数组`firstWord`中可用。

下面是代码示例:

```
let check = secondWord.**every**(letter => {
 **return** firstWord.**includes**(letter);
});/* It returns **true** if all the letters of secondWord are available in firstWord. Otherwise, it will return **false.** */
```

现在我们只需要在函数中返回变量`check`。因此，它将根据我们在函数参数`arr`中传递的两个单词返回 true 或 false。

这是我们算法的完整解决方案:

```
function mutation(**arr**) {
// Convert the two words into two arrays of letters.
  **const firstWord = arr[0].toLowerCase().split("");
  const secondWord = arr[1].toLowerCase().split("");**

/* Use the method every to check if all the letters of the   secondWord array are available in the firstWord array */
  **let check = secondWord.every(letter => {
    return firstWord.includes(letter);
  });**

/* return the check variable and it will return true or false depending on the two words that you pass to the function parameter arr */
  **return check;**
}mutation(["Aliennn", "line"]); //return true.
mutation(["Moojoo", "no"]); //returns false.
```

这就是这个算法，现在函数根据我们传递给函数参数`arr`的两个字符串(单词)返回 true 或 false。

# 结论

如你所见，这是我用 JavaScript 解决这个算法的方法。算法是提高你解决问题能力的好方法。这就是为什么你需要尽可能多地尝试它们。

感谢您阅读这篇文章。希望你觉得有用。

*你可能也喜欢:*

[](/10-awesome-front-end-project-ideas-for-code-newbies-b0ba03dc0bd) [## 给代码新手的 10 个很棒的前端项目想法

### 有用的前端 web 开发项目，提高您的编码技能。

javascript.plainenglish.io](/10-awesome-front-end-project-ideas-for-code-newbies-b0ba03dc0bd) [](/javascript-algorithm-sum-all-the-numbers-in-a-range-7b0d5fe43064) [## JavaScript 算法:对一个范围内的所有数字求和

### 让我们使用 JavaScript 来获得一个范围内所有数字的总和。

javascript.plainenglish.io](/javascript-algorithm-sum-all-the-numbers-in-a-range-7b0d5fe43064)