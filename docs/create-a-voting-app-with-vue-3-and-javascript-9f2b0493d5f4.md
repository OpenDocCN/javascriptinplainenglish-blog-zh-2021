# 用 Vue 3 和 JavaScript 创建一个投票应用

> 原文：<https://javascript.plainenglish.io/create-a-voting-app-with-vue-3-and-javascript-9f2b0493d5f4?source=collection_archive---------16----------------------->

![](img/d30111b8ebbb24e3317ada9565df3de6.png)

Photo by [Glen Carrie](https://unsplash.com/@glencarrie?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个投票应用程序。

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
vue create voting-app
```

并选择所有默认选项来创建项目。

# 创建投票应用程序

为了创建投票应用程序，我们编写:

```
<template>
  <form>
    <div>
      <label>What's your favorite fruit?</label>
      <input type="radio" value="apple" v-model="choice" /> apple
      <input type="radio" value="orange" v-model="choice" /> orange
      <input type="radio" value="grape" v-model="choice" /> grape
    </div>
    <button type="button" @click="vote">vote</button>
  </form>
  <div>
    <h1>result</h1>
    <p v-for="(value, key) of results" :key="key">{{ key }}: {{ value }}</p>
  </div>
</template><script>
export default {
  name: "App",
  data() {
    return {
      choice: "",
      results: {},
    };
  },
  methods: {
    vote() {
      if (!localStorage.getItem("vote-result")) {
        localStorage.setItem("vote-result", JSON.stringify({}));
      }
      const { choice } = this;
      const results = JSON.parse(localStorage.getItem("vote-result"));
      if (!Object.prototype.hasOwnProperty.call(results, choice)) {
        results[choice] = 0;
      }
      results[choice]++;
      localStorage.setItem("vote-result", JSON.stringify(results));
      this.results = JSON.parse(localStorage.getItem("vote-result"));
    },
  },
};
</script>
```

在模板中，我们有一个带有单选按钮的表单，它通过`v-model`绑定到`choice`反应属性。

投票按钮在被点击时运行`vote`方法。

div 呈现选项和每个选项的投票数。

`value`有票数。

`key`有选择的名字。

在脚本标签中，我们有`data`方法，它返回我们正在使用的反应属性。

在`vote`方法中，我们检查带有关键字`vote-result`的本地存储结果是否存在。

如果没有，我们调用`setItem`来添加条目。

然后我们用`vote-result`调用`getItem`得到结果，用`JSON.parse`解析返回的字符串。

然后我们检查选择是否存在于结果中。

如果`Object.prototype.hasOwnProperty.call(results, choice)`返回`true`，那么选择的属性存在于`results`中。

如果没有，我们添加属性并将其设置为 0。

然后我们将属性值增加 1 来注册投票。

然后我们调用`setItem`来更新本地存储条目。

然后我们得到它，再次解析它，并把它分配给`this.results`来更新它。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建投票应用。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)