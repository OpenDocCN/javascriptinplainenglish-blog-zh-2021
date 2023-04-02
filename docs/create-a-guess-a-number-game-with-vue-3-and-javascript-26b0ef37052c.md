# 用 Vue 3 和 JavaScript 创建一个猜数字游戏

> 原文：<https://javascript.plainenglish.io/create-a-guess-a-number-game-with-vue-3-and-javascript-26b0ef37052c?source=collection_archive---------14----------------------->

![](img/ac9a72481c72dd59bcdc15338e64bfe2.png)

Photo by [Gursimrat Ganda](https://unsplash.com/@gurysimrat?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个猜数字游戏。

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
vue create number-guessing-game
```

并选择所有默认选项来创建项目。

# 创建一个猜数字游戏

为了创建猜数字游戏，我们写道:

```
<template>
  <div v-if="started">
    <form @submit.prevent="submit">
      <div>
        <label>answer</label>
        <input v-model.number="answer" />
      </div>
      <button type="submit">check</button>
    </form>
    <p>{{ status }}</p>
  </div>
  <div v-else>
    <button type="button" @click="start">start</button>
    <p>{{ status }}</p>
  </div>
</template><script>
export default {
  name: "App",
  data() {
    return {
      rightAnswer: undefined,
      answer: 0,
      status: "",
      started: false,
    };
  },
  computed: {
    formValid() {
      return +this.answer >= 0;
    },
  },
  methods: {
    start() {
      this.rightAnswer = Math.ceil(Math.random() * 10);
      console.log(this.rightAnswer);
      this.started = true;
    },
    submit() {
      if (!this.formValid) {
        return;
      }
      const { answer, rightAnswer } = this;
      if (answer === rightAnswer) {
        this.status = "you got it";
        this.started = false;
      } else if (answer < rightAnswer) {
        this.status = "too low";
      } else {
        this.status = "too high";
      }
    },
  },
};
</script>
```

我们从添加游戏开始时显示的表单 div 开始。

当`started`为`true`时开始。

在它里面，我们有一个表单元素。

我们用`@sumbit`指令听`submit` evbent。

`prevent`修饰符阻止服务器端提交，让我们做客户端表单提交。

我们有一个输入，让玩家输入答案。

我们用`v-model`将输入值绑定到`answer`无功属性。

`number`修改器自动将输入的值转换为数字。

然后我们添加一个`type`设置为`submit`的按钮，让玩家提交表单。

我们还在表单中显示了`status`。

如果游戏没有开始，我们显示`status`和一个按钮让我们开始游戏。

然后我们继续添加组件选项对象。

在它里面，我们有`data`方法来返回反应属性和它们的初始值。

接下来，我们添加`formValid`来检查`answer`的反应属性，看它是否大于或等于 0。

`start`方法让我们通过生成`rightAnswer`并设置`started`到`true`来开始游戏。

接下来，我们添加`submit`方法来比较`answer`和`rightAnswer`。

首先，我们用`formValid`检查这个值是否是一个有效的数字。

如果不是，那么我们停止运行这个函数。

我们根据`answer`是等于、小于还是大于`rightAnswer`来显示不同的信息。

如果玩家得到了正确的答案，那么我们设置`started`到`false`来结束游戏。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建一个猜数字游戏。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)