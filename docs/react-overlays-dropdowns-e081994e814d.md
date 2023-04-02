# 反应-覆盖-下拉菜单

> 原文：<https://javascript.plainenglish.io/react-overlays-dropdowns-e081994e814d?source=collection_archive---------20----------------------->

![](img/27a8956a7c794b91360588c646a95c47.png)

Photo by [kazuend](https://unsplash.com/@kazuend?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

下拉菜单是我们必须经常添加到 React 应用程序中的东西。

为了使这项任务更容易，我们可以使用现有的组件库来添加它们。

在本文中，我们将看看如何使用 react-overlays 库将下拉菜单添加到 React 应用程序中。

# 下拉菜单

我们可以用`Dropdown`组件和`useDropdownMenu`和`useDropdownToggle`挂钩轻松添加下拉菜单。

例如，我们可以写:

```
import React, { useState } from "react";
import styled from "styled-components";
import Dropdown from "react-overlays/Dropdown";
import { useDropdownMenu, useDropdownToggle } from "react-overlays";const MenuContainer = styled("div")`
  display: ${(p) => (p.show ? "flex" : "none")};
  min-width: 150px;
  position: absolute;
  z-index: 1000;
  flex-direction: column;
  border: 1px solid #e5e5e5;
  background-color: white;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
`;const Menu = ({ role }) => {
  const { show, onClose, props } = useDropdownMenu({
    flip: true,
    offset: [0, 8]
  });
  return (
    <MenuContainer {...props} role={role} show={show}>
      <button type="button" onClick={onClose}>
        Item 1
      </button>
      <button type="button" onClick={onClose}>
        Item 2
      </button>
    </MenuContainer>
  );
};const Toggle = ({ id, children }) => {
  const [props, { show, toggle }] = useDropdownToggle();
  return (
    <button type="button" className="btn" id={id} {...props} onClick={toggle}>
      {children}
    </button>
  );
};const DropdownButton = ({ show, onToggle, drop, alignEnd, title, role }) => (
  <Dropdown
    show={show}
    onToggle={onToggle}
    drop={drop}
    alignEnd={alignEnd}
    itemSelector="button:not(:disabled)"
  >
    {({ props }) => (
      <div {...props} className="relative inline-block">
        <Toggle id="example-toggle">{title}</Toggle>
        <Menu role={role} />
      </div>
    )}
  </Dropdown>
);const ButtonToolbar = styled("div")`
  & > * + * {
    margin-left: 12px;
  }
`;export default function App() {
  const [show, setShow] = useState(false); return (
    <ButtonToolbar className="dropdown-example">
      <DropdownButton
        show={show}
        onToggle={(nextShow) => setShow(nextShow)}
        title={`${show ? "Close" : "Open"} Dropdown`}
      />
      <DropdownButton alignEnd title="Align right" />
      <DropdownButton drop="up" title="Drop up" />
      <DropdownButton role="menu" title="Role 'menu'" />
    </ButtonToolbar>
  );
}
```

首先，我们创建了`MenuContainer`组件，它有菜单按钮。

它是下拉菜单的容器。

它检查`show`道具以确定它是否显示。

我们让它绝对定位在我们点击菜单按钮的位置打开。

接下来，我们创建`Menu`组件来连接带有按钮的`MenuContainer`，当我们点击按钮时，它调用`onClose`。

这将关闭下拉菜单。

`onClose`函数由`useDropdownMenu`钩子返回。

我们将钩子返回的所有`props`传递给`MenuContainer`来控制它是打开还是关闭。

`show`功能让我们显示菜单。

然后我们添加`Toggle`组件来添加下拉切换。

`children`道具有按钮内容。

`toggle`功能让我们切换菜单。

`toggle`由`useDropdownToggle`道具返回。

然后我们添加`DropdownButton`将切换与菜单结合起来，让我们在点击按钮或点击外部时关闭菜单。

`ButtonToolbar`组件是另一个包含下拉按钮的 div。

我们添加了`DropdownButton`来打开下拉菜单，当我们点击它们的时候。

# 结论

我们可以通过 react-overlays 库轻松地将下拉菜单添加到 React 应用程序中。

*更多内容尽在* [***说白了***](https://plainenglish.io/)