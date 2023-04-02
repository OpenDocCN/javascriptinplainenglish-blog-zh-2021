# 使用 react-spring 库向我们的 React 应用程序添加动画

> 原文：<https://javascript.plainenglish.io/add-animation-to-our-react-app-with-the-react-spring-library-ea3d8a54217f?source=collection_archive---------18----------------------->

![](img/0cfa45c043e3e68b8aa73e637dc8dc8b.png)

Photo by [Joel Holland](https://unsplash.com/@joelholland?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有了 react-spring 库，我们可以轻松地在 react 应用程序中渲染动画。

在本文中，我们将了解如何开始使用 react-spring。

# 装置

我们可以通过运行以下命令来安装 react-spring 包:

```
npm install react-spring
```

# 基础动画

我们可以用`useSpring`钩子创建基本的动画。

例如，我们可以写:

```
import React from "react";
import { useSpring, animated } from "react-spring";export default function App() {
  const props = useSpring({ opacity: 1, from: { opacity: 0 } });
  return <animated.div style={props}>hello world</animated.div>;
}
```

我们调用`useSpring`钩子来设置动画完成后应用的`opacity`。

`from`属性具有动画之前的样式。

`animated.div`组件让我们创建一个可以动画显示的 div。

我们将`props`变量传递给`style`道具来对其进行样式化。

我们还可以制作文本动画:

```
import React from "react";
import { useSpring, animated } from "react-spring";export default function App() {
  const props = useSpring({ number: 1, from: { number: 0 } });
  return <animated.span>{props.number}</animated.span>;
}
```

当`props.number`从 0 变为 1 时，我们制作动画。

同样，我们可以用`scroll`属性滚动一个 div。

例如，我们可以写:

```
import React from "react";
import { useSpring, animated } from "react-spring";export default function App() {
  const props = useSpring({ scroll: 300, from: { scroll: 0 } });
  return (
    <animated.div
      scrollTop={props.scroll}
      style={{ overflowY: "scroll", height: 200 }}
    >
      {Array(100)
        .fill()
        .map((_, i) => (
          <p key={i}>{i}</p>
        ))}
    </animated.div>
  );
}
```

我们从顶部向下滚动 300 像素。

此外，我们可以将多种效果结合在一起:

```
import React from "react";
import { useSpring, animated, interpolate } from "react-spring";export default function App() {
  const { o, xyz, color } = useSpring({
    from: { o: 0, xyz: [0, 0, 0], color: "red" },
    o: 1,
    xyz: [10, 20, 5],
    color: "green"
  }); return (
    <animated.div
      style={{
        color,
        background: o.interpolate((o) => `rgba(210, 57, 77, ${o})`),
        transform: xyz.interpolate(
          (x, y, z) => `translate3d(${x}px, ${y}px, ${z}px)`
        ),
        border: interpolate([o, color], (o, c) => `${o * 10}px solid ${c}`),
        padding: o
          .interpolate({ range: [0, 0.5, 1], output: [0, 0, 10] })
          .interpolate((o) => `${o}%`),
        borderColor: o.interpolate({
          range: [0, 1],
          output: ["red", "#ffaabb"]
        }),
        opacity: o.interpolate([0.1, 0.2, 0.6, 1], [1, 0.1, 0.5, 1])
      }}
    >
      {o.interpolate((n) => n.toFixed(2))}
    </animated.div>
  );
}
```

我们调用`useSpring`钩子来生成一些值，这些值被传递给`style` prop。

我们将`o`、`x`、`y`和`z`插入到不同的值中，以改变 div 动画的样式。

我们可以将反作用弹簧钩子创建的值直接传入组件。

例如，我们可以写:

```
import React, { useState } from "react";
import { useSpring, animated } from "react-spring";export default function App() {
  const [state, setState] = useState(1);
  const props = useSpring({ x: state ? 1 : 0 });
  return (
    <>
      <button onClick={() => setState((state) => (state === 1 ? 0 : 1))}>
        toggle
      </button>
      <animated.div
        style={{
          transform: props.x
            .interpolate({
              range: [0, 0.25, 0.35, 0.45, 0.55, 0.65, 0.75, 1],
              output: [1, 0.97, 0.9, 1.1, 0.9, 1.1, 1.03, 1]
            })
            .interpolate((x) => `scale(${x})`),
          backgroundColor: "red",
          height: 100,
          width: 100
        }}
      />
    </>
  );
}
```

我们添加 div，然后我们可以通过设置`transform`道具来改变缩放比例。

我们将值从`range`映射到`output`。

并且`x`是与`range`中的值相对应的`output`的值。

# 结论

我们可以使用 react-spring 在 React 应用程序中添加基本动画。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**