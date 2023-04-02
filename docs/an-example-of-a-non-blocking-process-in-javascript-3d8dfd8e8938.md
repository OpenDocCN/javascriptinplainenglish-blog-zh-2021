# JavaScript 中非阻塞进程的一个例子

> 原文：<https://javascript.plainenglish.io/an-example-of-a-non-blocking-process-in-javascript-3d8dfd8e8938?source=collection_archive---------15----------------------->

## 通过示例了解如何使用回调和承诺创建非阻塞流程

![](img/5f8e11008c3fc985cda63a3ea3fb8086.png)

Photo by [James Harrison](https://unsplash.com/photos/vpOeXr5wmR4) on [Unsplash](http://unsplash.com)

JavaScript 是一种同步编程语言。这意味着它将从上到下按顺序执行您的代码块。但是多亏了 JavaScript 事件循环，我们能够通过使用回调函数和承诺函数来执行非阻塞过程。

这里有一些例子。

## 回调函数

```
// Example Parameter Function
const parameter = {
  firstName: 'John',
  lastName: 'Doe'
}// Example callback function (will run after delay function finish)
const callBackFunction = (result) => {
  console.log(result)
}// Example slow process or API call Function
const delayFunction = (callBack, parameter) => {

  // For replicate delay we use setTimeout as example
  setTimeout(() => {
    // Example slow process or api call return
    const result = `${parameter.firstName} ${parameter.lastName}`

    // Triggering the callback function after getting the result
    callBack(result)
  },1000)
}console.log('start')
// Run delay function
delayFunction(callBackFunction, parameter)
console.log('finish')// Output:
// Start
// Finish
// John Doe
```

## 承诺函数

```
// Example Parameter Function
const parameter = {
  firstName: 'John',
  lastName: 'Doe'
}// Example callback function (will run after delay function finish)
const callBackFunction = (result) => {
  console.log(result)
}// Example slow process or API call Function
const delayFunction = (parameter) => {
  return new Promise((resolve) => {

    // For replicate delay we use setTimeout as example
    setTimeout(() => {

    // Example slow process or api call return
    const result = `${parameter.firstName} ${parameter.lastName}`

    // Triggering the resolve promise after getting the result
    resolve(result)
  },1000)
  })
}console.log('start')
// Run delay function
delayFunction(parameter).then(callBackFunction)
console.log('finish')// Output:
// Start
// Finish
// John Doe
```

学习和使用非阻塞方法的好处是，您可以减少 JavaScript 主线程进程，提高代码性能，因此您的线程不会被阻塞，仍然可以运行剩余的每个进程。

在所有剩下的过程完成后，JavaScript 将检查事件循环，看看回调是否已经完成。完成后，它将运行回调函数。

## 结论

就这样，如果你觉得这篇文章有帮助，请在评论中告诉我们。也可以在[中](https://medium.com/@hanssagita)和 [LinkedIn](https://www.linkedin.com/in/hans-sagita/) 上关注我