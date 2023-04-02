# React 中哪里可以用钩子进行 API 调用？

> 原文：<https://javascript.plainenglish.io/where-can-we-make-api-calls-with-hooks-in-react-bd9022e1522e?source=collection_archive---------12----------------------->

![](img/aef0a32dca3227ecd375d804c1eeafd0.png)

Photo by [Andy Art](https://unsplash.com/@trojantry?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

发出 HTTP 请求是我们在 React 代码中经常要做的事情。

在这篇文章中，我们将看看在 React 组件中，我们应该在哪里使用 React 钩子进行 API 调用。

# 仅在装载时调用 API

为了只在组件挂载时进行 API 调用，我们可以使用带有空数组的`useEffect`回调作为第二个参数。

例如，我们可以写:

```
import { useEffect, useState } from "react";export default function App() {
  const [user, setUser] = useState({}); const getUser = async () => {
    const results = await fetch("https://randomuser.me/api/");
    const {
      results: [result]
    } = await results.json();
    setUser(result);
  }; useEffect(() => {
    getUser();
  }, []); return <div className="App">{JSON.stringify(user)}</div>;
}
```

我们有带`useState`钩子的`user`状态，它被设置为一个空对象。

然后我们定义了调用`fetch`发出 GET 请求的`getUser`函数。

我们调用`results.json()`方法来获得 JSON 响应。

然后我们调用`setUser`函数将响应设置为`user`状态的值。

然后在`useEffect`钩子中，我们调用`getUser`来发出请求。

空数组让我们在`App`挂载时运行`useEffect`回调。

然后我们向用户展示这个值。

# 每当一些属性或状态改变时，API 调用

要在属性或状态发生变化时进行 API 调用，我们可以编写:

```
import { useEffect, useState } from "react";export default function App() {
  const [id, setId] = useState(1);
  const [todo, setTodo] = useState({}); const getTodo = async () => {
    const results = await fetch(
      `https://jsonplaceholder.typicode.com/todos/${id}`
    );
    const data = await results.json();
    setTodo(data);
  }; useEffect(() => {
    getTodo();
  }, [id]); return (
    <div className="App">
      <button onClick={() => setId((id) => id + 1)}>increment id</button>
      <p>{JSON.stringify(todo)}</p>
    </div>
  );
}
```

我们有`id`和`todo`状态。

我们希望进行 API 调用来获取带有`id`值的数据。

为了发出请求，我们使用带有`id`的 URL 字符串调用`fetch`。

然后我们用`data`调用`setTodo`。

然后我们用回调调用`useEffect`来调用`getTodo`函数。

而我们在`[id]`数组里传入`useEffect`。

在那下面，我们有一个按钮可以调用`setId`来改变`id`的值。

我们在下面显示`todo`值。

现在，当我们单击按钮时，我们显示用给定的`id`发出请求后的最新响应。

要查看道具并在道具值更新时发出请求，我们可以编写:

```
import { useEffect, useState } from "react";const Todo = ({ id }) => {
  const [todo, setTodo] = useState({}); const getTodo = async () => {
    const results = await fetch(
      `https://jsonplaceholder.typicode.com/todos/${id}`
    );
    const data = await results.json();
    setTodo(data);
  }; useEffect(() => {
    getTodo();
  }, [id]);return <p>{JSON.stringify(todo)}</p>;
};export default function App() {
  const [id, setId] = useState(1); return (
    <div className="App">
      <button onClick={() => setId((id) => id + 1)}>increment id</button>
      <Todo id={id} />
    </div>
  );
}
```

我们有带`id`道具的`Todo`组件。

其余的代码与前面的例子相同。

# 结论

我们可以在用钩子创建的 React 组件中使用`useEffect`钩子进行 API 调用。

*更多内容看*[***plain English . io***](http://plainenglish.io)