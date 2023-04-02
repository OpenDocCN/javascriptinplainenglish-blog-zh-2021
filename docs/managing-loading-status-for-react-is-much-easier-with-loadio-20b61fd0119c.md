# 使用 Loadio 管理 React 的加载状态要容易得多

> 原文：<https://javascript.plainenglish.io/managing-loading-status-for-react-is-much-easier-with-loadio-20b61fd0119c?source=collection_archive---------5----------------------->

![](img/aeb30adc097408c4058c624e95953fe1.png)

# 介绍

许多项目包含异步调用。用户可能不知道这些操作，或者用户可能需要知道它们的状态。

为了通知用户这一点，加载组件显示在屏幕上，并通知用户有东西在运行。在这一点上，异步方法的管理应该以各种方式来管理，并且应该演示组件。

今天，我将向您展示如何使用 loadio 轻松处理这个问题。

[**loadio**](https://github.com/hepter/loadio) 软件包是一个简单易用的工具，允许您管理承诺的状态信息。

安装时使用:

```
# Yarn
$ yarn add loadio# NPM
$ npm install loadio
```

包装方法要遵循状态信息。

```
import { withPool } from "loadio"; 
const fetch = withPool(global.fetch);
```

或者用 PoolManager 直接添加 Promise。

```
PoolManager.append(fetch("get/data"));
```

仅此而已。通过调用已经包装好的新方法来代替旧方法，可以很容易地在主页上查看状态。

```
import { useStatus } from "loadio";
function HomePage({ isLoading }) {
  const status = useStatus();
  return (
    <>
      {isLoading ? "Loading..." : "Loaded!"}
      <button onClick={() => myWrappedfetch("get/data")}>Get</button>
    </>
  );
}
```

它还根据任务数量生成一定百分比的信息。

```
{
    isLoading?: boolean,
    percentage?: number,
    runningTasks?: number
}
```

React 组件的完整示例如下。

```
import React from "react";
import { withPool, withStatus } from "loadio"; 
const fetch = withPool(global.fetch);class HomePage extends React.Component { render(){
    const { isLoading, percentage } = this.props;  
    return (
      <>
        {isLoading ? "Loading..." : "Loaded!"}
        {percentage + "%"}
        <button onClick={() => fetch("get/data")}>Get</button>
      </>
    );
  }
}
export default withStatus(HomePage);
```

# 演示

# 结论

通过包装 Promise 方法或者直接添加它们，我们可以很容易地用百分比信息显示加载状态。

点击[这里](https://github.com/hepter/loadio)可以查看套餐详情。

谢了。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)