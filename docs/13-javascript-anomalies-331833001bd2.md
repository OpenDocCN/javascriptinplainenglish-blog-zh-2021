# 16 个 JavaScript 异常

> 原文：<https://javascript.plainenglish.io/13-javascript-anomalies-331833001bd2?source=collection_archive---------5----------------------->

## 值得了解的有趣的 JavaScript 事实

![](img/983776455ec1e4665ee1efe7e8b18498.png)

Photo by [Ben White](https://unsplash.com/@benwhitephotography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 1.类型为空的对象是 JavaScript 中的一个 bug

`null`是一个物体。

```
> typeof(null)
"object"
```

但是既然`null`没有值。所以，`null`应该不是`Object`的实例。

```
> null instanceof Object
false
```

# 2. **NaN** 的类型(不是数字)实际上是**‘数字’**

`NaN`(不是一个数字)正在成为一个数字。

```
> typeof(NaN)
"number"
```

# 3.(NaN === NaN) ->假

`NaN`不等于本身。其实`NaN`不等于什么。

```
> NaN === NaN
false
```

验证任何事情的唯一方法是`NaN`或不通过`isNaN()`。

```
if (isNaN(x)) {
   return ‘Not a Number!’
}
```

一个副作用是，如果你想找出一个数组中`NaN`值的索引，你将永远不会使用`indexOf()`。

```
let values = [1, NaN, 3]
```

*   求 1 和错的指数:求南的指数。

```
> values.indexOf(1)
0> values.indexOf(NaN)
-1
```

# 4.有两个零

通常，我们使用正值零。但是也有一个-0。

```
> console.log(-0)
-0console.log(+0)
0
```

但是`(-0).toString()`和`(+0).toString()`都返回`0`。

```
> (-0).toString()
0> (+0).toString()
0
```

再深入一点，我发现它们实际上是相等的。

```
> +0 === -0
true
```

# 5.1 + 2 == 3 但是 1.0 + 2.0！== 3.0

在 JavaScript 中，`0.1 + 0.2 == 0.3`返回 false。事实是，javascript 如何将浮点数存储为二进制。

```
> 0.1 + 0.2
0.30000000000000004> 0.1 + 0.2 == 0.3
false
```

# 6。10/0 - >无穷大**但 10/-0**->-无穷大

```
> console.log(10/0)
Infinity> console.log(10/-0)
-Infinity
```

# 7.Math.max()小于 Math.min()

`Math.max() > Math.min()`返回`false`这个事实听起来不对，但实际上很有道理。

```
> Math.max() > Math.min()
false
```

# `8\. []`等于`![]`

！[]的计算结果为 false，因为引用是真实的。[]可以转换为一个数值(本例中为 0 ),该数值为 falsy。因此:条件作为相等通过。如果你做了===那就是假的。

```
> [] == ![]
true
```

# 9.三个数的比较

问题出在表达式的第一部分。

```
1 < 2 < 3; // -> true
3 > 2 > 1; // -> false
```

# 10.字符串不是`String`的实例

```
"str"; // -> 'str'
typeof "str"; // -> 'string'
"str" instanceof String; // -> false
```

# **11。设 new Fn =新函数(' num '，' return num*num')**

它动态地创建函数。很少使用，但有时别无选择。

```
let new Fn = new Function(‘num’, ‘return num*num’)
```

# 12.JavaScript 是一种编译语言

该语言提前解析、优化和编译代码，并且只在运行时解释代码。

# 13.在**‘a’**数组下面有一个元素 init，但是这个长度仍然显示为 **0**

```
> Array.prototype.push(1)
1> let a = []
undefined> a.length
0> a[0]
1
```

# 14.真+假= 1

`Number(true)`等于 1，`Number(false)`等于 0，所以真+假= 1

```
> true + false
1
```

# 15\. [1, 2, 3] + [4, 5, 6] == 1,2,34,5,6

没有为数组定义+运算符。发生的事情是 Javascript 将数组转换成字符串，并将它们连接起来。

```
> [1, 2, 3] + [4, 5, 6]
1,2,34,5,6
```

如果你真的想组合两个数组，这是一个更好的方法:

```
> [...[1, 2, 3], ...[4, 5, 6]]
```

# 16\. !!””

您可以在任何值前添加两个感叹号来获得它的布尔表示。

```
> !!""
false
```

注意，任何有值的都是真的，任何有“空”值的都是假的。但是空数组是个例外。它由 true 表示。

```
> !![]true
```

## 结论

我希望你对这些小信息感兴趣。你知道我们忽略了哪些奇怪的 JavaScript 怪癖吗？如果有，请在评论中告诉我们。

*更多内容尽在*[***plain English . io***](http://plainenglish.io)