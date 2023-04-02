# 使用事件处理程序和 React 挂钩构建一个简单的 React 登录表单

> 原文：<https://javascript.plainenglish.io/build-a-simple-react-login-form-using-event-handlers-and-react-hook-4afb11391e48?source=collection_archive---------1----------------------->

## 一个简单的初学者友好的 React 登录表单教程，使用了 onChange 和 onSubmit 事件处理程序和 useState 钩子。

大家好！

![](img/b217d36a5e55a6d3d42a5ffed4828e1b.png)

我认为许多人在开始学习时面临困难。在我看来，一个人必须尝试构建简单的项目和概念，这样我们才能清楚地理解。

所以，在这里我将通过使用 React 构建一个简单的登录表单来帮助您，并提高您的 React 知识

这是另一个超级简单的项目。在这个项目中，我们正在构建一个简单的登录表单。你兴奋吗？

让我们开始吧。

**先决概念:**

1.  onClick、onChange 和 onSubmit ->事件处理程序
2.  useState() -> React 挂钩
3.  对象析构。

在开始这个项目之前，你应该清楚地知道上面的概念。

**步骤:**

*   使用以下命令创建一个名为“login-form”的 React 应用程序。

```
> npx create-react-app login-form
```

*   使用以下命令开始运行您的服务器。

```
> npm run start
```

*   用 React 钩子 useState()创建两个变量 data(要存储)、setData(要更新)。

```
const [data,setData] = useState({
     username:"",
     password:""
});
```

*   这里，在初始化时，我们将用户名和密码设置为空字符串。
*   创建一个包含两个输入的窗体，1。用户名和 2。密码

```
<form><input type="text" name="username" value={username}/><br/>
<input type="password" name="password" value={password}/><br/></form>
```

*   从数据中析构变量 username 和 password，并将其存储在 username 和 password 变量中，如下所示。

```
const {username,password} = data;
```

*   创建一个提交按钮。

```
<input type='submit' name="submit"/>
```

*   声明 onChange 事件。

```
const changeHandler = e => {setData({...data,[e.target.name]:[e.target.value]});}
```

*   (…data)表示每个数据。
*   [e . target . name]:[e . target . value]表示特定的用户名(名称)=特定的密码(值)。
*   在输入表单中添加 onChange 处理程序，如下所示。

```
<form onSubmit={submitHandler}><input type="text" name="username" value={username} onChange={changeHandler}/><br/><input type="password" name="password" value={password} onChange={changeHandler}/><br/><input type="submit" name="submit"/></form>
```

*   现在添加一个提交处理程序

```
const submitHandler = e => {e.preventDefault();console.log(data);}
```

这里 e.preventDefault()表示每次提交处理程序命中时，它都进入默认状态。

即，它将用户名和密码设置为空字段。

*   将 onSubmit 添加到表单中，如下所示。

```
<form onSubmit={submitHandler}>
```

因此，每当我们单击提交按钮，它就会触发提交处理程序，并在控制台中显示数据。

最后，整个代码将如下所示。

这是一个非常简单的登录表单，使用 React 和 useState 钩子以及 onChange，onSubmit 作为事件处理程序。

您也可以尝试同样的注册表单。

感谢阅读！我希望你们都通过阅读这篇文章获得了一些知识。

在接下来的日子里，我会带着更多像这样简单的 React 项目回来。所以，继续跟着我。

如果你想鼓励我，你可以点击下面的链接，给我买杯咖啡。它帮助我写更多有创意的文章。你的支持意义重大！谢谢你。

[***给我买杯咖啡***](https://ko-fi.com/hemanthraju) ☕️！！！！！😍

[**如果你 liked🧡读了这篇文章，你可能也会喜欢下面这篇文章。看看吧！**](http://cool)

[](/simple-react-counter-app-for-beginners-using-usestate-and-useeffect-hooks-2dbcc9876003) [## 简单的反作用计数器应用程序，适合初学者使用“使用状态”和“使用效果”挂钩

### 借助这个简单的计数器项目，学习“useState”和“use effect”React 钩子。

javascript.plainenglish.io](/simple-react-counter-app-for-beginners-using-usestate-and-useeffect-hooks-2dbcc9876003) 

保持微笑！

祝您愉快！

*更多内容看*[***plain English . io***](http://plainenglish.io/)