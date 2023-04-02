# 在 JavaScript/React/Angular 中停止使用 IFs

> 原文：<https://javascript.plainenglish.io/stop-using-ifs-in-javascript-react-angular-2e450a61c8b3?source=collection_archive---------7----------------------->

![](img/37580725cd8d675ae375a94615099944.png)

Photo by [Nadine Shaabana](https://unsplash.com/@nadineshaabana?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

不要到处用 if！我知道 if 逻辑在软件工程中很重要，但是我们可以做得更好。用这个逻辑但是要写得像个高级工程师。

我继续看到许多初级工程师这样做代码:

对于这个例子，我们也可以使用“switch case ”,但是我仍然认为对于这个特定的例子，最好的方法应该是这样的:

这两个代码做同样的事情，但是第二个比第一个干净得多，如果你使用 Typescript，它工作得很漂亮。

![](img/9b4ac93cae1dd7c0a3f74aaf911d539f.png)

现在你说:“是啊！但它只起作用，因为你只是打印一个字符串”。答案是:不！我们可以在很多情况下使用它，我们可以用它来返回函数，进行计算，返回 React 组件或进行惰性导入等。天空才是极限！！

## 为什么使用这个对象映射器而不是 Ifs？

1.  让你的代码更干净，更容易理解(记住，你的代码不是为你或者机器准备的。您的代码需要被编写成任何人都可以看到并且容易理解)
2.  迫使您将逻辑与数据分离，并让您在将要使用的变量和函数上命名
3.  让添加新选项变得非常容易，你只需要在映射器中添加一行新的内容

## 那么什么时候使用 if 呢？

就像生活中的所有事情一样，我们也有这样做的理由。对于 if，我仍然使用 if，在某些情况下，我们只是检查一个信息，比如:

但是如果我们添加更多的人到它里面，我总是把它转换成对象映射器。

## 结论

编程不仅仅是让代码工作，还包括在团队中创建易于维护的东西，以及创建客户可以信任的产品。

**感谢您的阅读！🙏**

如果你有什么要补充的，请在[推特](https://twitter.com/felipefurlaneti)上发给我，我会在这里补充！

*更多内容请看*[*plain English . io*](http://plainenglish.io/)*。在这里注册我们的* [*免费周报*](http://newsletter.plainenglish.io/) *。*