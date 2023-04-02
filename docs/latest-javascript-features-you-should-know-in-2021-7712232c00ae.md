# 新引入的 JavaScript 特性可以提升您的知识

> 原文：<https://javascript.plainenglish.io/latest-javascript-features-you-should-know-in-2021-7712232c00ae?source=collection_archive---------10----------------------->

## JavaScript 备忘单 2021

## 利用 ES2021 的新功能优化您的 JavaScript 代码。

![](img/06a45a9be00ec6d94eed5b30fbf4aa2d.png)

Photo by [Shahadat Rahman](https://unsplash.com/@hishahadat?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

你可能会看到大量标题相同的文章，比如“在 2021 年知道这个特性”或者“如果你是开发者，你必须知道这个”。

老实说，我的意图不是制作一个 clickbaity 标题，而是提供有用的内容。

由于 JavaScript 每天都在发展，最好让自己跟上变化和特性，让生活变得更轻松。

> 让我们用例子来了解这些 **ES2021** 的特性。

## 1.全部替换

此方法可用于替换整个字符串中的特定单词或字母，并返回新字符串。

模式可以是**字符串**或**正则表达式**。

```
const test = 'my name is atit';
const regex = /atit/gi;
console.log(test.replaceAll(regex, 'patel'));
// expected output: my name is patelconsole.log(test.replaceAll('atit', 'patel'));
// expected output: my name is patel
```

## 2.Promise.any()

如果一个承诺实现了，当你想展示一些东西时，这个方法会很有帮助。

```
const promise1 = Promise.reject(0);
const promise2 = new Promise(resolve =>
    setTimeout(resolve, 50, 'I will come first')
);
const promise3 = new Promise(resolve => setTimeout(resolve, 100, 'I am last'));const promises = [promise1, promise2, promise3];Promise.any(promises).then(el => console.log(el));
 //I will come first
```

如果要等待所有承诺或者等待所有服务响应怎么办？如果您不想移动到下一行代码，直到所有服务响应都来自服务，该怎么办？

我们可以用户 **Promise.all()**

```
const promise1 = new Promise(resolve =>
    setTimeout(resolve, 50, 'I will come first')
);
const promise2 = new Promise(resolve =>
    setTimeout(resolve, 100, 'I will come second')
);
const promise3 = new Promise(resolve => setTimeout(resolve, 1000, 'I am last'));
const promises = [promise1, promise2, promise3];Promise.all(promises).then(el => console.log(el));
//["I will come first", "I will come second", "I am last"]
```

(注意:根据您正在使用的框架，您可以使用 async/await 或 rxjs)

## 3.Weakref

"这个对象持有对另一个对象的弱引用，而不会阻止该对象被垃圾回收."

[](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakRef) [## WeakRef - JavaScript | MDN

### WeakRef 对象允许您持有对另一个对象的弱引用，而不会阻止该对象获取…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakRef) 

## 4.终结注册表

"当一个对象被垃圾回收时，你可以请求回调."

[](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/FinalizationRegistry) [## finalization registry-JavaScript | MDN

### FinalizationRegistry 对象允许您在对象被垃圾回收时请求回调。终结注册表…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/FinalizationRegistry) 

## 5.逻辑运算符

逻辑 OR 赋值(a ||= b)运算符仅在 a 为 false 时赋值。

```
const test = {
    val: 100,
    title: ''
};test.val || = 10;
console.log(test.val);
// expected output: 100test.title || = 'nothing inside';
console.log(test.title);
// expected output: "nothing inside"
```

逻辑 AND 赋值(a &&= b)运算符仅在 a 为真时赋值。

```
let val1 = 10;
let val2 = 0;val1 && = 20;
console.log(val1);
// expected output: 20val2 && = 40;
console.log(val2);
// expected output: 0
```

## 6.数字分隔符

这有助于提高数字的可读性。

```
const data = 1000000000000;const data = 1_000_000_000_000;
```

它对二进制、八进制和十六进制数字也很有用。

```
const data1 = 0b1010_0101; // binary
const data2 = 0o2_3_5_4; // octal
const data3 = 0xA_B_C_D_F; // hex
```

## 7.国际机场。列表格式

此方法可用于特定于语言的格式设置。

```
const data = ['test1', 'test', 'test3'];
const formattest1 = new Intl.ListFormat('en', {
    style: 'long',
    type: 'conjunction'
});console.log(formattest1.format(data));
// expected output: "test1, test, and test3" const formattest2 = new Intl.ListFormat('en', {
    style: 'narrow',
    type: 'unit'
});console.log(formattest2.format(data));
// expected output: "test1 test test3"
```

## 8.国际机场。日期时间格式

这对于特定语言的日期格式很有帮助。

```
const date = new Date("6/9/2021");
console.log(new Intl.DateTimeFormat('en-US').format(date));
// expected output: "6/9/2021"// can specify date and time format
console.log(new Intl.DateTimeFormat('en-GB', {
    dateStyle: 'full',
    timeStyle: 'long'
}).format(date));// "Wednesday, 9 June 2021 at 00:00:00 GMT-4"
```

# 延伸阅读:

*更多内容请看*[*plain English . io*](http://plainenglish.io/)