# 让我们以简单的方式来理解 Redux

> 原文：<https://javascript.plainenglish.io/lets-understand-redux-in-a-simple-manner-da85f296cb49?source=collection_archive---------9----------------------->

![](img/fd9fd2f2148d9801c6de5705dbf3fdbe.png)

Photo by [Nubelson Fernandes](https://unsplash.com/@nublson?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Redux 只是一个 JavaScript 应用程序的状态管理库，仅此而已！但是它的样板有点难。但是，如果你理解了函数式编程背后的概念，那么你就很容易理解 Redux。

我假设您对函数式编程有所了解。我是 React 开发人员，我使用了 **useState()** 钩子来存储组件内部的数据。但是当我需要共享我的组件的数据时，我通常应用“ **prop drilling** 方法。问题是，当我的应用程序规模扩大时，我在管理状态时面临许多问题。所以，我尝试了 **Redux** 和**T7 的味道，我非常喜欢。**

> Redux 只是一个工具，它将你的应用程序数据集中在商店内，Redux 为你提供了一些管理商店的功能技术。

基本上，Redux 只会给你提供两样东西:

# A.商店

# B.商店管理模式

# **A .商店**

它只是一个 JavaScript 文件，名为 *store，*，你可以把你的应用程序的所有数据放在里面。

store.js

由于我是 React 开发人员，所以我在 React 中使用了 Redux。所以，我必须导入 Redux 功能。我进口了两样东西，

1.创建商店

2.组合减速器

**createStore** 将帮助我为我的应用程序创建一个商店。

**combineReducer** 将帮助我将整个应用程序的数据合并到一个对象中。

不要担心减速器到底是什么。

现在，你知道 Redux 中的商店是什么了。这就是关于商店的一切。

# **B .商店管理模式**

B 点对你来说可能有点挑战，但是别担心！我会尽我所能。

> 管理存储的范例——这意味着 Redux 将为您提供一些插入/删除/更新/读取存储数据的模式。

Redux 为你提供了管理商店的三件事:

1.  行动
2.  还原剂
3.  派遣

**1。动作**

Action 可以是您的 JavaScript 文件，您可以在其中定义管理商店时要执行的操作类型。

action.js

你可能会被上面的动作代码弄糊涂——这只是函数式编程，没有别的。一个函数只是返回一个对象，在这个对象中，我们只有两个属性:*类型*和*有效载荷。*

我们已经宣布了我们想为我们的商店采取什么样的行动。现在，该是 Reducer 的时候了。

**2。减速器**

Reducer 只是您商店数据的一部分，不多也不少。

> **Slice 是你的应用**中单个特性的 Redux reducer 逻辑和动作的集合

假设，我们有两种类型的车辆:一种是**汽车**，另一种是**公共汽车。**和两辆车都有不同的属性，我们希望将两辆车的数据保存在我们的商店中。为此，我们必须制作两个 reducers(数据片)来管理存储。

reducer.js

我们已经为我们的商店制作了第一个数据缩减器或数据片。我在这个 reducer 中只定义了一个动作，但是我们可以想写多少就写多少。但是最好的做法是将您的相关操作写在您的 reducer 中。

这个缩减器只是管理数据流，也就是说，数据将如何传递，以及数据将如何保存在我们的存储中。基本上，reducer 持有数据将如何变化的逻辑。reducer 到此为止。

**3。派遣**

它只是一个方法，只需要我们的行动，reducer 就会读取它并在我们的存储中进行更改。

ReactComponent.js

正如您在上面看到的，我们已经在 React 组件中导入了 Redux 操作，并通过传递我们的操作来调度它。正如我在下面的 **index.js** 文件中所做的那样，您必须通过您的存储才能访问 Redux 存储；否则，useSelector 挂钩将不起作用。

index.js

因此，动作、缩减器和分派——这三者管理我们的商店，这就是管理 Redux 商店的“**范例”。**

最后，这篇文章是关于 Redux 的。Redux 有很多有趣的地方，但对于初学者来说，这已经足够入门了。如果你有任何关于 Redux 的问题，我很乐意回答。

请阅读 Redux 的官方文档以获得更好的理解。

[](https://redux.js.org/introduction/getting-started) [## Redux | Redux 入门

### Redux 是 JavaScript 应用程序的可预测状态容器。它帮助您编写行为一致的应用程序…

redux.js.org](https://redux.js.org/introduction/getting-started) 

*更多内容看* [***说白了. io***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费每周简讯这里***](http://newsletter.plainenglish.io/) ***。***