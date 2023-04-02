# 用 Vue 3 和 JavaScript 创建一个联系表单

> 原文：<https://javascript.plainenglish.io/create-a-contact-form-with-vue-3-and-javascript-8487b565f21f?source=collection_archive---------8----------------------->

![](img/2e9078b792e4a1218a8481767ebd3ba6.png)

Photo by [Miles Burke](https://unsplash.com/@milesb?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个联系人表单应用程序。

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
vue create contact-form
```

并选择所有默认选项来创建项目。

# 创建联系人表单

为了创建联系人表单应用程序，我们编写:

```
<template>
  <form @submit.prevent="submit" @reset="onReset">
    <div>
      <label>name</label>
      <input v-model="name" />
    </div> <div>
      <label>email</label>
      <input v-model="email" />
    </div> <div>
      <label>message</label>
      <textarea v-model="message"></textarea>
    </div> <button type="submit">submit</button>
    <button type="reset">reset</button>
  </form>
</template><script>
export default {
  name: "App",
  data() {
    return {
      name: "",
      email: "",
      message: "",
    };
  },
  computed: {
    formValid() {
      const { name, email, message } = this;
      return (
        name.length > 0 &&
        /(.+)@(.+){2,}\.(.+){2,}/.test(email) &&
        message.length > 0
      );
    },
  },
  methods: {
    onReset() {
      this.name = "";
      this.email = "";
      this.message = "";
    },
    submit() {
      if (!this.formValid) {
        return;
      }
      if (!localStorage.getItem("messages")) {
        localStorage.setItem("messages", JSON.stringify([]));
      }
      const messages = JSON.parse(localStorage.getItem("messages"));
      const { name, email, message } = this;
      messages.push({
        name,
        email,
        message,
      });
      localStorage.setItem("messages", JSON.stringify(messages));
    },
  },
};
</script>
```

我们用`form`元素创建一个表单。

我们添加了带有`@submit`指令的`submit`事件处理程序。

`prevent`修饰符让我们可以在客户端而不是服务器端提交表单。

`@reset`指令监听当我们点击一个`type`属性设置为`reset`的按钮时发出的重置事件。

因此，当我们单击 reset 按钮时，就会发出`reset`事件。

我们将输入与`v-model`相加，将输入值绑定到无功属性。

反应属性在我们在`data`方法中返回的对象中定义。

当我们单击属性设置为`submit`的按钮时，它会运行提交事件处理程序。

我们有`formValid`强制属性来检查每个值是否有效。

我们检查`name`和`message`的长度是否大于 0。

而那个`email`是邮件。

`onReset`方法将反应属性重置为空字符串。

`submit`方法使用`formValid`计算属性检查所有值是否有效。

然后，我们将输入的表单值存储在本地存储中。

我们检查带有关键字`messages`的本地存储条目是否存在。

否则，我们用空数组的初始值来创建它。

然后，在用`localStorage.getItem`获取值并用`JSON.parse`将它解析成一个对象之后，我们将一个新的条目推入其中。

然后我们存储`messages`数组，用`localStorate.setItem`将消息条目推入本地存储。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建联系人表单。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)