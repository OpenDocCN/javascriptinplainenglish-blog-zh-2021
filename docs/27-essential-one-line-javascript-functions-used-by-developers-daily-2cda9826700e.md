# 开发人员日常使用的 27 个基本的单行 JavaScript 函数

> 原文：<https://javascript.plainenglish.io/27-essential-one-line-javascript-functions-used-by-developers-daily-2cda9826700e?source=collection_archive---------0----------------------->

在本文中，我整理了 27 个单行 JavaScript 函数的列表，这些函数是每个开发人员日常使用和需要的。不管你是初级、**中级、**还是**专业** JavaScript 开发者。在某些时候，您会在日常工作或个人项目中使用这些功能。如果你每天都写代码，我保证你总是需要使用这些函数。我看了很多网上资源，整理了最有用的一行 JavaScript 函数。

![](img/92af9c4d4a15f35dabee5d6d16143580.png)

27 Daily Used One-Line JavaScript Functions Needed by Every Developer | Essential/Useful JavaScript Functions

# **让我们开始**

# 1.复制到剪贴板

一个有用的单行 JavaScript 函数，可以用来轻松地将任何文本复制到剪贴板。

Copy to Clipboard

# 2.获取特定范围内的随机数

一个基本的 JavaScript 函数，用于在特定的数字范围内生成一个随机数。您提供一个最小值和一个最大值作为参数，这个单行函数返回给定范围内的一个随机数。

Get a random number in a specific range

# 3.将 RGB 转换为十六进制

这个列表中的一个有用的函数，用来把 RGB 转换成十六进制代码。

Convert RGB to Hex

# 4.滚动到页面顶部

这个列表中另一个有用的 JavaScript 函数，用于自动滚动到网页的顶部。

Scroll to Page Top

# 5.找出两个日期之间的间隔天数

当您在 JavaScript 中处理日历/日期时，下一个函数是非常有用的一行程序。使用下面的代码找出两个给定日期之间的间隔天数。

Find the number of gap days between two dates

# 6.生成随机十六进制

你可以使用这个函数生成随机的十六进制颜色，这对前端项目非常有用。

Generate Random Hex

# 7.检查提供的日期是否是工作日

使用这个函数，您将能够检查作为参数传递的日期是工作日还是周末。

Check if the provided day is a weekday

# 8.转换温度华氏/摄氏

如果您在项目中处理温度，那么这两个函数是非常有用的 JavaScript 函数。这两个函数将帮助你把华氏温度转换成摄氏温度，反之亦然。

Convert Temprature Fahrenheit / Celsius

# 9.检查用户是否在苹果设备上

正如在许多项目中一样，我们需要实现基于设备的特性。您可以使用此功能来确定用户是否正在使用 Apple 设备。

Check if the user is on an Apple device

# 10.从日期中获取时间

您可以使用。toTimeString()方法，通过在正确的位置对字符串进行切片，我们可以从我们提供的日期中获取时间，或者获取当前时间。

Get the time from a date

# 11.从文本中剥离 HTML

一个非常方便的 JavaScript 单行函数，出于安全原因，它也很重要。用户可以提交基于标签的输入值。当接受用户输入时，可以在 DOMParser 的帮助下剥离用户输入的文本中的任何 HTML 元素。

Strip HTML From Text

# 12.切换(显示/隐藏)元素

使用 CSS display 属性值，您可以通过这种单行方法轻松地在显示/隐藏元素之间切换。

Toggle (show/hide) of an Element

# 13.反转一根绳子

您可以使用`split`、`join`和`reverse`方法反转一行中的字符串。

Reverse a String

# 14.将字符串大写

因为 JavaScript 没有提供内置的大写方法，所以使用这个单行函数可以大写一个字符串。

Capitalize a String

# 15.将小数四舍五入到特定的小数位数

当你处理数量时，小数的计算非常重要，应该非常精确和可靠。在 JavaScript 中，将小数舍入到固定的小数点位数是一件棘手的事情。内置的 JavaScript toFixed()方法可以很容易地完成这种转换，但是由于浮点运算的工作方式，它在某些情况下会产生奇怪的结果。

为了避免这种奇怪的行为，可以用指数表示法表示数字，并使用 Math.round()将小数四舍五入到给定的小数位数。

Round Decimals to a Certain Number of Decimal Places

# 16.打乱数组

您可以使用下面的代码来打乱一个数组。它使用`sort`和`random`方法。

Shuffle an Array

# 17.检测黑暗模式

使用下面的代码找出用户的设备是否处于黑暗模式。

Detect Dark Mode

