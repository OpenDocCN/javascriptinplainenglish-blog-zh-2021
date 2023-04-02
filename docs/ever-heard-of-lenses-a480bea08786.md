# 听说过镜片吗？

> 原文：<https://javascript.plainenglish.io/ever-heard-of-lenses-a480bea08786?source=collection_archive---------8----------------------->

## 透镜被用在函数式编程中，你可能在没有注意到的情况下使用它们！

![](img/a5be3c0838b20ce0e6aca06d5225e3b0.png)

Photo by [James Bold](https://unsplash.com/@jamesbold?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

# 定义

根据这个比喻，镜头允许我们聚焦于更大的物体(`V`)的特定部分(`U`):

# 请用案例！

在**不变性**的背景下更新对象的子部分时，镜头尤其有用。

在下面的例子中，我们只愿意更新一个`car`的`speed`。写`car.speed = { value: 60, unit: "km/h" };`将**不能**工作，因为`car`，内存中对`Car`对象的引用，是不变的。这样做，我们简化了变更检测机制(例如，如果使用 Redux)。

一个`Lens<Car, Speed>`只允许处理和更新`speed`，同时返回一个全新的`car`对象:

# 镜头容易构图！

![](img/0990eafa24fdf7d38109ae4fb77d79a5.png)

Photo by [Jakob Owens](https://unsplash.com/@jakobowens1?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

为了建造“更强”的透镜，可以使用管道透镜:

在前面的例子中，我们关注的是`speed`。但是现在，在`Speed`对象中，我们想关注它的值，假设单位保持不变。因此，我们创建了第二个镜头，并结合两个镜头:

```
Car --(focusOnSpeed)--> Speed --(focusOnValue)--> number
Car --(focusOnSpeedValue)--> number
```

# 减速器让事情变得更加有趣！

作为一种以不可变方式更新`State`的方式，Reducers 在函数式编程中被广泛使用。换句话说，它们允许计算一个更新的状态，而无需进行最终的突变(`state = updatedState`)。

看起来，透镜与渐缩管组合得非常好:

这有什么用？同样，在下面的例子中，它允许我们为一个`car`的唯一`speed`属性编写一个 reducer，并且最终仍然得到一个全新的`Car`对象:

# 这有印象吗？

Redux `combineReducers`，对！

看官方 [Redux 文档](https://redux.js.org/api/combinereducers)怎么说:

> 随着你的应用程序变得越来越复杂，你会想把你的 reducing 函数拆分成单独的函数，每个函数管理状态的独立部分。`combineReducers`辅助函数将一个值为不同减函数的对象转换成一个可以传递给`createStore`的减函数。

让我们好奇的看一下`combineReducers`(从第 181 行开始的[，来自 GitHub 上的 Redux’repository)背后的代码:](https://github.com/reduxjs/redux/blob/5855f71a43ce4a701b7e6ed1dbc083db83b766d7/src/combineReducers.ts#L181)

看到了吗？这正是我们对镜头所做的，尽管这里没有提到抽象。

就是这样！镜头是函数式编程的基本工具之一。我很高兴收到您的回复，因为我想您会发现大量的用例！

# 进一步阅读

*   [https://github.com/mathieueveillard/lenses](https://github.com/mathieueveillard/lenses)
*   [https://medium.com/javascript-scene/lenses-b85976cb0534](https://medium.com/javascript-scene/lenses-b85976cb0534)

*更多内容请看*[***plain English . io***](http://plainenglish.io/)