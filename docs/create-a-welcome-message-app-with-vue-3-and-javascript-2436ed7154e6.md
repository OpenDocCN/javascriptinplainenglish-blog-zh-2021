# 用 Vue 3 和 JavaScript 创建一个欢迎消息应用程序

> 原文：<https://javascript.plainenglish.io/create-a-welcome-message-app-with-vue-3-and-javascript-2436ed7154e6?source=collection_archive---------20----------------------->

![](img/2d816ca2d91159975501cd292b5199e3.png)

Photo by [Adam Jang](https://unsplash.com/@adamjang?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个欢迎消息应用程序。

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
vue create welcome-message
```

并选择所有默认选项来创建项目。

# 创建欢迎信息应用程序

为了创建欢迎消息应用程序，我们编写:

```
<template>
  <form @submit.prevent="submit">
    <div>
      <label>first name</label>
      <input v-model.trim="firstName" />
    </div>
    <div>
      <label>last name</label>
      <input v-model.trim="lastName" />
    </div>
    <button type="submit">submit</button>
  </form>
  {{ message }}
</template><script>
export default {
  name: "App",
  data() {
    return {
      firstName: "",
      lastName: "",
      message: "",
    };
  },
  computed: {
    formValid() {
      const { firstName, lastName } = this;
      return firstName.length > 0 && lastName.length > 0;
    },
  },
  methods: {
    submit() {
      if (!this.formValid) {
        return;
      }
      const { firstName, lastName } = this;
      this.message = `hello, ${firstName} ${lastName}`;
    },
  },
};
</script>
```

我们有两个输入字段的形式。

一个用于输入名字，一个用于输入姓氏。

为了将输入值绑定到反应属性，我们使用了`v-model`指令。

`trim`修饰符让我们从输入的值中删除开头和结尾的空白。

为了监听`submit`事件，我们在表单上有了`@submit`指令。

`prevent`修饰符让我们阻止服务器端提交，而进行客户端提交。

在组件对象中，我们用`data`方法返回一个带有反应属性及其初始值的对象。

接下来，我们添加`formValid` computed 属性来检查`firstName`和`lastName`的长度是否大于 0。

最后，我们添加了检查`formValid`是否为`true`的`submit`方法。

如果是，那么我们继续将`message`反应属性设置为欢迎消息字符串。

然后`message`显示在模板中的表单下方。

# 结论

我们可以用 Vue 3 和 JavaScript 创建一个欢迎消息应用。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)