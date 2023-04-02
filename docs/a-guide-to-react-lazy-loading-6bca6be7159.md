# 对延迟加载做出反应

> 原文：<https://javascript.plainenglish.io/a-guide-to-react-lazy-loading-6bca6be7159?source=collection_archive---------5----------------------->

## React 组件代码拆分指南

![](img/9fb9c1e6f5147ddead05dd0be5accda8.png)

Photo by [Clément Hélardot](https://unsplash.com/@clemhlrdt?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 我的旅程

随着我的单页应用程序的功能越来越丰富，它的大小也越来越大。事实上，每次我构建时，Webpack 都会警告我这一点。

```
WARNING in entrypoint size limit: The following entrypoint(s) combined asset size exceeds the recommended limit (244 KiB).
This can impact web performance.
Assets:
  static/js/main.ff956fb8.chunk.js (1.78 MiB)
```

用户需要等待这个 1.78MB 的文件完全加载到浏览器中，然后才能与它进行交互。如果网络连接很慢，这种感觉就像是永远。必须做些什么来让这种最初的体验变得更快。

# 代码拆分

代码分割将单个页面应用程序的代码分割成更小的块。不是全部请求，而是只请求当前需要的块。代码库分割得越多，每个块就越小，加载时间就越快。代码拆分是通过动态导入语法实现的。代替常规的导入语法，

```
import func from './func'func.doSomething()
```

动态导入返回一个承诺，该承诺将解析为导入模块的内容。

```
import('./func').then(func => func.doSomething());
```

Webpack(或其他捆绑器)将识别动态导入语法，并将`func`模块的内容放入它自己单独的代码块中。

# 惰性装载

但是这不是容易消耗的。兑现承诺不是一个快速简单的改变。幸运的是，React 通过其`lazy`函数使这变得简单多了。它与动态导入协同工作，为 React 组件启用代码拆分。

```
import React, { lazy } from 'react';const LazyLoad = lazy(() => import('./LazyLoad'));const App = () => {
  return <LazyLoad />;
};
```

现在，`App`和`LazyLoad`在不同的代码块中。仅当`App`被渲染时，请求被发送以获取`LazyLoad`代码块。当请求完成时，React 将呈现`LazyLoad`。您可以通过查看网络检查器中的 Javascript 请求来验证这一点。

# 焦虑

这也引入了一个问题。该组件不能立即呈现，因为它必须通过网络调用获取。这可能需要一些时间来完成。我们如何向用户展示一些东西，让他们知道有些东西正在加载，而不仅仅是坏了？

React 用`Suspense`组件解决了这个问题。该组件可以检测是否有任何子代(或孙代等)被延迟加载。当它们仍被请求时，`Suspense`将转而呈现指定的`fallback`。

```
const App = () => {
  return (
    <Suspense fallback="Loading">
      <LazyLoad />
    </Suspense>
  );
};
```

现在，当呈现 App 并发起获取`LazyLoad`代码的请求时，会呈现回退`Loading`。当这个请求完成时，React 将呈现`LazyLoad`。

# 块预取

为了最小化加载时间，如果您能够准确预测用户下一步需要什么，您还可以预取一些组件。例如，如果用户在登录页面上，您可以加载登录后主页。动态导入函数中带有`webpackPrefetch`键的行内注释将指示 Webpack 这样做。

```
const PrefetchLoad = lazy(() =>
  import(
    /* webpackPrefetch: true */ './PrefetchLoad'
  )
);

const App = () => {
  return (
    <Suspense fallback="Loading">
      {condition && <PrefetchLoad />}
    </Suspense>
  );
};
```

在这里，即使没有满足`condition`，应用程序也会抢先请求`PrefetchLoad`。当`condition`被满足时，`PrefetchLoad`将被立即渲染。

# 区块名称

默认情况下，代码分割块由创建它们的索引命名。在上面的例子中，`LazyLoad`包含在`0.chunk.js`中。如果有多个块，就很难知道哪个块对应于哪个代码。类似于[预取](#2e4d)，您可以使用`webpackChunkName`键指定带有行内注释的块名。

```
const LazyLoad = lazy(() =>
  import(/* webpackChunkName: 'lazyload' */ './LazyLoad')
);
```

现在，这个块将被称为`lazyload.chunk.js`以便于识别。

# 结论

在我的应用中，在实现延迟加载后，文件大小和初始加载时间显著下降。登录页面有自己的代码块，只有 5KB。此外，每个单独的路由都被分割成自己的块，常用的路由都被预取，以便在用户登录后可以立即使用。由于 React 惰性加载，所有这些代码拆分都是可能的。

*   [官方反应懒惰文档](https://reactjs.org/docs/code-splitting.html#reactlazy)
*   [本文 Github 回购](https://github.com/mjchang/medium/tree/master/lazy-loading)
*   [本文的 code sandbox](https://codesandbox.io/s/github/mjchang/medium/tree/master/lazy-loading)