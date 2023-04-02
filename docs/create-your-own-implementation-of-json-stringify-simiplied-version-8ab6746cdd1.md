# 如何创建自己的 JSON.stringify()实现

> 原文：<https://javascript.plainenglish.io/create-your-own-implementation-of-json-stringify-simiplied-version-8ab6746cdd1?source=collection_archive---------1----------------------->

## 创建自己的 JSON.stringify()实现的简化技术

![](img/e77a1fbc0b5c54e7926ab5234b7f21be.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

大多数 JavaScript 开发人员都会熟悉 JSON.stringify()，它用于比较对象，构建深度克隆对象和数组，还有助于实现 RESTful APIs。

因此，在本文中，我们将讨论如何创建我们自己的简化版本的这种方法。

JSON.stringify()方法将 JavaScript 对象或值转换为 JSON 字符串，稍后可以使用 JSON.parse()方法将该字符串解析回 JavaScript 对象或值。

如果你不熟悉这个功能，我强烈建议你看看 [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify) 的医生是怎么说的。

它的语法非常简单:

```
const obj = { x: 5, y: 6 };
console.log(JSON.stringify(obj));
// expected output: "{"x":5,"y":6}"
```

让我们从基本的测试用例开始:

正如您所看到的，它对于 4 种主要的数据类型非常简单:数字、布尔、字符串和对象。对于嵌套的对象结构，我们需要使用递归函数来处理它。对于数组来说，它也是一个对象，但要处理它，我们需要用 isArray 函数进行显式检查。让我们来看看这个例子:

如果您传递一个字符串或数字而不是一个对象，上面的函数也将以同样的方式工作和行为。这就是为什么我创建了单独的 if 块并返回值，这样那些 if 块就可以用于对象值的递归函数调用。

```
console.*log*((*JSON*.*stringify*(1) === *JSONStringify*(1))); -> TRUEconsole.*log*((*JSON*.*stringify*('s') === *JSONStringify*('s'))); -> TRUE
```

**下一步**

*   支持 null、Infinity 和 NAN 值。
*   忽略对象中的函数、未定义值和符号值。
*   添加对未定义的支持。
*   通过返回与 date.toISOString()相同的字符串来转换 Date 对象。
*   处理 NaN、Infinity 和未定义值的数组值，并将它们作为空值传递。

对于 Null、Infinity 和 NaN 值，我们可以创建自定义函数来识别它们并将其分组为一个值:

要忽略函数、符号和未定义的值:

支持日期对象:

处理数组值或嵌套数组值我们必须创建一个单独的函数来处理它并更新数组的递归调用:

# 最终实现:

以下是我试图涵盖的测试案例:

您可以使用这些案例并传递您自己的 stringifying 自定义实现，以检查您涵盖了哪些边缘案例。

# 结论

我注意到最近在面试中也有人问了一个编码问题来实现你的 stringify 函数。另外，了解 JavaScript 语言的深度以及本机方法是如何实现的也很有好处。坦率地说，它帮助我理解了幕后发生的事情以及 JavaScript 中每种数据类型的深度。

我把这段代码放到了 Github 上:

[](https://github.com/siddharth-sunchu/native-methods/blob/master/JSONStringfy.js) [## 西达斯-孙楚/本地方法

### JavaScript 的本地方法。创建一个帐户，为西达斯-孙楚/本土方法的发展作出贡献…

github.com](https://github.com/siddharth-sunchu/native-methods/blob/master/JSONStringfy.js) 

请随意建议或添加我可能遗漏或未考虑的任何边缘案例。

*更多内容看*[***plain English . io***](http://plainenglish.io/)