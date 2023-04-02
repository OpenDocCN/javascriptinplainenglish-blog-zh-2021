# 17 个救命的 JavaScript 一行程序🔥

> 原文：<https://javascript.plainenglish.io/17-life-saving-javascript-one-liners-part1-b0b0b32c9f61?source=collection_archive---------0----------------------->

## 拯救生命的 JavaScript 一行程序系列的第 1 部分。

在 JavaScript 的世界里，代码越少越好。今天，我将向您展示 34 个杀手级 JavaScript 一行程序(分为两部分)。

在这一部分，我将按顺序列出与 **DOM、数组和对象**相关的不同的一行程序。第二部分将按顺序讨论**琴弦、日期和一些杂七杂八的东西**。

看看第二部分⬇

[](/another-17-life-saving-javascript-one-liners-8c335bf73d2c) [## 另外 17 个救命的 JavaScript 一行程序🔥

### 拯救生命的 JavaScript 一行程序系列的第 2 部分。

javascript.plainenglish.io](/another-17-life-saving-javascript-one-liners-8c335bf73d2c) ![](img/feb0c8db649490606ef83a6937069ca2.png)

# 数字正射影像图

## 检查元素是否被聚焦

```
const hasFocus = (ele) => ele === document.activeElement;
```

## 获取一个元素的所有兄弟元素

```
const siblings = (ele) => [].slice.call(ele.parentNode.children).filter((child) => child !== ele);
```

## 获取选定的文本

```
const getSelectedText = () => window.getSelection().toString();
```

## 回到上一页

```
history.back();// Or
history.go(-1);
```

## 清除所有 cookies

```
const clearCookies = () => document.cookie
.split(';')
.forEach((c) =>(document.cookie = c.replace(/^ +/, '').replace(/=.*/, `=;expires=${new Date().toUTCString()};path=/`)));
```

## 将 cookie 转换为对象

```
const cookies = document.cookie.split(';').map((item) => item.split('=')).reduce((acc, [k, v]) => (acc[k.trim().replace('"', '')] = v) && acc, {});
```

# 数组

## 比较两个数组

```
// `a` and `b` are arrays
const isEqual = (a, b) => JSON.stringify(a) === JSON.stringify(b);// Or
const isEqual = (a, b) => a.length === b.length && a.every((v, i) => v === b[i]);// Examples
isEqual([1, 2, 3], [1, 2, 3]); // true
isEqual([1, 2, 3], [1, '2', 3]); // false
```

## 将对象数组转换为单个对象

```
const toObject = (arr, key) => arr.reduce((a, b) => ({ ...a, [b[key]]: b }), {});// Or
const toObject = (arr, key) => Object.fromEntries(arr.map((it) => [it[key], it]));// Example
toObject([
{ id: '1', name: 'Alpha', gender: 'Male' },
{ id: '2', name: 'Bravo', gender: 'Male' },
{ id: '3', name: 'Charlie', gender: 'Female' }],
'id');/*
{
'1': { id: '1', name: 'Alpha', gender: 'Male' },
'2': { id: '2', name: 'Bravo', gender: 'Male' },
'3': { id: '3', name: 'Charlie', gender: 'Female' }
}
*/
```

## 根据对象数组的属性进行计数

```
const countBy = (arr, prop) => arr.reduce((prev, curr) => ((prev[curr[prop]] = ++prev[curr[prop]] || 1), prev), {});// Example
countBy([
{ branch: 'audi', model: 'q8', year: '2019' },
{ branch: 'audi', model: 'rs7', year: '2020' },
{ branch: 'ford', model: 'mustang', year: '2019' },
{ branch: 'ford', model: 'explorer', year: '2020' },
{ branch: 'bmw', model: 'x7', year: '2020' },
],
'branch');
// { 'audi': 2, 'ford': 2, 'bmw': 1 }
```

## 检查数组是否不为空

```
const isNotEmpty = (arr) => Array.isArray(arr) && Object.keys(arr).length > 0;// Examples
isNotEmpty([]); // false
isNotEmpty([1, 2, 3]); // true
```

# 目标

## 检查多个对象是否相等

```
const isEqual = (...objects) => objects.every((obj) => JSON.stringify(obj) === JSON.stringify(objects[0]));// Examples
isEqual({ foo: 'bar' }, { foo: 'bar' }); // true
isEqual({ foo: 'bar' }, { bar: 'foo' }); // false
```

## 从对象数组中提取属性值

```
const pluck = (objs, property) => objs.map((obj) => obj[property]);// Example
pluck([
{ name: 'John', age: 20 },
{ name: 'Smith', age: 25 },
{ name: 'Peter', age: 30 },
],
'name');
// ['John', 'Smith', 'Peter']
```

## 反转对象的键和值

```
const invert = (obj) => Object.keys(obj).reduce((res, k) => Object.assign(res, { [obj[k]]: k }), {});// Or
const invert = (obj) => Object.fromEntries(Object.entries(obj).map(([k, v]) => [v, k]));// Example
invert({ a: '1', b: '2', c: '3' }); // { 1: 'a', 2: 'b', 3: 'c' }
```

## 从对象中删除所有空的和未定义的属性

```
const removeNullUndefined = (obj) => 
Object.entries(obj)
.reduce((a, [k, v]) => (v == null ? a : ((a[k] = v), a)), {});// Or
const removeNullUndefined = (obj) =>
Object.entries(obj)
.filter(([_, v]) => v != null)
.reduce((acc, [k, v]) => ({ ...acc, [k]: v }), {});// Or
const removeNullUndefined = (obj) => Object.fromEntries(Object.entries(obj).filter(([_, v]) => v != null));// Example
removeNullUndefined({
foo: null,
bar: undefined,
fuzz: 42}); 
// { fuzz: 42 }
```

## 按属性对对象进行排序

```
const sort = (obj) =>
Object.keys(obj)
.sort()
.reduce((p, c) => ((p[c] = obj[c]), p), {});// Example
const colors = {
white: '#ffffff',
black: '#000000',
red: '#ff0000',
green: '#008000',
blue: '#0000ff',
};sort(colors);/*
{
black: '#000000',
blue: '#0000ff',
green: '#008000',
red: '#ff0000',
white: '#ffffff',
}
*/
```

## 检查一个对象是否是一个承诺

```
const isPromise = (obj) =>
!!obj && (typeof obj === 'object' || typeof obj === 'function') && typeof obj.then === 'function';
```

## 检查对象是否是数组

```
const isArray = (obj) => Array.isArray(obj);
```

> 亲爱的读者:
> 
> 谢谢你的时间。如果你分享你的想法，我会很高兴。

> 编码快乐！

*更多内容看* [*说白了。报名参加我们的*](http://plainenglish.io/) [*免费周报*](http://newsletter.plainenglish.io/) *。在我们的* [*社区*](https://discord.gg/GtDtUAvyhW) *获得独家写作机会和建议。*