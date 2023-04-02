# 用 React 和 JavaScript 创建一个 Notes 应用

> 原文：<https://javascript.plainenglish.io/create-a-notes-app-with-react-and-javascript-4e7a3a1fa8cf?source=collection_archive---------13----------------------->

![](img/7ae5537fe034f6c53dbbb1d0362e54c7.png)

Photo by [Kelly Sikkema](https://unsplash.com/@kellysikkema?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个 notes 应用程序。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app notes
```

和 NPM 一起创建我们的 React 项目。

我们还需要添加`uuid`库，为每个笔记条目分配一个惟一的 ID。

要安装它，我们运行:

```
npm i uuid
```

# 创建 Notes 应用程序

为了创建 notes 应用程序，我们编写:

```
import React, { useMemo, useState } from "react";
import { v4 as uuidv4 } from "uuid";export default function App() {
  const [title, setTitle] = useState("");
  const [description, setDescription] = useState("");
  const [keyword, setKeyword] = useState("");
  const [notes, setNotes] = useState([]); const add = (e) => {
    e.preventDefault();
    setNotes((notes) => [
      ...notes,
      {
        id: uuidv4(),
        title,
        description
      }
    ]);
  }; const remove = (index) => {
    setNotes((notes) => notes.filter((_, i) => i !== index));
  }; const filteredNotes = useMemo(() => {
    if (!keyword) {
      return notes;
    }
    return notes.filter(({ title, description }) => {
      return title.includes(keyword) || description.includes(keyword);
    });
  }, [keyword, notes]); return (
    <div>
      <form onSubmit={add}>
        <h1>add note</h1>
        <div>
          <label>title</label>
          <input value={title} onChange={(e) => setTitle(e.target.value)} />
        </div>
        <div>
          <label>description</label>
          <input
            value={description}
            onChange={(e) => setDescription(e.target.value)}
          />
        </div>
        <button type="submit">add</button>
      </form> <form>
        <h1>search</h1>
        <div>
          <label>keyword</label>
          <input value={keyword} onChange={(e) => setKeyword(e.target.value)} />
        </div>
      </form>
      {filteredNotes.map((note, index) => {
        return (
          <div key={note.id}>
            <h2>{note.title}</h2>
            <p>{note.description}</p>
            <button type="button" onClick={() => remove(index)}>
              remove
            </button>
          </div>
        );
      })}
    </div>
  );
}
```

我们有`title`、`description`、`keyword`和`notes`州。

`title`和`description`有注释内容。

`keyword`是搜索笔记的关键字。

我们用`useState`钩子创建它们。

然后我们添加`add`函数来添加注释。

我们调用`e.preventDefault`来做客户端表单提交。

然后我们调用`setNotes`将注释条目添加到`notes`数组中。

我们通过向`setNotes`函数传递回调来实现这一点。

我们从回调参数中获取`notes`值，然后返回一个数组，并在末尾添加条目。

我们调用`uuidv4`为条目分配惟一的 ID。

接下来，我们创建`remove`函数来获取`index`并通过回调调用`setNotes`来移除条目。

在回调中，我们调用`filter`返回一个没有给定`index`的`notes`数组。

然后我们用`useMemo`钩子定义`filteredNotes`变量，返回经过`keyword`过滤的`notes`数组。

第二个数组包含要监视的值，以便更新返回值。

再往下，。我们有一个带有由类型为`submit`的按钮触发的`onSubmit`道具的表单，

输入分别设置`title`和`description`。

`value`被设定为状态。并且`onChange`用函数设置`title`和`description`状态。

`e.target.value`有输入值。

同样，我们对第二种形式也有类似的输入。

最后，我们将`filteredNotes`渲染成 div。

我们将`key`道具设置为一个唯一的 ID。

每个 div 都有一个按钮，当我们单击 remove 按钮时，这个按钮会调用`remove`。

# 结论

我们可以使用 React 和 JavaScript 轻松创建一个 notes 应用程序。

*更多内容请看*[***plain English . io***](http://plainenglish.io)