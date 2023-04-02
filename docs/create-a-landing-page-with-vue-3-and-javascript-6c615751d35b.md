# 用 Vue 3 和 JavaScript 创建一个登陆页面

> 原文：<https://javascript.plainenglish.io/create-a-landing-page-with-vue-3-and-javascript-6c615751d35b?source=collection_archive---------15----------------------->

![](img/a5182f95b60779b6fdac8e138d7e44f1.png)

Photo by [trevor pye](https://unsplash.com/@trevmepix?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个登陆页面。

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
vue create landing-page
```

并选择所有默认选项来创建项目。

# 创建登录页面

为了创建登录页面，我们编写:

```
<template>
  <form v-if="!submitted" @submit.prevent="submitted = true">
    <div>
      <label>your name</label>
      <input v-model.trim="name" />
    </div>
    <button type="submit">submit</button>
  </form>
  <div v-else>
    <p>Welcome {{ name }}</p>
    <p>The time is {{ dateTime }}</p>
  </div>
</template><script>
export default {
  name: "App",
  data() {
    return {
      name: "",
      dateTime: new Date(),
      timer: undefined,
      submitted: false,
    };
  },
  methods: {
    setDate() {
      this.dateTime = new Date();
    },
  },
  mounted() {
    this.timer = setInterval(() => {
      this.setDate();
    }, 1000);
  },
  beforeUnmount() {
    clearInterval(this.timer);
  },
};
</script>
```

我们有一个表格，让用户提交他们的名字。

在它的内部，我们有一个输入绑定到带有`v-model`的`name`反应属性。

`trim`修改器让我们修剪前导和尾随空白。

如果`submitted`是`false`，表单有`v-if`指令显示表单。

以及通过将`submitted`设置为`true`的提交按钮触发提交事件。

下面，我们应该通过显示`name`和`dateTime`来显示登陆页面的内容。

在脚本标签中，我们使用了`data`方法来返回我们的反应属性。

`setDate`方法将`dateTime`设置为当前日期。

`mounted`钩子调用`setInterval`来调用`setDate`来每秒更新`dateTime`。

当我们卸载组件时，`beforeUnmount`钩子调用`clearInterval`来清除计时器。

# 结论

我们可以用 Vue 3 和 JavaScript 创建一个登陆页面。

## *延伸阅读*

[](https://bit.cloud/blog/composing-reusable-landing-pages-in-components-l4mk36jk) [## 在组件中组合可重用的登录页面

### 最近，我们不得不创建一个登录页面，允许人们请求演示我们的产品。这一页是…

比特云](https://bit.cloud/blog/composing-reusable-landing-pages-in-components-l4mk36jk) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****