# 如何用 Express 和 NGINX 部署 React App

> 原文：<https://javascript.plainenglish.io/how-to-deploy-a-react-app-with-expressjs-and-nginx-29abeef08c67?source=collection_archive---------1----------------------->

在这篇博客文章中，我将向您解释如何使用 ExpressJS 作为后端服务来部署 React 应用程序。

![](img/04457f4efe85804ad98b1bfeb6260132.png)

Photo by [Roman Synkevych](https://unsplash.com/@synkevych?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Express 将使用`express.static`中间件为 React 应用提供服务。我们将首先在根路径上部署服务，然后在子路径上部署，我们将在服务器端和客户端完成所有需要的更改。让我们开始吧。

感觉懒？你可以跟着 Youtube 上的教程走:

repo:[https://github . com/enrico 89/react-app-express js-nginx/tree/express-js-react-app](https://github.com/enricop89/react-app-expressjs-nginx/tree/express-js-react-app)

# 项目概述

首先，让我们使用 create-react-app 样板文件创建一个 React 应用程序示例。命令`npx create-react-app my-app-nginx`将为此创建一个基本应用程序。

如果你想看到应用程序运行，运行`npm start`。该应用程序将显示 Create React 应用程序样板的默认视图。

下一步是安装`react-router-dom`，这样我们就可以在 React 应用上添加路线。我们将复制基本应用程序来展示路线是如何工作的:

```
import React from "react";
import {
  BrowserRouter as Router,
  Switch,
  Route,
  Link
} from "react-router-dom";export default function App() {
  return (
    <Router>
      <div>
        <nav>
          <ul>
            <li>
              <Link to="/">Home</Link>
            </li>
            <li>
              <Link to="/about">About</Link>
            </li>
            <li>
              <Link to="/users">Users</Link>
            </li>
          </ul>
        </nav> {/* A <Switch> looks through its children <Route>s and
            renders the first one that matches the current URL. */}
        <Switch>
          <Route path="/about">
            <About />
          </Route>
          <Route path="/users">
            <Users />
          </Route>
          <Route path="/">
            <Home />
          </Route>
        </Switch>
      </div>
    </Router>
  );
}function Home() {
  return <h2>Home</h2>;
}function About() {
  return <h2>About</h2>;
}function Users() {
  return <h2>Users</h2>;
}
```

此时，我们可以导航到`/users`、`/about`和`/`回家路径。客户端的最后一步是运行`npm run build`，这样我们的静态应用程序就可以由 ExpressJS 提供服务了。

## 服务器端

基本的服务器端实现如下:

```
const path = require('path');
const cors = require('cors');
const express = require('express');
const app = express(); // create express app
app.use(cors());

const bodyParser = require('body-parser');
app.use(bodyParser.json());

// add middlewares
const root = require('path').join(__dirname, 'build');
app.use(express.static(root));

app.use('/*', (req, res) => {
  res.sendFile(path.join(__dirname, 'build', 'index.html'));
});

// start express server on port 5000
app.listen(process.env.PORT || 5000, () => {
  console.log('server started');
});
```

需要注意的重要部分是:

*   `express.static(path.join(__dirname, 'build))`:我们告诉 ExpressJS 在`build`文件夹中查找静态文件。
*   因为我们使用的是`react-router-dom`，所以我们需要配置 ExpressJS 来服务`index.html`，即使客户端正在请求子路径，比如`/home`或`/about`。这是因为当有一个新的页面加载给一个`/home`时，服务器会寻找文件`build/home`但没有找到。服务器需要配置为通过服务`index.html`来响应对`/home`的请求。解决方案是配置我们上面的 Express 服务器为任何未知路径提供`index.html`:

```
app.use('/*', (req, res) => {
  res.sendFile(path.join(__dirname, 'build', 'index.html'));
});
```

# 在子路径上部署？

没问题，🧘‍♀️

如果您想在一个子路径上部署 React 应用程序，例如`mywebsite.com/app`，那么在服务器端和客户端都需要进行修改。在客户端，我会按照这个指南:[https://create-react-app . dev/docs/deployment/# building-for-relative-paths](https://create-react-app.dev/docs/deployment/#building-for-relative-paths)。

客户端的变化有三个:

1.  在 package.json 上添加`homepage`: Create React App 生成一个构建，假设您的应用程序托管在服务器根。如果你不想指定一个子路径，你可以设置`homepage:"."`，这样所有的资产路径都是相对于`index.html`的
2.  更改`react-router-dom`的`basename`:base name 是所有位置的基本 URL。例如:

```
export default function App() {  
  const basename = process.env.REACT_APP_BASENAME || null;  
  return (
   <Router basename={basename}> 
    .... 
   </Router>
}
```

3.运行`npm run build`脚本时更改`PUBLIC_URL`。如果将文件放入公共文件夹，webpack 将不会处理该文件。相反，**它将原封不动地复制到构建文件夹中**。要引用 public 文件夹中的资产，您需要使用一个名为 PUBLIC_URL 的环境变量。因此，如果您在子文件夹中部署 React 应用程序，您必须设置 PUBLIC_URL 来反映特定的子文件夹。这样，`index.html`会以 PUBLIC_URL 路径为前缀向服务器请求文件。例:[https://github . com/enrico 89/react-app-express js-nginx/blob/docker-express-js-react/. env . example](https://github.com/enricop89/react-app-expressjs-nginx/blob/docker-express-js-react/.env.example)

一旦您完成了更改，记得再次运行`npm run build`以便更新包。

现在我们必须转移到服务器端，更改 NGINX 配置。我们需要将位置块更改为:

```
server{
  location /app/ {        
    proxy_set_header Upgrade $http_upgrade;        
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;        
    proxy_pass   http://localhost:5000/;  
  }
}
```

如果您愿意，您可以按照视频中的过程进行操作:

Deploy to Subpath

# 结论

在这篇博文中，我们看到了如何使用 ExpressJS 来托管一个静态的 React 应用程序。

请在评论中告诉我你的想法。在推特[和 Youtube](https://twitter.com/enricop89) 上关注我，了解更多信息！

## 延伸阅读:

[](https://bit.cloud/blog/deploying-a-composable-react-app-to-netlify-l7rlluzs) [## 将可组合的 React 应用程序部署到 Netlify

### 在这篇博文中，我们将学习如何使用 Bit 来构建和部署一个可组合的 React 应用程序到 Netlify。在位…

比特云](https://bit.cloud/blog/deploying-a-composable-react-app-to-netlify-l7rlluzs) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***