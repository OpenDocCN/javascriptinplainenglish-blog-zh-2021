# 反应叠加—模式转换

> 原文：<https://javascript.plainenglish.io/react-overlays-modal-transitions-319a5d1009ce?source=collection_archive---------8----------------------->

![](img/f157f6278e867cd664d77b756d2ceed6.png)

Photo by [Joseph Keil](https://unsplash.com/@sephkeil?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

模态是我们必须经常添加到 React 应用程序中的东西。

为了使这项任务更容易，我们可以使用现有的组件库来添加它们。

在本文中，我们将看看如何使用 react-overlays 库将一个模型添加到 React 应用程序中。

# 模态转换

我们可以在打开反应叠加模式时添加过渡效果。

例如，我们可以写:

`styles.css`

```
.fade {
  opacity: 0;
  transition: opacity 500ms linear;
}.show {
  opacity: 1;
}.backdrop.fade.show {
  opacity: 0.5;
}.dialog {
  position: absolute;
  width: 400;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  border: 1px solid #e5e5e5;
  background-color: white;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
  padding: 20px;
}
```

`App.js`

```
import React, { useState } from "react";
import { Transition } from "react-transition-group";
import styled from "styled-components";
import Modal from "react-overlays/Modal";
import "./styles.css";
const FADE_DURATION = 500;const AModal = styled(Modal)`
  position: fixed;
  width: 400px;
  z-index: 1040;
  top: 20px;
  left: 30px;
  border: 1px solid #e5e5e5;
  background-color: white;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
  padding: 20px;
`;const fadeStyles = {
  entering: "show",
  entered: "show"
};const Fade = ({ children, ...props }) => (
  <Transition {...props} timeout={FADE_DURATION}>
    {(status, innerProps) =>
      React.cloneElement(children, {
        ...innerProps,
        className: `fade ${fadeStyles[status]} ${children.props.className}`
      })
    }
  </Transition>
);export default function App() {
  const [showModal, setShowModal] = useState(false);return (
    <div className="flex flex-col items-center">
      <button
        type="button"
        className="btn btn-primary mr-3"
        onClick={() => setShowModal((prev) => !prev)}
      >
        Show Animated Modal
      </button>
      <AModal
        show={showModal}
        onHide={() => setShowModal(false)}
        transition={Fade}
        backdropTransition={Fade}
        renderBackdrop={(props) => (
          <div {...props} className="backdrop absolute inset-0 bg-black z-40" />
        )}
        renderDialog={(props) => (
          <div
            {...props}
            className="fixed inset-0 z-50 flex items-center justify-center pointer-events-none"
          >
            <div className="dialog bg-white shadow rounded-lg pointer-events-auto">
              <h4 id="modal-label">I&apos;m fading in!</h4>
              <p>Anim pariatur</p>
              <button
                type="button"
                className="btn"
                onClick={() => setShowModal(false)}
              >
                Close
              </button>
            </div>
          </div>
        )}
      />
    </div>
  );
}
```

我们用样式组件的`styled`函数创建模型。

我们从 react-overlays 库中传入`Modal`组件来创建具有我们自己风格的模型。

同样，我们用`fadeStyles`对象设置淡入淡出的样式。

我们设置了动画播放时的淡入淡出效果。

然后在`App`中，我们添加按钮，通过调用`setShowModal`到`true`来打开模态。

我们使用`renderDialog`道具渲染模态中的项目。

它有一个函数返回一个分量作为值。

# 结论

当我们使用 react-overlays 添加模态时，我们可以在模态打开时添加过渡效果。

*在* [***查找更多内容***](https://plainenglish.io/)