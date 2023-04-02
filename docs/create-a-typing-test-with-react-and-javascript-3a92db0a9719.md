# 用 React 和 JavaScript 创建一个类型测试

> 原文：<https://javascript.plainenglish.io/create-a-typing-test-with-react-and-javascript-3a92db0a9719?source=collection_archive---------7----------------------->

![](img/4aac751ddcac6538a9c342fe0f7912b4.png)

Photo by [Luca Onniboni](https://unsplash.com/@lucaonniboni?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个类型测试。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app typing-test
```

和 NPM 一起创建我们的 React 项目。

# 创建打字测试

为了创建类型测试，我们编写:

```
import React, { useEffect, useMemo, useState } from "react";
const text =
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus sit amet tellus tortor. ";export default function App() {
  const [textToType] = useState(text);
  const [typedText, setTypedText] = useState("");
  const [timer, setTimer] = useState();
  const [elapsedMs, setElapsedMs] = useState(0);
  const [started, setStarted] = useState(false);
  const [wpm, setWpm] = useState(0); const parts = useMemo(() => {
    const splitTextToType = textToType.split("");
    let endIndexMatch = 0;
    for (const [index, s] of splitTextToType.entries()) {
      if (s !== typedText[index]) {
        endIndexMatch = index;
        break;
      }
    }
    return {
      matchedPart: textToType.slice(0, endIndexMatch),
      unmatchedPart: textToType.slice(endIndexMatch)
    };
  }, [textToType, typedText]); const start = () => {
    const timer = setInterval(() => {
      setElapsedMs((elapsedMs) => elapsedMs + 1);
      if (!started) {
        setStarted(true);
      }
    }, 1000);
    setTimer(timer);
  }; const restart = () => {
    setStarted(started);
    setElapsedMs(0);
    setTypedText("");
  }; useEffect(() => {
    if (parts.unmatchedPart.length === 1) {
      clearInterval(timer);
      setWpm(textToType.split(" ").length / (elapsedMs / (60 * 1000)));
    }
  }, [parts, textToType, timer, elapsedMs]); if (parts.unmatchedPart.length > 1) {
    return (
      <div>
        <div>
          <b>{parts.matchedPart}</b>
          {parts.unmatchedPart}
        </div>
        <button onClick={start}>start</button>
        <textarea
          disabled={!started}
          value={typedText}
          onChange={(e) => setTypedText(e.target.value)}
          style={{ width: "90vw", height: "300px" }}
        ></textarea>
      </div>
    );
  } else {
    return (
      <div>
        Your words per minute is {wpm}
        <button onClick={restart}>restart</button>
      </div>
    );
  }
}
```

我们用输入的文本来定义`textToType`状态，以完成测试。

`typedText`有我们输入的文本。

`timer`有打字测试的计时器。

`elaspedMs`以毫秒为单位设置经过的时间。

`started`设置测试是否已经开始。

`wpm`每分钟字数达到了吗？

接下来，我们用`useMemo`钩子创建`parts`变量。

它的回调函数返回一个对象，其中包含我们输入的部分和我们还没有输入的部分。

有我们输入的部分。

有我们尚未输入的部分。

我们通过计算最后一个索引得到`matchedPart`，在这个索引中，我们输入的文本与`text`字符串中的内容相匹配。

我们分割`textToType`字符串并将其存储在`splitTextToType`中

然后我们循环遍历`splitTextToType`，得到`typedText`的第一个与`splitTextToType`数组不匹配的索引。

接下来，我们定义开始测试的`start`函数。

我们调用`setInterval`来创建设置`elaspedMs`状态的定时器。

它还将`started`状态设置为`false`。

回调每秒运行一次。

我们调用`setTimer`来设置`timer`值。

`restart`功能只是将数值重置为初始值。

在`useEffect`回调中，我们检查`parts.unmatchedPart`属性的长度，并清除`clearInterval`为`unmatchedPart`为 1 的计时器。

我们调用`setWpm`来设置每分钟的字数。

第二个数组包含我们正在观察的反应状态，只要其中任何一个发生变化，回调就会运行。

然后我们用`parts.unmatchedPart.length > 1`检查测试是否完成。

如果`parts.unmatchedPart.length > 1`是`true`，那么测试还没有完成，所以我们呈现了已键入和未键入的文本。

然后我们渲染按钮让 ys 开始测试。

我们有一个文本区域让用户输入测试。

如果`started`是`false`，我们禁用文本区域。

我们用`value`和`onChange`获取并设置输入的值。

否则，测试完成，我们显示每分钟的单词和一个按钮，我们可以单击该按钮重新开始测试。

# 结论

我们可以用 React 和 JavaScript 轻松创建一个类型测试。

*更多内容请看*[***plain English . io***](http://plainenglish.io)