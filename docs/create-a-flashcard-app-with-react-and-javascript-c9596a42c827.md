# 用 React 和 JavaScript 创建一个抽认卡应用

> 原文：<https://javascript.plainenglish.io/create-a-flashcard-app-with-react-and-javascript-c9596a42c827?source=collection_archive---------11----------------------->

![](img/1e05559fc0e92554ed8c96393c635caf.png)

Photo by [ben o'bro](https://unsplash.com/@benobro?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个抽认卡应用程序。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app flashcard
```

和 NPM 一起创建我们的 React 项目。

我们需要`uuid`来让我们轻松地为抽认卡项目创建唯一的 id。

要添加它，我们运行:

```
npm i uuidv4
```

# 创建抽认卡应用程序

为了创建抽认卡应用程序，我们编写:

```
import { useState } from "react";
import { v4 as uuidv4 } from "uuid";export default function App() {
  const [item, setItem] = useState({});
  const [items, setItems] = useState([]); const add = (e) => {
    e.preventDefault();
    const { question, answer } = item;
    const formValid = question && answer;
    if (!formValid) {
      return;
    }
    setItems((items) => [
      ...items,
      {
        id: uuidv4(),
        ...item
      }
    ]);
  }; const deleteItem = (index) => {
    setItems((items) => items.filter((_, i) => i !== index));
  }; return (
    <div className="App">
      <form onSubmit={add}>
        <div>
          <label>question</label>
          <input
            value={item.question}
            onChange={(e) =>
              setItem((item) => ({ ...item, question: e.target.value }))
            }
          />
        </div>
        <div>
          <label>answer</label>
          <input
            value={item.answer}
            onChange={(e) =>
              setItem((item) => ({ ...item, answer: e.target.value }))
            }
          />
        </div>
        <button type="submit">submit</button>
      </form>
      {items.map((item, index) => {
        return (
          <div key={item.id}>
            <b>question</b>
            <p>{item.question}</p>
            <b>answer</b>
            <p>{item.answer}</p>
            <button onClick={() => deleteItem(index)}>delete</button>
          </div>
        );
      })}
    </div>
  );
}
```

我们用`useState`钩子创建了`item`和`items`状态。

然后我们用`add`函数给`items`添加一个项目。

在函数中，我们调用`e.preventDefault()`来做客户端表单提交。

然后我们检查`question`和`answer`是否被设置。

如果是，那么我们调用`setItems`通过回调将一个项目添加到`items`数组中。

回调获取现有的`items`值，并返回一个新数组，新数组后面附加了新项。

`deleteItem`函数用回调函数调用`setItems`，该回调函数返回不带给定`index`条目的`items`数组。

在表单中，我们将`onSubmit`属性设置为`add`，这样当我们点击提交按钮时`add`就会运行。

输入有`value`和`onChange`属性，因此我们将输入的值绑定到属性。

我们向`setItem`传递一个回调，将属性设置为`e.target.value`，它具有输入的值。

下面，我们将`items`渲染成元素。

我们需要将`key`属性设置为一个惟一的 ID，以便 React 可以识别每个条目。

它还有一个按钮，当我们点击它时，它会用`index`调用`deleteItem`。

# 结论

我们可以用 React 和 JavaScript 轻松创建一个抽认卡应用。

*更多内容请看*[***plain English . io***](http://plainenglish.io)