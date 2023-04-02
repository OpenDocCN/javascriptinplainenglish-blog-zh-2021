# 磨砂编码:字谜回文(JS)

> 原文：<https://javascript.plainenglish.io/coding-for-scrubs-anagram-palindrome-js-34f95ebcd551?source=collection_archive---------6----------------------->

![](img/191baf13edb0736888d3658b10d01b46.png)

欢迎回到本系列的**第 2 部分**，**磨砂编码**！如前所述，我是擦洗，这个系列是为了帮助我成为一个更好的程序员。如果这篇文章对你有帮助，请不要忘记分享、鼓掌和跟随！:')

今天，我们将讨论 JavaScript 中的字谜回文。这个特殊的问题是在最近的一次技术采访中给我的。

让我们开始吧！

# 1.什么是字谜回文？

首先，字谜是通过重新排列另一个字谜的字母而形成的单词、短语或名字，如*听*，由*沉默*形成。第二，回文是向前和向后相同时形成的单词、短语或名字。如果您还没有，请查看我们之前的文章“为磨砂编码:回文”

[](https://aysikh.medium.com/coding-for-scrubs-palindromes-js-7eb0830a0f4a) [## 磨砂编码:回文(JS)

### 欢迎来到我的系列节目《为磨砂编码》我对编码世界是陌生的，所以为了帮助自己变得更好…

aysikh.medium.com](https://aysikh.medium.com/coding-for-scrubs-palindromes-js-7eb0830a0f4a) 

现在，如果我们把这两个定义放在一起，我们将观察一个混乱的单词或短语是否可以变成回文。示例:*yaak*可以重新排列并创建为单词 *kayak。*

# 2.伪代码

既然我们知道了字谜回文是什么。我们必须考虑解决这个问题的最好方法。让我们继续并回顾我们的回文问题。

我们知道，在回文中，除了一个字母之外，每个字母都必须有一对。请记住，如果字符串的长度是偶数，那么所有的字母都必须有一对，但是如果长度是奇数，那么一个字母不需要一对。我们在常规回文函数中做的是比较字符串中的第一个字母和最后一个字母。但是因为我们有一个词被打乱了，解决这个问题的最好方法是什么？

我们需要一个新的数组，它可以让我们从传入的字符串中插入每个字母。在我们建立了这个新的数组之后，我们将创建一个循环来循环传递的单词。此数组将删除重复的字母，表示该字母有其对。这个数组几乎可以容纳数组中没有一对的所有字母。这就是我们的条件语句发挥作用的地方。如果我们创建的新数组已经包含该字母，我们将把它从数组中移除。在完成对单词的解析后，我们将检查数组的长度，如果数组大于 2，则返回 false。

让我们一步一步来写吧！

```
**1.** Create a new empty array to hold the letters without their pair
**2.** Create a for loop to iterate through the word we're passing in
**3.** Create a variable to keep track of each letter in the string
**4\.** Create our conditional statement to check to see if the new array holds any letters from our string and if it does we are going to remove it. Else we are going to push that letter into the new array
**5.** After iterating through the string, we want to check the length of our empty array. If the length of the new array is < 2, return true, else return false
```

# 3.创建函数

让我们继续并遵循我们的伪代码！

```
function isAnagramPalindrome(string) {
   let array = []                    **// create an empty array**
   for(let i = 0; i < string.length; i++){    **// for loop to iterate**
      let letter = string[i]         **// to keep track of each letter**
   }
}
```

到目前为止，我们已经创建了空数组。我们也可以称之为 singleLettersArray 或 oddArray。无论哪一个清楚地表明这是一个数组，它将保存我们没有一对的字母。

接下来，我们创建了我们的`for loop`，设置`*i*` 从索引 0 开始迭代，直到到达字符串的末尾。使用我们的变量`i`，我们将使用它来跟踪字符串中的每个字母。

```
function isAnagramPalindrome(string) {
   let array = []
   for(let i = 0; i < string.length; i++){
      let letter = string[i]
      if(array.includes(letter){          **// if array has the letter**
         array.splice(array.indexOf(letter), 1)         **// remove it**
      }
      else {
         array.push(letter)              **// else put letter in array**
      }
    }
}
```

继续我们的条件语句。
如果数组包含字符串中的字母。

```
if(array.includes(letter)
```

然后我们将使用`.splice()`，它通过移除或替换现有元素和/或在适当的位置添加新元素来改变数组的内容。

[](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice) [## Array.prototype.splice()

### 该方法通过移除或替换现有元素和/或在…中添加新元素来更改数组的内容

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice) 

然后我们要找到这个字母在数组中的位置，并删除它。所以，我们需要使用`.indexOf()`来找到这封信。

[](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf) [## Array.prototype.indexOf()

### indexOf()方法返回在数组中可以找到给定元素的第一个索引，如果没有找到，则返回-1

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf) 

```
array.splice(array.indexOf(letter), 1)
```

但是如果这个字母不在数组中，我们会把它添加到数组中。

```
else { 
  array.push(letter) 
}
```

太棒了。希望到目前为止一切都有意义。现在，我们到了最后一步！

```
function isAnagramPalindrome(string) {
   let array = []
   for(let i = 0; i < string.length; i++){
      let letter = string[i]
      if(array.includes(letter){
         array.splice(array.indexOf(letter), 1)
      }
      else {
         array.push(letter)
      }
    }
    if(array.length < 2) {
       return true
    }
    else {
       return false
    }
}
```

现在我们检查数组的长度是否小于 2。请记住，只有一个字母允许没有一对。我们也可以把这个变成三元语句。

```
array.length < 2 ? true : false 
```

# 结论

我们做到了！

```
function isAnagramPalindrome(string) {
   let array = []
   for(let i = 0; i < string.length; i++){
      let letter = string[i]
      if(array.includes(letter){
         array.splice(array.indexOf(letter), 1)
      }
      else {
         array.push(letter)
      }
    }
    array.length < 2 ? true : false
}
```

看看我们！我们太聪明了。感谢阅读，下期再见！

![](img/e3e0349d2af03f56937f62be37ba8746.png)