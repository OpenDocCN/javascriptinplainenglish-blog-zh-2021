# 如何在一条语句中处理 Undefined、Null 和 Empty:JavaScript

> 原文：<https://javascript.plainenglish.io/how-to-handle-undefined-null-and-empty-in-one-statement-javascr-44edbb045744?source=collection_archive---------14----------------------->

## 在一条语句中处理未定义、null 和空的条件:JavaScript

![](img/b218b2e98773bfcab9a6f598a4548682.png)

image source/ javascript

如果你想检查任何对象或变量，它是空的、未定义的或空的，你可以下次在 T2 IF T3 语句中这样做

```
var value = ""if(value){// this block will not get executed}else{// this block will get executed}
```

因为上面的语句等于这个

```
var value = ""if(value !== null && value !== undefined && value !== ""){// this block will not get executed}else{// this block will get executed}
```

# **感谢读者**

这是我在 Medium 上的第一篇帖子，我写的是我的个人爱好，以及我在 tech 中学到的任何有意义的东西，我会试着贴在这里，对其他人有所帮助。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)