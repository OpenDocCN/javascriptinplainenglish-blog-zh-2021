# 用 Vue 3 和 JavaScript 创建一个回文检查器

> 原文：<https://javascript.plainenglish.io/create-a-palindrome-checker-with-vue-3-and-javascript-9586da502e2d?source=collection_archive---------17----------------------->

![](img/3dfca77aeb04af11e9224612d360ec72.png)

Photo by [Sincerely Media](https://unsplash.com/@sincerelymedia?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个回文检查器。

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
vue create palindrome-checker
```

并选择所有默认选项来创建项目。

# 创建回文检查器

为了创建回文检查器，我们编写:

```
<template>
  <form>
    <div>
      <label>word to check</label>
      <input v-model="word" />
    </div>
  </form>
  <div>Is Palindrome:{{ isPalindrome ? "Yes" : "No" }}</div>
</template><script>
export default {
  name: "App",
  data() {
    return {
      word: "",
    };
  },
  computed: {
    isPalindrome() {
      const { word } = this;
      return word === word.split("").reverse().join("");
    },
  },
};
</script>
```

表单中有输入字段。

我们用`v-model`将输入值绑定到`word`反应属性。

在那下面，我们有返回`word`反应属性的`data`方法。

然后我们添加`isPalindrome`计算属性来检查`this.word`是否是一个回文。

我们通过检查反转的字符串是否和原来的相同来检查它是否是一个回文。

我们调用`split`将它拆分成一个字符数组。

然后我们调用`reverse`来反转数组。

然后我们调用`join`将字符连接回一个字符串。

然后我们在模板中显示这个值。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建一个回文检查器。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容看* [***说白了. io***](https://plainenglish.io/)