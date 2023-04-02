# 从我的节点包朋友那里得到一点帮助

> 原文：<https://javascript.plainenglish.io/react-with-a-little-help-from-my-node-package-friends-bdf8a57a6e7a?source=collection_archive---------15----------------------->

![](img/1f957b913dc72642ba6800fb751f45f7.png)

Photo by [Paul Esch-Laurent](https://unsplash.com/@pinjasaur?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在使用 React 制作一个琐事应用程序时，我使用了几个不同的包，我想在这里谈谈为什么我认为它们是有用的。

在我继续学习编码的旅程中，我喜欢写下我的学习经历，因为它帮助我反思我所做的事情，并希望包含一些对其他人有用的信息。说完了，让我们开始吧！

我发现了一个很好的资源，可以通过 [Open Trivia Database](https://opentdb.com/) 收集琐事问题。该数据库免费使用，允许用户提交问题的开放贡献，并有许多类别和困难可供选择。它对我的总体需求非常有用，但也有一个问题。因为问题是由许多用户创建的，所以它们的格式不尽相同。一些问题的文本在问题正文及其答案文本中使用了 HTML 实体。例如，像这样的问题:

*“谁在《比尔·泰德的精彩冒险》中扮演两个有名无实的角色？”*

显示为:

*T9【x22】；谁扮演&中的两个挂名角色？账单&# x26；泰德&# x27；■精彩冒险&# x27；？& #x22:*

我将这些数据保存到我自己的后台数据库中，以创建定制游戏，所以我的分析欲希望一切都是一致的。如果我还决定以后操纵任何数据，如果一切都是一致的，那么编写方法会容易得多。为此，Mathias Bynens 提供了一个名为 [he](https://github.com/mathiasbynens/he) 的包，它是一个用 JavaScript 编写的 HTML 编码器/解码器。现在，让我们从上面的例子琐事问题，解码它:

现在，所有传入的数据都被快速轻松地格式化了。这个包也将使用 HTML 实体对字符串进行编码，但是我只使用了 decode 函数。

从那里开始，我创建的琐事游戏是一个使用 React 的单页应用程序(SPA ),它在顶部有一个导航栏，用户可以在菜单之间单击以创建新游戏，查看他们的统计页面，或玩游戏。导航栏将始终存在，但其他组件(称为 NewGame、Game 和 Stats，以供将来参考)不会堆叠在彼此之上，而是会在页面上相互替换。我决定采用的方法是使用 [React 路由器](https://reactrouter.com/web/guides/quick-start)。这样，我可以使用`<Redirect />`组件来更改页面上显示的组件，同时也给我的应用程序提供了在更改当前呈现在页面上的组件时动态更新 URL 的功能。

我使用“react-router-dom”附带的组件设置了导航栏:

使用方便的`<NavLink />`组件，创建一个样式化的链接，默认情况下，多个链接并排呈现。`activeStyle`道具允许外观改变来指示它当前被选中的时间。相当整洁！现在有了一个指向特定 URL 的链接当然很好，但是如果没有一个组件来呈现这个特定的 URL，这是没有用的。这就是`<Route />`组件的用武之地。

导航栏下有三个路线组件。第一个有一条`“/game/new”`的路径。当当前 URL 匹配该路径时，`<NewGame />`组件将呈现在导航栏下面。注意`exact path`标志。说明这一点意味着组件只有在 URL 完全匹配时才会被呈现。澄清一下，没有声明一个`exact path`匹配的路径的任何部分仍然会呈现那个组件。如果 URL 是`“/game/new”`，那么路径为`“/game”`的`<Game />`组件仍然会呈现。根据应用程序的不同，在某些情况下可能需要这种行为，但是在我的例子中，我希望在导航栏下一次只显示一个组件。

React 路由器是一个非常有用的包。实际上非常有用，其中还有一个组件值得一提。上面提到的`<Game />`组件应该只在它先从用户那里收集了一些信息之后才呈现。因为直接链接到`“/game”` URL 不是一个好主意，重定向到它是一个好办法。反应路由器再次救援！`<Redirect />`组件可以处理这个问题，但是需要一点额外的工作。一旦在组件的`render()`方法中被读取，它将导航到新的位置并呈现与该 URL 相关联的组件。

下面的`<NewGame />`组件展示了这是如何付诸实践的:

最终目标是在`User.js`中只呈现导航条下面的`<Game />`组件，并附带用户输入的数据。游戏不应该在没有启动所需数据的情况下渲染，因为`<Redirect />`一渲染就激活，它必须只在满足特定条件时才渲染。在这种情况下，一旦提交了表单，就会触发`handleOnSubmit()`事件处理程序，并添加带有`<Game/>`URL 值的“redirect”键。`redirect()`函数从`this.state.redirect`返回带有目标路径的`<Redirect />`。`<Redirect/>`中的状态对象`{ gameData: this.state }`允许将 props 传递给重定向到的组件，在本例中是`<Game/>`。这可以通过`this.props.location.state`从该组件中访问。

将所有这些联系在一起的是三元运算符:

`this.state.redirect ? this.redirect() : null`

当`handleOnSubmit()`触发时，它在状态中设置新的“重定向”键，状态被更新，组件重新呈现，由于三元运算符的条件现在为真，它将调用返回`<Redirect/>`组件的`redirect()`函数。这将改变网址为`"/game"`和渲染`<Game/>`。因为这条路线是用`exact path`声明的，所以它将取代导航栏下面的`<NewGame/>`组件。

使用 React Router 内置的三个组件，我能够相对容易地改变路线并实现 SPA 的良好流程。通过确保我所有的数据都是统一格式的，这个包允许我防止以后出现意外的问题。这就是用 JavaScript 开发应用程序的美妙之处。有无数的代码库，如果它节省了一些时间和大量的麻烦，那么为什么不通过一些朋友的帮助呢？

*更多内容请看*[***plain English . io***](http://plainenglish.io/)