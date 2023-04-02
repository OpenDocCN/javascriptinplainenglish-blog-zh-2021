# 使用反应路由器设置授权保护

> 原文：<https://javascript.plainenglish.io/auth-guard-and-react-router-46bb7a7160aa?source=collection_archive---------20----------------------->

基于用户的身份验证呈现特定的路由或页面很重要，这也是为什么我惊讶地看到，当涉及到 reactor 中的身份验证防护时，我的谷歌搜索结果并不尽如人意。有时你只需要更好的理解(或词汇)来利用谷歌的力量并做出反应。反应路由器有[本例为](https://reactrouter.com/web/example/auth-workflow)。这很好。他们利用[使用](https://usehooks.com/useAuth/)。不过，我觉得这有点难，因为它可以更简单！方法如下:

```
state = { auth: false};
```

嘣。我们结束了！恭喜！

![](img/eb25c77839e892f206529ffab29404ab.png)

好吧，还有一点。

```
{ this.state.auth ? <SomeComponent /> : <h1>Please login!</h1> }
```

您可以在组件的 JSX 中使用三元表达式！因此，只有当 this.state.auth 为“真”时，这才会渲染<somecomponent>。对于来自服务器的成功登录请求，我们将 auth 设置为 true，如下所示:</somecomponent>

```
.then(res => res.json())
.then(json => this.setState({ auth: true }));
```

这是假设您在登录不成功的任何时候抛出一个错误。这实际上就是简单的身份验证和条件渲染的全部内容。当用户没有登录或注销时，您只需使用这个. setState({ auth: false })。

现在，还有其他方法可以做到这一点。使用 rails 时，您可以在控制器中设置一个 before_action，在调用任何方法之前检查用户是否登录。您在这里可以看到更多。您仍然需要前端的错误处理，所以总体上这需要做更多的工作。这种编程的全部思想是尽可能少地编码。如果您还有其他资源，请在下面发表评论！

此外，感谢[艾莉亚·穆阿利](https://medium.com/@aryamurali)精彩的[帖子](https://medium.com/@aryamurali/embed-code-in-medium-e95b839cfdda)。