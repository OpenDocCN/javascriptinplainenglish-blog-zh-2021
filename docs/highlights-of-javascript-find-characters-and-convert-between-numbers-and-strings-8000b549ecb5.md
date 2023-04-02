# JavaScript 的亮点—查找字符并在数字和字符串之间转换

> 原文：<https://javascript.plainenglish.io/highlights-of-javascript-find-characters-and-convert-between-numbers-and-strings-8000b549ecb5?source=collection_archive---------8----------------------->

![](img/31bbf5d2593386b2298780ca9179ee3a.png)

Photo by [T. Q.](https://unsplash.com/@tq_photos?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

学习 JavaScript，必须先学基础。

在本文中，我们将研究 JavaScript 语言的最基本部分。

# 在字符串中的某个位置查找字符

我们可以用`charAt`方法或方括号符号在字符串中的某个位置找到一个字符。

例如，我们可以写:

```
let firstChar = 'james'.charAt(0)
```

那么`firstChar`就是`'j'`。

这与以下内容相同:

```
let firstChar = 'james'[0]
```

它们是一样的，所以方括号更常用，因为它更短。

# 替换字符

`replace`方法让我们替换字符。

例如，我们可以写:

```
let newText = text.replace("World War II", "the Second World War");
```

用`“the Second World War”`代替`“World War II”`。

它会搜索它的第一个实例并替换它。

要搜索它的所有实例并替换它们，我们需要使用一个正则表达式:

```
let newText = text.replace(/World War II/g, "the Second World War");
```

`g`旗代表全球。这意味着它将取代所有这些。

# 舍入数字

我们可以使用`Math.round`方法来舍入数字。

例如，我们可以写:

```
let score = Math.round(11.1);
```

然后我们用`Math.round`把 11.1 四舍五入到 11。

它舍入到最接近的整数。

当小数为. 5 时，该函数向上舍入。

为了总是向上舍入到最接近的整数，我们可以使用`Math.ceil`方法:

```
let score = Math.ceil(11.1);
```

然后我们得到 12。

为了总是向下舍入到最接近的整数，我们可以使用`Math.floor`方法:

```
let score = Math.floor(11.1);
```

# 生成随机数

JavaScript 附带了一个生成随机数的函数。

`Math.random`方法让我们创建一个介于 0 和 1 之间的随机数。

例如，我们可以写:

```
let randomNumber = Math.random();
```

返回的数字有 16 位小数。

# 将字符串转换为整数和小数

将带有数字的字符串转换成整数或小数是我们经常要做的事情。

我们可以使用`parseInt`方法将字符串转换成整数。

我们可以使用`parseFloat`方法将一个字符串转换成十进制数。

例如，我们可以写:

```
let currentAge = prompt("Enter your age.");
let age = parseInt(currentAge);
```

我们有`parseInt`方法将输入的数字转换成整数。

`prompt`总是返回一个字符串，所以我们必须把它转换成一个整数。

要将输入的文本转换成十进制数，我们可以使用`parseFloat`:

```
let currentAge = prompt("Enter your age.");
let age = parseFloat(currentAge);
```

# 将字符串转换为数字，反之亦然

要将字符串转换成数字，我们可以使用`Number`全局函数:

```
let num = Number('123');
```

那么`num`就是`123`。

要将数字转换成字符串，我们可以使用`toString`方法:

```
let num = 1234;
let numberAsString = num.toString();
```

`numberAsString`就是`'1234'`。

# 结论

我们可以在字符串中查找和替换字符串。

此外，我们可以在数字和字符串之间转换，并用 JavaScript 生成数字。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**