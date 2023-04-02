# 用 Vue 3 和 JavaScript 创建一个密码生成器应用

> 原文：<https://javascript.plainenglish.io/create-a-password-generator-app-with-vue-3-and-javascript-2ccfb6777c04?source=collection_archive---------15----------------------->

![](img/985c46ef6fed504f288d8d0e0d280782.png)

Photo by [Dan Nelson](https://unsplash.com/@danny144?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个密码生成器应用程序。

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
vue create password-generator
```

并选择所有默认选项来创建项目。

# 创建密码生成器

为了创建密码生成器应用程序，我们编写:

```
<template>
  <form @submit.prevent="generatePassword">
    <div>
      <label>length</label>
      <input v-model.number="length" />
    </div>
    <button type="submit">generate password</button>
  </form>
  <div>{{ password }}</div>
</template><script>
const string = "abcdefghijklmnopqrstuvwxyz";
const numeric = "0123456789";
const punctuation = "!@#$%^&*()_+~`|}{[]:;?><,./-=";export default {
  name: "App",
  data() {
    return {
      length: 10,
      password: "",
    };
  },
  computed: {
    formValid() {
      const { length } = this;
      return +length > 0;
    },
  },
  methods: {
    generatePassword() {
      const { length, formValid } = this;
      if (!formValid) {
        return;
      }
      let character = "";
      let password = "";
      while (password.length < length) {
        const entity1 = Math.ceil(
          string.length * Math.random() * Math.random()
        );
        const entity2 = Math.ceil(
          numeric.length * Math.random() * Math.random()
        );
        const entity3 = Math.ceil(
          punctuation.length * Math.random() * Math.random()
        );
        let hold = string.charAt(entity1);
        hold = password.length % 2 === 0 ? hold.toUpperCase() : hold;
        character += hold;
        character += numeric.charAt(entity2);
        character += punctuation.charAt(entity3);
        password = character;
      }
      password = password
        .split("")
        .sort(() => {
          return 0.5 - Math.random();
        })
        .join("");
      this.password = password.substr(0, length);
    },
  },
};
</script>
```

我们有一个带有`@submit`指令的表单来监听提交事件。

`prevent`让我们在客户端而不是服务器端提交。

在表单中，我们用`v-model`将输入字段绑定到`length`反应属性。

`number`修饰符让我们将绑定值自动转换成一个数字。

在它下面，我们有一个 generate password 按钮，它将`type`设置为`submit`来触发提交事件。

在表单下面，我们显示了`password`。

在脚本标签中，我们有`string`、`numeric`和`punctuation`变量，我们从这些变量中获取字符来生成密码。

`data`方法返回反应属性。

`formValid`反应属性检查`length`是否大于 0，这样我们就可以生成一个有效长度的密码。

在`generatePassword`方法中，我们获取并使用`length`和`formValid`属性。

在生成密码之前，我们首先检查`formValid`。

然后我们添加一个`while`循环，用给定的`length`生成一个密码。

我们用`Math.random`随机得到一个字母、数字和标点符号。

然后，我们将挑选出来的字符附加到`character`上。

然后我们用`sort`的方法洗牌。

`0.5 — Math.random()`确保我们在回调中返回一个随机数，所以我们打乱了`password`中的字符。

最后，我们将给定`length`的`password`切割分配给`this.password`反应属性。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建一个密码生成器。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)