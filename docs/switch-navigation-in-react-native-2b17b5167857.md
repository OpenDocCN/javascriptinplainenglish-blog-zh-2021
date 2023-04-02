# 在 React Native 中切换导航

> 原文：<https://javascript.plainenglish.io/switch-navigation-in-react-native-2b17b5167857?source=collection_archive---------19----------------------->

## 使用 React Navigation 的切换导航机制将登录用户直接重定向到主页

![](img/1f96bfe5b440499885ffab8ef1538146.png)

Source ([link](https://www.progress.com/blogs/the-react-native-sdk-for-kinvey-is-now-available))

最近，我开发了一个 React 本地应用程序，如果用户已经登录，我需要将用户直接重定向到主页。一种方法是在登录页面的`componentDidMount`生命周期事件中检查登录的用户，但是它没有提供良好的用户体验。用户每次打开应用程序时，都会看到从登录到主页的转变。此外，如果您的登录流程中有多个页面，就会变得更加混乱。

在这篇短文中，我将展示使用 React Navigation 的授权流在 React 本机应用程序中管理授权流的最佳方式。

[https://reactnavigation.org/docs/auth-flow](https://reactnavigation.org/docs/auth-flow)

# 先决条件

让我们假设您已经有了一个包含多个页面的 React 本地应用程序设置。您的`App.js`可能看起来像这样:

上面的代码片段显示了登录流程 ie 有 3 个不同的屏幕。【T2>`ConfigureCalendar`>`Calendars`

为了使切换导航工作，其中一组页面显示用于登录流，另一组页面在用户登录后显示，我们需要有一个标志来告诉我们用户是否登录。这可以通过使用 Redux 和 Redux persist 轻松实现。如果您还没有安装 Redux persist，您可以参考这篇文章来了解如何安装。

[](https://blog.jscrambler.com/how-to-use-redux-persist-in-react-native-with-asyncstorage) [## 如何在 React Native 中使用 Redux Persist with async storage | Jscrambler 博客

### Redux Persist 是一个允许在应用程序的本地存储中保存 Redux 存储的库。在反应原生…

blog.jscrambler.com](https://blog.jscrambler.com/how-to-use-redux-persist-in-react-native-with-asyncstorage) 

# 履行

## 步骤 1:在 App.js 中使用 Redux 状态

有了上面的设置，我们只需要使用`App.js`文件中的 Redux 状态。注意，我们使用`useSelector`来访问 Redux 状态，然后使用`user.isLoggedIn`标志来为登录前后的流提供不同的堆栈。

## 步骤 2:在登录的最后一步设置登录标志

接下来，我们只需要在登录的最后一步设置`user.isLoggedIn`标志。我们在登录流程的最后一步使用了`useDispatch`，并使用`setLoggedIn` Redux 动作设置了`isLoggedIn`标志。

注意:

*   在其他登录页面，您可以使用`navigation.navigate('Page')`导航到下一个登录页面
*   **重要提示:**在登录的最后一步，您无需手动导航至主页。我们的 switch navigator 将把用户重定向到主页。

就是这样。切换导航现在应该可以在您的应用程序中流畅地工作了。下次当用户打开应用程序时，主页将直接为他们打开。

我希望这篇文章对你有所帮助。请务必在评论中让我知道你的想法。考虑成为中级[会员](https://utkarshabakshi.medium.com/membership)，继续阅读我所有的优质文章以及数以千计的其他故事。

你可以在这个[列表](https://utkarshabakshi.medium.com/list/react-native-development-0d5f690f6585)中找到我关于 React 原生开发的其他文章。

*更多内容请看*[***plain English . io***](http://plainenglish.io)