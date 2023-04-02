# 如何在 React 中将数据从子组件发送到父组件

> 原文：<https://javascript.plainenglish.io/how-to-send-data-from-a-child-react-component-to-the-parent-component-16bb434e0280?source=collection_archive---------4----------------------->

![](img/8cf1376b0c25beab7438876cac8d27db.png)

Photo by [Colin Maynard](https://unsplash.com/@invent?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时在我们的 React 应用程序中，我们必须将数据从子组件发送到其父组件。

在本文中，我们将了解如何将数据从子 React 组件发送到其父组件。

# 将函数传递给子组件

为了将数据从父组件传递给子组件，我们可以将函数作为道具传递给子组件。

例如，我们可以写:

```
import React, { useState } from "react";const Counter = ({ parentCallback }) => {
  const [count, setCount] = useState(0); return (
    <button
      onClick={() => {
        const newValue = count + 1;
        setCount(newValue);
        parentCallback(newValue);
      }}
    >
      Click me {count}
    </button>
  );
};export default function App() {
  const callback = (val) => {
    console.log(val);
  }; return (
    <div>
      <Counter parentCallback={callback} />
    </div>
  );
}
```

我们有接受`parentCallback`道具的`Counter`组件。

在组件中，我们有从`useState`钩子创建的`count`状态。

然后我们有一个带`onClick`回调的按钮，它用`newValue`调用`parentCallback`。

在`App`组件中，我们将`callback`函数作为`parentCallback`属性的值传递给`Counter`组件。

现在，当我们单击 Click me 按钮时，我们应该看到`console.log`函数运行，其中`val`是我们在`Counter`中传递给`parentCallback`的值。

# 结论

通过从父组件向子组件传递函数，我们可以将数据从子 React 组件发送到父组件。

然后在子组件中，我们可以用我们想要的参数调用它，将参数值传递回父组件。

*更多内容看* [***说白了. io***](http://plainenglish.io/)