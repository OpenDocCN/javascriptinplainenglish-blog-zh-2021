# 用 D3 向 React 应用程序添加图形——加载 JSON、XML 和 TSV

> 原文：<https://javascript.plainenglish.io/adding-graphics-to-a-react-app-with-d3-loading-json-xml-and-tsv-cc5b1579a4a5?source=collection_archive---------18----------------------->

![](img/42ba637a81e51fd1336ea980f1c2e2d4.png)

Photo by [Toa Heftiba](https://unsplash.com/@heftiba?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

D3 让我们可以轻松地向前端 web 应用添加图形。

Vue 是一个流行的前端 web 框架。

他们合作得很好。在本文中，我们将了解如何使用 D3 为 Vue 应用添加图形。

# 正在加载 JSON

我们可以加载存储在外部文件中的 JSON。

例如，我们可以写:

`public/data.json`

```
[
  {
    "name": "John",
    "age": 30,
    "city": "New York"
  },
  {
    "name": "Jane",
    "age": 20,
    "city": "San Francisco"
  }
]
```

`src/App.js`

```
import React, { useEffect } from "react";
import * as d3 from "d3";const readJson = async () => {
  const data = await d3.json("/data.json");
  for (const { name, age } of data) {
    console.log(name, age);
  }
};export default function App() {
  useEffect(() => {
    readJson();
  }, []); return <div className="App"></div>;
}
```

我们有从`data.json`读取数据的`readJson`函数。

然后我们遍历包含已解析条目的`data`数组。

我们得到:

```
John 30
Jane 20
```

记录在案。

# 正在加载 XML 文件

D3 还附带了加载 XML 文件的`d3.xml`方法。

例如，我们可以写:

`public/data.xml`

```
<?xml version="1.0" encoding="UTF-8"?>
<root>
<row>
    <name>John</name>
    <age>30</age>
</row>
<row>
    <name>Jane</name>
    <age>32</age>
</row>
</root>
```

`src/App.js`

```
import React, { useEffect } from "react";
import * as d3 from "d3";const readXml = async () => {
  const data = await d3.xml("/data.xml");
  for (const n of data.documentElement.getElementsByTagName("name")) {
    console.log(n.textContent);
  }
};export default function App() {
  useEffect(() => {
    readXml();
  }, []); return <div className="App"></div>;
}
```

在`readXml`函数中，我们调用`d3.xml`来读取数据。

然后我们获取带有`name`标签的元素，然后遍历返回的项目。

# 加载制表符分隔的文件

我们可以用`d3.tsv`方法加载制表符分隔的文件。

例如，我们可以写:

`public/data.tsv`

```
name age city
John 30 New York
Jane 20 San Francisco
```

`src/App.js`

```
import React, { useEffect } from "react";
import * as d3 from "d3";const readTsv = async () => {
  const data = await d3.tsv("/data.tsv");
  for (const { name, age, city } of data) {
    console.log(name, age, city);
  }
};export default function App() {
  useEffect(() => {
    readTsv();
  }, []); return <div className="App"></div>;
}
```

我们称之为`readTsv`方法。

然后我们遍历解析过的行并记录它们。

然后我们得到:

```
John 30 New York 
Jane 20 San Francisco
```

已登录控制台。

# 结论

我们可以在 Vue 应用中用 D3 加载 CSV、TSV、XML 和 JSON 文件。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**