# 使用样式化的 React Modal 和 react-overlays 向 React 应用程序添加模态

> 原文：<https://javascript.plainenglish.io/add-a-modal-to-a-react-app-with-styled-react-modal-and-react-overlays-ed9ec3fc2f00?source=collection_archive---------17----------------------->

![](img/a471d0bc486af092b0c92fee23a00d63.png)

Photo by [Joseph Keil](https://unsplash.com/@sephkeil?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

模态是我们必须经常添加到 React 应用程序中的东西。

为了使这项任务更容易，我们可以使用现有的组件库来添加它们。

在本文中，我们将看看如何使用样式化的 React Modal 和 react-overlays 库将一个模型添加到 React 应用程序中。

# 风格反应模式

风格化的 React 模态库让我们可以轻松地将模态添加到 React 应用程序中。

要安装它，我们运行:

```
npm i styled-react-modal
```

然后我们可以通过写来使用它:

```
import React, { useState } from "react";
import Modal, { ModalProvider } from "styled-react-modal";
import { ThemeProvider } from "styled-components";const StyledModal = Modal.styled`
  width: 20rem;
  height: 20rem;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: white;
`;function FancyModalButton() {
  const [isOpen, setIsOpen] = useState(false); function toggleModal(e) {
    setIsOpen(!isOpen);
  } return (
    <div>
      <button onClick={toggleModal}>Click me</button>
      <StyledModal
        isOpen={isOpen}
        onBackgroundClick={toggleModal}
        onEscapeKeydown={toggleModal}
      >
        <span>I am a modal!</span>
        <button onClick={toggleModal}>Close me</button>
      </StyledModal>
    </div>
  );
}export default function App() {
  return (
    <ThemeProvider theme={{}}>
      <ModalProvider>
        <FancyModalButton />
      </ModalProvider>
    </ThemeProvider>
  );
}
```

我们添加了`FancyModalButton`组件来添加模态触发器。

在组件内部，我们在组件内部添加了`StyledModal`。

它是从`Modal.style`标签创建的。

我们用`isOpen`道具控制`StyledModal`是打开还是关闭。

当背景被点击时，道具让我们运行代码。

而`onEscapeKeydown`让我们在按下 Esc 键时运行代码。

我们只是切换`isOpen`状态来打开或关闭模态，因为我们将它作为`isOpen`属性的值传递。

然后，我们通过在`ThemeProvider`和`ModalProvider`中传递样式化的模态来使用它。

# 反应-覆盖

我们可以使用 react-overlays 库向 react 应用程序添加一个模型。

要安装它，我们运行:

```
npm install react-overlays
```

与 NPM 或:

```
yarn add react-overlays
```

用纱线。

然后我们可以通过写来使用它:

```
import React, { useState } from "react";
import styled from "styled-components";
import Modal from "react-overlays/Modal";const Backdrop = styled.div`
  position: fixed;
  z-index: 1040;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: #000;
  opacity: 0.5;
`;const AModal = styled(Modal)`
  position: fixed;
  width: 400px;
  z-index: 1040;
  top: 20px;
  left: 30px;
  border: 1px solid #e5e5e5;
  background-color: white;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
  padding: 20px;
`;export default function App() {
  const [show, setShow] = useState(false); const renderBackdrop = (props) => <Backdrop {...props} />; return (
    <div className="modal-example">
      <button
        type="button"
        className="btn btn-primary mb-4"
        onClick={() => setShow(true)}
      >
        Open Modal
      </button> <AModal
        show={show}
        onHide={() => setShow(false)}
        renderBackdrop={renderBackdrop}
      >
        <div>
          <h4 id="modal-label">Text in a modal</h4>
          <p>Lorem ipsum</p>
        </div>
      </AModal>
    </div>
  );
}
```

我们创建了`Backdrop`组件，这是一个应用了一些样式的 div。

然后我们创建`AModal`组件，它是一个有固定位置的模态。

我们还设置了背景颜色和阴影来添加一些效果来显示模态。

在`App`中，我们有一个按钮，通过用`true`调用`setShow`来打开模态。

如果`show`是`true`，我们有`AModal`组件显示模态。

我们传入`Backdrop`组件作为`renderBackdrop`的值来渲染背景。

`onHide`是我们隐藏情态时的称呼。

# 结论

我们可以通过样式化的 React Modal 和 react-overlays 库轻松地将 Modal 添加到 React 应用程序中。

*详见*[***plain English . io***](https://plainenglish.io/)