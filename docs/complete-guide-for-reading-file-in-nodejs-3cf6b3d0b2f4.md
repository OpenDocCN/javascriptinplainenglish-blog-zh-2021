# Node.js 中读取文件的完整指南

> 原文：<https://javascript.plainenglish.io/complete-guide-for-reading-file-in-nodejs-3cf6b3d0b2f4?source=collection_archive---------3----------------------->

## 探索在 Node.js 中读取文件的方法。

![](img/1af70e9d9047bd4d75cedd8571fc4cb3.png)

Photo by [Drew Coffman](https://unsplash.com/@drewcoffman?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在本帖中，我们将了解

*   在 Node.js 中读取文件的三种方法
*   哪一个是我最喜欢的方法？
*   为什么我会选择它作为我最喜欢的方式？

事不宜迟，我们开始吧。

# Node.js 中读取文件的三种方法

从标题中，我们清楚地知道在 Node 中有 3 种读取文件的方法。它们被称为**承诺**方式、**回调**方式和**同步**方式。

让我们来看看承诺的方式。

## 用答应的方式读文件

**Promise** 方式使我们能够使用现代的异步 Javascript 特性——**async**和**wait**。请参考下面的示例代码。

运行上面的代码会得到这样的输出。

```
Start reading file
Running other operation
content <Buffer ef bb bf 22 6c 6f 73 74 22 2c 22 6b 6e 69 66 65 22 2c 22 70 61 63 6b 22 2c 22 63 61 6c 6c 22 2c 22 74 61 6c 65 73 22 2c 22 70 72 6f 64 75 63 74 69 6f ... 1721522 more bytes>
Finished reading file
```

## 用回调方式读取文件

回调方式的方法是使用`fs.readFile`节点 API。当文件被完全读入内存时，这个方法给了我们回调。让我们看看下面的代码示例。

运行上面的代码也会得到类似的输出。

```
Start reading file
Running other operation
content <Buffer ef bb bf 22 6c 6f 73 74 22 2c 22 6b 6e 69 66 65 22 2c 22 70 61 63 6b 22 2c 22 63 61 6c 6c 22 2c 22 74 61 6c 65 73 22 2c 22 70 72 6f 64 75 63 74 69 6f ... 1721522 more bytes>
Finished reading file
```

## 用同步方式读取文件

同步方式是使用`fs.readFileSync`节点 API 实现的。

运行上面的代码会得到下面的输出。

```
Start reading file
content <Buffer ef bb bf 22 6c 6f 73 74 22 2c 22 6b 6e 69 66 65 22 2c 22 70 61 63 6b 22 2c 22 63 61 6c 6c 22 2c 22 74 61 6c 65 73 22 2c 22 70 72 6f 64 75 63 74 69 6f ... 1721522 more bytes>
Finished reading file
Running other operation
```

这里值得一提的是**同步方式会阻塞下一行执行，直到文件被成功读取**。正如你在上面看到的，`Runnint other operation`日志只在`Finished reading file`之后显示。

# 哪种方式是我最喜欢的，为什么？

> 无极道

我最喜欢的方式是**承诺方式**。在我最喜欢的选择过程中，有两个因素是我要考虑的:

*   代码可读性和流行度
*   阻塞与非阻塞

## 代码可读性和流行度

从流行的角度来看，`async`和`await`是 JavaScript 世界中现代流行的异步代码编写方式。随着代码库的增长，我相信我们会看到更多使用`async`和`await` 而不是回调方式。

从代码可读性的角度来看，与回调方法相比，promise 方法看起来更干净，可读性也更好。通过使用`async`和`await`，从上到下读取代码的流程非常流畅。

## 阻塞与非阻塞

**承诺方式**和**回调方式**都为整个系统提供了更好的效率，因为它在读取文件时不会阻塞代码。

而同步方式将阻止代码执行，直到文件被读入内存。

# 结论

在本指南中，我们探讨了在 Node.js 中读取文件的不同方法。此外，我还根据代码可读性和受欢迎程度以及阻塞与非阻塞代码选择了自己喜欢的方法。

但是，请记住，我们并没有在本指南中考虑每种不同方法的性能。我可能会在下一篇文章中这样做。如果性能是主要关注点，请查看我即将发布的帖子。

感谢阅读，我希望你发现这是有帮助的。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)