# React 材质用户界面入门

> 原文：<https://javascript.plainenglish.io/get-started-with-material-ui-for-react-apps-feacedced55a?source=collection_archive---------18----------------------->

## 如何开始为 React 应用程序使用 Material UI 框架。

# 什么是材质 UI？

Material UI 是为设计 React 应用程序而制作的前端框架。它为我们提供了内置的 React 组件，可以导入这些组件并用于构建好看的用户界面。

# 装置

为了设置材质界面，我们可以把它安装成一个 NPM 包或者使用 Yarn。

```
npm install @material-ui/core// Or

yarn add @material-ui/core
```

安装完成后，您就可以开始在 React 应用程序中使用材质 UI 组件了。

# 使用

现在我们将导入一个[按钮](https://material-ui.com/components/buttons/)组件，并在一个示例 React 应用程序中使用它。

```
import React from 'react';
import ReactDOM from 'react-dom';
import Button from '@material-ui/core/Button';

function App() {
  return (
    <Button variant="contained" color="primary">
      Click Me!
    </Button>
  );
}

ReactDOM.render(<App />, document.querySelector('#root'));
```

# 摘要

Material UI 是快速启动和运行 React 应用程序的好方法。最近，我不得不在大约一周前的一次黑客马拉松上学习它。出乎我意料的是，它超级容易上手！我肯定会在未来的 React 应用中使用这个框架。

## 参考

*   [物料 UI 单据](https://material-ui.com/)