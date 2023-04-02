# React 中的代码拆分—您需要知道的一切

> 原文：<https://javascript.plainenglish.io/code-splitting-in-react-all-you-need-to-know-392b0dfeb1fa?source=collection_archive---------1----------------------->

## React 中代码拆分的深入探讨。

许多 JavaScript 框架将所有依赖项捆绑到一个大文件中。这使得将 JavaScript 添加到 HTML 页面变得很容易。这个包只需要一个链接标签，而且设置页面所需的调用也更少，因为所有的 JavaScript 都在一个地方。

然而，在某一点上，一个包变得太大，在这一点上解释和执行代码的开销降低了页面的加载速度，而不是加速。

![](img/794a1528cf80a63194616c90e98411bf.png)

[link](https://www.google.com/url?sa=i&url=https%3A%2F%2Fdev.to%2Fben%2Fcomment%2F1a1p4&psig=AOvVaw0ajNg7EccWTU6bWFp1Nxb0&ust=1640890207155000&source=images&cd=vfe&ved=0CAsQjRxqFwoTCIiH6tbWifUCFQAAAAAdAAAAABAm)

这就是代码分割可以帮助你的地方。代码分割允许您有策略地从包中省略某些依赖项，然后只在需要的地方插入它们。这意味着它们只有在需要的时候才会被加载——只有在需要的时候才加载 JavaScript，这加快了页面的加载时间。

# 如何在 React 中进行代码拆分

![](img/9328e2a0fcabd7a3874e974faccabcd5.png)

[link](https://www.google.com/url?sa=i&url=https%3A%2F%2Ftwitter.com%2Fswyx%2Fstatus%2F1158369440326721537&psig=AOvVaw1Svbs9nvfv6QgDU0_MaKql&ust=1640890216832000&source=images&cd=vfe&ved=2ahUKEwiB_ZfF1on1AhVwrWoFHcrAAqUQjRx6BAgAEAk)

## **动态导入**

在 React 中分割代码的最简单方法是使用动态导入语法。有些绑定器可以本地解析动态导入语句，而有些则需要一些配置。动态导入语法适用于静态站点生成和服务器端呈现。

**之前:**

```
import { add } from './math';
console.log(add(16, 26));
```

**之后:**

```
import("./math").then(math => {
  console.log(math.add(16, 26));
});
```

这确保了只有在真正需要的时候才加载这个包。

## **使用 React.lazy**

`React.lazy`函数让你把一个动态导入渲染成一个常规组件。

**之前:**

```
import MyComponent from './MyComponent';
```

**之后:**

```
const MyComponent = React.lazy(() => import('./MyComponent'));
```

`React.lazy`接受一个必须调用动态`import()`的函数。这必须返回一个`Promise`，它解析为一个带有包含 React 组件的`default`导出的模块。

***注意*** *—组件必须呈现在* ***悬念*** *组件内，在加载时显示回退内容。*

```
import React, { Suspense } from 'react';

const MyComponent = React.lazy(() => import('./MyComponent'));

function MainComponent() {
  return (
    <div>
      <Suspense fallback={<div>Loading...</div>}>
        <MyComponent />
      </Suspense>
    </div>
  );
}
```

在等待组件加载时，`fallback` prop 接受您想要呈现的任何 React 元素。您可以将`Suspense`组件放在惰性组件之上的任何地方。您甚至可以用一个`Suspense`组件包装多个惰性组件。[ [链接](https://reactjs.org/docs/code-splitting.html) ]

现在，如果 ***网络调用*** 失败，您可以在代码中使用**错误边界**来显示错误。一旦创建了错误边界，当出现网络错误时，可以在惰性组件上方的任何地方使用它来显示错误状态。

```
import React, { Suspense } from 'react';
import MyErrorBoundary from './MyErrorBoundary';const MyComponent = React.lazy(() => import('./MyComponent'));

function MainComponent() {
  return (
    <div>
      <MyErrorBoundary>
        <Suspense fallback={<div>Loading...</div>}>
          <MyComponent />
        </Suspense>
      </MyErrorBoundary>
    </div>
  );
}
```

# **在哪里引入代码拆分**

决定在应用程序的什么地方引入代码分割可能有点棘手。你需要确保你选择的位置可以平均分割包，但不会破坏用户体验。

![](img/e30785f38ed93373cb4eb66979bd9184.png)

[link](https://www.google.com/url?sa=i&url=https%3A%2F%2Fmedium.com%2F%40mattdlockyer%2Fyoure-using-materialize-css-wrong-470b593e78e9&psig=AOvVaw1-64Xr4pI69_nropyL60i8&ust=1640890370803000&source=images&cd=vfe&ved=0CAsQjRxqFwoTCMjyhpzXifUCFQAAAAAdAAAAABAJ)

## **基于路由的代码拆分**

一个好的起点是路线。网络上的大多数人都习惯于页面转换，这需要花费一些时间来加载。您还倾向于一次重新呈现整个页面，因此您的用户不太可能同时与页面上的其他元素进行交互。

```
import React, { Suspense, lazy } from 'react';
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';

const Home = lazy(() => import('./routes/Home'));
const About = lazy(() => import('./routes/About'));

const App = () => (
  <Router>
    <Suspense fallback={<div>Loading...</div>}>
      <Switch>
        <Route exact path="/" component={Home}/>
        <Route path="/about" component={About}/>
      </Switch>
    </Suspense>
  </Router>
);
```

## **基于组件的代码拆分**

React 还允许您基于组件而不是原始功能来拆分代码。React-loadable 函数使您能够创建一个定制的加载器，该加载器只需动态导入一次所需的代码块。将动态导入包装在加载器中可以防止它们被包含在页面加载包中。

```
import Loadable from 'react-loadable';

function ProgressIndicator() {
  return <div>In Progress...</div>;
}

const LoaderContainerComponent = Loadable({
  loader: () => import('./loadable-another-component'),
  LoadingComponent: ProgressIndicator
});

class MyComponent extends React.Component {
  render() {
    return <LoaderContainerComponent/>;
  }
}
```

**现在去享受拆分代码的乐趣吧**

![](img/03d09cf04a943c1f64dd751452af14f8.png)

**延伸阅读:**

[](https://reactjs.org/docs/code-splitting.html#route-based-code-splitting) [## 代码分解-反应

### 大多数 React 应用程序会使用 Webpack、Rollup 或 Browserify 等工具“捆绑”文件。捆绑是一个过程…

reactjs.org](https://reactjs.org/docs/code-splitting.html#route-based-code-splitting) [](https://blog.logrocket.com/code-splitting-in-react-an-overview/) [## React 中的代码拆分:概述

### 尽管 JavaScript 是一种简单的语言，但它可以生成复杂得惊人的代码库。部分原因是…

blog.logrocket.com](https://blog.logrocket.com/code-splitting-in-react-an-overview/) 

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/)***[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的**[***社区不和谐***](https://discord.gg/GtDtUAvyhW) ***获得独家获取写作机会和建议。*******