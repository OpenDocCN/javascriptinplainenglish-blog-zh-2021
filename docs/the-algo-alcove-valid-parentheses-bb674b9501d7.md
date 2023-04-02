# “有效括号”LeetCode 算法问题:Algo Alcove

> 原文：<https://javascript.plainenglish.io/the-algo-alcove-valid-parentheses-bb674b9501d7?source=collection_archive---------14----------------------->

![](img/235b0509916baf596f4a58bd325d70ab.png)

Photo by [Glenn Carstens-Peters](https://unsplash.com/@glenncarstenspeters?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

也许你可能遇到的最简单但最重要的算法问题之一是“有效括号”问题。它使用了一种常见的问题解决技术，称为“频率计数”以及一种经典的数据结构:堆栈。

# 这个问题

> 给定一个仅包含字符`'('`、`')'`、`'{'`、`'['`和`']'`的字符串`s`，确定输入的字符串是否有效。
> 
> 在以下情况下，输入字符串有效:
> 
> 左括号必须用相同类型的括号括起来。
> 
> 左括号必须以正确的顺序结束。

这是一个简单的林挺问题，可以帮助您确定一个字符串是否正确地结束了所有的括号和方括号(没有什么比搜索代码试图找到多余的花括号在哪里更糟糕的了)。

# 思维过程

一个人的第一想法可能是:*我必须计算所有的开括号，并确保有同样多的闭括号与之匹配。*

这种想法基本上是正确的，但是我们还需要一种方法来确定每个右括号是在左括号之后的。我们不想要这样的字符串:`')))((('`。

因此，我们需要一种方法来跟踪最后一个开括号**是什么，以及在它之前所有其他开括号的顺序。这听起来像是一个**堆栈。****

堆栈遵循 LIFO 排队顺序(后进先出),这意味着我们总是将最后一个左括号放在堆栈的顶部，当我们找到它的匹配时，可以弹出它。

我们还需要一个**哈希映射**来轻松检查右括号和匹配的左括号(不要让字符串看起来像`'[){]'`)。

# 伪代码

*   创建一个**散列映射**，它将“闭括号”作为键，将它们匹配的“开括号”作为值。
*   创建一个**堆栈**。
*   在字符串中循环。
*   如果角色是**开**，将其加入堆栈。
*   如果字符是**闭合的，**弹出堆栈，检查闭合字符是否与堆栈中的开放字符匹配(使用哈希映射)。
*   如果它们不匹配，则返回 false。
*   如果循环结束并且没有错误发生，则返回 true。

**解决方案**

第一部分很简单:声明你的地图和栈。

```
const validParentheses = (s) => {
    let map = {
        ')': '(',
        ']': '[',
        '}': '{'
    };
    let stack = []; 
```

然后，遍历字符串，将每个开放结构添加到堆栈中。

```
for (let char of s) {
    if (char === '(' || char === '[' || char === '{') {
        stack.push(char);
    }
```

如果这个结构是封闭的，就在栈顶检查它。

```
if (char === ')' || char === ']' || char === '}') {
    let candidate = stack.pop();
    if (map[char] !== candidate) {
        return false;
    };
```

然后，我们只要在循环结束时返回 true，我们就完成了。下面是完整的代码:

```
const validParentheses = (s) => {
    let map = {
        ')': '(',
        ']': '[',
        '}': '{'
    };
    let stack = []; for (let char of s) {
        if (char === '(' || char === '[' || char === '{') {
            stack.push(char);
        } if (char === ')' || char === ']' || char === '}') {
            let candidate = stack.pop();
            if (map[char] !== candidate) {
                return false;
            };
        };
    };
return true;
};
```

就是这样。这个问题很简单，但它显示了对大量算法基础的扎实理解。习惯于了解不同的问题解决技术，以及如何利用不同的数据结构，对于回答如此多的问题至关重要。

感谢阅读！请在下面留下您可能希望我在未来的博客中涉及的其他算法的任何评论。

编码快乐！

*更多内容看*[***plain English . io***](http://plainenglish.io/)