# Preact 入门

> 原文：<https://javascript.plainenglish.io/getting-started-with-front-end-development-with-preact-f14c6d701a1f?source=collection_archive---------11----------------------->

## Preact 类似于 react，但要小得多

![](img/6ecdcf61fef61866b9ed7fc697aa7ed1.png)

Photo by [Maksim Larin](https://unsplash.com/@maksimcul8r?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Preact 是一个前端 web 框架，类似于 react。

它比 React 小，也不复杂。

在本文中，我们将了解如何开始使用 Preact 进行前端开发。

# 入门指南

我们可以导入 Preact 模块并调用`render`来呈现我们想要的内容。

例如，我们可以写:

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>app</title>
  </head>
  <body>
    <script type="module">
      import { h, Component, render } from "https://unpkg.com/preact?module";
      const app = h("h1", null, "Hello World");
      render(app, document.body);
    </script>
  </body>
</html>
```

我们从`preact`模块调用`h`方法来呈现一个元素。

`h`的第一个参数是标签名。

第二个参数是元素属性。

第三个参数是内容。

然后我们用`app`和`document.body`调用`render`来渲染`body`中的`app`。

# JSX 的替代品

我们也可以使用模板字符串来呈现元素。

为此，我们写道:

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>app</title>
  </head>
  <body>
    <script type="module">
      import { h, Component, render } from "https://unpkg.com/preact?module";
      import htm from "https://unpkg.com/htm?module";
      const html = htm.bind(h);
      function App(props) {
        return html`<h1>Hello ${props.name}!</h1>`;
      } render(html`<${App} name="james" />`, document.body);
    </script>
  </body>
</html>
```

我们导入`html`函数并将`html`中的`this`值绑定到`h`函数。

然后，我们可以使用模板字符串来呈现我们的内容。

我们将道具传递给`App`，就像我们传递给 React 一样。

然后我们用`App`的模板字符串再次调用带有`html`标签的`render`。

# Preact CLI

我们可以使用 Preact CLI 创建一个生产就绪的 Preact 项目。

为了全局安装它，我们运行:

```
npm install -g preact-cli
```

然后，我们可以使用以下内容进行生产构建:

```
npm run build
```

# 预动作 X

Preact X 提供了许多新功能。

一个特征包括片段。它是一个容器组件，允许我们在一个根容器中添加多个组件。

例如，我们可以写:

```
import { Component, render, Fragment } from "preact";export default class App extends Component {
  render(props, { results = [] }) {
    return (
      <>
        <div>foo</div>
        <div>bar</div>
      </>
    );
  }
}if (typeof window !== "undefined") {
  render(<App />, document.getElementById("root"));
}
```

我们导入`Fragment`组件，然后我们可以使用`<>`和`</>`符号来添加我们的片段。

这就像它在 React 中的工作方式。

# componentDidCatch

我们可以用`componentDidCatch`方法捕捉错误。

例如，我们可以写:

```
import { Component, render } from "preact";export default class App extends Component {
  state = { errored: false }; componentDidCatch(error) {
    this.setState({ errored: true });
  } render(props, state) {
    if (state.errored) {
      return <p>error</p>;
    }
    return props.children;
  }
}if (typeof window !== "undefined") {
  render(<App />, document.getElementById("root"));
}
```

捕捉在`render`或其他生命周期方法中出现的任何错误。

# 结论

我们可以使用 Preact 轻松创建简单的应用程序。