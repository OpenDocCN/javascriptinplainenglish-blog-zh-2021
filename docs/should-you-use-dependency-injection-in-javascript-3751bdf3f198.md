# JavaScript 中应该使用依赖注入吗？

> 原文：<https://javascript.plainenglish.io/should-you-use-dependency-injection-in-javascript-3751bdf3f198?source=collection_archive---------6----------------------->

![](img/5ea5649f308812cfc9df3b5d61a89942.png)

Photo Courtesy of Dr Magaziner

*最初发布于*[*https://fek . io*](https://fek.io/blog/should-you-use-dependency-injection-in-java-script)*。*

Please subscribe to the Polyglot Engineer Channel

我看过一些关于 JavaScript 和其他语言的帖子，劝阻使用依赖注入。在我工作的一家公司，我甚至有一个老板告诉他的开发人员，我们永远不应该使用依赖注入。

依赖注入(DI)，有时也称为“控制反转”，是指一个对象接收它所依赖的其他对象或函数来实现其部分功能。这可以通过使用构造函数或属性设置通过对象实例化传递对象来实现。这在 Java 或 C#等静态类型语言中很常见。在静态类型的面向对象世界中，有许多专门为管理依赖关系而构建的流行框架。

DI 允许在运行时加载特定的功能。能够在运行时更改对象功能的一个优点是提供了更大的灵活性，并使我们的应用程序更加松散耦合。一个非常常见的用例是在测试过程中使用模仿。在 [Node.js](https://nodejs.org) 中有一些很棒的库，比如 [Sinon](https://sinonjs.org/) 使得模仿变得非常容易，但是我们可以通过使用 DI 来完成同样的任务。

# 测试场景

在测试中，用 mock 或 fake 替换与数据库或网络请求通信的代码是很常见的。这是因为在许多 CI/CD 工作流中，构建或测试服务器可能无法访问实际服务所需的数据库服务器或网络。对于 DI 来说，这是一个用模拟或伪造的服务替换实际服务的绝佳用例。

使用 DI 有许多不同的原因，但测试是最常见的原因之一。

# 可怜的芒迪

我有一个多年来一直使用的技术，用于在我的应用程序中配置 DI，不管它们是静态类型的还是像 JavaScript 一样的鸭类型的，我喜欢称之为“可怜人的依赖注入”。使用这种技术，如果在对象实例化时没有传入所需的对象，我通常会创建默认的依赖对象。

假设我们有一个 cart 对象，它需要计算某个位置的税率。在许多电子商务系统中，这种数据必须根据用户的位置来计算，每个位置的销售税都不同。我们可以创建一个工厂函数，该函数创建一个购物车，该购物车带有一个用于计算税款的可注入函数。

看看下面的例子，我们正在创建一个对象，它具有向购物车中添加商品以及计算总计和小计的函数。我们有一个函数，可以传递给我们的设置构造函数对象`taxrepository`。我们将使用这个函数来计算我们的税款。

让我们创建一个测试函数来计算我们的税收。我们会让这成为一个没有任何副作用的纯函数。

```
function calculateMyTax(subtotal) {
    return subtotal * 0.11;
}
```

当我们用工厂函数实例化这个对象时，我们可以把它传递给我们的 settings 对象；

我们现在可以得到小计，并计算税收。

# 违约行为

我定义的所有对象，每当构造函数中不包含可注入行为时，我都会尝试创建默认值。这样，如果有人在没有传入所需对象的情况下使用我的对象，它将得到一个错误或一个默认函数，如果它在构造函数中丢失的话。如果 settings 对象中没有传递`taxrepository`,我们可以修改工厂函数来使用默认值。

如果调用我们函数的开发人员忘记将`taxrepository`传递给构造函数，我们也可能希望我们的工厂函数失败。

# 依赖注入框架

DI 框架在 Java 和。NET 开发，但是也有可以用于 JavaScript 的 DI 框架。其中一个框架叫做 [di4js](https://github.com/gedbac/di4js) ，可以在浏览器中使用 Node.js 或者普通的旧 JavaScript。下面是 di4js 自述中的一个例子；

This example is from the di4js Github repo

# 结论

![](img/46bbbbc7810b15743d5167361f3088a6.png)

依赖注入是一个非常强大的工具，用于配置应用程序在创建对象时使用某些依赖。无论您使用的是“穷人的”依赖注入还是成熟的 DI 框架，它都是在应用程序中配置不同行为的非常有用的工具。

[*更多内容看 plainenglish.io*](http://plainenglish.io/)