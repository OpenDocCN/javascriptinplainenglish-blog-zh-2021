# JavaScript 中的继承与组合

> 原文：<https://javascript.plainenglish.io/inheritance-vs-composition-in-javascript-174142a25bc3?source=collection_archive---------13----------------------->

## 代码速赢

## 两种面向对象编程技术的简要比较。

![](img/36e636d925d353295023feb3e62b016b.png)

Photo by [Christian Crocker](https://unsplash.com/@christian_crocker?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

当我开始学习编码时，使用**继承**向我解释了面向对象编程，这是一种使用父子层次结构组织类的技术。子类从其父类获得**状态**和**行为**，然后可以添加额外的状态和行为，变得更加具体。

例如:

在上面的例子中，`Jedi`和`Sith`类都可以使用`forcePush`方法，因为它们都继承了它们共享的父类`ForceUser`的能力。然而，只有`Sith`类可以使用`forceChoke`方法，只有`Jedi`类可以使用`mindTrick`方法。

## *这种继承方式有什么好处？*

*   我不必重写`forcePush`方法，因为它会自动提供给`ForceUser`类的所有子类。
*   我创建了一个代码层次结构，清楚地表示了父母、子女和兄弟姐妹之间的关系。

但事实是，原力比这更微妙。我严格的等级制度不公平。

当我在高中玩*星球大战绝地武士:绝地学院*的时候，绝地大师凯尔·卡塔恩告诉他的学生，绝地武士拥有原力的所有能力。你如何使用这些能力决定了你的定位。

也就是说，我显然遇到了继承模型的问题。我无法创造一个能强行窒息的绝地。只有西斯类有那个能力。蹩脚。

如果我:

*   只需复制一些代码并将`forceChoke`方法添加到`Jedi`类中？
*   把`forceChoke`加到`ForceUser`类就行了？这样，绝地和西斯都继承了它？

这两种选择都有点糟糕。

第一个选项意味着我将有两个`forceChoke`的实现。如果我需要更新那个方法呢？我现在必须在两个地方做。我失去了唯一的真相来源。另外，我复制了代码。一般来说，这通常是值得避免的。

第二个选项意味着所有绝地和西斯都可以使用`forceChoke`。但是实际上有多少绝地武士需要这种能力呢？我现在给了所有绝地一种能力，他们中的大多数人永远不会使用。我正朝着“上帝对象”的方向前进——移动祖先的行为和状态层次，以便更多的子类可以继承它们。那是一个[码气味](https://en.wikipedia.org/wiki/Code_smell)。

这就是组合优于继承的论点出现的地方。

组合是指当你以这样的方式编写代码时，对象/类是按照它们能做什么来组织的，而不是试图完全决定/预测它们现在和将来是什么。

对于继承，当你第一次计划你的代码时，你必须做猜测。有了组合，你可以在不牺牲灵活性的情况下混合和匹配行为。

下面是一个使用函数合成的例子:

在上面的例子中:

*   我定义了一些函数，这些函数返回(作为对象文字)我想要组合在一起的行为。
*   我定义了一个`ForceUser`函数，给它传递了一个名字，并将这个名字保存在一个名为`state`的对象中。
*   `ForceUser`返回一个对象(使用 [spread 语法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax#spread_in_object_literals))，由我想要提供的行为组成。现在，`kyle`是一个拥有我想要的所有行为的对象。而且，由于一个[闭包](https://medium.com/swlh/quick-wins-with-code-closures-in-javascript-deda4113055c)，这些行为都可以永久地引用来自`state`对象的任何值。

我现在有了一个`ForceUser`的实现，只有它需要的行为。

我们不再受绝地、西斯等概念的限制。

我在互联网上已经看到了前面例子的很多变体。我很少发现在使用 ES6 类语法的同时使用复合的例子。

我想尝试一下如何做到这一点。如果这对你有帮助，很好。如果这冒犯了你的感情，我道歉。

在本例中:

*   我从定义一些函数开始，这些函数将行为作为对象文字返回。我决定将`state`重命名为`self`，不过，我会说到的。
*   我定义了一个`ForceUser`类。注意，我仍然将`forcePush`定义为该类的一个方法。那是因为我相当有信心一个`ForceUser`应该永远有那个能力。
*   为了添加额外的状态和行为，我在构造函数中做了一些设置工作。我创建了一个名为`addToClass`的方法，它接受状态或行为，并使用`this`关键字将其添加到类实例中。这是一种低级的帮助方法，当我创建一个类的实例时，它允许我从对象文字中添加状态或行为。
*   当`stateObj`被传递到`addToClass()`时，这是非常简单的。然而，当我传递`behaviorComposer`时，我传递的是一个回调函数。然后在构造函数内部调用它，并通过`this`传递该实例的上下文。这样，所有行为都可以访问状态。所以无论你在哪里看到引用的`self`，都等同于`this`。

我现在有一个`ForceUser`类，它将`forcePush`赋予每个人，其他行为可以按菜单添加。

我喜欢这种方法，但是`addToClass`方法与`ForceUser`完全无关。我觉得以某种方式分离出来是值得的，实际上我最终使用了继承。将较低级别的功能分离到它自己的父类中:

我更喜欢这个实现。使用继承来根据抽象层次分离逻辑，似乎是创建父子关系的一个不太好的理由。现在，我的`ForceUser`课感觉真的很精瘦。在这种情况下，我甚至不需要定义构造函数(有一个默认的用于派生类的构造函数)。

我还选择将我的`behaviorComposer`回调参数内联，而不是在我创建类实例的地方之外定义它。那只是个人喜好的事情。

# 离别的思绪

*   我喜欢星球大战。
*   比起继承，我更喜欢作曲，但是两者可能都有时间和地点。
*   尽管如此，你还是应该坚持写作。希望这篇文章能帮助你理解这样做的一些方法。

感谢阅读！😄看看我在 quickwinswithcode.com 的一些早期文章

## 资源:

*   [码闻](https://en.wikipedia.org/wiki/Code_smell)
*   [传播语法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax#spread_in_object_literals)
*   [关闭](https://medium.com/swlh/quick-wins-with-code-closures-in-javascript-deda4113055c)

*更多内容请看*[***plain English . io***](http://plainenglish.io/)