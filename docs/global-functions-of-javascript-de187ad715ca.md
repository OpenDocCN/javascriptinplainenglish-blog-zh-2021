# JavaScript 中常用全局函数的初学者指南

> 原文：<https://javascript.plainenglish.io/global-functions-of-javascript-de187ad715ca?source=collection_archive---------9----------------------->

## JavaScript 初学者指南

## JavaScript 中常用的全局函数有哪些？

![](img/13673ab85bac4a48b559826352ccc701.png)

一些关于 JavaScript 的基础知识将帮助你在 Postman 中为你的 API 测试自动化编写更好的脚本。

我们将看看一些全局函数及其用法。一旦你学会了它们，你就会知道何时何地在你的脚本中使用它们。

这些全局函数是全局调用的，而不是直接在一个对象上返回它们的结果。

***1。String():***

这个函数将对象的值转换成字符串。

*例如:*

```
var bool = Boolean(0);result = String(bool); // false
```

**2。encodeURI():**

这个函数编码 URI，代表字符的 UTF-8 编码。它转义所有字符，除了:

```
A-Z a-z 0-9 ; , / ? : @ & = + $ - _ . ! ~ * ' ( ) #
```

`decodeURI()`功能是解码一个编码的 URI。

*例如:*

```
const uri = ‘[https://test.com/?x=](https://test.com/?x=)шеллы';
const encoded = encodeURI(uri);
console.log(encoded); // [https://test.com/?x=%D1%88%D0%B5%D0%BB%D0%BB%D1%8B](https://test.com/?x=%D1%88%D0%B5%D0%BB%D0%BB%D1%8B)const decoded = decodeURI(uri);
console.log(decoded); // [https://test.com/?x=](https://test.com/?x=)шеллы
```

***3。encodeURIComponent():***

该函数对包含特殊字符的 URI 分量进行编码。

函数的作用是:解码一个编码的 URI 分量。

*例如:*

```
const uri = ‘#^$&%&^';
const encodedComp = encodeURIComponent(uri);
console.log(encodedComp); // %23%5E%24%26%25%26%5Econst decodedComp = decodeURIComponent(uri);
console.log(decodedComp); // #^$&%&^
```

***4。isFinite():***

该函数判断传递的数字是否为有限数字，如果该值为+infinity、-infinity 或 NaN，则返回 false，否则返回 true。

```
var text= isFinite(“Test”); // falsevar eg = isFinite(910); // truevar eg = isFinite(null); // true, would’ve been false with the
 // more robust Number.isFinite(null)
```

***5。*编号():**

这个方法将变量转换成数字。

例如:

```
var num1 = Number(true);console.log(num1); // 1var num2 = Number(“123”);console.log(num2); // 123
```

***6。parseInt():***

这个函数解析一个字符串并返回一个整数。只返回字符串中的第一个数字。如果第一个字符不能转换为数字，parseInt()返回 NaN。

例如:

```
var int1= parseInt(“12.67”);console.log(int1); // 12var int2= parseInt(“45 90 12”);console.log(int2); // 45
```

***7 . parse float():***

这个函数解析一个字符串并返回一个浮点数。

此函数确定指定字符串中的第一个字符是否为数字。如果是，它将解析字符串，直到到达数字的末尾，并将数字作为数字而不是字符串返回。

例如:

```
var float1= parseFloat(“12.67”);console.log(float1); // 12.67var float2= parseFloat(“45 90 12”);console.log(float2); // 45
```

***8。isNan():***

此函数确定一个值是否为 NaN(非数字)。

例如:

```
var nan1= isNan(“3435”);console.log(nan1); // falsevar nan2= isNan(“test”);console.log(nan2); // true
```

**9*。eval():***

该函数计算表示为字符串的 JavaScript 代码。

eval()函数的参数是一个字符串。如果 eval()的参数不是字符串，则 eval()返回不变的参数。

```
var a = 5;
var b= 2;
var res= eval(“x * y”);console,log(res); // 10
```

我发现这些很有趣，也很有用！请让我知道你的想法。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)