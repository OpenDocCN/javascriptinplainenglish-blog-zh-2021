# JavaScript ES2021 中的“promise.any”和“promise.race”

> 原文：<https://javascript.plainenglish.io/promise-any-and-promise-race-in-es2021-3250733b48eb?source=collection_archive---------7----------------------->

## ES2021 中的新诺言功能— **《诺言.竞赛》**和**《诺言.任何》**

![](img/5e407ce4f49e6c4e5459125d565f1e41.png)

Working with Promise Any and Race (promise.any and promise.race)

TechnoFunnel 发表了另一篇关于 ES2021 中新的 Promise 特性的文章。我们将展示在您的应用程序中使用这些新函数的用法和好处。让我们创建一些承诺，并引入“ **promise.any** ”和“ **promise.race** ”关键字使其相同。

用 JavaScript 创造承诺:

[https://gist.github.com/Mayankgupta688/2223d8b21191db1e21428115d61366ee](https://gist.github.com/Mayankgupta688/2223d8b21191db1e21428115d61366ee)

在上面的代码中，我们使用“ **new promise** ”关键字创建了一个简单的 Promise，它将“resolve”和“reject”作为参数。一旦承诺被解析，我们可以进一步给承诺附加一个回调函数。

[https://gist.github.com/Mayankgupta688/797cb54fda86145714d485a54dd773fd](https://gist.github.com/Mayankgupta688/797cb54fda86145714d485a54dd773fd)

在上面的代码中，一旦承诺在 3 秒内被解决，回调函数就被触发。附加到 resolve 关键字的数据可供回调函数进一步处理。

[https://gist.github.com/Mayankgupta688/a24ab73ed4702c145f02611b439fe66b](https://gist.github.com/Mayankgupta688/a24ab73ed4702c145f02611b439fe66b)

# 拒绝承诺

类似于“解析”承诺，我们也可以拒绝承诺，并为其附加一个回调函数。当出现拒绝场景时，将调用传递给“then”关键字的第二个函数。

[https://gist.github.com/Mayankgupta688/a24ab73ed4702c145f02611b439fe66b](https://gist.github.com/Mayankgupta688/a24ab73ed4702c145f02611b439fe66b)

[https://codesandbox.io/s/currying-brook-9dd62?file=/src/index.js](https://codesandbox.io/s/currying-brook-9dd62?file=/src/index.js)

# 与多个承诺一起工作

让我们在代码中添加多个承诺，并尝试在不同的时间间隔解析这些承诺。我们将添加 4 个承诺，分别在间隔 3500、800、300 和 1000 后解决。

[https://gist.github.com/Mayankgupta688/35aca3941f20a326e13832032ecba4d2](https://gist.github.com/Mayankgupta688/35aca3941f20a326e13832032ecba4d2)

上面给出了添加到代码中的多个承诺。现在让我们看看“ **Promise.any** ”和“ **Promise.race** ”的用例场景。

# 使用“promise.any”

在这一节中，我们将看看使用“promise.any”的用例场景。

[https://gist.github.com/Mayankgupta688/f5284b5fa57c8045833b2e37ec4139d5](https://gist.github.com/Mayankgupta688/f5284b5fa57c8045833b2e37ec4139d5)

在上面的代码中，我们创建了 4 个不同的承诺，它们在不同的时间间隔后被解析。使用“ **promise.any** ”，如果任何一个承诺被解决，回调函数被调用。回调函数等待第一个承诺被解析，并使用从列表中第一个解析的承诺接收的数据调用回调函数。

从上面的承诺列表来看，“thirdPromise”是最先解决的承诺。一旦“第三承诺”将在 300 毫秒内解决，与“承诺.任何”相关联的回调函数将被调用，并且回调函数将包含由承诺三解决的数据。

简而言之，“ **promise.any** ”从数组中提到的承诺列表中查找首先解决的承诺。

[https://codesandbox.io/s/ancient-frog-o9po7?file=/src/index.js](https://codesandbox.io/s/ancient-frog-o9po7?file=/src/index.js)

# Promise.any for Reject 场景

让我们看看 300 毫秒后会发生的拒绝场景，这是提到的承诺列表中最快的解决或拒绝。

[https://gist.github.com/Mayankgupta688/1c3b4d7f24635455cbc01f3f1bf936be](https://gist.github.com/Mayankgupta688/1c3b4d7f24635455cbc01f3f1bf936be)

在上面的代码中，我们可以看到有一个承诺在 300ms 后被拒绝。在上述情况下，将为 800 毫秒后解析的“secondPromise”调用“promise.any”函数回调，而不是为列表中被拒绝的承诺调用。

[https://codesandbox.io/s/fervent-water-qn0wc?file=/src/index.js](https://codesandbox.io/s/fervent-water-qn0wc?file=/src/index.js)

# 使用“promise.race”

类似于“ **promise.any** ”，其中回调函数在成功解析或拒绝列表中的任何一个承诺时被调用。" **promise.race** "从承诺列表中寻找第一个解决或拒绝的承诺。

[https://gist.github.com/Mayankgupta688/7a35e62f904ce1fed4c68be735100033](https://gist.github.com/Mayankgupta688/7a35e62f904ce1fed4c68be735100033)

在上面的代码中，我们可以看到，在任何承诺得到解决或被拒绝之前，其中一个承诺被拒绝。一旦收到拒绝，就调用回调函数。“第三次承诺”被拒绝 300 毫秒后，将立即调用“ **promise.race** ”回调。

[https://codesandbox.io/s/practical-greider-pmizl?file=/src/index.js](https://codesandbox.io/s/practical-greider-pmizl?file=/src/index.js)

# 结论

“any”和“race”之间的基本区别在于，race 对已解析和已拒绝的承诺执行回调函数，而“any”函数在列表中第一次成功解析承诺时执行。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)