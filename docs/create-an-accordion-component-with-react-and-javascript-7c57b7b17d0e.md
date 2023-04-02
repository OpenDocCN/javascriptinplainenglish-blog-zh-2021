# 用 React 和 JavaScript 创建一个 Accordion 组件

> 原文：<https://javascript.plainenglish.io/create-an-accordion-component-with-react-and-javascript-7c57b7b17d0e?source=collection_archive---------7----------------------->

![](img/55e9315dfebbb9bfe7ce53bfb4301820.png)

Photo by [David Vilches](https://unsplash.com/@circvs?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个 accordion 组件。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app accordion
```

和 NPM 一起创建我们的 React 项目。

# 创作手风琴

为了创建手风琴，我们编写:

```
import React, { useState } from "react";export default function App() {
  const [contents, setContents] = useState(
    Array(10)
      .fill()
      .map((_, i) => {
        return {
          title: `title ${i}`,
          description: `description ${i}`,
          expanded: false
        };
      })
  ); return (
    <div className="App">
      <style>
        {`
          .title {
            cursor: pointer;
            display: flex;
            justify-content: space-between;
          } .title,
          .description {
            border: 1px solid black;
            padding: 5px;
          }
        `}
      </style>
      {contents.map((c, i) => {
        return (
          <div key={c.title}>
            <div
              className="title"
              onClick={() => {
                const c = [...contents];
                c[i].expanded = !c[i].expanded;
                setContents(c);
              }}
            >
              <div>
                <b>{c.title}</b>
              </div>
              <div>
                {c.expanded ? <span>&#x2191;</span> : <span>&#x2193;</span>}
              </div>
            </div>
            {c.expanded && <div className="description">{c.description}</div>}
          </div>
        );
      })}
    </div>
  );
}
```

我们有包含手风琴内容的`contents`数组。

接下来，我们添加`style`标签，为 accordion 标题和内容添加样式。

然后我们将`contents`数组渲染成一个标题为 div 的手风琴。

`onClick`属性被设置为复制`contents`数组的函数。

然后我们切换索引为`i`的`contents`条目的`expanded`属性。

然后我们用`c`调用`setContents`来更新`contents`数组。

在包装器内部，我们显示了`c.title`值。

在此之下，我们根据`c.expanded`的值添加代码以显示`c.title`右侧的箭头。

`&#x2191;`为向上箭头，`&#x2193;`为向下箭头。

而在那下面，我们展示的是`c.expanded`为`true`时的描述 div。

# 结论

我们可以用 Reactr 和 JavaScript 添加一个手风琴。