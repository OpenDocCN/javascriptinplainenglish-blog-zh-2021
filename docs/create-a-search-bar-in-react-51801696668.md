# 在 React 中创建一个搜索栏

> 原文：<https://javascript.plainenglish.io/create-a-search-bar-in-react-51801696668?source=collection_archive---------3----------------------->

## 使用简单的表情词典应用程序学习反应

![](img/03527e88d50757fbd42c45db27a5e9e5.png)

Photo by [Christin Hume](https://unsplash.com/@christinhumephoto?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们知道如何在普通 JS 中获取输入，并在更改时添加事件侦听器和提交按钮来获取输入值并处理输出。

在本文中，我们将学习如何在 React 中做同样的事情，并在这个过程中创建一个有趣的应用程序。

# 关于应用程序

我们将创建一个表情符号字典应用程序，用户可以在输入框中键入表情符号，表情符号的含义将显示在输出中。如果找不到表情符号，我们会显示为“找不到表情符号”。

## 步骤 1:创建 React 应用程序

在命令行中使用以下命令安装 react 模板应用程序，这将创建一个包含所有 React 依赖项的 starter react 应用程序。

```
npx create-react-app emoji-app
```

## 步骤 2:创建字典

我们不是为这个简单的应用程序创建一个数据库来存储我们的数据。我们将把它存储在一个带有键-值对的 JS 对象中，其中键是表情符号，值是表情符号的含义

```
const emojiDictionary = {
  "😊": "Smiling",
  "😳": "disbelief",
  "😔": "sad",
  "🥡": "takeout box",
  "❤️": "love",
  "😑": "annoyance",
  "✔": "correct",
  "👏": "clap",
  "🙌": "high five",
  "😎": "cool"
};
```

## 步骤 3:使用 React 钩子设置状态

我们使用 React 中的 useState 函数为我们的应用程序创建一个状态。

我们在状态中需要两个元素——表情符号和意义

表情符号将存储用户输入，含义将包含表情符号含义，该含义将显示为输出

```
const [emoji, setEmoji] = useState("");
const [meaning, setMeaning] = useState("");
```

## 步骤 4:接受用户的输入

输入标签将有一个 onChange 事件，每当输入栏发生变化时，该事件就会被触发

```
<input
        onChange={changeHandler}
        value={emoji}
        placeholder={"Search your emoji"}
        className="input-element"
 />
```

## 步骤 5: onChange 处理程序和显示输出

创建一个 onChange 处理函数，它接受输入值，设置含义并显示输出。

```
function changeHandler(event) {
    const inputEmoji = event.target.value;
    setEmoji(inputEmoji);if (inputEmoji in emojiDictionary) {
      setMeaning(emojiDictionary[inputEmoji]);
    } else {
      setMeaning("Emoji not found");
    }
  }
```

setMeaning 钩子重新呈现组件，含义显示为输出。完整的应用程序代码如下所示，供您参考。

```
import './App.css';
import React, { useState } from "react";const emojiDictionary = {
  "😊": "Smiling",
  "😳": "disbelief",
  "😔": "sad",
  "🥡": "takeout box",
  "❤️": "love",
  "😑": "annoyance",
  "✔": "correct",
  "👏": "clap",
  "🙌": "high five",
  "😎": "cool"
};const emojis = Object.keys(emojiDictionary);function App() {
  const [emoji, setEmoji] = useState("");
  const [meaning, setMeaning] = useState("");function changeHandler(event) {
    const inputEmoji = event.target.value;
    setEmoji(inputEmoji);if (inputEmoji in emojiDictionary) {
      setMeaning(emojiDictionary[inputEmoji]);
    } else {
      setMeaning("Emoji not found");
    }
  }function emojiClickHandler(inputEmoji) {
    setMeaning(emojiDictionary[inputEmoji]);
  }return (
    <div className="App">
      <h1>Emoji Detector</h1>
      <input
        onChange={changeHandler}
        value={emoji}
        placeholder={"Search your emoji"}
        className="input-element"
      />
      <h2> {emoji} </h2>
      <h3> {meaning} </h3>
      {
        emojis.map((emoji) => (
          <span
            onClick={() => emojiClickHandler(emoji)}
            className="emoji"
          >
            {emoji}
          </span>
        ))
      }
    </div>
  );
}export default App;
```

现在，您可以创建一个简单的输入处理应用程序，接受用户的输入并显示输出。

谢谢你一直读到最后，希望这篇文章对你有所帮助。请关注我，获取更多此类文章！

# 参考

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)