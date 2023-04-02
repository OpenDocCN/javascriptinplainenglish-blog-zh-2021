# JavaScript 备忘单—数字、字符串和正则表达式

> 原文：<https://javascript.plainenglish.io/javascript-cheat-sheet-numbers-strings-and-regex-8dbc504c88cf?source=collection_archive---------15----------------------->

![](img/c64f880e1320980e91164df4b7be0c08.png)

Photo by [Kelly Sikkema](https://unsplash.com/@kellysikkema?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 是 web 编程中最流行的编程语言之一。

在本文中，我们将了解现代 JavaScript 的基本语法。

# 数字

`toFixed`方法让我们四舍五入一个数字:

```
(3.14).toFixed(0);  // returns 3
```

`toPrecision`方法让我们四舍五入一个数字:

```
(3.14).toPrecision(1);  // returns 3.1
```

`valueOf`方法返回一个数字:

```
(3.14).valueOf();
```

`Number`函数让我们将任何东西转换成数字:

```
Number(true);
```

`parseInt`将非数值转换为整数:

```
parseInt("3 months");
```

`parseFloat`将非数值转换为浮点数:

```
parseFloat("3.5 days");
```

`Number`函数也有一些常量属性。

它们包括:

*   `Number.MAX_VALUE` —最大可能的 JS 编号
*   `Number.MIN_VALUE` —尽可能小的 JS 编号
*   `Number.NEGATIVE_INFINITY` —负无穷大
*   `Number.POSITIVE_INFINITY` —正无穷大

# 数学

我们可以用`Math`对象做各种数学运算。

`Math.round`将数字四舍五入为整数:

```
Math.round(4.1);
```

`Math.pow`以指数为底:

```
Math.pow(2, 8)
```

`Math.sqrt`取一个数的平方根:

```
Math.sqrt(49);
```

`Math.abs`取一个数的绝对值:

```
Math.abs(-3.14);
```

`Math.ceil`取一个数字的上限:

```
Math.ceil(3.14);
```

`Math.floor`一号楼:

```
Math.floor(3.14);
```

`Math.sin`取一个数的正弦值:

```
Math.sin(0);
```

`Math.cos`取一个数的余弦值:

```
Math.cos(0);
```

`Math.min`返回列表中的最小数:

```
Math.min(1, 2, 3)
```

`Math.max`返回列表中的最大数量:

```
Math.max(1, 2, 3)
```

`Math.log`取一个数的自然对数:

```
Math.log(1);
```

`Math.exp`将`e`提升至给定功率:

```
Math.exp(1);
```

`Math.random()`随机生成一个 0 到 1 之间的数字:

```
Math.random();
```

我们可以一起使用`Math.floor`和`Math.random`生成任意随机数:

```
Math.floor(Math.random() * 5) + 1;
```

5 是最大值，1 是最小值。

# **全局功能**

我们可以使用`String`函数将非字符串值转换成字符串:

```
String(23);
```

我们也可以对原始值和对象调用`toString`来做同样的事情:

```
(23).toString();
```

`Number`函数让我们将非数字转换成数字:

```
Number("23");
```

`decodeURI`不可预见的网址:

```
decodeURI(enc);
```

`encodeURI`编码网址:

```
encodeURI(uri);
```

我们可以用`decodeURIComponent:`解码 URI 分量

```
decodeURIComponent(enc);
```

我们可以用`encodeURIComponent`将一个字符串编码成 URI 字符串:

```
encodeURIComponent(uri);
```

`isFinite`让我们检查一个数字是否是有限的。

`isNaN`检查值是否为`NaN`。

`parseFloat`让我们将一个值解析成一个浮点数。

`parseInt`让我们将非数字值解析成整数。

# 正则表达式

JavaScript regex 有以下修饰符:

*   `i` -执行不区分大小写的匹配
*   `g` -进行全局匹配
*   `m` -执行多行匹配

它们可以有以下模式:

*   `\` —转义符
*   `\d` —查找一个数字
*   `\s` -查找空白字符
*   `\b`-在单词的开头或结尾找到匹配项
*   `n+`-至少包含一个 n
*   `n*` -包含零个或多个出现的 n
*   `n?` -包含零个或一个出现的 n
*   `^` —管柱开始
*   `$` —字符串结束
*   `\uxxxx`-查找 Unicode 字符
*   `.` ——任意单个字符
*   `(a|b)` — a 或 b
*   `(…)` —组段
*   `[abc]` —在范围(a、b 或 c)内
*   `[0–9]` —括号中的任意数字
*   `[^abc]`-不在范围内
*   `\s` —空白
*   `a?` —零或一个`a`
*   `a*` —零个或多个`a`
*   `a*?`-0 或以上，不冻
*   `a+` —一项或多项`a`
*   `a+?` —一个或多个，不冻
*   `a{2}` —恰好是`a`中的 2 个
*   `a{2,}` — 2 种或 2 种以上`a`
*   `a{,5}` —最多 5 个`a`
*   `a{2,5}` —第 2 ~ 5 项，共`a`
*   `a{2,5}?` —第 2 ~ 5 项`a`，未冷冻
*   `[:punct:]` —任何穿孔符号
*   `[:space:]` —任何空格字符
*   `[:blank:]` —空格或制表符

# 结论

JavaScript 附带了许多有用的函数。

我们可以使用正则表达式来匹配字符串中的模式。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)