# 用 Vue 3 和 JavaScript 创建一个天气应用

> 原文：<https://javascript.plainenglish.io/create-a-weather-app-with-vue-3-and-javascript-9cd8fac99e?source=collection_archive---------15----------------------->

![](img/a8955b4bc60cdef0d38b0019c6364374.png)

Photo by [Wolfgang Hasselmann](https://unsplash.com/@wolfgang_hasselmann?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个天气应用程序。

# 创建项目

我们可以用 Vue CLI 创建 Vue 项目。

要安装它，我们运行:

```
npm install -g @vue/cli
```

与 NPM 或:

```
yarn global add @vue/cli
```

用纱线。

然后我们运行:

```
vue create weather-app
```

并选择所有默认选项来创建项目。

# 创建天气应用程序

为了创建天气应用程序，我们编写:

```
<template>
  <form @submit.prevent="getWeather">
    <div>
      <label>city</label>
      <input v-model.trim="city" />
    </div>
    <button type="submit">get weather</button>
  </form>
  <div>
    <p>feels like: {{ result.feels_like }}</p>
    <p>humidity: {{ result.humidity }}</p>
    <p>pressure: {{ result.pressure }}</p>
    <p>temperature: {{ result.temp }}</p>
    <p>high: {{ result.temp_max }}</p>
    <p>low: {{ result.temp_min }}</p>
  </div>
</template><script>
const APIKEY = "your-key";export default {
  name: "App",
  data() {
    return {
      city: "",
      result: {},
    };
  },
  methods: {
    async getWeather() {
      if (!this.city) {
        return;
      }
      const res = await fetch(
        `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=${APIKEY}`
      );
      const { main } = await res.json();
      this.result = main;
    },
  },
};
</script>
```

我们有一个输入表单，可以让我们进入城市。

我们用`v-model`将输入值绑定到`city`反应属性。

`trim`修饰符让我们删除输入值前后的空格。

`@submit`指令让我们监听当我们单击 get weather 按钮时触发的提交事件。

`prevent`让我们阻止服务器端提交，进行客户端提交。

在下面，我们显示响应的结果。

在脚本标签中，我们使用了`data`方法来返回反应属性。

`getWeather`方法调用`fetch`向 Open Weather Map API 发出请求，根据输入的`city`获取天气数据。

然后我们调用`res.json`将响应转换成 JavaScript 对象。

最后，我们将它赋给`this.result`，这样我们就可以在模板中显示它。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建一个天气应用。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)