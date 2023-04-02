# 用 JavaScript 中的助手格式化日期

> 原文：<https://javascript.plainenglish.io/formatting-dates-with-custom-helpers-in-javascript-973f11ea8c5d?source=collection_archive---------9----------------------->

![](img/6af691026cc8e7ad5dba2586a8a8787d.png)

The Land Before Time

# 介绍

我正在为公寓设计一个 HUD(平视显示器),上面会有一些重要的项目，比如:当前天气、7 天天气预报以及我们所有室内植物的植物护理说明。这个 React 应用程序基于 Ruby on Rails RESTful API，最终将从一个平板电脑上访问，该平板电脑显著地显示在一面重要的墙上，运行在本地 Raspberry Pi 服务器上。

当然，我可以买一个谷歌主页，亚马逊 Alexa 之类的东西，或者苹果什么的，但是这有什么意思呢？

# 时代

对于我的应用程序的天气部分，我使用的是[的 OpenWeather](https://openweathermap.org/) 的免费 [OneCall API](https://openweathermap.org/api/one-call-api) 。你会得到这样的回应:

Example API Response

## UNIX 纪元

我不知道你怎么想，但是当日期/时间信息以基于“纪元”以来的秒数的 [UNIX 格式](https://en.wikipedia.org/wiki/Unix_time)书写时，我在读取它时有一点麻烦。比如`595832400` Epoch？是的，我在 90 年代看了大约 100 倍的[](https://en.wikipedia.org/wiki/The_Land_Before_Time)*之前的土地，他们从来没有用过那个词。*

*幻想出 UNIX 时代的酷猫们决定这个重要的日子应该是 1970 年 1 月 1 日。巧合的是，这一天美国总统理查德·尼克松签署了国家环境政策法案，使之成为法律……但是我跑题了。*

## *JavaScript 纪元*

*为了保持事情的趣味性，JavaScript 工厂的人决定从任何时候到 1970 年 1 月 1 日之间的时间应该以毫秒为单位。因此，我们必须获取返回的日期/时间对象，并将其乘以 1000(也就是一秒钟内有多少毫秒)。因此，如果我们把土地的释放日期放在时间之前，`595832400`并将其转换为毫秒，我们将得到`595832400 * 1000 = 595832400000`*

# *日期对象*

*假设我想从我的日期对象中获取一周中的某一天。我会这样做:*

```
*let date = new Date(595832400000)let day = date.getDay() 
day // => 5*
```

*所以返回一个数字，这意味着我们要做更多的工作。*

```
*const dayMap = {  
  0: "Sunday",  
  1: "Monday",  
  2: "Tuesday",  
  3: "Wednesday",  
  4: "Thursday",  
  5: "Friday",  
  6: "Saturday"
}dayMap[day] // => "Friday"*
```

*现在我们有点进展了，但是让我们玩得更开心一点。如果我只想呈现前三个字母，或者前两个字母。我想把它作为一个选项，而不是仅仅把`dayMap`硬编码成更短的字符串。*

*看一看`uppercaseAbbreviate()`。它有两个参数:1)日期(“星期一、星期二等”)，2)指定返回的字符数的选项。现在我们需要把这些都转换成大写:`“FRI”`。怎么会？*

1.  *只选择前 3 个字母。*
2.  *将数组中的每个字符大写。*

```
*let day = "Friday"day.slice(0, 3) //=> "Fri"
// this slices the string from the first character, 
// at the 0th index, all the way up to and including 
// the 3rd character, "i"day.slice(0, 3).toUpperCase()
// here we capitalize every member of the string
//=>"FRI"*
```

# *收场白*

*坦白说:有一个名为 [Day.js](https://day.js.org/docs/en/display/format) 的很棒的库，它让所有这些变得更容易，但是知道如何深入事物如何工作的本质以及如何将工具添加到您的工具箱中是很重要的！*

*[](https://day.js.org/docs/en/display/format) [## 格式化 Day.js

### 根据传入的标记字符串获取格式化的日期。要转义字符，请用方括号将它们括起来…

day.js.org](https://day.js.org/docs/en/display/format)*