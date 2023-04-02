# 用 Vue 3 和 JavaScript 创建一个打字测试

> 原文：<https://javascript.plainenglish.io/create-a-typing-test-with-vue-3-and-javascript-a3fbbd57a8f3?source=collection_archive---------13----------------------->

![](img/41152659b2eb53815a15e899463d2e1e.png)

Photo by [Christin Hume](https://unsplash.com/@christinhumephoto?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个类型测试。

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
vue create typing-test
```

并选择所有默认选项来创建项目。

# 创建类型测试

为了创建类型测试，我们编写:

```
<template>
  <div v-if="parts.unmatchedPart.length > 1">
    <div>
      <b>
        {{ parts.matchedPart }}
      </b>
      {{ parts.unmatchedPart }}
    </div>
    <button @click="start">start</button>
    <textarea
      :disabled="!started"
      v-model="typedText"
      style="width: 90vw; height: 300px"
    ></textarea>
  </div>
  <div v-else>
    Your words per minute is {{ wpm }}
    <button @click="restart">restart</button>
  </div>
</template><script>
const textToType =
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus sit amet tellus tortor. ";
export default {
  name: "App",
  data() {
    return {
      textToType,
      typedText: "",
      timer: undefined,
      elapsedMs: 0,
      wpm: 0,
      started: false,
    };
  },
  computed: {
    parts() {
      const { textToType } = this;
      const splitTextToType = textToType.split("");
      let endIndexMatch = 0;
      for (const [index, s] of splitTextToType.entries()) {
        if (s !== this.typedText[index]) {
          endIndexMatch = index;
          break;
        }
      }
      return {
        matchedPart: textToType.slice(0, endIndexMatch),
        unmatchedPart: textToType.slice(endIndexMatch),
      };
    },
  },
  methods: {
    start() {
      this.timer = setInterval(() => {
        this.elapsedMs++;
        if (!this.started) {
          this.started = true;
        }
      }, 1000);
    },
    restart() {
      this.started = false;
      this.elapsedMs = 0;
      this.typedText = "";
    },
  },
  watch: {
    parts(val) {
      if (val.unmatchedPart.length === 1) {
        clearInterval(this.timer);
        this.wpm =
          textToType.split(" ").length / (this.elapsedMs / (60 * 1000));
      }
    },
  },
};
</script>
```

我们检查是否用`parts.unmatchedPart.length > 1`表达式完成了类型测试。

`parts.unmatchedPart`有我们没有输入到文本区域的部分。

在 div 内部，我们显示文本。输入的部分用粗体显示，带有`b`标签。

剩余部分存储在`parts.unmatchedPart`属性中。

在那下面，我们有开始按钮，当我们点击它开始游戏时，它会调用`start`。

文本区是我们键入文本以完成键入测试的地方。

在带有`v-else`指令的 div 中，我们显示了我们希望在测试完成时显示的内容。

我们向用户显示`wpm`。

我们有一个重启按钮，当我们点击它的时候可以调用`restart`。

在 script 标签中，我们有了带有我们想要输入的文本的`textToType`。

在`data`方法中，我们返回一个具有反应属性的对象。

`typedText`有我们正在键入的文本。

`elapsedMs`是我们开始测试后经过的时间。

`wpm`有每分钟字数结果。

`started`表示是否开始打字测试。

我们还有`parts` computed 属性来获取`textToType`。

我们把它分开，这样我们就可以很容易地检查我们输入的部分在哪里结束。

`endIndexMatch`拥有最后一个字符的索引，该字符与我们应该键入的内容相匹配。

在方法的最后，我们返回一个带有`matchedPart`的对象，它是我们输入的带有`textToType`部分的字符串。

`unmatchedPart`有我们没有输入的`textToType`字符串的一部分。

`start`通过回调调用`sertInterval`来开始打字测试，以增加`this.elaspedMs`开始计算经过的时间。

如果是`false`，我们将`this.started`设置为`true`。

`restart`方法将值重置为初始值。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建一个类型测试。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)