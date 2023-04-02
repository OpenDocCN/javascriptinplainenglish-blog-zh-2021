# 使用 react-modal-video 和 React-response-Modal 向 React 应用程序添加模态

> 原文：<https://javascript.plainenglish.io/add-a-modal-to-a-react-app-with-react-modal-video-and-react-responsive-modal-a9b21173c7f?source=collection_archive---------10----------------------->

![](img/46383cfeaff554ffd9ecc354e814ca26.png)

Photo by [Zuriela Benitez](https://unsplash.com/@zuriela_10?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

模态是我们必须经常添加到 React 应用程序中的东西。

为了使这项任务更容易，我们可以使用现有的组件库来添加它们。

在本文中，我们将看看如何使用 react-modal-video 和 React-response-modal 库向 React 应用程序添加一个模态。

# 反应模式视频

react-modal-video 库允许我们将视频模型添加到 react 应用程序中。

要安装它，我们运行:

```
npm i react-modal-video
```

然后我们可以通过写来使用它:

```
import React, { useState } from "react";
import ModalVideo from "react-modal-video";
import "react-modal-video/scss/modal-video.scss";export default function App() {
  const [isOpen, setOpen] = useState(false); return (
    <React.Fragment>
      <ModalVideo
        channel="youtube"
        autoplay
        isOpen={isOpen}
        videoId="sSZNLAIL65M"
        onClose={() => setOpen(false)}
      /> <button className="btn-primary" onClick={() => setOpen(true)}>
        open
      </button>
    </React.Fragment>
  );
}
```

我们添加了`ModalVideo`组件来添加视频模态。

`channel`道具让我们用视频来设置站点。

`autoplay`启用自动播放。

`isOpen`有模态打开状态。

`videoId`有视频的 ID 要嵌入到模态中。

`onClose`是在我们关闭模态时运行的。

其他受支持的网站包括 Vimeo 和 Yorku。

我们可以用`ratio`道具设置长宽比。

`allowFullScreen`让我们启用全屏显示。

`animationSpeed`设置打开或关闭模态时动画的速度。

我们还可以用`modalVideo`、`modalVideoClose`、`modalVideoBody`、`modalVideoInner`等道具来设置模态各部分的类名。

# 反应-响应-模态

react-response-modal 库是另一个允许我们将模态添加到 React 应用程序中的库。

要安装它，我们运行:

```
npm i react-responsive-modal
```

和 NPM 一起安装。

我们也可以通过运行以下命令安装纱线:

```
yarn add react-responsive-modal
```

然后我们可以通过写来使用它:

```
import React, { useState } from "react";
import "react-responsive-modal/styles.css";
import { Modal } from "react-responsive-modal";export default function App() {
  const [open, setOpen] = useState(false);
  const onOpenModal = () => setOpen(true);
  const onCloseModal = () => setOpen(false); return (
    <div>
      <button onClick={onOpenModal}>Open modal</button>
      <Modal open={open} onClose={onCloseModal} center>
        <h2>Simple centered modal</h2>
      </Modal>
    </div>
  );
}
```

我们导入带有模态样式的 CSS 文件。

我们有`open`状态，当它是`true`时打开模态，否则关闭它。

然后我们添加带有`Modal`组件的模态。

我们传入`open`状态作为`open`属性的值来控制它。

当`onClose`运行时，我们将`open`设置为`false`，此时我们关闭模态。

`center`在屏幕上居中情态。

模态内容是`Modal`组件的子组件。

# 结论

react-modal-video 和 react-response-modal 库让我们可以轻松地将模态添加到 React 应用程序中。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)