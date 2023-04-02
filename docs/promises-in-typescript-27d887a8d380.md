# 打字稿中的承诺

> 原文：<https://javascript.plainenglish.io/promises-in-typescript-27d887a8d380?source=collection_archive---------17----------------------->

![](img/03c2d84ace3c4d3e7e1805f6646c3ac0.png)

[Hopefully he has the candy you are looking for](https://pixabay.com/images/id-3047319/)

想象一下，你去店主那里买糖果。你要了一颗糖果，店主答应了(即承诺他/她会尽量给你一颗)。店主可能会花 15 秒或者 2 分钟找到你要的糖果，然后把它交给你。你下一步的行动取决于店主的反应。如果店主给你糖果，你付钱，然后吃掉它。如果店主说他们没有糖果，你可以要些别的或者继续。关键是在你采取任何行动之前，你要等待店主的承诺。这正是承诺在 TypeScript 中的工作方式。

假设您正在构建一个应用程序，其中您需要执行一个异步任务，并且您希望下一个代码块等到异步任务完成后再执行它。这就是承诺发挥作用的地方。

# 1.创造承诺

![](img/b67b4a2a1ff650934902ba9885ed106e.png)

[*Trying to find this candy is the Promise*](https://pixabay.com/photos/candy-sweetmeats-sweets-dessert-1961536/)

只需创建一个 promise 类的对象，并将 resolve 和 reject 函数作为参数传递给构造函数，就可以创建一个 Promise。在我们的类比中，这是我们店主的承诺。

> ***解决*** —承诺成功时。(店主找到了糖果。)
> 
> ***拒绝*** —承诺不成功时。(店主没有找到糖果。)

```
private tryToFindCandy(candyName: string): Promise<boolean>{
  let findCandyPromise = new Promise((resolve, reject) => {
    setTimeout(()=>{
      if(candyExists(candyName)){
         resolve(true);
      } else {
         reject(false)
      }
    }, 5000)
  }) 
  return findCandyPromise;
}
```

按照我们的类比，我们有一个名为 tryTo *FindCandy* 的函数，它返回*findCandyPromise*promise*。*承诺解决，糖果存在则拒绝，糖果不存在则拒绝。(这在 setTimeout 函数内部，使函数异步)

***注:*** *更实际的情况是，在 findCandyPromise 中会有一个 API 调用或文件读/写操作或任何类型的代码，需要一些时间来处理并获得响应。*

# **2。处理一个承诺**

![](img/316803f7a641aa8d1a70e17e9eb0d15e.png)

[One way to handle the returned promise](https://pixabay.com/photos/hunger-hungry-eating-cookie-413685/)

可以使用**然后*、* catch 最后**来处理承诺。

*   **然后** — *承诺完成的时候。(* ***注:承诺是解决了还是拒绝了并不重要。只要有一个响应我们就到达那么块*** *)。这里我们可以有两个回调函数，一个用于已解决的承诺，另一个用于承诺被拒绝的情况。*
*   **捕捉** — *当承诺遇到运行时错误。(就像一个试抓块)*
*   **最终**——*在执行完 then/catch 块后。(这用于执行一些需要在异步任务之后运行的操作，而不管异步任务中发生了什么。)*

我们的承诺会这样处理:

```
private buyAndEatCandy(): void {
  this.tryToFindCandy("Mars").then(res => {
    payAndEat();         **// The Shopkeeper found the candy**
  }, rej => {
    askForAnotherCandy();**// The Shopkeeper couldn't find the candy**
  }).catch(err => {
    console.log("Something weird happened"); **// Some Runtime Error**
  }).finally(() => {
    goHome();            **// After all is said and done. Go Home :)**
  })
}
```

恭喜你！现在你知道如何正确地创造和使用承诺。你可以用这个做很多事情。

一个函数可以调用多个异步函数。这就是承诺链和承诺分组的用武之地。

# **3。连锁承诺**

![](img/e8389ab5d49e6a3b803f9ccd5d579b0f.png)

[One link after the other](https://pixabay.com/photos/chain-link-metal-strong-connect-690088/)

回到我们的类比，假设你现在正在排队。店主现在必须给你一个承诺，完成它，转向下一个顾客，重复同样的事情。现在我们正在讨论一个接一个地运行多个异步任务。这就是承诺的连锁属性的来源。 ***注意，下一个异步任务只有在前一个任务完成后才运行。***

让我们在代码中加入承诺链:

```
private buyAndEatCandy(): void {
  this.tryToFindCandy("Mars").then(res => {
    payAndEat();
    this.tryToFindCandy("Bounty").then(res => { **// Next customer**
      payAndEat();
      this.tryToFindCandy("Tobelorone").then(res => { **// Next one**
        payAndEat();
      }
    }
  }
}
```

为了简单起见，这里我们已经放弃了拒绝和错误处理模块。

# 4.分组承诺

![](img/2cbe2e4417c135fd3a16ac92da2deaa4.png)

[Group your promises and keep them close](https://pixabay.com/photos/bonfire-camping-fire-flame-group-1867275/)

现在，让我们假设你正在治疗你的三个朋友，你把他们带来了。你们每个人心里都有不同的糖果。店主会倾听你们所有人的请求，向你们所有人承诺他会努力找到它，然后回来给你们所有人一个集体回复。**请注意，在你得到集体回应之前，需要完成所有的个人承诺。如果任何一个承诺被拒绝，你会得到一个集体拒绝。**

我们实现这一点的方法是创建一个充满这些承诺的数组。为了处理这个承诺数组，我们需要使用 promise 类的 all 方法来创建一个包含数组中所有这些承诺的新承诺。然后，我们可以在新创建的承诺上使用 Then、catch 和 finally。

让我们在代码中对一些承诺进行分组:

```
private findCandyByNames(candyNames: Array<string>): {
  let candyPromises;          **// This will hold all our promises**
  for (let index = 0; index < candyNames.length; index++){
    let candyName = candyNames[index];
 **// Now we push promise returned from tryToFindCandy method we 
    // created before to an array for each one of the candy names.**
    candyPromises.push(this.tryToFindCandy(candyName));
  }
 **// Return a promise using all** let newPromise = Promise.all();
 **// Handle newPromise like any other promise** newPromise.then((res)=>{
    **// When all promises are resolved**
    this.payAndEat();
  }, (rej)=>{
    **// When any of the promises is rejected**
    this.askForAnotherCandy();
  }).catch(err => {
    console.log("Some Runtime Error");
  }). finally(()=>{
    **// When all the promises are either resolved or one of them is    //rejected**
    this.goHome();
  })**;**
}
```

现在，您可以并行(通过分组)或顺序(通过链接)处理多个异步方法。这两者都是非常强大的工具，并且是处理多异步代码块的干净方法。

# **5。即时承诺解决方案**

![](img/1040628227e85ece2329d95759884640.png)

[Did someone say Instant?](https://pixabay.com/photos/polaroid-camera-instant-photography-1245924/)

你也可以立即解决或拒绝承诺，就像这样:

```
let resolvedPromise = new Promise.resolve();
let rejectedPromise = new Promise.reject();
```

这有一个非常合适的应用。其中一种情况是，您有一个函数，它有条件地执行一个异步任务并返回一个承诺。在这种情况下，即使异步代码不会运行，您也需要返回一个承诺。

关于承诺，这就是你需要知道的全部。只要确保你的店主信守承诺。没有人喜欢食言。