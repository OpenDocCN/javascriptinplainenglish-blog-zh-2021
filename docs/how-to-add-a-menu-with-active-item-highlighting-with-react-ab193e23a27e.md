# 如何用 React 添加带有活动项目高亮的菜单？

> 原文：<https://javascript.plainenglish.io/how-to-add-a-menu-with-active-item-highlighting-with-react-ab193e23a27e?source=collection_archive---------14----------------------->

![](img/628f551a1a05af5aa13c9d8302d13795.png)

Photo by [Sunrise Photos](https://unsplash.com/@sunrisephotography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望添加一个菜单，在 React 应用程序中突出显示活动菜单项。

在本文中，我们将看看如何添加一个菜单，用 React 突出显示活动项目。

# 添加带有活动项目突出显示的菜单

要在 React 应用程序中添加一个带有活动项目高亮显示的菜单，我们可以监听`mouseenter`和`mouseleave`事件。

当发出`mouseenter`事件时，我们给悬停在上面的项目添加高亮。

当发出`mouseleave`事件时，我们清除所有项目上的高亮显示。

我们将`onMouseEnter`属性设置为`mouseenter`事件处理程序，将`onMouseLeave`属性设置为`mouseleave`事件处理程序。

为此，我们写道:

```
import { useState } from "react";export default function App() {
  const [hoveredItem, setHoveredItem] = useState("");
  const resetHover = () => setHoveredItem(""); return (
    <div className="App">
      <style>
        {`
          .hovered {
            color: red;
          }
        `}
      </style>
      <ul>
        <li
          className={hoveredItem === "apple" ? "hovered" : undefined}
          onMouseEnter={() => setHoveredItem("apple")}
          onMouseLeave={resetHover}
        >
          apple
        </li>
        <li
          className={hoveredItem === "orange" ? "hovered" : undefined}
          onMouseEnter={() => setHoveredItem("apple")}
          onMouseLeave={resetHover}
        >
          orange
        </li>
        <li
          className={hoveredItem === "grape" ? "hovered" : undefined}
          onMouseEnter={() => setHoveredItem("apple")}
          onMouseLeave={resetHover}
        >
          grape
        </li>
        <li
          className={hoveredItem === "pear" ? "hovered" : undefined}
          onMouseEnter={() => setHoveredItem("apple")}
          onMouseLeave={resetHover}
        >
          pear
        </li>
        <li
          className={hoveredItem === "banana" ? "hovered" : undefined}
          onMouseEnter={() => setHoveredItem("apple")}
          onMouseLeave={resetHover}
        >
          banana
        </li>
      </ul>
    </div>
  );
}
```

我们有`hoveredItem`状态来跟踪哪个项目被突出显示。

我们用`resetHover`函数调用`setHoveredItem`函数，用一个空字符串来重置`hoveredItem`的值。

在那下面，我们有带有样式的`style`标签，用于`hovered`类，它有当我们突出显示一个项目时应用的样式。

然后我们有了动态应用了`className`的`li`元素。

当`hoveredItem`值与我们传递给`setHoveredItem`函数的值相同时，我们应用`hovered`类。

`onMouseEnter`道具被设置为设置`hoveredItem`状态的功能。

当我们的鼠标离开`li`元素时，`onMouseLeave`道具被设置为`resetHover`函数来重置`hoveredItem`值。

现在，当我们将鼠标悬停在某个项目上时，我们应该会看到鼠标悬停的项目变成红色。

当鼠标离开项目时，项目会变回黑色。

# 结论

我们可以添加一个菜单，用 React easily 突出显示活动项目。

为此，我们只需监听`mouseenter`和`mouseleave`事件，并相应地应用该类来添加高亮显示。

*更多内容看*[***plain English . io***](http://plainenglish.io)