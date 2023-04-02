# 如何在疯狂计算的同时动态更新反应组件

> 原文：<https://javascript.plainenglish.io/how-to-dynamically-update-a-react-component-whilst-computing-like-a-maniac-8198b59f8a21?source=collection_archive---------1----------------------->

![](img/3f65dac70a17003954855c6f44042c34.png)

Photo by [Sammy Williams](https://unsplash.com/@sammywilliams?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我最近遇到了一个问题，我正在执行一个连续的计算，返回中间结果，我想实时显示在反应组件中。不管我怎么尝试，组件只会在计算的*结束*时更新，只有那时中间结果才会同时出现。

起初，我认为我错过了一些关于反应状态管理的东西，但是在遇到几个死胡同之后，我想到了在后台进行的密集处理不允许组件更新发生。幸运的是，我可以用几个非常简单的例子来说明这个问题(和一个解决方案)。

# 它应该如何工作

通常，人们通过内置于反应中的`useState()`机制来更新组件。让我们从一个显示列表的简单应用程序开始:

```
function App() {
  const [items, setItems] = useState(['x', 'y']); useEffect(() => {
    itemsGenerator(setItems);
  }, []) return (
    <div className="App">
      <header > HOWDY
        <MyList {...{ items }} />
      </header>
    </div>
  );
}
```

我用一个数组初始化一个名为`items`的状态，组件 MyList(未显示)显示`items`中的内容。这是基本的反应材料。

当组件被加载时`useEffect`钩子从我的项目“生成器”开始。我使用引号是因为它不是一个生成器*函数*(我在后面会讲到)。

```
const itemsGenerator = (setItems) => {
  arr.forEach((item) => {
    setTimeout(() => setItems((prevState) => prevState.concat(item)), 1000 * delayCt++)
  })
}
```

生成器使用`setTimeout()`以递增的时间间隔更新项目状态。当我运行这个程序时，我看到`MyList`每隔一秒钟一次添加一个新项目。太好了。

# 如何打破它

正如我之前所说的，在后台运行一个计算密集型的操作，这并不那么简单。可以创建一个生成器来连接 JavaScript 的单个事件循环。

```
const itemsGenerator2 = (setItems) => {
  var index = 0;
  while (index < arr.length) {
    const thenTime = Date.now()
    while (Date.now() - thenTime < 1000);  // tight wait loop
    const item = arr[index++] setItems((prevState) => prevState.concat(item))
  }
}
```

该功能与前一个发生器相同，每秒更新`items`状态。你会注意到这次它没有使用`setTimeout()`了:它只是紧循环运行，不断检查`Date.now()`直到第二次通过，同时迭代数组中的每个元素。

这不适用于实时更新`MyList`。不是每一个项目分开一秒钟添加到列表中，而是所有项目在三秒钟后出现在列表中。

# 如何修复它

处理 JavaScript 单线程的线程都因为`while`循环而被捆绑。没有时间处理 UI 事件了。解决方案是创建一个新线程，所有计算密集型的事情都在这里发生。这释放了事件处理。Web workers 是一种启动线程的简单方法，所以我将使用它们。

```
const itemsGenerator3 = (setItems) => {
  let worker = new Worker('itemsGenerator3.js')
  worker.postMessage('Go!')
  worker.onmessage = e => {
    if (/Kill me.*/.test(e.data)) {
      worker.terminate();
    } else {
      setItems((prevState) => prevState.concat(e.data))
    }
  }
}
```

这个新的生成器创建一个工作线程，告诉它“开始！”，并等待响应。除非工作人员要求终止，否则每个响应(假设为一个项目)都被附加到`items`状态。工作线程的代码(也叫做`itemsGenerator3,` **对不起**)驻留在网站上的一个公共文件夹中(**而不是**藏在应用程序源文件夹中)。

```
const arr = ["nnn", "ooo", "ppp", "qqq"];onmessage = e => {
  if (e.data !== 'Go!')
    postMessage("no go")
  else {
    var index = 0;
    while (index < arr.length) {
      const thenTime = Date.now()
      while (Date.now() - thenTime < 1000);  // tight wait loop
      const item = arr[index++] postMessage(item)
    }
    postMessage("Kill me! Kill me now!")
  }
}
```

工人等待“开始！”信息，然后起飞。它使用与前面的生成器相同的 tight while 循环，但不更新`items`状态；相反，它会向`itemsGenerator3()`呼叫者发送一条消息。当数组耗尽时，它会通知调用方，以便终止工作线程。

现在我的列表每秒更新一项。

# 如果我们使用一个真正的生成器函数会发生什么？

生成器函数有一个`yield`命令，它可能会让你认为它产生了事件处理线程，但事实并非如此——它产生了一个值，仅此而已。事实上，如果我尝试使用一个生成器函数，我会看到非常奇怪的事情发生。

```
function* itemTrueGenerator() {
  var index = 0;
  while (index < arr.length) {
    const thenTime = Date.now()
    while (Date.now() - thenTime < 1000);  // tight wait loop
    const item = arr[index++]
    yield item
  }
}const itemsGenerator4 = (setItems) => {
  const it = itemTrueGenerator()
  let item = it.next() while (!item.done) {
    const itemValue = item.value
    console.log({ itemValue })
    setItems(prevState => {
      console.log({ prevState, itemValue })
      prevState.concat(itemValue)
    }
    )
    console.log('next')
    item = it.next()
  }
}
```

`itemsGenerator4()`函数调用一个真正的生成器函数，使用那个可怕的 while 循环每秒产生值。唉，这真的把事情弄糟了。注意`itemsGenerator4()`中的`console.log()`语句。见证人:

```
App.js:56 {itemValue: 'nnn'}
App.js:56 {prevState: Array(2), itemValue: 'nnn'}
App.js:60 next
App.js:54 {itemValue: 'ooo'}
App.js:60 next
App.js:54 {itemValue: 'ppp'}
App.js:60 next
App.js:54 {itemValue: 'qqq'}
App.js:60 next
react-dom.development.js:3942 [Violation] 'message' handler took 4003ms
App.js:56 {prevState: undefined, itemValue: 'ooo'}
App.js:56 {prevState: undefined, itemValue: 'ooo'}
```

生成器工作正常，但是 setItems()调用…嗯，不太好。我很想告诉你这里发生了什么，但这超出了我的理解范围。如果我遇到一个好的解释，我会发布一个后续。

— —

这篇文章的源代码是这里的。