# 18.从 URL 获取查询参数

非常有用的功能，当你处理网址，查询参数。通过将 url 作为函数的参数传递，可以很容易地从 url 中检索查询参数。

Get Query Params from URL

# 19.获取一组数字的平均值

JavaScript reducer 允许在一行中计算多个数组的平均值。Reduce 方法在编写许多问题的单行解决方案时非常有用，例如在一组数字中寻找总和或最大值。

Get the Average of an Array of Number

# 20.检查当前用户是否支持触摸事件

Check if the current user has touch events supported

# 21.找到一年中的某一天

另一个非常有用的与日期/日历相关的 JavaScript 函数。它基本上为您提供了一年中的天数。例如，2 月 6 日是一年 365 天中的 37 天。

Find the day of year

# 22.获取浏览器 Cookie 的值

JavaScript 的一个有用的短函数，用来获取浏览器 cookie 的值。

Get Value of a browser Cookie

# 23.清除所有浏览器 Cookies

另一个与 cookie 相关的一行程序，通过使用`document.cookie`访问 cookie 并清除它，可以轻松清除网页中存储的所有 cookie。

Clear All browser Cookies

# 24.获取随机布尔值(真/假)

该函数将使用`Math.random()`方法返回一个布尔值(真或假)。`Math.random`将创建一个介于 0 和 1 之间的随机数，之后我们检查它是高于还是低于 0.5。这意味着有 50%的机会得到真或假。

Get a random boolean value (true/false)

# 25.删除数组中的重复项

**在 JavaScript 中设置**只存储唯一的项目。我们可以使用这个行为从数组中删除重复的项。但是，它只适用于存储原始数据的数组。因此，您必须编写一个多行解决方案来删除存储对象的数组中的重复项。但是，在简单的场景中，这仍然是一个相当不错的删除重复的方法。

Remove Duplicates in an Array

# 26.检查日期是否有效

使用此 Js 函数检查用户日期输入的有效性。

Check if Date is Valid

# **27。从数组中随机获取一个物品**

这个一行程序从输入数组中返回一个随机项，作为参数传递给函数。

Get a random item from an array

# 结论:

如果你有扩展这个列表的想法，请在评论中提出你的想法。我很乐意用你的建议来扩展这个列表。如果你喜欢这篇文章，并希望在未来看到更多的内容，那么别忘了关注我。编码快乐！

# 关于作者:

我在 [Lucid 公司做全栈开发者。工作室](https://medium.com/u/cb727ce3b3c0?source=post_page-----4ef4ecbdcc1b--------------------------------)我非常有兴趣学习并与社区分享我的知识。如果你喜欢我的作品，请在 LinkedIn 上联系我:Sayyed Hammad Ali。

# 您可能喜欢的其他文章:

[](/10-must-have-chrome-extensions-for-web-developers-ed40e3e1081f) [## 网络开发者必备的 10 个 Chrome 扩展

### 对开发者最有用的 Chrome 扩展

javascript.plainenglish.io](/10-must-have-chrome-extensions-for-web-developers-ed40e3e1081f) [](/3-uses-of-in-javascript-why-pro-developers-love-using-javascript-operator-565bc8b235a4) [## “？”的 3 种用法在 JavaScript❓

### 怎么(？/ ?？/ ?。)运算符在 JavaScript 中工作，以及为什么开发人员喜欢使用它们

javascript.plainenglish.io](/3-uses-of-in-javascript-why-pro-developers-love-using-javascript-operator-565bc8b235a4) 

**来源的信用:**

1.  [https://modernweb.com/45-javascript-tips-tricks-practices/](https://modernweb.com/45-javascript-tips-tricks-practices/)
2.  [https://dev . to/savio Martin/20-killer-JavaScript-one-liners-94f](https://dev.to/saviomartin/20-killer-javascript-one-liners-94f)
3.  [https://www . that sanegg . com/blog/13-JavaScript-one-liners-that % E2 % 80% 99ll-make-you-look-like-a-pro/](https://www.thatsanegg.com/blog/13-javascript-one-liners-that%E2%80%99ll-make-you-look-like-a-pro/)
4.  [https://livecodestream . dev/post/awesome-JavaScript-one-liners-to-look-like-a-pro/](https://livecodestream.dev/post/awesome-javascript-one-liners-to-look-like-a-pro/)

*更多内容看* [*说白了。报名参加我们的*](http://plainenglish.io/) [*免费每周简讯*](http://newsletter.plainenglish.io/) *。在我们的* [*社区*](https://discord.gg/GtDtUAvyhW) *获得独家写作机会和建议。*