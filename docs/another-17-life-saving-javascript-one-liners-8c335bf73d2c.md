# 另外 17 个救命的 JavaScript 一行程序🔥

> 原文：<https://javascript.plainenglish.io/another-17-life-saving-javascript-one-liners-8c335bf73d2c?source=collection_archive---------5----------------------->

## 拯救生命的 JavaScript 一行程序系列的第 2 部分。

在第一部分中，我按顺序列出了与 **DOM、数组和对象**相关的不同的一行程序。在这一部分，我将按顺序列出与**字符串、日期和一些杂七杂八的东西**相关的其他不同的命令行程序。

看看第一部分⬇

[](/17-life-saving-javascript-one-liners-part1-b0b0b32c9f61) [## 17 个救命的 JavaScript 一行程序🔥

### 拯救生命的 JavaScript 一行程序系列的第 1 部分。

javascript.plainenglish.io](/17-life-saving-javascript-one-liners-part1-b0b0b32c9f61) ![](img/426be60e6135cde086d8292943fc94dc.png)

# **琴弦**

## 检查路径是否是相对的

```
const isRelative = (path) => !/^([a-z]+:)?[\\/]/i.test(path);// Examples
isRelative('/foo/bar/baz'); // false
isRelative('C:\\foo\\bar\\baz'); // false
isRelative('foo/bar/baz.txt'); // true
isRelative('foo.md'); // true
```

## 将字符串的第一个字符变为小写

```
const lowercaseFirst = (str) => `${str.charAt(0).toLowerCase()}${str.slice(1)}`;// Example
lowercaseFirst('Hello World'); // 'hello World'
```

## 重复一串

```
const repeat = (str, numberOfTimes) => str.repeat(numberOfTimes);
```

## 检查字符串是否是十六进制颜色

```
const isHexColor = (color) => /^#([0-9A-F]{3}|[0-9A-F]{4}|[0-9A-F]{6}|[0-9A-F]{8})$/i.test(color);// Examples
isHexColor('#012'); // true
isHexColor('#A1B2C3'); // true
isHexColor('012'); // false
isHexColor('#GHIJKL'); // false
```

# 日期

## 将“am/pm”后缀添加到小时中

```
// `h` is an hour number between 0 and 23
const suffixAmPm = (h) => `${h % 12 === 0 ? 12 : h % 12}${h < 12 ? 'am' : 'pm'}`;// Examples
suffixAmPm(0); // '12am'
suffixAmPm(5); // '5am'
suffixAmPm(12); // '12pm'
suffixAmPm(15); // '3pm'
suffixAmPm(23); // '11pm'
```

## 计算两个日期之间不同的天数

```
const diffDays = (date, otherDate) => Math.ceil(Math.abs(date - otherDate) / (1000 * 60 * 60 * 24));// Example
diffDays(new Date('2014-12-19'), new Date('2020-01-01')); // 1839
```

## 检查日期是否有效

```
const isDateValid = (...val) => !Number.isNaN(new Date(...val).valueOf());isDateValid("December 17, 1995 03:24:00"); // true
```

# **杂项**

## 检查代码是否在 Node.js 中运行

```
const isNode = typeof process !== 'undefined' && process.versions != null && process.versions.node != null;
```

## 检查代码是否正在浏览器中运行

```
const isBrowser = typeof window === 'object' && typeof document === 'object';
```

## 将 URL 参数转换为对象

```
const getUrlParams = (query) =>Array.from(new URLSearchParams(query)).reduce((p, [k, v]) => Object.assign({}, p, { [k]: p[k] ? (Array.isArray(p[k]) ? p[k] : [p[k]]).concat(v) : v }),{});// Examples
getUrlParams(location.search); // Get the parameters of the current URLgetUrlParams('foo=Foo&bar=Bar'); // { foo: "Foo", bar: "Bar" }// Duplicate key
getUrlParams('foo=Foo&foo=Fuzz&bar=Bar'); // { foo: ["Foo", "Fuzz"], bar: "Bar" }
```

## 检测黑暗模式

```
const isDarkMode = window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches;
```

## 交换两个变量

```
[a, b] = [b, a];
```

## 复制到剪贴板

```
const copyToClipboard = (text) => navigator.clipboard.writeText(text);// Example
copyToClipboard("Hello World");
```

## 将 RGB 转换为十六进制

```
const rgbToHex = (r, g, b) => "#" + ((1 << 24) + (r << 16) + (g << 8) + b).toString(16).slice(1);// Example
rgbToHex(0, 51, 255); // #0033ff
```

## 生成随机的十六进制颜色

```
const randomColor = () => `#${Math.random().toString(16).slice(2, 8).padEnd(6, '0')}`;// Or
const randomColor = () => `#${(~~(Math.random() * (1 << 24))).toString(16)}`;
```

## 生成一个随机的 IP 地址

```
const randomIp = () => Array(4).fill(0)
.map((_, i) => Math.floor(Math.random() * 255) + (i === 0 ? 1 : 0))
.join('.');// Example
randomIp(); // 175.89.174.131
```

## 使用节点加密模块生成随机字符串

```
const randomStr = () => require('crypto').randomBytes(32).toString('hex');
```

> 亲爱的读者:
> 
> 谢谢你的时间。如果你分享你的想法，我会很高兴。

> 编码快乐！❤

*更多内容请看*[***plain English . io***](http://plainenglish.io/)