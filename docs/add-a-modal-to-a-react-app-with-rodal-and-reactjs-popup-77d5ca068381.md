# 使用 Rodal 和 Reactjs-popup 向 React 应用程序添加模态

> 原文：<https://javascript.plainenglish.io/add-a-modal-to-a-react-app-with-rodal-and-reactjs-popup-77d5ca068381?source=collection_archive---------14----------------------->

![](img/e05e1bb4f5102a1dab75be52f04fb0d2.png)

Photo by [Andre Ouellet](https://unsplash.com/@ledoc?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

模态是我们必须经常添加到 React 应用程序中的东西。

为了使这项任务更容易，我们可以使用现有的组件库来添加它们。

在本文中，我们将看看如何使用 Rodal 和 Reactjs-popup 库向 React 应用程序添加一个模态。

# 罗达尔

我们可以通过运行以下命令来添加 Rodal 库:

```
npm i rodal --save
```

然后我们可以通过写来使用它:

```
import React, { useState } from "react";
import Rodal from "rodal";
import "rodal/lib/rodal.css";export default function App() {
  const [visible, setVisible] = useState(false); return (
    <div>
      <div>
        <button onClick={() => setVisible(true)}>show</button> <Rodal visible={visible} onClose={() => setVisible(false)}>
          <div>Content</div>
        </Rodal>
      </div>
    </div>
  );
}
```

我们导入 Rodal 库及其样式。

然后我们将`visible`道具设置为`visible`状态，这样我们就可以控制它何时显示。

我们将`visible`设置为`true`来显示模态。

`onClose`是在我们点击关闭按钮时运行的。

在其中，我们用`false`调用`setVisible`来关闭模态。

它有许多其他选项作为道具。

`width`设置 wdith。`height`设置 hrigjt。

`showMask`控制我们是否显示遮罩。

`animation`设置动画类型。

`enterAnimation`和`leaveAnimation`设置显示或隐藏模态时的动画..

`duration`设置动画的持续时间。

`closeOnEsc`让我们在按下 escape 键时关闭模态。

例如，我们可以通过书写来使用它们中的一些:

```
import React, { useState } from "react";
import Rodal from "rodal";
import "rodal/lib/rodal.css";export default function App() {
  const [visible, setVisible] = useState(false); return (
    <div>
      <div>
        <button onClick={() => setVisible(true)}>show</button> <Rodal
          enterAnimation="zoom"
          leaveAnimation="zoom"
          closeOnEsc
          visible={visible}
          onClose={() => setVisible(false)}
        >
          <div>Content</div>
        </Rodal>
      </div>
    </div>
  );
}
```

其他可用的动画类型包括:

*   `fade`
*   `flip`
*   `door`
*   `rotate`
*   `slideUp`
*   `slideDown`
*   `slideLeft`
*   `slideRight`

# Reactjs-popup

Reactjs-popup 库允许我们添加一个附加到触发器元素的弹出窗口。

要安装它，我们运行:

```
npm i reactjs-popup
```

然后我们可以通过写来使用它:

```
import React from "react";
import Popup from "reactjs-popup";
import "reactjs-popup/dist/index.css";export default function App() {
  return (
    <div>
      <div>
        <Popup trigger={<button> Trigger</button>} position="right center">
          <div>Popup content here !!</div>
        </Popup>
      </div>
    </div>
  );
}
```

我们导入带有相关样式的`Popup`组件。

然后我们将`trigger`道具设置到触发元素。

`position`让我们用一个字符串设置弹出窗口的位置。

我们可以在标签之间添加任何我们想要的内容。

我们还可以通过添加`modal`道具来使用它打开一个模态:

```
import React from "react";
import Popup from "reactjs-popup";
import "reactjs-popup/dist/index.css";export default function App() {
  return (
    <div>
      <div>
        <Popup trigger={<button> Trigger</button>} modal nested>
          {(close) => (
            <div className="modal">
              <button className="close" onClick={close}>
                &times;
              </button>
              <div className="header"> Modal Title </div>
              <div className="content">Lorem ipsum</div>
              <div className="actions">
                <Popup
                  trigger={<button className="button"> Trigger </button>}
                  position="top center"
                  nested
                >
                  <span>Lorem ipsum</span>
                </Popup>
                <button
                  className="button"
                  onClick={() => {
                    console.log("modal closed ");
                    close();
                  }}
                >
                  close modal
                </button>
              </div>
            </div>
          )}
        </Popup>
      </div>
    </div>
  );
}
```

`close`功能可用于关闭模态。

`nested`道具让我们在模态中打开另一个模态。

# 结论

我们可以使用 Rodal 和 react-popup 库将模态添加到 React 应用程序中。

*阅读更多在*[***plain English . io***](https://plainenglish.io/)