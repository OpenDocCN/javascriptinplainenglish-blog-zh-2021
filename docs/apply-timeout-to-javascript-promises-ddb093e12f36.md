# 对 JavaScript 承诺应用超时

> 原文：<https://javascript.plainenglish.io/apply-timeout-to-javascript-promises-ddb093e12f36?source=collection_archive---------15----------------------->

## 何时以及如何对 JavaScript 承诺应用超时

![](img/7230fb026b3c011e19969b610d23a5ad.png)

JavaScript 承诺没有任何时间与之相关联。我们可以使用一个`.then()`函数，等待承诺被解决或拒绝。我们甚至可以等待它，如果异步任务在合理的时间内完成，这两种方法都可以。但是在任务可能需要很长时间的情况下，我们可能希望让用户知道。我们希望在这种情况下对 JavaScript 承诺应用超时。

幸运的是，有一个 [JavaScript Promise combinator 函数](https://www.wisdomgeek.com/development/web-development/javascript/javascript-promises-combinators-race-all-allsettled-any/)可以帮助我们做到这一点:

# 承诺.比赛

race 接受一系列承诺，并等待第一个承诺完成。先解决或拒绝的承诺将被返回。

例如:

```
const promise1 = new Promise((res) => setTimeout(() => res("promise1"), 1000));
const promise2 = new Promise((res, rej) => setTimeout(() => rej("promise2"), 500));const result = await Promise.race([p1, p2]);
// promise2
```

不管它是被解决还是被拒绝，结果都将是 promise 2，因为它首先完成。

同样值得一提的是，函数的参数是承诺。它也可以使用异步函数。

```
const asyncFunction = async (time, name) => {
 await new Promise((res) => setTimeout(res, time));
 return name;
}const result = await Promise.race(
  [asyncFunction(1000, "promise1"),
  asyncFunction(500, "promise2")
]);// promise2
```

# 对 JavaScript 应用超时承诺

利用上面的知识，我们可以通过使用 Promise.race 很容易地将 timeout 应用于 JavaScript promises。

我们将添加另一个承诺，在时间限制到达后拒绝。无论哪个承诺先完成，都将被归还。

```
const timeout = (promise, time) => {
  return Promise.race(
    [promise,
    new Promise((res, rej) => setTimeout(rej, time))]
  );
}
```

我们可以使用这个助手函数在任何需要的时候对 JavaScript 承诺应用超时:

```
// takes 100ms
const promiseFunction = async () => {
 await new Promise((res) => setTimeout(res, 100));
 return "promise";
}const result = await timeout(promiseFunction(), 1000);
// promise
// because it finishes before the timeout of 1000 ms// timeouts in 100 ms
await timeout(fn(), 50);
// error
```

同样值得一提的是，承诺不会被终止，它会继续执行，而承诺的结果会被丢弃。

# 处理错误

在上面的实现中，来自拒绝的错误和任何其他错误是不可区分的。因此，我们可以添加一个异常参数作为超时函数的输入，它将被用作拒绝值。然后，我们可以唯一地确定错误的原因，并相应地编写我们的处理逻辑。

我们还将使用 Promise.finally()为超时添加一个清除超时，以便对超时对象进行一些垃圾收集。

```
const timeout = (promise, time, exceptionValue) => {
 let timer;
 return Promise.race([
  promise,
  new Promise((res, rej) =>
                 timer = setTimeout(rej, time, exceptionValue))
 ]).finally(() => clearTimeout(timer));
}
```

这就是我们为 JavaScript 承诺添加超时所需要做的一切。如果你有任何问题，欢迎在下面留言。

*原载于 2021 年 6 月 10 日 https://www.wisdomgeek.com**的* [*。*](https://www.wisdomgeek.com/development/web-development/javascript/apply-timeout-to-javascript-promises/)

*更多内容请看*[***plain English . io***](http://plainenglish.io/)