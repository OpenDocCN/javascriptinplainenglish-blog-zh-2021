# 用 React 和 JavaScript 创建一个待办事项应用

> 原文：<https://javascript.plainenglish.io/create-a-to-do-list-app-with-react-and-javascript-1bcfd87c4f4e?source=collection_archive---------18----------------------->

![](img/ecd9a4c87f71214879b1e15b9996bb84.png)

Photo by [Arisa Chattasa](https://unsplash.com/@golfarisa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个待办事项应用程序。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app todo-list
```

和 NPM 一起创建我们的 React 项目。

我们需要`uuid`来让我们轻松地为我们的待办事项创建唯一的 id。

要添加它，我们运行:

```
npm i uuidv4
```

# 创建待办事项应用程序

为了创建待办事项应用程序，我们编写:

```
import { useState } from "react";
import { v4 as uuidv4 } from "uuid";export default function App() {
  const [todo, setTodo] = useState("");
  const [todos, setTodos] = useState([]); const submit = (e) => {
    e.preventDefault();
    setTodos((todos) => [
      ...todos,
      {
        id: uuidv4(),
        todo
      }
    ]);
  }; const deleteTodo = (index) => {
    setTodos((todos) => todos.filter((_, i) => i !== index));
  }; return (
    <div className="App">
      <form onSubmit={submit}>
        <input value={todo} onChange={(e) => setTodo(e.target.value)} />
        <button type="submit">Add</button>
      </form>
      {todos.map((t, i) => {
        return (
          <div key={t.id}>
            {t.todo}
            <button onClick={() => deleteTodo(i)}>delete</button>
          </div>
        );
      })}
    </div>
  );
}
```

我们有绑定到输入框的`todo`状态。

`todos`州有一系列的待办事项。

在`submit`方法中，我们将待办事项添加到`todos`数组中。

我们调用`e.preventDefault()`来停止服务器端表单提交。

然后我们通过回调调用`setTodos`来获取`todos`并返回一个包含原始`todos`项的数组。

之后，我们将新的项目添加到它。

它有一个从`uuidv4`函数创建的`id`。

`todo`有待办事项文本。

当我们点击删除按钮时，调用`deleteTodo`函数。

在其中，我们用一个接受原始`todos`数组的回调来调用`setTodos`方法。

然后我们返回一个没有给定条目的数组`index`。

我们用`filter`方法过滤掉那个条目。

然后在`return`语句中，我们有一个表单，它的`input`元素带有`value`和`onChange`属性来获取输入值，并分别用`onChange`回调来设置它。

`onSubmit`以`submit`函数为其值。`submit`是我们点击添加按钮时调用的。

在那下面，我们有一个`todos.map`回调函数，它返回一个呈现了`t.todo`的 div 和一个当我们点击它时删除该项的按钮。

`key`道具设置为`t.id`唯一 ID。

这有助于 React 正确识别呈现的数组项。

# 结论

我们可以使用 React 和 JavaScript 轻松创建待办事项应用程序。

*更多内容看*[***plain English . io***](https://plainenglish.io/)