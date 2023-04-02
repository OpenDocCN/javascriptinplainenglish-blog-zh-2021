# JavaScript Async 和 Await——您的异步伙伴

> 原文：<https://javascript.plainenglish.io/javascript-async-and-await-your-asynchronous-buddies-516fb5b1750?source=collection_archive---------7----------------------->

![](img/ef2015e31eac81ec9b21103b409a1c8a.png)

Photo by [Niels Kehl](https://unsplash.com/@photographybyniels?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

`async`和`await`关键字帮助我们更方便地处理[承诺](https://jscurious.com/a-brief-guide-to-promises-in-javascript/)，比使用`then()`和`catch()`的常规承诺处理更具可读性。

让我们看看如何使用`.then()`和`.catch()`来消费承诺。

```
let flag = true;let promise = new Promise((resolve, reject) => {
    setTimeout(() => {
      if(flag) resolve('I am resolved');
      else reject(new Error('I am rejected'));
    }, 1000);
});promise.then(res => console.log(res)).catch(err => console.log(err));
// I am resolved
```

上面的承诺可以用下面这样的`async`和`await`来消费。

```
async function demo() {
    let promise = new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve('I am resolved');
        }, 1000);
    });

    let res = await promise;
    console.log(res);  // I am resolved
}demo();
```

> *`*await*`*关键字只能在* `*async*` *函数中使用。**

# *异步关键字*

*如果我们在任何函数前使用`async`,那么函数将返回一个承诺。如果函数没有显式返回任何承诺，那么它将隐式地将承诺包装在返回值周围。让我们看一个例子。*

```
*async function greet() {
    return 'Welcome';
}greet().then(res => console.log(res));
// Welcome*
```

# *await 关键字*

*关键字`await`等待一个承诺，并暂停该行中的代码，直到承诺得到解决。记住 await 关键字应该总是在`async`函数中使用，否则它将抛出一个错误。*

```
*async function foo() {
    let promise = new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve('I am resolved');
        }, 1000);
    });let res = await promise;
    console.log(res);
    console.log('end');
}foo();
// I am resolved
// end*
```

*这里，代码执行在使用`await`的那一行暂停，并在承诺完成时继续执行。因此，在 1 秒钟后，承诺将被解决，控制台声明将被打印。*

# *处理错误*

*我们可以使用 [try…catch](https://jscurious.com/javascript-error-handling-using-try-catch/) 块来处理`async` / `await`中的错误。*

```
*async function foo() {
    let promise = new Promise((resolve, reject) => {
        setTimeout(() => {
            reject(new Error('I am rejected'));
        }, 1000);
    });try {
        let res = await promise;
        console.log(res);
    } catch (e) {
        console.log(e);
    }
}foo();
// Error: I am rejected*
```

# *参考*

*   *[JavaScript 中的承诺](https://jscurious.com/a-brief-guide-to-promises-in-javascript/)*
*   *[JavaScript 中的回调函数](https://jscurious.com/callback-functions-in-javascript/)*
*   *[使用 try…catch 的 JavaScript 错误处理](https://jscurious.com/javascript-error-handling-using-try-catch/)*

**更多内容请看*[***plain English . io***](http://plainenglish.io)*