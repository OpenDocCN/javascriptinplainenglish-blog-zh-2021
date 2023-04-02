# 如何在反应应用程序中处理路由

> 原文：<https://javascript.plainenglish.io/how-to-handle-routing-in-your-react-application-b46d8b13b83a?source=collection_archive---------13----------------------->

## 您需要了解的关于反应路由的所有信息-

![](img/7ce735eed1ea7f456679c1ff6d353e85.png)

Photo by [Nathan Dumlao](https://unsplash.com/@nate_dumlao?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/route?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

组织正在转向单页应用程序(SPAs)，以满足客户和内置应用程序用户不断增长的需求。单页应用程序很大程度上依赖于 JavaScript，当用户与应用程序交互时，他们并不要求整个页面重新加载。相反，对于每一个用户请求，单个页面都是动态更新的，在整个用户旅程中提供了更有效的界面。因此，spa 已经成为软件开发行业的新常态。

SPA 有许多视图，你需要一个路由器来处理 URL，而不是传统的多应用程序，来浏览这些视图。反应路由器处理这个问题，使用户界面和应用程序的网址同步。

> 反应路由器允许您以声明方式处理路由。声明性路由策略使您能够操纵应用程序中的数据流，并以增强的可读性构建直观的路由，试图使其方便地处理您的应用程序体系结构。

所以，让我们通过本文来看看如何在您的反应应用程序中使用路由。

# 安装和设置反应路由器

使用`create-react-app`创建新的反应应用程序后，您需要安装反应路由器包。有两种版本，网络版本和本地版本。我们需要在这里安装网络版。

在终端中使用以下命令安装软件包:

```
npm install react-router-dom
```

一旦安装了软件包，就必须为每个软件包创建一组具有不同路由的组件。在这里，我创建了一个简单的 ToDo 应用程序，因此我们将有计划任务、已完成任务和未完成任务的单独组件。

您的三个组件`Scheduled Tasks`组件、`Completed Tasks`组件、`Missed Tasks`组件如下。

```
import React from ‘react’;export default function ScheduledTasks() { return <**h2**>Scheduled Tasks</**h2**>;}
```

```
import React from ‘react’;export default function CompletedTasks() { return <**h2**>Completed Tasks</**h2**>;
}
```

```
import React from ‘react’;export default function MissedTasks() { return <**h2**>Missed Tasks</**h2**>;}
```

作为下一步，您必须连接路由，但是首先，您需要在应用程序中呈现基本组件。

打开`App.js`并在带有类名“todo”的`<div>`标签中附上一个带有网站名称(My ToDos)的`<h1>`标签。这将作为一个模板。在任何页面上，toDos 和`<h1>`标记将被渲染。这将是显示其他组件的根组件。您可以在每个页面上为完整的应用程序插入您想要的导航栏或标题组件。

```
import React from ‘react’;
import ‘./App.css’;function App() {
 return (
 <div className=”toDos”>
 <h1>My ToDos</h1>
 </div>
 );
}export default App;
```

现在，当您拥有所有组件时，为了给应用程序提供空间，请应用一些填充。

```
.toDos {
 padding: 20px;
}
```

# 添加路由

在这一部分中，我们将为每个页面构建一个具有独立路由的基本路由器。为了保证组件被正确呈现，您将使用`<Link>`组件来安排您的路线，以插入不会导致页面刷新的到项目的超链接。

打开`App.js`开始创建路线。`<h1>`标签应该作为全球页面的标题。因为我们希望它显示在每个页面上，就在标签“配置路由器”之后。接下来，`import ScheduledTasks`和`<div>`内部进行渲染。

从 react-router-dom 导入`BrowserRouter`、`Route`和`Switch`。

```
import React from ‘react’;
import { BrowserRouter, Route, Switch } from ‘react-router-dom’;
import ‘./App.css’;import ScheduledTasks from ‘../ScheduledTasks /ScheduledTasks’;function App() {
 return (
 <div className=”wrapper”>
 <h1>My ToDos</h1>
 <ScheduledTasks />
 </div>
 );
}export default App;
```

# 路由器组件

我们要做的下一件事是将我们的`<App>`组件放在`<Router>`组件中。在我们创建基于浏览器的应用程序时，您可以选择 React Router API 的两种类型的路由器:

*   浏览器路由器
*   哈希鲁特

它们背后的关键区别在它们生成的 URL 中是显而易见的。`<BrowserRouter>`是两者中最常见的，因为它利用 HTML5 历史 API 使您的 UI 与 URL 同步，而 URL 的散列段由`<HashRouter>` (window.location.hash)使用。如果您需要提升不使用历史 API 的遗留浏览器，您可以使用`<HashRouter>`。相反，对于大多数用例来说，`<BrowserRouter>`是最好的选择。

# 链接和布线组件

React 路由器最重要的特性是`<Route>`组件。如果实际位置对应于路线的路径，这将呈现任何 UI。最好是，`<Route>`组件应该有一个称为路径的属性，如果路径与实际位置一致，它就会被渲染。

否则，`<Link>`组件用于跨页面导航。它类似于 HTML 的锚元素。使用锚链接将导致整个页面刷新，这是我们不希望的。然后我们可以使用`<Link>`或者重定向到一个特定的 URL，让视图重新呈现而不刷新。

现在，要构建一个基本路由器，插入 BrowserRouter 组件。在每一页上，该组件之外的所有内容都将被呈现，因此将其插入到您的`<h1>`标签之后。

```
import React from ‘react’;
import { BrowserRouter, Route, Switch } from ‘react-router-dom’;
import ‘./App.css’;import ScheduledTasks from ‘../ScheduledTasks /ScheduledTasks‘;function App() {
 return (
 <div className=”toDos”>
     <h1>My ToDos</h1>
       <BrowserRouter>
         <ScheduledTasks />
       </BrowserRouter>
 </div>
 );
}export default App;
```

然后，在 BrowserRouter 中插入交换机组件。这个组件就像 JavaScript switch 语句一样，将触发适当的路由。对于每条路线，在`Switch`中附加一个路线组件。在这个图中，您需要以下路线:`/scheduledtasks`、`/completedtasks`和`/missingtasks`。路径将被路由组件作为参数，并将包围一个子组件。每当路由被激活时，子组件就会出现。

如果你尝试一个路由，比如[http://localhost:3000/scheduled tasks，](http://localhost:3000/scheduledtasks,)你会发现`ScheduledTasks`组件。符合模式的第一条路线由`Switch`组件呈现。

> 每条路线都将与/兼容，因此每个页面都将呈现它，这也意味着排序很重要。因为路由器一旦发现匹配就会退出，所以通常会将更精确的路由放在不太精确的路由之前。

如果您希望路线仅匹配指定的路线，而不匹配任何子路线，则可以应用精确属性。对于 eg，它会匹配`/scheduledtasks`而不是`/scheduledtasks` `/scheduledtasksdate`，带有`<Route exact path=”/scheduledtasks “>`。

```
import React from ‘react’;
import { BrowserRouter, Route, Switch } from ‘react-router-dom’;
import ‘./App.css’;import ScheduledTasks from ‘../ScheduledTasks /ScheduledTasks ‘;
import CompletedTasks from ‘../CompletedTasks /CompletedTasks ‘;
import MissedTasks from ‘../MissedTasks /MissedTasks ;function App() {
 return (
 <div className=”toDos”>
   <h1>My ToDos</h1>
     <BrowserRouter>
       <Switch>
         <Route path=”/scheduledtasks”>
            <ScheduledTasks />
         </Route>
         <Route path=”/completedtasks”>
             <CompletedTasks />
         </Route>
         <Route path=”/missedtasks”>
            <MissedTasks />
         </Route>
       </Switch>
     </BrowserRouter>
 </div>
 );
}export default App;
```

现在已经有了许多组件，可以为用户构建导航来切换页面了。

为了表明我们正在设计主页的导航部分，使用`<nav>`元素。然后用一个列表项(`<li>`)和一个`Link`为每个 ToDo 附加一个无序列表(`<ul>`)。最后，将`<nav>`段转移到浏览器路由器内。这确保了反应路由器操纵链路组件。

```
import React from ‘react’;
import { BrowserRouter, Link, Route, Switch } from ‘react-router-dom’;
import ‘./App.css’;import ScheduledTasks from ‘../ScheduledTasks /ScheduledTasks ‘;
import CompletedTasks from ‘../CompletedTasks /CompletedTasks ‘;
import MissedTasks from ‘../MissedTasks /MissedTasks ‘;function App() {
 return (
 <div className=”toDos”>
    <h1>My ToDos</h1>
      <BrowserRouter>
       <nav>
         <ul>
          <li>
            <Link to=”/scheduledtasks”>Scheduled Tasks </Link>
          </li>
          <li>
            <Link to=”/completedtasks”>Completed Tasks</Link>
          </li>
          <li>
            <Link to=”/missedtasks”>Missed Tasks</Link>
          </li>
         </ul>
       </nav>
       <Switch>
          <Route path=”/scheduledtasks”>
             <ScheduledTasks />
          </Route>
          <Route path=”/completedtasks”>
             <CompletedTasks />
          </Route>
          <Route path=”/missedtasks”>
             <MissedTasks />
          </Route>
      </Switch>
    </BrowserRouter>
 </div>
 );
}export default App;
```

现在，我们已经为每个组件构建了一条路线，并引入了导航，无需使用 Link 组件刷新页面就可以在路线间移动。

# 嵌套路由

路线会扩大，显得更复杂。React Router 使用嵌套路由在子组件中呈现更精确的路由细节。最后一步，在`App.js`中，我们添加了路线。

它有很多好处:它在一个位置保存所有的路线，本质上为我们的应用程序提供了一个站点地图。但它可能会迅速发展，难以阅读和管理。

> 嵌套路由明确地将路由数据组织到呈现其他组件的组件中，允许您在应用程序中构建小型模板。

假设您需要对 ToDos 应用程序应用另一个级别。待办事项有很多种，如关键、非关键，并且可以显示每种待办事项的详细信息。您有两个选择:您可以使用当前路线，并附加一个带有搜索参数的特定类型的 to do，比如？类型=关键。您还可以在包含特殊名称(如`/scheduledtasks/critical`)的基本 URL 之后构建一个新的路由。

首先，为不同的 ToDos 类型制作新组件。

```
import React from ‘react’;export default function Critical() {

return(
 <h3>Critical</h3>
 );
}
```

接下来打开`ScheduledTasks.js` 。这是您要连接嵌套路径的地方。

你必须做两件事。最初，用 UseRouteMatch 钩子，抓取当前方向。然后，为了显示相关的组件，制作当前的`<Switch>`和`<Route>`组件。

`UseRouteMatch`导入将返回一个包含 URL 和路径的对象。析构对象以打开路径。这将作为您新路线的基础:

```
import React from ‘react’;
import { useRouteMatch } from ‘react-router-dom’;
import Critical from ‘./Critical’;export default function ScheduledTasks() {
 const { path } = useRouteMatch();return (
 <>
 <**h2**>Scheduled Tasks</**h2**>
 {type === critical && <**Critical** />}
 </>
 );
}
```

首先，你必须导入`Switch`和`Route`来引入新的路线。新的路线将与您在`App.js`中所做的相同，所以您不需要使用`BrowserRouter` 来捆绑它们。添加新路径，但在路由前添加路径前缀。新组件将精确地显示在您放置它的地方，所以在`<h2>`之后添加新的路线。

```
import React from ‘react’;
import { Switch, Route, useRouteMatch } from ‘react-router-dom’;
import Critical from ‘./Critical;export default function ScheduledTasks() {
 const { path } = useRouteMatch();
 return (
 <>
 <h2>Scheduled Tasks</h2>
   <Switch>
     <Route path={`${path}/critical`}>
      <Critical />
     </Route>
   </Switch>
</>
 );
}
```

它保存了孩子们和他们父母的路线。并非所有项目都使用嵌套路由:有些项目考虑提供一个显式列表。这是球队选择和延续的问题。为您的项目选择最佳的解决方案，然后您总是可以在以后对其进行改进。

# 摘要

正如我们在整篇文章中讨论的，React 路由器是每个 React 应用程序的主要部分。当您创建用户可以无缝导航的单页应用程序时，您将需要路径来将应用程序分成可访问的部分。

*在* [***查找更多内容***](https://plainenglish.io/)