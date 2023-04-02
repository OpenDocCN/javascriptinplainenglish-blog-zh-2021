# 成帧器动作—共享布局动画

> 原文：<https://javascript.plainenglish.io/framer-motion-shared-layout-animations-4d83e10a4690?source=collection_archive---------12----------------------->

![](img/46407ee22a707c93cc31e115e7a01b09.png)

Photo by [Johannes Plenio](https://unsplash.com/@jplenio?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有了 Framer Motion 库，我们可以轻松地在我们的 React 应用程序中呈现动画。

在本文中，我们将了解如何开始使用 Framer Motion。

# 共享布局动画

我们可以使用`AnimateSharedLayout`组件创建共享布局动画。

例如，我们可以写:

`App.js`

```
import React, { useState } from "react";
import { AnimatePresence, AnimateSharedLayout, motion } from "framer-motion";
import "./styles.css";function Item({ text }) {
  const [isOpen, setIsOpen] = useState(false);const toggleOpen = () => setIsOpen(!isOpen);return (
    <motion.li layout onClick={toggleOpen} initial={{ borderRadius: 10 }}>
      <motion.div layout>{text}</motion.div>
      <AnimatePresence>{isOpen && <Content />}</AnimatePresence>
    </motion.li>
  );
}function Content() {
  return (
    <motion.div
      layout
      initial={{ opacity: 0 }}
      animate={{ opacity: 1 }}
      exit={{ opacity: 0 }}
    >
      <div className="row" />
      <div className="row" />
      <div className="row" />
    </motion.div>
  );
}const items = [
  { text: "foo", id: 1 },
  { text: "bar", id: 2 },
  { text: "baz", id: 3 }
];export default function App() {
  return (
    <AnimateSharedLayout>
      <motion.ul layout>
        {items.map(({ text, id }) => (
          <Item text={text} key={id} />
        ))}
      </motion.ul>
    </AnimateSharedLayout>
  );
}
```

`styles.css`

```
html,
body {
  min-height: 100vh;
  padding: 0;
  margin: 0;
}* {
  box-sizing: border-box;
}body {
  background-repeat: no-repeat;
  display: flex;
  justify-content: center;
  align-items: center;
}.App {
  font-family: sans-serif;
  text-align: center;
}ul,
li {
  list-style: none;
  margin: 0;
  padding: 0;
}ul {
  width: 300px;
  display: flex;
  flex-direction: column;
  background: white;
  padding: 20px;
  border-radius: 25px;
}li {
  background-color: rgba(214, 214, 214, 0.5);
  border-radius: 10px;
  padding: 20px;
  margin-bottom: 20px;
  overflow: hidden;
  cursor: pointer;
}li:last-child {
  margin-bottom: 0px;
}.avatar {
  width: 40px;
  height: 40px;
  background-color: #666;
  border-radius: 20px;
}.row {
  width: 100%;
  height: 8px;
  background-color: #999;
  border-radius: 10px;
  margin-top: 12px;
}
```

我们有`Item`组件，可以切换 div 的内容。

这是通过`AnimatPresence`组件完成的，如果是`true`，该组件将显示`Content`组件的内容。

`row`类创建了我们想要展示的小节。

在`App`中，我们将`AnimateSharedLayout`组件包裹在`ul`周围，让我们为每个`li`显示相同的动画。

动画在一组不共享状态的组件之间同步。

我们还可以在添加或移除不同组件时，使用通用`layoutId`在它们之间执行动画。

当带有`1ayoutId`道具的组件从树的某个部分移除并添加到其他部分时，新组件将自动从旧组件的位置设置动画。

例如，我们可以写:

`App.js`

```
import React, { useState } from "react";
import { AnimateSharedLayout, motion } from "framer-motion";
import "./styles.css";export default function App() {
  const [selected, setSelected] = useState(colors[0]);return (
    <AnimateSharedLayout>
      <ul>
        {colors.map((color) => (
          <Item
            key={color}
            color={color}
            isSelected={selected === color}
            onClick={() => setSelected(color)}
          />
        ))}
      </ul>
    </AnimateSharedLayout>
  );
}function Item({ color, isSelected, onClick }) {
  return (
    <li className="item" onClick={onClick} style={{ backgroundColor: color }}>
      {isSelected && (
        <motion.div
          layoutId="outline"
          className="outline"
          initial={false}
          animate={{ borderColor: color }}
          transition={spring}
        />
      )}
    </li>
  );
}const colors = ["red", "green", "blue", "yellow"];const spring = {
  type: "spring",
  stiffness: 500,
  damping: 30
};
```

`styles.css`

```
html,
body {
  min-height: 100vh;
  padding: 0;
  margin: 0;
}* {
  box-sizing: border-box;
}body {
  background-repeat: no-repeat;
  display: flex;
  justify-content: center;
  align-items: center;
}.App {
  font-family: sans-serif;
  text-align: center;
}ul {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: column;
  flex-wrap: nowrap;
  width: 280px;
  height: 380px;
}.item {
  width: 100px;
  height: 50px;
  margin: 20px;
  position: relative;
  cursor: pointer;
  flex-shrink: 0;
}.outline {
  position: absolute;
  top: -20px;
  left: -20px;
  right: -20px;
  bottom: -20px;
  border: 10px solid white;
}
```

我们在`li`周围添加了一个框，通过切换`Item`组件中的`isSelected`状态来点击该框。

在`styles.css`中，我们有`outline`类来定义轮廓。

这是在我们切换`li`时切换的。

在`App`组件中，选择我们使用`setSelected`功能点击的项目。

# 结论

我们可以添加共享布局动画，以执行跨一组不共享状态的组件同步的动画。

我们还可以在添加或移除不同组件时使用通用`layoutId`在它们之间执行动画。

喜欢这篇文章吗？如果是这样的话，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获得更多类似内容吧！**