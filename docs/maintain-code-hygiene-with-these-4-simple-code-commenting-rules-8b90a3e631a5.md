# 用这 4 个简单的代码注释规则保持代码卫生

> 原文：<https://javascript.plainenglish.io/maintain-code-hygiene-with-these-4-simple-code-commenting-rules-8b90a3e631a5?source=collection_archive---------10----------------------->

## 在 2021 年，您可以遵循简单而强大的协议

![](img/f3d9bbd93a35b4ce801b1999d41d8b5a.png)

Photo by [CDC](https://unsplash.com/@cdc?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/clean?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

> “代码从不说谎，评论有时会说谎。”——罗恩·杰弗里斯

代码注释！有些人说它很丑，有些人说这是标准的好习惯。

> 评论是用“高级”英语语句描述你的程序将要做什么的“艺术”。

在这里，我列出了 4 个简单的协议，以遵循当写评论。

虽然这些建议可以应用于任何编程语言，但我们将使用 JavaScript 在实践中加以说明。

# 1.只评论具有业务逻辑复杂性的东西

*评论是道歉，不是要求。好的代码大多是文档本身。*

下面一个看起来很糟糕。

```
function hashIt(data) {
  // The hash
  let hash = 0;

  // Length of string
  const length = data.length;

  // Loop through every character in data
  for (let i = 0; i < length; i++) {
    // Get character code.
    const char = data.charCodeAt(i);
    // Make the hash
    hash = (hash << 5) - hash + char;
    // Convert to 32-bit integer
    hash &= hash;
  }
}
```

好多了

```
function hashIt(data) {
  let hash = 0;
  const length = data.length;

  for (let i = 0; i < length; i++) {
    const char = data.charCodeAt(i);
    hash = (hash << 5) - hash + char;

    // Convert to 32-bit integer
    hash &= hash;
  }
}
```

# 2.删除失效代码

版本控制的存在是有原因的。在你的历史中留下旧的代码。

```
doStuff();
// doOtherStuff();
// doSomeMoreStuff();
// doSoMuchStuff();
```

代替

```
doStuff();
```

# 3.删除期刊评论，这就是`Git logs are for`

记住，使用版本控制！不需要死代码、注释代码，尤其是日志注释。使用`git log`获取历史！

```
/**
 * 2016-12-20: Removed monads, didn't understand them (RM)
 * 2016-10-01: Improved using special monads (JP)
 * 2016-02-03: Removed type-checking (LI)
 * 2015-03-14: Added combine with type-checking (JR)
 */
function combine(a, b) {
  return a + b;
}
```

这样看起来不错。很明显！

```
function combine(a, b) {
  return a + b;
}
```

# 4.位置标记？移除它们

它们通常只会增加噪音。让函数和变量名以及适当的缩进和格式赋予代码视觉结构。

一塌糊涂

```
////////////////////////////////////////////////////////////////////////////////
// Scope Model Instantiation
////////////////////////////////////////////////////////////////////////////////
$scope.model = {
  menu: "foo",
  nav: "bar"
};////////////////////////////////////////////////////////////////////////////////
// Action setup
////////////////////////////////////////////////////////////////////////////////
const actions = function() {
  // ...
};
```

现在让我们把事情清理一下

```
$scope.model = {
  menu: "foo",
  nav: "bar"
};const actions = function() {
  // ...
};
```

这篇文章的灵感来自于这篇 [GitHub](https://github.com/ryanmcdermott/clean-code-javascript#comments) 的报道。

## 编码快乐& 2021 年新年快乐！