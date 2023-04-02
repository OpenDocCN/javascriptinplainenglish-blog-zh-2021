# JavaScript 备忘单—错误和字符串

> 原文：<https://javascript.plainenglish.io/javascript-cheat-sheet-errors-and-strings-3fb0fbe587d?source=collection_archive---------12----------------------->

![](img/3417e398db149470c11263161936400b.png)

Photo by [Sticker Mule](https://unsplash.com/@stickermule?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 是 web 编程中最流行的编程语言之一。

在本文中，我们将了解现代 JavaScript 的基本语法。

# 错误

我们可以使用 try-catch 块从可能引发错误的代码中捕捉错误:

```
try { 
  undefinedFunction();
} catch (err) { 
  console.log(err.message);
}
```

不管`finally`块是否抛出错误，我们都可以运行代码:

```
try {
  undefinedFunction();
} catch (err) {
  console.log(err.message);
} finally {
  console.log('done');
}
```

我们可以通过编写以下代码来抛出错误:

```
throw new Error('error')
```

JavaScript 附带了各种错误类:

*   `RangeError` —数字超出范围
*   `ReferenceError` —出现非法引用
*   `SyntaxError` —出现语法错误
*   `TypeError` —出现了一个类型错误
*   `URIError` —`encodeURI()`出现错误

# 输入值

我们可以从带有`value`属性的输入元素中获取输入的值:

```
const val = document.querySelector("input").value;
```

# 圆盘烤饼

我们可以用`isNaN`检查`NaN`值:

```
isNaN(x)
```

# 延迟后运行代码

我们可以使用`setTimeout`函数在延迟后运行代码:

```
setTimeout(() => {}, 1000);
```

# 功能

我们可以用关键字`function`声明函数:

```
function addNumbers(a, b) {
  return a + b;;
}
```

# 更新 DOM 元素内容

我们可以通过设置`innerHTML`属性来更新 DOM 元素的内容:

```
document.getElementById("elementID").innerHTML = "Hello World";
```

# 输出数据

为了将数据记录到控制台，我们调用`console.log`:

```
console.log(a);
```

我们还可以显示一个带有`alert`的警告框:

```
alert(a);
```

同样，我们可以通过调用`confirm`来显示一个确认对话框:

```
confirm("Are you sure?");
```

我们可以通过`prompt`功能要求用户输入:

```
prompt("What's your age?", "0");
```

# 评论

我们可以用`//`给 JavaScript 代码添加注释:

```
// One line
```

我们可以添加一个多行注释:

```
/* Multi line
comment */
```

# 用线串

我们可以用引号声明字符串:

```
let abc = "abcde";
```

同样，我们可以用`\n`添加一个新的行字符:

```
let esc = 'I don\'t \n know';
```

我们用`length`属性得到一个字符串的长度:

```
let len = abc.length;
```

我们用`indexOf`得到给定字符串中子串的索引:

```
abc.indexOf("abc");
```

同样，我们可以用`lastIndexOf`得到一个字符串中最后一个出现的子字符串:

```
abc.lastIndexOf("de");
```

我们可以用`slice`方法得到给定索引之间的子串:

```
abc.slice(3, 6);
```

方法让我们用另一个子串替换一个子串:

```
abc.replace("abc","123");
```

我们可以用`toUpperCase`将字符串转换成大写:

```
abc.toUpperCase();
```

我们可以用`toLowerCase`将字符串转换成大写:

```
abc.toLowerCase();
```

我们可以用`concat`将一个字符串与另一个字符串组合起来:

```
abc.concat(" ", str2);
```

我们可以用`charAt`或`[]`得到给定索引处的字符:

```
abc.charAt(2);
abc[2];
```

`charCodeAt`方法让我们得到给定索引处的字符代码:

```
abc.charCodeAt(2);
```

`split`方法允许我们按照给定的分隔符拆分字符串:

```
abc.split(",");
```

我们可以用一个空字符串来分割一个字符串:

```
abc.split("");
```

将字符串拆分成字符数组。

我们可以用`toString`把一个数字转换成给定基数的字符串:

```
128.toString(16);
```

# 结论

我们可以用 JavaScript 抛出和捕捉错误。

我们可以使用各种方法来处理字符串。

喜欢这篇文章吗？如果是这样，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*多内容于* [***中***](https://plainenglish.io/)