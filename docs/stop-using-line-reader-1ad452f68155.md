# 为什么你应该停止使用行阅读器

> 原文：<https://javascript.plainenglish.io/stop-using-line-reader-1ad452f68155?source=collection_archive---------11----------------------->

## 如何仅使用核心 Node.js 功能异步地逐行读取文件。

![](img/dc666518df28df79bc94034f3f3dbe90.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

今天，我浪费了几个小时的时间试图用 Node.js 读取另一个文件的内容。

## 背景

在 TripActions，我们使用[本地化](https://lokalise.com/)来翻译(也就是本地化)我们的应用。如果您以前从未本地化过应用程序，那么主要的工作是用变量替换所有静态文本，将文本放在基于键值对的文件中。我们在后端使用 Java，所以我们使用`.properties`文件。

一旦你的应用程序超过 300 个键值对，这个文件就会变得越来越难以管理，这就为复制或丢失键打开了方便之门。这带来了一个问题，尤其是当你管理多种不同的语言，每种语言都有自己的`.properties`文件，并且你继续构建应用程序，添加更多的键并更新现有的键。

最近，我一直在开发工具来使这个过程变得更容易，自动完成寻找重复或丢失钥匙的过程。

## 问题

我们最近遇到的一个问题是该工具在检测未使用的键时过于热心，导致它们被删除。调查表明，这是因为这些键是动态生成的，在运行时将一个字符串键与一个变量连接起来。这意味着现有的工具无法将这些动态变量与密钥文件相匹配。

## 过程

借用我在 ES-lint 中看到的语法，我决定在动态变量之前添加一个注释，表示预期的键。

The note before the dynamic variable shows all expected string values for web.email.TRAVEL_RESTRICTIONS_NOTIFICATIONS_EMAIL.common.notifications

下一个挑战更加困难——遍历文件，检查每个文件的注释，然后返回变量。

第一步是拿到文件。我使用了与 [Glob](https://www.npmjs.com/package/glob) 配对的`fs.readFile`，允许我创建通配符路径，获取 foundation src 目录(我的电子邮件模板存储在那里)中的所有 HTML 文件。

我的`getDynamicKeys`函数被设置为构建并返回一个数组，这就是我使用 reduce 的原因(我喜欢 Reduce)。累加器开始是一个空数组。对于每个文件，我们等待累加器解析并检查文件是否包含(`includes`)我们的`@deduper-dynamic-variable`字符串。

从文件中取出字符串是我觉得最麻烦的部分。我试了试，但一点也没用。我尝试的另一种方法是使用 substring 和`indexOf`来获取注释的开始和结束，然后返回它。它确实感觉超级笨重，而且对于一个文件中有许多注释的情况来说，伸缩性不好。

在这一点上，我决定稍微旋转一下，一行一行地遍历这些文件。我知道使用 Node 的`readFileSync`方法和使用`file.split(/\r?\n/)`分割文件对于大文件来说是非常占用内存的，所以我需要一个替代方法。

进入[行阅读器](https://www.npmjs.com/package/line-reader)。这个包允许你一行一行的循环代码。它的问题是，尽管获得了约 31，000 的周下载量，但自 2016 年以来(撰写本文时的 5 年)一直没有更新。它本身不支持承诺，严重依赖回调(你可以连接[蓝鸟](https://github.com/petkaantonov/bluebird)，但这是自节点 10 中承诺的[优化以来的另一个过时且大部分多余的项目)。](https://github.com/petkaantonov/bluebird#note)

我试着按照说明编写自己的承诺实现[，但是承诺没有解决，并且不能触发——这是一个已知的问题](https://github.com/nickewing/line-reader#promises)。

幸运的是，我在 Node.js 的帖子中看到了 [Atta](https://medium.com/u/833553eed52?source=post_page-----1ad452f68155--------------------------------) 的[如何逐行读取文件。](https://attacomsian.com/blog/reading-a-file-line-by-line-in-nodejs)

## 读取线 FTW

Readline 是 Node.js 中的一个原生模块，专门用于处理像我们这样的问题。我们将文件通过管道传输到读取流中，然后监听事件。

对于每个行事件，我们检查该行是否包含`@deduper-dynamic-variable`字符串。如果是，我们开始记录并将一个空数组推到`deduperStrings`数组的末尾。然后我们捕获下一行，直到这一行包含结束注释`-->`。我们对整个文件都这样做，在关闭时，我们用`deduperStrings`数组解析承诺。

这只是一个概念证明，并不是完全可靠的——例如，可能会有缺少结束注释的问题。

## 将这一切结合在一起

将`getDynamicKeysStrings`插入我们现有的代码简单易懂，主要使用核心 Node.js 模块(除了 glob)，并且易于编写测试。

这表明您不需要使用行阅读器包。Readline 提供了相同的功能，也是一个核心节点模块，可以很容易地用承诺包装。对我来说，这是显而易见的。

感谢您花时间阅读本文。

***大卫***

***高级前端开发者@***[***trip actions***](https://tripactions.com/)***(通常是*** [***招聘***](https://grnh.se/cbeb241d1) ***！)***

*更多内容请看*[*plain English . io*](http://plainenglish.io/)