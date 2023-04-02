# JavaScript 中承诺的简要指南

> 原文：<https://javascript.plainenglish.io/a-brief-guide-to-promises-in-javascript-226f33f5230e?source=collection_archive---------14----------------------->

![](img/fa08ef5195bc4ff0021aeb5428e64e27.png)

Photo by [James Harrison](https://unsplash.com/@jstrippa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 中的`Promise`是一个在异步操作完成后返回结果的对象。承诺的结果可以是成功，也可以是失败。

承诺有三种状态。

*   待定—承诺还没有结果。
*   履行——承诺已经完成。
*   拒绝-承诺已被拒绝。

```
let promise = new Promise((resolve, reject) => {
    const number = Math.round(Math.random() * 10);
    if(number <= 5) {
        resolve('Success');
    } else {
        reject(new Error('Failed'));
    }
});
```

为了创建一个`Promise`，我们使用带有`new`关键字的`Promise()`构造函数。`Promise()`构造函数接受一个名为“executer”的回调函数，该函数接受两个参数，即 resolve 和 reject。

我们需要在 executer 函数获得结果时调用`resolve()`函数，在有错误时调用`reject()`函数。

现在，为了使用`Promise`，我们使用`Promise`方法，如`then()`、`catch()`和`finally()`。

# Promise.then()

`then()`方法可以接受两个回调函数，第一个在`Promise`被解析时执行，第二个在`Promise`被拒绝时执行。

```
function getPromise(isTrue) {
    return new Promise((resolve, reject) => {
        if(isTrue) {
            resolve('Success');
        } else {
            reject(new Error('Failed'));
        }
    });
}getPromise(true).then(
    response => console.log('Promise is resolved with result = ' + response),
    error => console.log('Promise is rejected with error = ' + error.message)
);
// Promise is resolved with result = SuccessgetPromise(false).then(
    response => console.log('Promise is resolved with result = ' + response),
    error => console.log('Promise is rejected with error = ' + error.message)
);
// Promise is rejected with error = Failed
```

如果我们想分别处理成功和失败的案例，那么我们可以只对成功使用`then()`，对失败使用`catch()`。

# Promise.catch()

`catch()`方法采用一个回调函数，当`Promise`被拒绝时执行该函数。

```
function getPromise(isTrue) {
    return new Promise((resolve, reject) => {
        if(isTrue) {
            resolve('Success');
        } else {
            reject(new Error('Failed'));
        }
    });
}getPromise(false)
.then(response => console.log('Promise is resolved with result = ' + response))
.catch(error => console.log('Promise is rejected with error = ' + error.message))
// Promise is rejected with error = Failed
```

如果我们同时在`then()`和`catch()`中处理错误，那么一旦出现错误，只有`then()`内部的错误处理程序执行，而不是`catch()`内部的处理程序。

```
let promise = new Promise((resolve, reject) => {
    reject(new Error('An error occurred'));
});promise.then(null, () => console.log('Error caught inside then'))
.catch(() => console.log('Error caught inside catch'))
// Error caught inside then
```

如果在`then()`的错误处理器中出现任何错误，那么它将在`catch()`中被捕获。

```
let promise = new Promise((resolve, reject) => {
    reject(new Error('Error occurred in Promise'));
});promise.then(null, 
    err => {
        console.log('Error caught inside then, message: ' + err.message);
        throw new Error('Error occured in then');
    })
.catch(err => {
    console.log('Error caught inside catch, message: ' + err.message);
});// Error caught inside then, message: Error occurred in Promise
// Error caught inside catch, message: Error occured in then
```

# 无极. finally()

`finally()`方法接受一个回调函数，该函数在`Promise`被解析或拒绝后执行。

# 论成功

```
let promise = new Promise((resolve, reject) => {
    resolve('Success');
});promise.then(res => console.log(res))
.catch(err => console.log(err.message))
.finally(() => console.log('Executing Finally'));
// Success
// Executing Finally
```

# 失败时

```
let promise = new Promise((resolve, reject) => {
    reject(new Error('Failed'));
});promise.then(res => console.log(res))
.catch(err => console.log(err.message))
.finally(() => console.log('Executing Finally'));
// Failed
// Executing Finally
```

# 承诺链

我们可以通过链接方法`then()`、`catch()`和`finally()`一个接一个地执行一系列异步操作。

```
takeOrder()
.then(order => makeOrder(order))
.then(order => serveOrder(order))
.then(status => console.log(status))
.catch(err => console.log(err));
```

这里`takeOrder()`将返回一个在第一个`then()`方法中使用的`Promise`。`makeOrder()`将返回一个将在第二个`then()`方法中消耗的`Promise`，而`serveOrder()`将再次返回一个将在第三个`then()`方法中消耗的`Promise`。如果任何承诺中出现任何错误，那么它将在`catch()`方法中被捕获。

# Promise.all()

`Promise.all()`方法将一个可重复的承诺作为输入，并返回一个`Promise`，当所有承诺都被解析或其中任何一个被拒绝时，该方法被解析。

```
function getPromise(delay) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve(delay + 100);
        }, delay);
    })
}Promise.all([getPromise(1000), getPromise(3000), getPromise(2000)])
.then(responses => console.log(responses))
.catch(error => console.log(error));
```

# 承诺.竞赛()

`Promise.race()`方法接受一个可重复的承诺，并返回一个`Promise`,一旦任何承诺被解析或拒绝，该方法就会被解析/拒绝。

```
let promise1 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('Promise 1');
    }, 1000);
});let promise2 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('Promise 2');
    }, 500);
});Promise.race([promise1, promise2])
.then(res => console.log(res)) // Promise 2
.catch(err => console.log(err));
```

## 你可能也喜欢

*   [理解 JavaScript 中的异步和等待](https://jscurious.com/understanding-async-and-await-in-javascript/)
*   [JavaScript 中的回调函数](https://jscurious.com/callback-functions-in-javascript/)
*   [用于过滤器搜索的 HTML 数据列表标签](https://jscurious.com/html-datalist-tag-for-filter-search/)
*   [JavaScript 获取 API 进行 HTTP 请求](https://jscurious.com/javascript-fetch-api-to-make-http-requests/)
*   [20 种节省你时间的 JavaScript 速记编码技巧](https://jscurious.com/20-javascript-shorthand-techniques-that-will-save-your-time/)

*更多内容请看*[***plain English . io***](http://plainenglish.io)