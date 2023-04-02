# 如何将 React-Redux 与本地存储同步

> 原文：<https://javascript.plainenglish.io/how-to-synchronize-react-redux-with-local-storage-a2498564c295?source=collection_archive---------1----------------------->

使用本地存储来缓存 API 调用，以获得最佳体验

![](img/0eafb7af0f02c484f426e59f4fb3b1d3.png)

## 简介:

React Redux 作为一个全局状态管理系统与 React 一起使用时，是一个经过验证的解决方案。许多公司在招聘时要求 Redux 和 React 相结合。

## 为什么要坚持？

Redux 是一个很好的解决方案，用于在令人敬畏的组件之间共享状态，但是更多的时候，当您在一个新的选项卡或页面刷新中打开应用程序时，会面临一个挑战，这会导致状态丢失，如果处理不当，会导致 React for nested values 出现黑屏。

## **如何坚持？**

您可以使用几个解决方案来解决这个问题。我们可以使用一个定制的钩子来获取 Redux 状态，并将其放入本地存储中，但是尽管这种方法可能有其好处，但它就像重新发明轮子一样，可能弊大于利。

**我的坚持之道？**

我使用一个名为 redux-persist 的库，这是一个非常著名的包，每周下载量超过 50 万次，它使用起来非常简单、直观，并且可以完成任务。

```
// configureStore.js

import { createStore } from 'redux'
import { persistStore, persistReducer } from 'redux-persist'
import storage from 'redux-persist/lib/storage' // defaults to localStorage for web

import rootReducer from './reducers'

const persistConfig = {
  key: 'root',
  storage,
}

const persistedReducer = persistReducer(persistConfig, rootReducer)

export default () => {
  let store = createStore(persistedReducer)
  let persistor = persistStore(store)
  return { store, persistor }
}
```

只需几行代码就可以实现基本设置:您的存储与本地存储同步。

添加到应用程序

```
import { PersistGate } from 'redux-persist/integration/react'

// ... normal setup, create store and persistor, import components etc.

const App = () => {
  return (
    <Provider store={store}>
      <PersistGate loading={null} persistor={persistor}>
        <RootComponent />
      </PersistGate>
    </Provider>
  );
};
```

除此之外，您还可以在每次构建时传递键名来自动递增和废弃缓存，以避免与代码和本地存储不匹配。

通过这种设置，您可以将 Redux 状态的一部分列入黑名单或白名单。

例如，如果您希望每次都更新一个状态，您可以将它添加到黑名单中，也可以编写其他逻辑来根据需要进行处理。

因为该库提供了多个 API，比如 purge flush 等等。

作为一名软件工程师，请继续关注更多真实世界的例子和用例。

和平！

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)