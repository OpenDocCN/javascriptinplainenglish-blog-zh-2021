# 3 JavaScript 中的对象初始化简写符号

> 原文：<https://javascript.plainenglish.io/3-object-initialization-shorthand-notations-in-javascript-8c057691153b?source=collection_archive---------14----------------------->

![](img/a4df38aadaba4bb82c7824f966125345.png)

我最近在做一个项目，在这个项目中，我试图用一种简写符号来解构一个变量的赋值。我在研究让一个特定的场景发挥作用的不同方法。在做这项研究时，我发现 ES2015 增加了 3 个新的对象初始化速记符号，我以前不知道有这种符号。所以我决定和大家分享这些。

**注意:**和大多数好东西一样，这些东西在 ie 浏览器上不工作。所以如果你支持它，当微软以后不再支持 IE 时，这些仍然是你的武器库。

# 对象初始化简写符号是什么意思？

默认情况下，对象初始化可以使用`Object.create()`、`new Object`或使用对象初始化器的文字符号来完成。对象初始化器是最常见的方式之一:

```
const foo= {
  bar: 1,
  baz: 2
}
```

在特定的场景中，有一些方法可以使这种初始化简洁明了，我们将在这篇文章中详细介绍这些方法。

ES2015 增加了 3 个新的对象初始化简写符号:

*   速记属性名
*   速记方法名称
*   计算属性名

# 速记属性名

这是最广为人知的对象初始化简写符号。每当对象上的属性名键与范围内的变量名相同时，我们可以在构造对象时省略属性值。

这意味着代码曾经是:

```
const bar = 1;
const foo: {
  bar: bar ,
  baz: 2
}
```

现在可以是:

```
const bar = 1;
const foo: {
  bar,
  baz: 2
}
```

# 速记方法名称

当我第一次看到它时，我有点惊讶，因为我一直都知道简写的属性名。但是我从来没有想到同样的情况也可以应用到函数/方法名上。使用简写方法名，我们可以在对象内部创建方法时完全省略 function 关键字。

有这样的代码:

```
const bar = 1;
const foo: {
  bar,
  baz: function() {
  // logic
  }
}
```

可能人手不足:

```
const bar = 1;
const foo: {
  bar,
  baz() {
  // logic
  }
}
```

我们已经习惯了这种形式的课程，这不是一个巨大的胜利，但这篇文章是关于人手不足，我喜欢这些新的介绍。

# 计算属性名

这是所有 3 个对象初始化速记中最有趣的一个。它允许我们将一个表达式作为对象的属性名进行计算。因此，我们现在可以在对象名中使用动态键。

你做过这个吗？

```
const obj = {}, key = 'bar';
obj[key] = 'baz';
```

这是可能的，因为 JavaScript 对象是字典，这给了我们向它们添加动态键的可能性。但这对我来说一直是个痛苦。不再是了！

```
let key = 'bar';
let obj = {
  [key]: 'baz',
}
```

而且会成功的！能够注入动态密钥的想法可能看起来微不足道，但它提供了许多可能性。我们甚至可以在其中添加复杂的表达式，甚至可以使用模板文字:

```
let key = 'bar';
const prefix = '_prefix'
let obj = {
  [key + '_expression']: 'baz',
  [`key${prefix}`]: 'baz',
}
```

这些是我们必须讨论的 3 个对象初始化简写符号。虽然这些是现有方法的语法糖，但它们是我们在创建对象时最常用的任务。小的改进累积起来。如果你想更深入地了解 JavaScript，你可以阅读我们关于 [JavaScript rest 和 spread 操作符和析构](https://www.wisdomgeek.com/development/web-development/rest-and-spread-operator-three-dots-that-changed-javascript/)的文章。

你会使用这些吗？请在下面的评论中告诉我们吧！

*原载于 2021 年 2 月 2 日*[*【https://www.wisdomgeek.com】*](https://www.wisdomgeek.com/development/web-development/javascript/object-initialization-shorthand-notations-in-javascript/)*。*