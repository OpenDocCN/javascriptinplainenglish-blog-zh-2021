# 在 JavaScript 中玩弄承诺，然后等待

> 原文：<https://javascript.plainenglish.io/playing-with-promises-then-and-await-in-javascript-75f4b5372f4d?source=collection_archive---------15----------------------->

## 承诺能为我做什么？

![](img/155c8e6a67a8de41f6a179a2c1c9fc31.png)

Photo by [Joshua Aragon](https://unsplash.com/@goshua13?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 我们不喜欢等待！

人类不喜欢等待。如果有可能，我们在等待的时候也在做其他的事情。

JavaScript 中的**承诺**也可以用同样的方式来思考。承诺是一项工作加上一个结果，当工作完成时就会被激发。

**承诺的核心是定义工作。**当这个**工作完成后，**承诺返回一个**“已解决”。同时，你可以做或让别人做事情。…嘣！…** 这是 **Async(异步)！**

# 但是为什么要承诺呢？

在我们更仔细地研究承诺之前，让我们简单地讨论一下**原因:**等待任务完成是从**很早就在**的 JavaScript 中引入的。为此，使用了机制**“回调”**。

回调是一个简单的普通函数，它将被完成的作业调用**。每个 JavaScript 初学者都知道这一点:**

```
setTimeout(callback, 1000);
```

“回调”是一个在 1000 毫秒后调用的函数。是的… **它是异步的。好吧，没有工作。让我们把 1000 毫秒当作一项工作来做。**

```
function callback() {
   console.log("Auf Wiedersehen!");
}
setTimeout(callback, 1000);
console.log("Guten Tag!");// Guten Tag!
////.. is waiting 1000 milliseconds
// Auf Wiedersehen!
```

**简单！…和异步！**

# 问题是

但是如果**是一个有特定时间的任务**并且**之后有另一个有特定时间的任务**并且**之后有另一个有特定时间的任务** …并且…并且…然后我们需要注意**全部完成**:

```
setTimeout(() => {
  setTimeout(() => {
    setTimeout(() => {
      setTimeout(() => {
        setTimeout(() => {
          setTimeout(() => {
            console.log("Fertig!");
          }, 1000);
        }, 1000);
      }, 1000);
    }, 1000);
  }, 1000);
}, 1000);
console.log("Und los:");
// Und los:
//// waiting for 6 seconds
// Fertig!
```

**《回调地狱》还是《末日金字塔》！**形象更大的工作岗位！机器可以读取。对人类来说不是最好的。为了避免这个死亡金字塔，我们可以使用承诺。

# 让我们去寻找承诺

让我们和 **setTimeout** 呆一会儿。好了，这里没有**的本机代码**对**的 setTimeout** 作为承诺。但是我们可以对它做一点修改:

```
const job = resolve => setTimeout(resolve, 1000);
const myPromise = () => new Promise(job);
```

有一个**工作**和一个**承诺**。工作是承诺的核心。该作业是一个带有参数“ **resolve** ”的函数。工作是**在工作完成后**调用参数“解决”**。该参数是回调。**

好的，这里真的有一些函数并且我也使用了现代的 [**箭头函数符号**](https://javascript.info/arrow-functions-basics) …我以旧的 JavaScript 风格形成它。那可能会有一点帮助。

```
function myPromise(){
    function job(resolve){
        setTimeout(resolve, 1000);
    }
    return new Promise(job)
}
```

# 让我们玩诺言吧

现在我们可以**稍微玩一下**。示例:JavaScript 在调用 myPromise 时**不会等待。**

```
console.log("Und los:");
myPromise();
myPromise();
myPromise();
myPromise();
myPromise();
myPromise();
console.log("Fertig!");
// Und los:
//// not waiting for
// Fertig!
```

**这是真正的异步。**承诺产生了。并且代码**立即准备好**。承诺范围内的工作得到了很好的履行。

如果 JavaScript 也不等待，我们为什么还需要**那些承诺？我们是否也可以使用**回调**？默认情况下，JavaScript 不会等待**。这很好，因为承诺起了作用。如果我们希望 JavaScript 等待每一个，那么我们**需要明确地告诉 JavaScript:******

```
console.log("Und los");
await myPromise();
await myPromise();
await myPromise();
await myPromise();
await myPromise();
await myPromise();
console.log("Fertig")
// Und los:
//// is waiting for 6 seconds
// Fertig!
```

**单词**“await”**让**停止 JavaScript 代码，等待解析**承诺。这也更容易阅读。**

# **Await 不是异步的？！**

**最后，确实如此。**但是**承诺能做的**更多。**当作业在承诺中执行时，承诺的值为**“待定”**。一个**“Await”**等待，直到**未决被解决**。“await”的反义词是每个承诺都有**属性“then”**。然而，只有当我们将上述过程变得更加复杂和更加异步时，这才变得令人兴奋。**

```
const randomTimer = () => {
  const ms = Math.round(Math.random() * 5000);
  const job = resolve => setTimeout(() => resolve(ms), ms);
  return new Promise(job);
};
```

**函数 **"randomTimer"** 返回一个**作业**内的**承诺**，该**在一个**随机时间内以毫秒**(毫秒)为单位解决**。对于初学者:在第一行，你有一个**随机数“ms”**的定义。在第二行，将“**作业”**包装成一个函数，其参数是“ **resolve** ”(这是另一个函数..一个**回调**)。setTimeout 现在有一个函数作为第一个参数，它调用回调函数**“resolve”**，并以“**ms”**作为参数。好吧，这对于初学者来说并不容易。但是检查一下，然后继续。**

# **这个“然后”真的是异步的！**

**接下来，我们需要一个消费者。**假设这是一个女孩，正在等待随机定时器:****

```
const girl = promise => {
  promise.then(result =>
    console.log(`I'm the girl and I waited for ${result / 1000} seconds`)
  );
};
```

**…还有一个男孩也是:**

```
const boy = promise => {
  promise.then(result =>
    console.log(`I'm the boy and I waited for ${result / 1000} seconds`)
  );
};
```

**现在我们可以做这样的事情:**

```
girl(randomTimer());
// I'm the girl and I waited for 3.065 seconds
```

****每一个承诺**都有一个**然后**。如果承诺的**未决**已经**结束**，那么“将**被解雇**。“then”的自变量是一个带有自变量“**结果**的函数。这是来自“**random timer**”—“**ms**”的参数值。**

```
const girlTime = randomTimer();
girl(girlTime);
const boyTime = randomTimer();
boy(boyTime);
const timeForBoth = randomTimer();
girl(timeForBoth);
boy(timeForBoth);// I'm the girl and I waited for 0.74 seconds
// I'm the boy and I waited for 0.74 seconds
// I'm the boy and I waited for 0.934 seconds
// I'm the girl and I waited for 3.42 seconds
```

**好的，**“time for both”。这是什么？**另一个**优点**的承诺。我们可以多次传递生成的承诺。一旦**待处理状态被解决**，即工作完成，解决将在各处被触发**。这意味着**“then”**将在**相同的应许所在的任何地方被调用。**
理论上，我们可以这样做:****

```
const girlTime = randomTimer();
girl(girlTime);
girlTime.then(() => console.log("girl time is over"));
const boyTime = randomTimer();
boyTime.then(() => console.log("boy time is over"));
boy(boyTime);
const timeForBoth = randomTimer();
girl(timeForBoth);
timeForBoth.then(() => console.log("both time is over"));
boy(timeForBoth);//I'm the girl and I waited for 0.864 seconds
//girl time is over
//I'm the girl and I waited for 1.763 seconds
//both time is over
//I'm the boy and I waited for 1.763 seconds
//boy time is over
//I'm the boy and I waited for 4.038 seconds
```

# **代码**

**我们来看看**全代码:****

```
const init = async () => {
  console.log("Start");
  const girlTime = randomTimer();
  girl(girlTime);
  girlTime.then(() => console.log("girl time is over"));
  const boyTime = randomTimer();
  boyTime.then(() => console.log("boy time is over"));
  boy(boyTime);
  const timeForBoth = randomTimer();
  girl(timeForBoth);
  timeForBoth.then(() => console.log("both time is over"));
  boy(timeForBoth);
  await Promise.all([boyTime, girlTime, timeForBoth]);
  console.log("All Promises done");
};const randomTimer = () => {
  const ms = Math.round(Math.random() * 5000);
  const job = resolve => setTimeout(() => resolve(ms), ms);
  return new Promise(job);
};const girl = promise => {
  promise.then(result =>
    console.log(`I'm the girl and I waited for ${result / 1000} seconds`)
  );
};const boy = promise => {
  promise.then(result =>
    console.log(`I'm the boy and I waited for ${result / 1000} seconds`)
  );
};await init();
```

# **什么是承诺？**

**promise 不仅仅是一个你可以**生成 Promise 对象(用 new Promise())** 的类。它还具有静态属性。这里，就是 **Promise.all(Array)** 。这很简单:Promise.all **接受一组承诺**，它本身就是一个承诺。正如我们在上面学到的，我们也可以用“await”等待**一个承诺。显式地，用 Promise.all(Array)我们等待所有其他的承诺。****

# **最重要的结论**

****JavaScript 是异步的，句号。**如果你想**保持 JavaScript 同步，**你**不会用这种计算机语言走远**。
**回调是一种经过验证的处理异步的方式**，但是它们已经**过时了。****

**回调和承诺的最大区别在于回调必须总是在实际异步作业之前**创建。之后，您**不能再次更改回调**。****

**承诺要灵活得多。一旦创建了承诺，它就可以**传递到任何其他位置。**一旦“未决”完成，异步作业中的“解决”被触发，**每个有承诺的人都会被通知。嘣！砰！****

****所以要学会承诺！****

**…但是，如果工作无法完成或工作陷入困境，会发生什么呢？当我有更多的关注者时，我会在其他地方了解更多。:)**

***多内容于* [***浅显易懂***](http://plainenglish.io/)**