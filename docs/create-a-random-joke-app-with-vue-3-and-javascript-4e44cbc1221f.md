# 用 Vue 3 和 JavaScript 创建一个随机笑话应用

> 原文：<https://javascript.plainenglish.io/create-a-random-joke-app-with-vue-3-and-javascript-4e44cbc1221f?source=collection_archive---------16----------------------->

![](img/c8607f920ae3001de7d9ac738cb5601d.png)

Photo by [Priscilla Du Preez](https://unsplash.com/@priscilladupreez?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个随机笑话应用程序。

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
vue create joke-app
```

并选择所有默认选项来创建项目。

# 创建随机笑话应用程序

我们可以通过编写以下代码来创建随机笑话应用程序:

```
<template>
  <div>
    <p>{{ joke }}</p>
    <button @click="getJoke">get new joke</button>
  </div>
</template><script>
export default {
  name: "App",
  data() {
    return {
      joke: "",
    };
  },
  methods: {
    async getJoke() {
      const res = await fetch("https://api.chucknorris.io/jokes/random");
      const data = await res.json();
      this.joke = data.value;
    },
  },
  beforeMount() {
    this.getJoke();
  },
};
</script>
```

我们在 p 元素中显示`joke`值。

这个按钮让我们在点击它的时候得到笑话

它调用`getJoke`来获得一个新的笑话。

在`getJoke`方法中，我们调用`fetch`来获得笑话值。

它发出一个 GET 请求，从 URL 获取笑话。

URL 是 Chuck Norris API。

它使用从响应中返回 JSON 对象的`json`方法返回一个带有对象的承诺。

然后我们从 JSON 对象获取`value`属性来设置`joke`反应属性。

在`beforeMount`方法中，我们调用`getJoke`以便在页面加载时显示笑话。

# 结论

我们可以使用 Vue 3 和 JavaScript 轻松创建一个随机笑话应用程序。

*阅读更多尽在* [***说白了. io***](https://plainenglish.io/)