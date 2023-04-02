# 用 Vue 3 和 JavaScript 创建一个传递消息的应用程序

> 原文：<https://javascript.plainenglish.io/create-a-pass-the-message-app-with-vue-3-and-javascript-2b577aa5017c?source=collection_archive---------14----------------------->

![](img/b99c509495651a1cac96c96004859559.png)

Photo by [Adam Jang](https://unsplash.com/@adamjang?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个传递消息应用程序。

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
vue create pass-the-message
```

并选择所有默认选项来创建项目。

# 创建传递消息应用程序

为了创建传递消息应用程序，我们编写:

```
<template>
  <form @submit.prevent="pass">
    <label>message you like to pass</label>
    <input v-model="message" />
    <button type="submit">submit</button>
  </form>
  <h1>last message delivered</h1>
  <p>{{ prevMessage }}</p>
</template><script>
export default {
  name: "App",
  data() {
    return {
      message: "",
      prevMessage: "",
    };
  },
  methods: {
    pass() {
      this.prevMessage = this.message;
      this.message = "";
    },
  },
};
</script>
```

我们有一个表单，可以让我们输入要传递的消息。

我们用`v-model`将输入的值绑定到`message`反应属性。

另外，我们用`pass`方法收听`submit`事件。

`prevent`修饰符阻止默认的服务器端提交行为。

在`pass`方法中，我们将`prevMessage`反应属性的值设置为`message`。

我们将`this.mnessage`设置为空字符串来清空输入。

现在，当我们输入一些内容并点击提交时，消息会显示在最后一条消息标题的下方。

`data`消息方法返回`message`和`prevMessage`反应属性的初始值。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建一个 pass the message 应用程序。

*详见*[***plain English . io***](https://plainenglish.io/)