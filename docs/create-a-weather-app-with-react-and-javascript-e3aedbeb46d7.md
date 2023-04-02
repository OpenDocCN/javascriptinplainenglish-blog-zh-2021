# 用 React 和 JavaScript 创建一个天气应用

> 原文：<https://javascript.plainenglish.io/create-a-weather-app-with-react-and-javascript-e3aedbeb46d7?source=collection_archive---------13----------------------->

![](img/d52f9378b7afd833db40affa9527f759.png)

Photo by [Wim van 't Einde](https://unsplash.com/@wimvanteinde?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个天气应用程序。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app weather-app
```

和 NPM 一起创建我们的 React 项目。

# 创建天气应用程序

为了创建天气应用程序，我们编写:

```
import React, { useState } from "react";
const APIKEY = "your-key";export default function App() {
  const [city, setCity] = useState("");
  const [result, setResult] = useState({}); const getWeather = async (e) => {
    e.preventDefault();
    if (!city) {
      return;
    }
    const res = await fetch(
      `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${APIKEY}`
    );
    const { main } = await res.json();
    setResult(main);
  }; return (
    <div>
      <form onSubmit={getWeather}>
        <div>
          <label>city</label>
          <input value={city} onChange={(e) => setCity(e.target.value)} />
        </div>
        <button type="submit">get weather</button>
      </form>
      {result && (
        <div>
          <p>feels like: {result.feels_like}</p>
          <p>humidity: {result.humidity}</p>
          <p>pressure: {result.pressure}</p>
          <p>temperature: {result.temp}</p>
          <p>high: {result.temp_max}</p>
          <p>low: {result.temp_min}</p>
        </div>
      )}
    </div>
  );
}
```

我们将`APIKEY`变量设置为 OpenWeather API 的 API 键。

API 密匙可以从[https://home.openweathermap.org/api_keys](https://home.openweathermap.org/api_keys)免费获得。

接下来，我们定义`city`状态，我们用它来绑定城市字段的输入值。

`result`字段显示天气结果。

接下来，我们定义`getWeather`函数通过`city`获取天气数据。

在它里面，我们调用`e.preventDefault()`让我们做客户端表单提交。

然后我们检查`city`是否被设置。

如果设置了，那么我们用`fetch`向开放天气 API 发出一个 API 请求。

并且我们调用`setResult`来设置结果。

下面，我们创建一个表单，将`onSubmit`属性设置为`getWeather`，这样当我们单击 get weather 按钮时就会调用`getWeather`。

在表单内部，我们有一个设置为`value`和`onChange`属性的输入。

`onChange`设置为设置`city`状态值的函数。

`e.target.value`有输入值。

在表单下方，我们在用户上方显示了`result`属性。

# 结论

我们可以用 React 和 JavaScript 轻松创建一个天气应用。

*更多内容请看*[***plain English . io***](http://plainenglish.io)