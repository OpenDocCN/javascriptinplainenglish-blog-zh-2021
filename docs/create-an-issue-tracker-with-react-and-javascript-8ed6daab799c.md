# 使用 React 和 JavaScript 创建问题跟踪器

> 原文：<https://javascript.plainenglish.io/create-an-issue-tracker-with-react-and-javascript-8ed6daab799c?source=collection_archive---------13----------------------->

![](img/037a8a408271ff06d00761f642dbcf0c.png)

Photo by [Sari Fayomie](https://unsplash.com/@sarifayomie?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将了解如何使用 React 和 JavaScript 创建问题跟踪器。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app issue-tracker
```

和 NPM 一起创建我们的 React 项目。

此外，我们必须安装`uuid`包，让我们为问题条目分配唯一的 id。

为此，我们运行:

```
npm i uuid
```

# 创建问题跟踪器

为了创建问题跟踪器，我们写道:

```
import React, { useState } from "react";
import { v4 as uuidv4 } from "uuid";export default function App() {
  const [issue, setIssue] = useState({
    description: "",
    priority: "low",
    assignee: ""
  });
  const [issues, setIssues] = useState([]); const addIssue = (e) => {
    e.preventDefault();
    const { description, priority, assignee } = issue;
    const formValid = description && priority && assignee;
    if (!formValid) {
      return;
    }
    setIssues((issues) => [
      ...issues,
      { id: uuidv4(), description, priority, assignee }
    ]);
  }; const deleteIssue = (index) => {
    setIssues((issues) => issues.filter((_, i) => i !== index));
  }; return (
    <div className="App">
      <form onSubmit={addIssue}>
        <div>
          <label>description</label>
          <input
            value={issue.description}
            onChange={(e) =>
              setIssue((issue) => ({ ...issue, description: e.target.value }))
            }
          />
        </div> <div>
          <label>priority</label>
          <select
            value={issue.priority}
            onChange={(e) =>
              setIssue((issue) => ({ ...issue, priority: e.target.value }))
            }
          >
            <option>low</option>
            <option>medium</option>
            <option>high</option>
          </select>
        </div> <div>
          <label>assignee</label>
          <input
            value={issue.assignee}
            onChange={(e) =>
              setIssue((issue) => ({ ...issue, assignee: e.target.value }))
            }
          />
        </div>
        <button type="submit">add issue</button>
      </form>
      {issues.map((issue, index) => {
        return (
          <div key={issue.id}>
            <p>description: {issue.description}</p>
            <p>priority: {issue.priority}</p>
            <p>assignee: {issue.assignee}</p>
            <button type="button" onClick={() => deleteIssue(index)}>
              delete issue
            </button>
          </div>
        );
      })}
    </div>
  );
}
```

我们定义了作为对象的`issue`状态。

然后我们定义`issues`状态，这是一个数组。

接下来，我们定义`addIssue`函数向`issues`添加项目。

在其中，我们调用`e.preventDefault`进行客户端表单提交。

然后我们检查`description`、`priority`和`assignee`是否有值。

如果有，那么我们用回调函数调用`setIssues`，返回一个添加了新条目的`issues`数组的副本。

`uuidv4`函数返回`issues`条目的唯一 ID。

接下来，我们定义`deleteIssue`函数，该函数用回调函数调用`setIssues`，该回调函数返回一个没有给定`index`条目的`issues`数组的副本。

在那下面，我们添加一个表单，将`onSubmit`属性设置为`addIssue`，让我们向`issues`数组添加一个条目。

在它里面，我们有 2 个输入和一个选择元素，并设置了它们的`value`和`onChange`道具。

`value`有每个字段的值。

和`onChange`道具让我们设置值。

我们将它们设置为使用回调函数调用`setIssue`的函数，该回调函数使用新属性返回`issue`对象的副本，覆盖现有属性。

然后，当我们单击类型为`submit`的按钮时，它会运行`onSubmit`处理程序。

接下来，我们调用`issues.map`来用`issue`值渲染 div。

在那下面，我们添加一个按钮，将`onClick`属性设置到一个函数中，该函数调用`deleteIssue`来删除给定`index`的问题。

# 结论

我们可以用 React 和 JavaScript 创建一个问题跟踪器。

*更多内容尽在*[***plain English . io***](http://plainenglish.io)