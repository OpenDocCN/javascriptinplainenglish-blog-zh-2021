# React 路由器举例说明

> 原文：<https://javascript.plainenglish.io/react-router-explained-with-examples-8a924c9bfee9?source=collection_archive---------15----------------------->

## 通过实例了解 React 路由器。

![](img/e01ce3945ea9c23b6c224d18c45385f6.png)

Image created with ❤️️ By author.

React Router 是 React 中非常有用和著名的库。它允许您在 React 应用程序的多个页面之间导航，而无需向服务器发出新的请求。

使用 React router，JavaScript 将不断地呈现在页面中，您可以在几个不同的路由之间切换，而不必重新加载浏览器。因此，如果你想创建一个多页面 React 应用程序，我会一直推荐使用 React router，因为在我看来，它非常强大且易于使用。

在本文中，我们将了解使用 React 路由器库的基础知识。让我们开始吧。

# 安装 React 路由器

在使用 create-react-app 设置我们的项目之后，我们要做的第一件事是安装 react 路由器包，因为它不是核心 React 库的一部分。

为此，我们需要在我们的机器上安装 NPM 和 NodeJS。之后，只需进入 React 项目文件夹中的终端，键入下面的命令，使用 NPM 安装软件包。

另外，请记住，我们将使用 React 路由器的版本 5，所以使用`**@ 5**`来指定。

下面是一个例子:

```
**npm install react-router-dom@5**
```

如果你愿意，你也可以使用 YARN 来安装这个包。这里有一个例子:

```
**yarn add react-router-dom**
```

现在我们已经安装了这个包，我们可以开始使用它了。

# 使用 React 路由器

我们将创建一个使用 React 路由器的简单示例。我们将建立一个简单的导航栏，包含三个链接到三个不同的页面(主页，关于，联系)。

您可以在下面的 Codepen 示例中查看它:

Codepen by author.

正如你所看到的，你可以在页面之间导航，而不必重新加载应用程序。这就是 React 路由器的强大之处。

为此，我们必须在 React 应用程序的`src`文件夹中创建 4 个不同的 JavaScript 文件:`Nav.js`、`Home.js`、`About.js`和`Contact.js`。您可以查看我的 [CodeSandbox](https://codesandbox.io/s/pedantic-villani-wshq4?file=/src/App.js) 示例中的所有文件结构和代码。

所以我们要做的第一件事就是转到我们的文件`App.js`，从包中导入所有的路由组件。

```
**import { BrowserRouter as Router, Switch, Route} from 'react-router-dom'**
```

除此之外，我们需要为我们的页面导入所有其他组件。

然后，我们必须用`<Router>`标签包装整个应用程序，以便整个应用程序使用路由功能。

看看下面的例子:

```
//App.jsimport React from 'react'
import Nav from './Nav'
import Home from './Home'
import About from './About'
import Contact from './Contact'
**import { BrowserRouter as Router, Switch, Route} from 'react-router-dom'**const App = () => {
  return (
    **<Router>**
      <div className='container'>
        <Nav />
        **<Switch>**
          **<Route exact path='/'>**
            <Home />
          **</Route>**
          **<Route path='/about'>**
            <About />
          **</Route>
**          **<Route path='/contact'>**
            <Contact />
          **</Route>**
        **</Switch>**
      </div>
    **</Router>**
  )
}export default App;
```

正如你所看到的，我们将所有东西都包装在组件`<Router>`中，并且在组件`<Switch>`中呈现所有页面。

切换组件确保一次只显示一条路线，这允许我们在页面之间导航。

正如您在上面看到的，您还需要将每个页面或组件包装在一个名为`<Route>`的组件中，这个组件是我们从包中导入的。每个路由都有一个包含每个页面路由的路径属性。

对于 home 路由，您还需要添加属性`exact`，因为所有其他路由都像 home 路由一样以斜线`/`开头。如果不为 home route 添加属性`exact`，app 只会渲染 home 组件。这就是我们的文件`App.js`，现在我们需要创建页面和导航栏。

*首页:*

```
//Home.jsimport React,{useEffect} from 'react'const Home = () => {
  useEffect(()=> document.title = "Home", [])
  return (
    <div className='home'>
      <h2>Home page</h2>
      <p>This is the home page! Welcome!</p>
    </div>
  )
}export default Home
```

*关于页面:*

```
//About.jsimport React,{useEffect} from 'react'const About = () => {
  useEffect(() => document.title = 'About',[])
  return (
    <div className='about'>
      <h2>About</h2>
      <p>We are a company that cares about customers. We do our best here.</p>
    </div>
  )
}export default About
```

*联系人页面:*

```
//Contact.jsimport React,{useEffect} from 'react'const Contact = () => {
  useEffect(() => document.title = 'Contact',[])
 return (
  <div className="contact">
   <h2>Contact</h2>
   <p>Get in touch with us by contacting us!</p>
  </div>
 )
}export default Contact
```

现在，我们已经为页面创建了所有组件。让我们创建包含链接的导航栏，单击这些链接可以在页面之间导航。

下面是代码示例:

```
//Nav.jsimport React from 'react'
**import { Link } from 'react-router-dom'**const Nav = () => {
 return (
   <nav>
     **<Link to='/'>**Home**</Link>**
     **<Link to='/about'>**About**</Link>**
 **<Link to='/contact'>**Contact**</Link>
**   </nav>
 )
}export default Nav
```

正如你在上面看到的，我们没有使用标签`<a>`，而是使用了从 React 路由器包中导入的组件`Link`。

就是这样，现在你只需要添加一些造型，如果你想的话。您可以访问 [Codesandbox](https://codesandbox.io/s/pedantic-villani-wshq4?file=/src/Nav.js) 中的所有代码。

# 结论

如您所见，这只是如何在您的项目中使用 React Router 的一个简单实用的示例。我喜欢这个库的一点是，你可以在页面之间导航，而不必重新加载。这对性能有好处，因为它不会在你点击链接的时候请求服务器。

感谢您阅读这篇文章。希望你觉得有用。

**更多阅读**

[](/useful-javascript-questions-you-might-face-during-interviews-a7e0d64e3946) [## 面试中你可能会遇到的有用的 JavaScript 问题

### 为你接下来的面试准备一些 JavaScript 问题。

javascript.plainenglish.io](/useful-javascript-questions-you-might-face-during-interviews-a7e0d64e3946) 

[*更多内容尽在 plainenglish.io*](http://plainenglish.io/)