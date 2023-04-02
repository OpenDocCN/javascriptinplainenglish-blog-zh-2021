# 如何向 React 应用添加 Redux

> 原文：<https://javascript.plainenglish.io/how-to-add-redux-to-a-react-app-1bcb06c81bce?source=collection_archive---------13----------------------->

本文介绍了如何将 Redux 添加到 React TypeScript 应用程序中。

![](img/54b7b9261b32c47c71e0d97a7ac52e5e.png)

Photo by [Nubelson Fernandes](https://unsplash.com/@nublson?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 录像

观看 [YouTube 视频](https://youtu.be/upcZZAN7Gt8?list=PLVgOtoUBG2mdLpj6qT5DXfg5_pGPTDrJZ):

# 演示

[CodeSandbox 演示](https://codesandbox.io/s/react-redux-typescript-oof6n):

# 先决条件

给定一个由[引导的应用，创建 React 应用](https://create-react-app.dev/):

```
$ npx create-react-app my-app --template typescript && cd my-app
```

# 安装

安装依赖项:

*   [@ reduxjs/工具包](https://www.npmjs.com/package/@reduxjs/toolkit)
*   [@types/react-redux](https://www.npmjs.com/package/@types/react-redux)
*   [react-redux](https://www.npmjs.com/package/react-redux)

使用 npm:

```
$ npm install @reduxjs/toolkit @types/react-redux react-redux
```

或者用纱线:

```
$ yarn add @reduxjs/toolkit @types/react-redux react-redux
```

# 薄片

创建[切片](https://redux-toolkit.js.org/api/createSlice):

# 商店

创建[商店](https://redux.js.org/api/store):

# 供应者

使用`[<Provider>](https://react-redux.js.org/api/provider)`使存储对所有嵌套组件可用:

# 成分

创建组件:

[UI 通过](https://react-redux.js.org/introduction/why-use-react-redux#integrating-redux-with-a-ui)[挂钩](https://react-redux.js.org/api/hooks)与 Redux 集成。

不在`[useSelector](https://react-redux.js.org/api/hooks#useselector)`中键入回调函数将抛出 TypeScript 错误:

```
Property 'counter' does not exist on type 'DefaultRootState'.
```

这可以通过键入`state`来修复:

# 钩住

或者，键入[挂钩](https://react-redux.js.org/api/hooks):

为便于在组件中使用:

# 资源

*   [react-redux-typescript-app](https://github.com/remarkablemark/react-redux-typescript-app)
*   [CRA-template-redux-typescript](https://github.com/reduxjs/cra-template-redux-typescript)
*   [cra-template-redux](https://github.com/reduxjs/cra-template-redux)

[*本文原载于 2021 年 8 月 1 日《remarkablemark.org》。*](https://b.remarkabl.org/2RYxRyh)

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)