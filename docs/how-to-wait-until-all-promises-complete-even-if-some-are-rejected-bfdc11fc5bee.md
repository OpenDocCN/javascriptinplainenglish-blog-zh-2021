# 如何等到所有承诺完成即使有些被拒绝？

> 原文：<https://javascript.plainenglish.io/how-to-wait-until-all-promises-complete-even-if-some-are-rejected-bfdc11fc5bee?source=collection_archive---------10----------------------->

![](img/58560b63d7769f39950e7f8a197a9299.png)

Photo by [marcos mayer](https://unsplash.com/@mmayyer?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能想等到所有的承诺都完成，但我们可能想不管一些承诺是否被拒绝都继续下去。

在这篇文章中，我们将看看如何等到所有的承诺都完成，即使有些被拒绝。

# 承诺。都解决了

`Promise.allSettled`方法让我们继续运行`then`回调，而不管所有承诺是否完成。

例如，我们可以写:

```
Promise.allSettled([
  Promise.resolve(1),
  Promise.resolve(2),
  Promise.reject(3),
]).then(([result1, result2, result3]) => {
  console.log(result1, result2, result3)
});
```

那么`result1`就是`{status: “fulfilled”, value: 1}`。

`result2`是`{status: “fulfilled”, value: 2}`。

而`result3`就是`{status: “rejected”, reason: 3}`。

`status`拥有每个诺言的状态。

并且`value`如果承诺被解决，则具有解决的值。

如果承诺被拒绝，则`reason`具有被拒绝的值。

我们也可以用`async`和`await`语法编写相同的代码。

例如，我们可以写:

```
(async () => {
  const [result1, result2, result3] = await Promise.allSettled([
    Promise.resolve(1),
    Promise.resolve(2),
    Promise.reject(3),
  ])
  console.log(result1, result2, result3)
})()
```

对于`result1`、`result2`和`result3`，我们得到与之前相同的值。

# 承诺.全部带地图

我们可以在 promise 数组上调用`map`。

然后我们传入一个回调函数，该函数对任何被拒绝的承诺调用`catch`。

只有当承诺被拒绝时，`catch`回调才会运行，所以如果`catch`没有运行，我们要么返回承诺本身。

否则，我们通过`catch`回调运行返回一个承诺。

所以我们可以写:

```
Promise.all(
    [
      Promise.resolve(1),
      Promise.resolve(2),
      Promise.reject(3),
    ]
    .map(p => p.catch(e => e))
  )
  .then(([result1, result2, result3]) => {
    console.log(result1, result2, result3)
  });
```

我们用`p => p.catch(e => e)`调用`map`来返回任何被拒绝的承诺和一个被捕获的承诺。

在`catch`回调中，我们返回拒绝原因。

然后在`then`回调中，我们可以照常析构承诺结果。

所以我们得到`result1`是 1。

`result2`是 2。

而`result3`是 3。

我们可以用`async`和`await`编写相同的代码，方法是:

```
(async () => {
  const [result1, result2, result3] = await Promise.all([
      Promise.resolve(1),
      Promise.resolve(2),
      Promise.reject(3),
    ]
    .map(p => p.catch(e => e))
  )
  console.log(result1, result2, result3)
})()
```

我们得到了和以前一样的结果。

# 结论

`Promise.allSettled`方法是在承诺运行后运行代码的最佳方式，不管承诺运行的结果如何。

如果我们不想用那个，我们也可以将`Promise.all`与`map`和`catch`一起使用。

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)