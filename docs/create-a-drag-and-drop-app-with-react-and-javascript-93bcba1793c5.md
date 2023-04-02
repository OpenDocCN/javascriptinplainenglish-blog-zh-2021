# 用 React 和 JavaScript 创建一个拖放应用程序

> 原文：<https://javascript.plainenglish.io/create-a-drag-and-drop-app-with-react-and-javascript-93bcba1793c5?source=collection_archive---------11----------------------->

![](img/02da479bf600f4f32663483d7e695962.png)

Photo by [Auto Fan](https://unsplash.com/@autofan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个拖放应用程序。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app drag-and-drop
```

和 NPM 一起创建我们的 React 项目。

# 创建拖放应用程序

为了创建拖放应用程序，我们编写:

```
import React, { useState } from "react";export default function App() {
  const [origin, setOrigin] = useState(["apple", "orange", "grape"]);
  const [target, setTarget] = useState([]); const drag = (ev, text) => {
    ev.dataTransfer.setData("text", text);
  }; const drop = (ev) => {
    const text = ev.dataTransfer.getData("text");
    const index = origin.findIndex((o) => o === text);
    setOrigin((origin) => origin.filter((_, i) => i !== index));
    setTarget((target) => [...target, text]);
  }; return (
    <div>
      <style>
        {`
          .draggable {
            border: 1px solid black;
            margin-right: 5px;
          }

          #target {
            border: 1px solid black;
            width: 95vw;
            height: 100px;
            padding: 5px;
          }
          `}
      </style>
      <h2>Draggable Elements</h2>
      {origin.map((o) => {
        return (
          <div
            className="draggable"
            draggable
            onDragStart={(e) => drag(e, o)}
            key={o}
            onClick={(e) => e.stopPropagation()}
          >
            {o}
          </div>
        );
      })} <h2>Target</h2>
      <div id="target" onDragOver={(e) => e.preventDefault()} onDrop={drop}>
        {target.map((t) => {
          return (
            <div className="draggable" key={t}>
              {t}
            </div>
          );
        })}
      </div>
    </div>
  );
}
```

我们将`origin`数组状态呈现到可以拖放的项目中。

`target`数组有被丢弃的项目。

接下来，我们有`drag`函数，它调用`ev.dataTransfer.setData`来设置我们想要拖动的数据。

第一个参数是我们可以用来获取数据的密钥。

第二个参数是对应键的数据。

接下来，我们有了用键调用`ev.dataTransfer.getData`来获取数据的`drop`方法。

然后我们调用`origin.findIndex`来查找数据的索引。

接下来，我们用回调函数调用的`setOrigin`从`origin`中移除项目，该回调函数返回没有`index`的`origin`数组的副本。

我们用一个回调函数调用`setTarget`，该回调函数返回一个追加了`text`值的`target`数组的副本。

在那下面，我们有一些用于拖放项目和容器的样式。

在那下面，我们渲染`origin`项。

为了使它们可以拖动，我们添加了`draggable`道具。

然后我们添加`onDragStart`道具，设置一个调用`drag`的函数。

`onClick`设置为一个函数，调用`e.stopPropagation`来阻止点击事件冒泡到父项和祖先项。

下面，我们用`onDragOver`和`onDrop`道具渲染`target`物品。

`onDragOver`被设置为`e.preventDefault()`的一个函数，这样我们就可以进行投放了。

并且`onDrop`被设置为`drop`以让我们将数据从`origin`移动到`target`。

# 结论

我们可以使用 React 和 JavaScript 轻松创建一个拖放应用程序。

*更多内容看*[***plain English . io***](http://plainenglish.io)