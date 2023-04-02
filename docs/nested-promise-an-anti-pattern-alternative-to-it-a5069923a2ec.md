# 嵌套承诺、反模式和替代方案指南

> 原文：<https://javascript.plainenglish.io/nested-promise-an-anti-pattern-alternative-to-it-a5069923a2ec?source=collection_archive---------2----------------------->

![](img/6978658db60996e144794c706cfa0e1e.png)

JavaScript 中的 Promise 是一种流行的设计模式，用于处理 Node.js 中的异步任务。它可以处理许多任务的并行/串行执行以及它们的链接规则。在我的[上一篇文章](/promise-in-javascript-with-all-the-methods-b7357196a57e)中，我们学习了承诺的基础知识以及常见的承诺实用方法。

在这篇文章中，我们将学习嵌套承诺和它们的替代品。不要再浪费时间了，让我们跳进嵌套的承诺。

## 嵌套承诺:

承诺为您提供了返回语句和错误抛出，而在延续传递方式下，您会丢失这些语句和错误抛出。嵌套 promise 是指在内部调用 child promise。然后是父母的承诺和这种继续。我们举个例子，一个开发者想先创建一个用户账号，然后是订阅信息，最后是订阅购买历史。这将看起来像这样:

```
return promise1.then(promise1_output=> {
 return promise2.then(promise2_output => {
  return promise3.then(promise3_output => {
   console.log(promise3_output) // this continue
  })
 })
})
```

在上面的代码中，promise2 仅在 promise1 解析时执行& promise3 仅在 promise2 解析时执行。在承诺嵌套中，当您在 then 方法中返回承诺时，如果返回的承诺已经被解决/拒绝，它将立即调用后续的 then/catch 方法，否则它将等待。如果承诺不返回，它将并行执行。

这些嵌套的承诺将从它们的外部范围访问变量，否则被称为“承诺金字塔”，它将向右增长。如果做得不正确，这个承诺金字塔最终会导致被称为 ***的承诺——回调地狱*** 。

在嵌套过程中，如果您忘记返回嵌套的承诺，将导致反模式，您的解析/拒绝不会冒泡到顶部。可能使承诺变得混乱的核心问题是没有正确地记录返回值，并且没有使用类似`Promise.all`的东西显式地阻止承诺解析。有了一连串的承诺，你应该考虑用`.finally`来清理逻辑，以防出错。有时候，嵌套承诺变得不可避免。这将不可避免地导致我们谈到的回调地狱，因此为了解决这个问题，ES7 提出了 Async/await。

## 嵌套承诺的替代方案:

Async/Await 是我们在语言中得到支持的承诺的扩展。这个特性基本上充当了承诺之上的语法糖，使得异步代码更容易编写和阅读。它们让异步代码看起来更像老派的同步代码。

**async** 关键字，你把它放在函数声明的前面，把它变成一个 [async 函数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)。调用异步函数返回一个承诺。这是异步函数的特点之一——它们的返回值肯定会被转换成承诺。异步函数的优势只有在与 **await** 关键字结合使用时才变得明显。`await`仅适用于常规 JavaScript 代码中的异步函数。

`await`放在任何基于异步承诺的函数前面，暂停该行代码，直到承诺实现，然后返回结果值。您可以在调用任何返回承诺的函数时使用`await`，包括 web API 函数。

让我们使用 async-await 重写嵌套的承诺

```
async function userInfo() {
 const promise1 = await new Promise((resolve, reject) => {
  resolve('USer account created!');
 });
 if (promise1) {
  const promise2 = await new Promise((resolve, reject) => {
   resolve('Subscription created!');
  });
  if (promise2) {
   const promise3 = await new Promise((resolve, reject) => {
    resolve('Subscription history created!');
   });
  }
 }
}
```

不需要在每个基于承诺的方法的末尾链接一个`.then()`块，只需要在方法调用之前添加一个`await`关键字，然后将结果赋给一个变量。`await`关键字使 JavaScript 运行时暂停执行该行代码，直到异步函数调用返回结果——如果后续代码依赖于该结果，这非常有用！

对于错误处理，可以使用带有`async` / `await.`的同步`try...catch`结构

```
async function userInfo() {
 try {
  const promise1 = await new Promise((resolve, reject) => {
   resolve('USer account created!');
  });
  ...
 } catch (err) {
  console.log(err)
 }
}
```

async/await 建立在 promises 之上，所以它兼容 promises 提供的所有特性。这包括`Promise.all()`——您可以等待一个`Promise.all()`调用，以一种看起来像简单同步代码的方式将所有结果返回到一个变量中。

```
async function promiseAllDemo() {
 try {
  const promise1 = Promise.resolve("hello world");
  const promise2 = "Promise 2";
  const promise3 = new Promise((resolve, reject) => {
   setTimeout(resolve, 100, 'foo');
  });
  const resolvedPromises = await Promise.all([promise1, promise2,  promise3])
} catch (err) {
  console.log(err)
 }
}
```

## 结论:

Async/await 提供了一种很好的、简化的方式来编写更易于阅读和维护的异步代码。

***感谢阅读。原载于 2021 年 6 月 2 日***[***https://noob 2 geek . in***](https://noob2geek.in/2021/06/02/nested-promise-an-anti-pattern-alternative-to-it/)***。***

*更多内容请看*[*plain English . io*](http://plainenglish.io/)