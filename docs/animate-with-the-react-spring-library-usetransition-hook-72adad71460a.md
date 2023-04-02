# 使用反应弹簧库制作动画——使用过渡挂钩

> 原文：<https://javascript.plainenglish.io/animate-with-the-react-spring-library-usetransition-hook-72adad71460a?source=collection_archive---------6----------------------->

![](img/b27024c637642cd1b6dd94a883af4d8f.png)

Photo by [Boris Smokrovic](https://unsplash.com/@borisworkshop?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有了 react-spring 库，我们可以轻松地在 react 应用程序中渲染动画。

在本文中，我们将了解如何开始使用 react-spring。

# 使用过渡

我们可以使用`useTransition`钩子向 React 组件添加转换。

例如，我们可以写:

```
import React, { useState } from "react";
import { useTransition, animated } from "react-spring";const arr = [
  { text: 1, key: 1 },
  { text: 2, key: 2 },
  { text: 3, key: 3 }
];export default function App() {
  const [items] = useState(arr);
  const transitions = useTransition(items, (item) => item.key, {
    from: { transform: "translate3d(0,-40px,0)" },
    enter: { transform: "translate3d(0,0px,0)" },
    leave: { transform: "translate3d(0,-40px,0)" }
  });
  return transitions.map(({ item, props, key }) => (
    <animated.div key={key} style={props}>
      {item.text}
    </animated.div>
  ));
}
```

用`useTransition`钩子动画化`arr`数组的渲染。

我们从`useState`钩子创建了`items`状态。

然后我们将它作为第一个参数传递给`useTransition`钩子。

在第二个参数中，我们传入一个函数来返回每个项目的`key`属性，这是它的唯一 ID。

React 使用它来跟踪项目。

第三个参数有一个对象，它带有我们希望在动画之前使用`from`属性呈现的样式。

`enter`属性有项目进入时显示的样式。

并且`leave`属性具有当项目离开时显示的样式。

现在我们应该看到数字移到了屏幕上。

我们也可以使用`useTransition`钩子在组件之间切换。

例如，我们可以写:

```
import React, { useState } from "react";
import { useTransition, animated } from "react-spring";export default function App() {
  const [toggle, set] = useState(false);
  const transitions = useTransition(toggle, null, {
    from: { position: "absolute", opacity: 0 },
    enter: { opacity: 1 },
    leave: { opacity: 0 }
  });
  return (
    <>
      <button onClick={() => set(!toggle)}>toggle</button>
      {transitions.map(({ item, key, props }) =>
        item ? (
          <animated.div style={props} key={key}>
            <span role="img" aria-label="smile">
              😄
            </span>
          </animated.div>
        ) : (
          <animated.div style={props} key={key}>
            <span role="img" aria-label="smile">
              🤪
            </span>
          </animated.div>
        )
      )}
    </>
  );
}
```

我们有`toggle`状态，用按钮切换。

然后我们调用`useTransition`钩子，通过将`toggle`状态作为第一个参数传入来应用样式。

第三个参数是我们制作动画时想要应用的样式。

当`item`在 truthy 和 falsy 之间切换时，会显示相应的表情符号，因为我们调用`transitions.map`来映射转换和。

`item`具有`toggle`所具有的值。

我们还可以用它来呈现条件为`true`时显示的内容。

例如，我们可以写:

```
import React, { useState } from "react";
import { useTransition, animated } from "react-spring";export default function App() {
  const [show, set] = useState(false);
  const transitions = useTransition(show, null, {
    from: { position: "absolute", opacity: 0 },
    enter: { opacity: 1 },
    leave: { opacity: 0 }
  });
  return (
    <>
      <button onClick={() => set(!show)}>toggle</button>
      {transitions.map(
        ({ item, key, props }) =>
          item && (
            <animated.div key={key} style={props}>
              <span role="img" aria-label="smile">
                ✌️
              </span>
            </animated.div>
          )
      )}
    </>
  );
}
```

然后当`item`为`true`时，当`show`为`true`时，表情符号被显示。

# 结论

我们可以使用`useTransition`钩子轻松地向 React 组件添加转换。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**