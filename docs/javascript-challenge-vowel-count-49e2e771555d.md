# JavaScript 挑战:元音计数

> 原文：<https://javascript.plainenglish.io/javascript-challenge-vowel-count-49e2e771555d?source=collection_archive---------6----------------------->

## 使用 JavaScript 解决一个简单的编码难题。

![](img/b7acb0a7af1270e618db706967c76fd4.png)

Photo by [Anthony Riera](https://unsplash.com/@frenchriera?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

提高你解决问题技能的最好方法之一就是尝试解决编码挑战和算法。解决问题是所有开发人员的必备技能。这是毫无疑问的。

今天我浏览了一下 CodeWars，试图用 JavaScript 解决一些编码难题。老实说，我解决了一些简单的问题，我决定选择一个，和你一起解决。

在本文中，我们将使用 JavaScript 来解决一个简单的编码挑战，即计算字符串中的元音字母。所以让我们开始吧。

# 说明

我们有一个名为`getVowelCount()`的函数，它接受一个字符串作为它的参数。我们的工作是迭代字符串，并检查一个字符串包含的元音(a-e-o-u-i)的数量。

例如，字符串`"Hello"`包含两个元音`e`和`o`。

看看下面的例子:

```
**function getVowelCount**(str) {
  //Your code here.
}getVowelCount("Hello"); //Should return 2.
getVowelCount("Mehdi"); //Should return 2.
getVowelCount("HELLOOO"); //Sould return 4.
```

如您所见，挑战非常简单。我们只需要返回传递给函数的字符串中元音的数量。

# 解决挑战

我解决这个挑战的方法是首先创建一个设置为 0 的变量，我们将在这个变量中存储我们在字符串中找到的元音数。每当我们在字符串中找到一个元音时，我们会给变量加 1。

我们将使用 for 循环遍历字符串中的每个字母，并检查元音字母。

让我们首先创建变量，并将我们的字符串设置为小写，这样我们在检查元音字母时就不用考虑字母大小写了。我们还将创建一个包含五个元音的数组。

下面是一个例子:

```
function getVowelCount(str) {
  **var vowelsCounter = 0;
  str = str.toLowerCase();
  var vowels = ["a","e","i","o","u"];**
}
```

现在让我们创建 for 循环来迭代字符串字母，并使用元音数组中的方法`includes`检查字符串`str`中是否有元音。如果是这样的话，每当我们在字符串上迭代时发现一个元音，我们就给变量`vowelsCounter`加 1。

这里举个例子:

```
for (**let i of str**) {
    if (**vowels.includes(i)**) **vowelsCount++**;
  }
```

现在我们只需要返回函数中的变量`vowelsCounter`。

这是我们的完整解决方案:

```
function getVowelCount(str) {
  **var vowelsCounter = 0;
  str = str.toLowerCase();
  let vowels = ["a","e","i","o","u"];** for (**let i of str**) {
    if (**vowels.includes(i)**) **vowelsCounter++**;
  }
  return **vowelsCounter;**}getVowelCount("Awesome"); //returns 4.
getVowelCount("John"); //returns 1.
```

就是这样，这就是我们解决挑战的方法。现在，每当您将一个字符串传递给函数时，它将返回该字符串中可用的元音数。

# 结论

如您所见，如果您想提高 JavaScript 解决问题的技能，这是一个简单的编码挑战。这是我解决这个问题的方法。如果你有更好的解决方法，请告诉我。

感谢您阅读这篇文章。希望你觉得有用。

**更多阅读**

*如果你对 JavaScript 和网络开发相关的更有用的内容感兴趣，你可以* [*订阅*](https://mehdiouss.ck.page/) *我的时事通讯。*

*您也可以喜欢:*

[](/6-best-places-to-find-remote-developer-jobs-e1d4f58e4756) [## 寻找远程开发人员工作的 6 个最佳地点

### 在这里您可以找到最新的远程开发人员工作。

javascript.plainenglish.io](/6-best-places-to-find-remote-developer-jobs-e1d4f58e4756) 

*多内容于* [*中*](http://plainenglish.io/)