# Redux-Saga 入门的 9 步计划

> 原文：<https://javascript.plainenglish.io/getting-started-with-redux-saga-fbcb76126f1f?source=collection_archive---------14----------------------->

![](img/9d13ac7d9fccd1229e84802219e17d07.png)

当你听到 Redux 的时候，你首先想到的可能是全球商店。没错，但是 Redux 在一个项目中的实现方式有很多种。

今天，我们将主要关注 Redux-Saga。

![](img/68ed5b042f9f5ea91bceeb6dc7d4c54e.png)

Photo by [Gia Oris](https://unsplash.com/@giabyte?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在深入 Redux-Saga 之前，我们先了解一下 Redux 是什么。

Redux 是一个状态容器，允许应用程序的任何部分以一致的方式访问/修改状态变量。

那是什么意思？

![](img/da5eff980ff12206beaeba080c3c4494.png)

Photo by [Kelsey Chance](https://unsplash.com/@kchance8?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

让我们想象一下，你在你的房子里，和你的朋友们开派对。你有一个由不同食物组成的厨房，你和你的朋友可以根据需要去拿。当你从厨房拿食物时，你实质上是在改变厨房的状态。当你意识到厨房食物不足时，你可以去冰箱给厨房储备食物。

以类似的方式，Redux 允许我们检索和修改多个组件共享的全局值。这些组件就像我们的朋友一样，都试图访问同一个全球商店，也就是我们的厨房。与此同时，他们还可以为我们的全球商店重新进货，改造我们的“厨房”，用更多的食物填满它。

现在简单说一下 Redux-Thunk 和 Redux-Saga 的表现。

我们来看看下面的流程:

*动作创建者- >动作- >分派- >减少者- >全局状态- >动作创建者*

…等等。

如果你想知道更多关于如何设置 Redux 的细节，请阅读这篇文章:

[](https://medium.com/weekly-webtips/what-is-redux-and-how-data-flow-within-redux-fb675900fed1) [## 什么是 Redux，数据如何在 Redux 中流动

### 没错！储物应该是你想到的第一个词。

medium.com](https://medium.com/weekly-webtips/what-is-redux-and-how-data-flow-within-redux-fb675900fed1) 

简而言之，程序中有动作创建者，它们是执行某种动作的函数(API 调用、显示加载指示器等)。一旦完成，我们就向 reducer 发送一个动作。

缩减器更新全局状态，任何使用全局状态的组件都会立即看到变化。

![](img/bc56c131b0c462f23f77b344d761df98.png)

Photo by [Kelly Sikkema](https://unsplash.com/@kellysikkema?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

容易记住对吗？再来看看 Redux-Saga。

*视图层- >动作- > saga 中间件- >全局存储- >视图层*

…等等。

它与我们拥有的 Redux Thunk 非常相似。然而，中间件理解和处理动作的行为是不同的。

为了理解其中的区别，让我们从一个 Redux-Saga 项目开始。

**第一步:**运行`npx create-react-app sample-redux-app`

**第二步:**运行`npm install — save react-redux redux redux-saga`

这些将是为项目实现 Redux-Saga 所需的库。

**步骤 3:** 运行`npm install`来完成项目所需的其余包的设置。

**第 4 步:**转到 **src/index.js** ，用以下内容替换代码:

在这里，我们通过提供者包装整个应用程序，提供应用程序 redux 功能。

**第五步:**转到 **src** ，创建一个名为 **store** 的文件夹。在该文件夹中，创建一个名为 **configureStore.js** 的文件，内容如下:

在这里，我们创建中间件层，并使用我们的根 reducer 创建一个全局存储，根 reducer 是这个应用程序中所有 reducer 的组合。

注意这里有一条线叫做`sagaMiddleware.run(rootSaga)`。在 Redux-Saga 中，调度操作是通过生成器处理的。

我们这么想吧——在 Redux-Saga 中，有 watcher 函数。除了拉动未来的动作，他们实际上不做任何事情。它们相当于监听器函数，知道在触发时调用哪个调度函数。我们将在本文后面进一步讨论这一点。

**第六步:**转到 **src** 创建一个名为 **sagas** 的文件夹。创建一个名为 **rootSaga.js** 的文件，内容如下:

这里的这个文件包含一个观察器(或者监听器，如果更直观的话)函数，它可以监听所有其他的传奇故事。现在让我们看看其他的传奇文件。

**第七步:**转到 **src/sagas** ，创建一个名为 **category.js** 的文件:

**第 8 步**:现在转到 **src/sagas** ，创建另一个名为 **count.js** 的文件:

在这里，我们创建了观察器函数— watchCategorySagas 和 watchCountSagas。这些功能将被合并到一个 rootSaga 中，由主应用程序监听。

嗯…听？我们在说什么？

让我们修改一下 **app.js** ，并加入一些使用这些 saga 函数的例子。

**第九步:**转到 **src** ，用以下内容修改 **app.js** :

在这里，用户可以单击“+”或“-”，这将触发“向上计数”或“向下计数”类型的调度操作。当一个动作被触发时，sagas 中的 watcher 函数监听并将该动作映射到将被调用的函数。

让我们来看看来自 **src/sagas/count.js** 的这段代码:

当调度函数触发' COUNT_UP '时，调用 countUpAsync 函数。countUpAsync(或 countDownAsync)是修改 redux 状态的部分。

你可能会想，如果我们有 Redux-Thunk，那么为什么还要使用 Redux-Saga 呢？反之亦然。有了 Redux-Saga，继续使用 Redux Thunk 还有意义吗？

让我们这样来看一下 Redux-Thunk:您调用了一个动作创建器函数。它将调用一个 API，并根据 API 的结果更新全局状态。动作调度器和 API 逻辑在一个动作调度器功能中混合使用。

另一方面，Redux-Saga 需要很好地了解发生器和 redux/saga 效果函数是如何工作的。

什么是效果函数？这些效果函数包含一些要由中间件解析的信息。它告诉中间件，当观察器函数接收到一个动作时，调用回调时应该采用什么行为。

![](img/d4653f1c656e4d79180726ea7b8386ac.png)

Photo by [Kévin JINER](https://unsplash.com/@kevinjiner?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

那么，使用 Redux-Thunk 与 Redux-Saga 相比有哪些优势？

对于一个初学者项目来说，Redux Thunk 非常容易学习，特别是如果你想一开始就学习 reaction。您需要关心的只是一个动作创建器，它既可以进行异步调用(主要是 API 调用)，也可以将动作发送到中间件，然后由中间件更新存储。视图利用选择器从存储中读取并显示数据——仅此而已。

另一方面，Redux-Saga 有很多有用的助手功能，这些功能都是由 redux-saga/effects 提供的。这些函数使我们能够管理副作用，例如使异步调用更容易以更可预测的方式访问和管理。此外，测试更容易，因为生成器逻辑与所有异步调用逻辑以及更新状态的逻辑是分开的。

您应该使用哪一种？这要由你来决定。

*更内容于* [*通俗易懂*](http://plainenglish.io/)