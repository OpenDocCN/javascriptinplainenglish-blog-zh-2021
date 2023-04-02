# 使用 D3 向 React 应用添加图形—格式化 tsv 和加载 CSV

> 原文：<https://javascript.plainenglish.io/adding-graphics-to-a-react-app-with-d3-format-tsvs-and-load-csvs-8520da109f65?source=collection_archive---------10----------------------->

![](img/d4b13d8b015cb355a1f1042d980b2f94.png)

Photo by [Clark Van Der Beken](https://unsplash.com/@snapsbyclark?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

D3 让我们可以轻松地向前端 web 应用添加图形。

React 是一个流行的前端 web 框架。

他们合作得很好。在本文中，我们将了解如何使用 D3 向 React 应用程序添加图形。

# tsvFormat

我们可以使用`tsvFormat`方法将对象数组转换成制表符分隔的字符串。

例如，我们可以写:

```
import React, { useEffect } from "react";
import * as d3 from "d3";const data = [
  { year: 2011, population: 10 },
  { year: 2012, population: 20 },
  { year: 2013, population: 30 }
];
export default function App() {
  useEffect(() => {
    const string = d3.tsvFormat(data, ["year", "population"]);
    console.log(string);
  }, []); return <div className="App"></div>;
}
```

那么`string`就是:

```
year population
2011 10
2012 20
2013 30
```

我们传入一个对象数组作为第一个参数。

第二个参数有一个列标题字符串数组。

# tsvFormatRows

我们可以调用`tsvFormatRows`方法将嵌套数组转换成制表符分隔的字符串。

例如，我们可以写:

```
import React, { useEffect } from "react";
import * as d3 from "d3";const data = [
  [2011, 10],
  [2012, 20],
  [2013, 30]
];
export default function App() {
  useEffect(() => {
    const string = d3.tsvFormatRows(data);
    console.log(string);
  }, []); return <div className="App"></div>;
}
```

通过`data`使用`tsvFormatRows`方法。

然后我们得到:

```
2011 10
2012 20
2013 30
```

记录在案。

# 计时器

我们可以添加 D3 自带的定时器，为 React 应用程序添加动画。

我们可以调用`d3.timer`方法来创建一个定时器:

```
import React, { useEffect } from "react";
import * as d3 from "d3";export default function App() {
  useEffect(() => {
    const timer = d3.timer(function (duration) {
      console.log(duration);
      if (duration > 150) {
        timer.stop();
      }
    }, 100);
  }, []); return <div className="App"></div>;
}
```

我们用一个回调函数调用`timer`,这个回调函数的参数是`duration`。

然后如果`duration`大于 150ms，那么我们调用`timer.stop`来停止定时器。

# 正在加载 CSV

我们可以用`d3.csv`方法在 React 应用程序中加载 CSV。

例如，我们可以写:

`public/data.csv`

```
name,age
John,30
Jane,32
```

`src/App.js`

```
import React, { useEffect } from "react";
import * as d3 from "d3";const readCsv = async () => {
  const data = await d3.csv("/data.csv");
  for (const { name, age } of data) {
    console.log(name, age);
  }
};export default function App() {
  useEffect(() => {
    readCsv();
  }, []); return <div className="App"></div>;
}
```

我们用`readCsv`函数从`public/data.csv`中读取数据。

然后我们遍历`data`数组，该数组包含已解析的 CSV 行。

我们得到了:

```
John 30 
Jane 32
```

# 结论

我们可以在 React 应用中用 D3 读取和创建 CSV 和 tsv。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**