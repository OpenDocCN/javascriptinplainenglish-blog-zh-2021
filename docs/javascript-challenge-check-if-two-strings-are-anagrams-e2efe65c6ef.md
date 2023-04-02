# JavaScript 挑战:检查两个字符串是否是字谜

> 原文：<https://javascript.plainenglish.io/javascript-challenge-check-if-two-strings-are-anagrams-e2efe65c6ef?source=collection_archive---------7----------------------->

## **检查两个字符串是否是字谜的 JavaScript 挑战**

![](img/f47280107b58bc431a8097fe53ff5539.png)

Photo by [cottonbro](https://www.pexels.com/@cottonbro?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/hands-typing-on-a-laptop-keyboard-5483077/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

在这个挑战中，给你两个单词，你需要检查它们是否有相同的字母单词并且只出现一次。

## **插图**

## **什么是变位词？**

根据维基百科，变位词是通过重新排列不同单词或短语的字母形成的单词或短语，通常使用所有原始字母一次。例如，单词变位词本身可以被重新排列成 nag a ram，单词 binary 可以被重新排列成 brainy，单词 adobe 可以被重新排列成 deny。

因此，在这个挑战中，我们将编写一个算法来检查两个给定的字符串是否是变位词。这意味着两个字符串有相同的字母，并且在单词中只使用一次。

有些变位词: ***(种族，关心)(部分，陷阱)(心脏，地球)(膝盖，敏锐)(猫王，生命)(倾听，沉默)***

让我们跳进来。

为了编写这个程序，在编写程序之前，我们应该考虑一些事情。

*   检查字符串中的空格和双空格
*   检查字符串是小写还是大写

## **挑战**

首先，我们将声明函数。请记住，我们的函数将接受两个都是字符串的参数。

我们必须注意这些字符串，因为它们中的一些可能是大写字母，或者是双空格，或者是单空格。因此，我们需要检查空间，并在有空间的情况下移除它们。之后，我们需要检查字符串是否为大写，并将字符串转换为小写。

检查和删除空格。有两种方法可以用来删除空格。我们可以使用:

***replace()*** -这个方法返回一个新的字符串，其中指定的字符串/正则表达式被替换。

***【replace all()***-这个方法返回一个新的字符串，其中一个模式的所有匹配都被替换掉了。

***Replace()*** 在我们有单个空格的情况下非常有效，在我们想要替换双精度和单个空格的情况下，我们可以利用***Replace all()***string 方法。

它有两个参数(pattern，replacement)- pattern —要替换的子字符串或正则表达式。替换(replacement )-用此替换替换阵列。

对于我们的例子，我们将使用 ***。*replace all()**方法。

现在我们有一个干净的字符串。因为我们的变位词包含字母替换(洗牌)，我们需要洗牌并排序我们的字符串。通过对字符串进行排序，它将确保我们按字母顺序排列它们。

## **重新整理字符串**

现在我们可以使用 split 方法将字符串分成有序的子字符串列表，并将它们返回到一个数组中。

此后，我们可以使用。*sort()【数组方法】按字母顺序对数组进行排序。现在我们有了按字母顺序排序的数组。*

*我们使用。 ***join()*** array 方法将数组中的元素转换成字符串。为了代码的可读性，我们可以将所有的方法链接在一起。*

*现在我们有两个按字母顺序排列的字符串，我们可以使用 if 语句来检查字符串是否相等，就这样。*

*现在我们可以检查这些数字是否是字谜。*

***最终解决方案和测试***

*我们对变位检查器的最终解决方案应该类似于此。*

## ***结论***

*这是学习字符串方法和操作的一个很好的挑战。*

*感谢您阅读这篇文章。此外，如果您发现我的内容有用，并且您不是媒体会员，您可以在此处[获得您的媒体会员资格](https://amjohnphilip.medium.com/membership)(媒体推荐链接)以无限制地访问所有内容并支持我们作为作者。*

## ***更多阅读内容***

*[](/javascript-challenge-find-the-missing-number-in-an-array-67689a10a74e) [## JavaScript 挑战:找到数组中缺少的数字

### 在给定的按 1 排序的自然数数组中查找缺失数字的 JavaScript 挑战

javascript.plainenglish.io](/javascript-challenge-find-the-missing-number-in-an-array-67689a10a74e) [](/3-tips-i-use-to-maximize-move-beyond-tutorials-b1b2f59322c0) [## 我用来最大化和超越教程的 3 个技巧

### 我如何充分利用编程教程？

javascript.plainenglish.io](/3-tips-i-use-to-maximize-move-beyond-tutorials-b1b2f59322c0) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*