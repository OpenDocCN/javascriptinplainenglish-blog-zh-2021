# 如何在 JavaScript 中将二进制文件转换成文本文件，反之亦然

> 原文：<https://javascript.plainenglish.io/how-to-convert-from-binary-to-text-in-javascript-and-viceversa-b617d9044436?source=collection_archive---------9----------------------->

![](img/04bf1ae1f30678bcd3bc8bd53cfe0305.png)

Photo by [Ariel](https://unsplash.com/@arielbesagar?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/@arielbesagar?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

我今天有点晚了。昨天圣诞老人狂欢了一场。我不能告诉你他回来的时间！他甚至弄乱了精灵的密码，再也无法破译他们的信息。幸运的是，或者不幸的是，加密代码相当脆弱。弱到一行代码就足以解密。

# 谜题:奇怪的信息📜

![](img/2897befa63d0a5540200401f902f8152.png)

今天的问题，第 9 期[开发降临日历🎅](https://github.com/devadvent/puzzle-9)是一个二进制数的转换问题。什么是二进制数？维基百科很好地解释了这一点:

> 二进制数是以 2 为基数的数字系统或二进制数字系统表示的数，这是一种仅使用两个符号的数学表示方法:通常是“0”(零)和“1”(一)。

# 将数字转换成不同的基数

在二进制数中，数字的范围是从`0`到 `1`，仅此而已。他们只有两个，但他们是一切。从一系列的 0 和 1 开始，我们可以制造电脑，互联网，一切。还要写消息。我们不习惯阅读二进制数，这使事情变得有点复杂。我们必须将不同的序列转换成一个我们能更好处理的数字系统，通常是十进制。

将一个数从一种基数转换成另一种基数是有规则的。JavaScript 提供了 [parseInt()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt) 方法。这个方法有两个参数:

*   表示数字的字符串格式的值
*   表示所用基数的数字

`parseInt()`返回字符串表示的以 10 为基数的数值。

让我们举个例子:

另一方面，如果我想做相反的过程，将十进制数转换成不同基数的数，我可以使用[object . prototype . tostring()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/toString)方法。我发现我总是通过暗示数字是以 10 为基数来使用它将字符串转换成数字。此方法采用数值参数。该参数指示转换基础。实际上，为了编写上面的示例，我使用了以下代码:

这是结果:

# 将数字转换为文本

解决了将数字从一种基数转换到另一种基数的问题之后，问题仍然存在:如何将数字转换成字符？我可以使用 [String.fromCharCode()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/fromCharCode) 。此方法接受 0 到 65535 (0xFFFF)之间的数字序列作为参数，表示 unicode 字符的 UTF-16 编码。

长话短说，`0`和`65535`之间的每个数字代表一个独特的角色。`fromCharCode()`方法允许你将一个数字转换成相应的字符。它的逆方法是[string . prototype . charcodeat()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/charCodeAt)方法:它将一个字符转换成一个数字代码。为了玩，我可以这样写:

# 用二进制解码文本

我有解答这个小测验所需的所有工具。唯一的额外困难是数据的格式:它存储在一个被读取为多行字符串的`message.data`文件中。

我使用 [String.prototype.split()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/split) 创建一个数组。我必须使用正则表达式来表示换行符，因为它在 Windows(我使用的)和 Linux(GitHub 用来验证解决方案的正确性)上是不同的。

我得到了这样一个函数:

或者，我可以用类似的函数得到相同的结果:

仅此而已。

但是在结束之前，我想报告两个有趣的链接。第一篇是几个月前 Mehdi Aoussiad 写的一篇类似的文章。这对我很有帮助。

[](/how-to-convert-from-binary-to-text-in-javascript-3e881c7fd8c7) [## 如何在 JavaScript 中从二进制转换成文本

### 让我们使用 JavaScript 将二进制转换成文本

javascript.plainenglish.io](/how-to-convert-from-binary-to-text-in-javascript-3e881c7fd8c7) 

第二篇文章涉及如何将一个数从十进制转换成二进制:它与问题的解决没有严格的关系，但仍然很有趣。

[](https://masteringjs.io/tutorials/fundamentals/decimal-to-binary) [## 将十进制转换成二进制

### 二进制数是以 2 为基数表示的数，与传统的以 10 为基数的十进制数相反。正在转换…

masteringjs.io](https://masteringjs.io/tutorials/fundamentals/decimal-to-binary) 

最后，本系列中关于 [Dev 降临节日历的上一篇文章🎅](https://github.com/devadvent/readme):

[](/how-to-generate-an-array-of-pairs-from-an-array-in-javascript-edbbb5cdd8da) [## 如何在 JavaScript 中从数组生成数组对

### 经历了过去几天的麻烦，精灵们应该休息一下了。所以他们决定组织一个秘密圣诞老人。在…

javascript.plainenglish.io](/how-to-generate-an-array-of-pairs-from-an-array-in-javascript-edbbb5cdd8da) 

感谢阅读！敬请关注更多内容。

***不要错过我的下一篇文章—报名参加我的*** [***中邮箱列表***](https://medium.com/subscribe/@el3um4s)

[](https://el3um4s.medium.com/membership) [## 通过我的推荐链接加入 Medium—Samuele

### 阅读萨缪尔的每一个故事(以及媒体上成千上万的其他作家)。不是中等会员？在这里加入一块…

el3um4s.medium.com](https://el3um4s.medium.com/membership) 

*原载于 2021 年 12 月 10 日 https://blog.stranianelli.com*[](https://blog.stranianelli.com/how-to-convert-from-binary-to-text-in-javascript/)**。**

**更多内容看* [***说白了就是***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费每周简讯这里***](http://newsletter.plainenglish.io/) ***。****