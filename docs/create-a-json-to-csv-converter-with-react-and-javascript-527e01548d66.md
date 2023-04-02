# 用 React 和 JavaScript 创建一个 JSON 到 CSV 的转换器

> 原文：<https://javascript.plainenglish.io/create-a-json-to-csv-converter-with-react-and-javascript-527e01548d66?source=collection_archive---------10----------------------->

![](img/2c9a67d46de5f8c8923756bf7adb9c54.png)

Photo by [Johann Siemens](https://unsplash.com/@johannsiemens?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建 JSON 到 CSV。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app json-to-csv
```

和 NPM 一起创建我们的 React 项目。

# 创建 JSON 到 CSV 转换器应用程序

为了创建 JSON 到 CSV 转换器应用程序，我们编写:

```
import React, { useState } from "react";export default function App() {
  const [json, setJson] = useState("");
  const [csv, setCsv] = useState(""); const convert = async (e) => {
    e.preventDefault();
    const parsedJson = JSON.parse(json);
    if (
      !Array.isArray(parsedJson) ||
      !parsedJson.every((p) => typeof p === "object" && p !== null)
    ) {
      return;
    }
    const heading = Object.keys(parsedJson[0]).join(",");
    const body = parsedJson.map((j) => Object.values(j).join(",")).join("n");
    setCsv(`${heading}${body}`);
  }; return (
    <div>
      <form onSubmit={convert}>
        <div>
          <label>json</label>
          <textarea
            value={json}
            onChange={(e) => setJson(e.target.value)}
          ></textarea>
        </div>
        <button type="submit">convert</button>
      </form>
      <div>
        <label>csv</label>
        <textarea value={csv}></textarea>
      </div>
    </div>
  );
}
```

我们定义了`json`和`csv`状态来分别保存 JSON 和 CSV 字符串。

然后我们定义`convert`函数将`json`转换成`csv`。

在函数中，我们调用`e.preventDefault()`来做客户端表单提交。

然后我们解析`json`字符串。

如果 JSON 不是 JSON 数组，或者有任何不是对象的项，那么我们就停止运行这个函数。

否则，我们继续将 JSON 转换成 CSV。

我们使用属性名作为标题。

我们用`Object.keys`方法得到它们。

然后我们调用`parsedJson.map`将值映射到字符串，用逗号连接这些值，然后用一个新的行字符将它们连接在一起。

然后我们用`heading`和`body`的组合来调用`setCsv`。

在那下面，我们有一个将`onSubmit`属性设置为`convert`的表单。

当我们点击转换按钮时，`convert`运行，因为它的类型被设置为`submit`。

表单中的文本区域通过`value`和`onChange`属性绑定到`json`状态。

`onChange`道具被设置为用`e.target.value`调用`setJson`的函数。

在表单下方，我们显示了一个包含`csv`的文本区域。

我们通过设置`value`道具来显示它。

# 结论

我们可以用 React 和 JavaScript 创建一个 JSON 到 CSV 的转换器。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)