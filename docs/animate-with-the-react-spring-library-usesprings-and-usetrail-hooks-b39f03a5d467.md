# 使用 react-spring 库制作动画——使用弹簧和使用轨迹挂钩

> 原文：<https://javascript.plainenglish.io/animate-with-the-react-spring-library-usesprings-and-usetrail-hooks-b39f03a5d467?source=collection_archive---------6----------------------->

![](img/d0eaf1a951582f05e35b13af35b17540.png)

Photo by [Anisur Rahman](https://unsplash.com/@arjabedbd?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有了 react-spring 库，我们可以轻松地在 react 应用程序中渲染动画。

在本文中，我们将了解如何开始使用 react-spring。

# 使用弹簧

挂钩让我们可以创建多个弹簧，每个弹簧都有自己的配置。

例如，我们可以写:

```
import React from "react";
import { animated, useSprings } from "react-spring";const items = [
  { text: "foo", opacity: 0.3, id: 1 },
  { text: "bar", opacity: 0.6, id: 2 },
  { text: "baz", opacity: 0.9, id: 3 }
];export default function App() {
  const springs = useSprings(
    items.length,
    items.map((item) => ({ opacity: item.opacity, from: { opacity: 0 } }))
  ); return (
    <>
      {springs.map((props, i) => (
        <animated.div style={props} key={i}>
          {items[i].text}
        </animated.div>
      ))}
    </>
  );
}
```

使用`useSprings`钩子为每个项目创建动画样式。

第一个参数是要创建的样式对象的数量。

第二个参数是我们想要应用的样式的数组。

然后在 JSX 中，我们通过将`props`传递给`style`道具来应用样式。

我们也可以用`set`和`stop`功能控制我们的动画。

例如，我们可以写:

```
import React from "react";
import { animated, useSprings } from "react-spring";const items = [
  { text: "foo", opacity: 0.3, id: 1 },
  { text: "bar", opacity: 0.6, id: 2 },
  { text: "baz", opacity: 0.9, id: 3 }
];export default function App() {
  const [springs, set, stop] = useSprings(items.length, (index) => ({
    opacity: items[index].opacity,
    from: { opacity: 0 }
  })); return (
    <>
      <button onClick={() => set((index) => ({ opacity: 1 }))}>start</button>
      <button onClick={() => stop()}>stop</button>
      {springs.map((props, i) => (
        <animated.div style={props} key={i}>
          {items[i].text}
        </animated.div>
      ))}
    </>
  );
}
```

我们有相同的`items`数组。

我们使用带有函数的`useSpring`钩子作为第二个参数，而不是一个样式数组。

用一个函数作为第二个参数调用它，除了`springs`之外，还会给我们`set`和`stop`函数，

`set`函数让我们以给定的风格运行动画。

而`stop`功能让我们停止动画。

然后我们以同样的方式显示动画 div。

# 使用踪迹

`useTrail`让我们用一个配置创建多个弹簧。

例如，我们可以写:

```
import React from "react";
import { animated, useTrail } from "react-spring";const items = [
  { text: "foo", id: 1 },
  { text: "bar", id: 2 },
  { text: "baz", id: 3 }
];export default function App() {
  const trail = useTrail(items.length, { opacity: 1, from: { opacity: 0 } }); return (
    <>
      {trail.map((props, i) => (
        <animated.div style={props} key={i}>
          {items[i].text}
        </animated.div>
      ))}
    </>
  );
}
```

第一个参数是要创建的动画样式对象的数量。

第二个参数是要创建的动画样式。

然后我们可以像使用`useSprings`钩子一样应用它们。

# 结论

我们可以用`useSprings`和`useTrail`钩子为一组组件创建动画。