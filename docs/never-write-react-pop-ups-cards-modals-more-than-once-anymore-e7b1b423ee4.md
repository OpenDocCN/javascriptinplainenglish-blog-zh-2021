# 再也不要写一次以上的反应弹出卡/模式了！

> 原文：<https://javascript.plainenglish.io/never-write-react-pop-ups-cards-modals-more-than-once-anymore-e7b1b423ee4?source=collection_archive---------10----------------------->

![](img/0414f5e5aed6bd0a2838e10dccbabe6f.png)

# 介绍

在今天的帖子中，我将告诉你我使用的一个包，我已经将它转换成一个包并为 React 社区发布。

使用 React 开发应用程序时，有时我们需要在屏幕上显示一个类似弹出窗口的窗口。根据所使用的包，这可能很容易，但偶尔也会很麻烦。我们通常希望通过将一个组件放在一个地方，来管理和使用我们希望在屏幕上显示为模态或弹出窗口的组件。

有许多方法可以重用根目录中的组件。为了被再次使用，创建的组件可能需要再次在根目录中定义，但是在这种情况下，我们可能必须编辑和更新根目录中的主组件。这些组件有时可能需要大量的数据，我们可能需要每次都从用户那里获得新的信息。

为了解决这些问题并提供易用性而开发的 [cardon](http://github.com/hepter/cardon) 允许将容器组件添加到根组件中一次，并在屏幕上显示弹出的卡片。

使用这些创建来同时显示的卡片就像调用一个函数一样简单。此外，我们不需要编辑任何文件来添加新的卡组件。可选地，该函数可以使用参数调用并异步等待，直到卡关闭。让我们用一个示例应用程序来表示这一点。

# 例子

*   首先，将 cardon 作为依赖项安装。

```
# Yarn
$ yarn add cardon# NPM
$ npm install cardon
```

*   将 CardonContainer 组件放在根文件中。

```
// App.jsx
import { CardonContainer } from "cardon";
function App() {
  return (
    <div>
       <Main />
+      <CardonContainer />
    </div >
  );
}
export default App;
```

*   创建一个名为`'cardon'`或任何名字的文件夹，然后把你的卡片放在那里。
*   像下面这样包装你想用作卡片的组件。

可重复使用卡的示例:

```
// ./cardon/MyModalCard.jsx
import { withCardon } from "cardon";
import React from "react";function MyModalCard({ visible, get, title }) {
  return (
    <Modal open={visible} onClose={get(null)}>
      My Reusable '{title}' Modal!
      <button onClick={get(true)}>Yes</button>
      <button onClick={get(false)}>No</button>
    </Modal>
  );
}
export default withCardon(MyModalCard);
```

或者使用 TypeScript:

```
// ./cardon/MyModalCard.tsx
import { withCardon } from "cardon";
import React from "react";interface Props {
    title: string 
} 
function MyModalCard({ visible, get, title }) {
  return (
    <div>
      My Reusable '{title}' Card!
      <button onClick={get(true)}>Yes</button>
      <button onClick={get(false)}>No</button>
    </div>
  );
}
export default withCardon<Props, boolean>(MyModalCard)
```

*   导入组件并到处调用下面的函数，瞧！

电话示例:

```
let result = await MyModalCard.show({ title: "Awesome" });
//...
//...
// Not required for hiding it, but might need to hide manually for some cases before user action.
MyModalCard.hide();
```

呼叫用法示例:

```
import React from "react";
import { MyModalCard } from "./cardon/MyModalCard";
function HomePage() {
  const [modalResult, setModalResult] = React.useState(false);
  const showModal = async () => {
    let result = await MyModalCard.show({ title: "Awesome" });
    setModalResult(result);
  }; return (
    <>
      {modalResult ? "Yes" : "No"}
      <button onClick={showModal}>Show</button>
    </>
  );
}
```

*   这里的一个关键点是名为“get(result:any)=>VoidFunction”的函数，它提供了能够返回值的函数的创建。我们必须创建并使用回调函数，以便在该函数的帮助下返回值。

您可以在该项目的主页上找到更详细的描述。

# 演示

# 结论

我已经介绍了一种不同的方式来管理卡片并轻松地再次展示它们。提前感谢您的评论和支持。

**GitHub 项目** [**链接**](https://github.com/hepter/cardon)

# 另请参阅:

[使用 loadio](https://mustafa-kuru.medium.com/managing-loading-status-for-react-is-much-easier-with-loadio-20b61fd0119c) 管理 React 的加载状态要容易得多

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)