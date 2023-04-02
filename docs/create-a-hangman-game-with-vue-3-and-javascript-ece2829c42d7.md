# 用 Vue 3 和 JavaScript 创建一个刽子手游戏

> 原文：<https://javascript.plainenglish.io/create-a-hangman-game-with-vue-3-and-javascript-ece2829c42d7?source=collection_archive---------21----------------------->

![](img/e8fc372145124fd38fd059741b83023c.png)

Photo by [Erik Mclean](https://unsplash.com/@introspectivedsgn?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个刽子手游戏。

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
vue create hangman
```

并选择所有默认选项来创建项目。

# 创建一个刽子手游戏

为了创建刽子手游戏，我们编写:

```
<template>
  <div v-if="isWin">
    you win
    <button type="button" @click="reset">reset</button>
  </div>
  <div v-else>
    <div v-if="guessesLeft > 0">
      <p>guesses left: {{ guessesLeft }}</p>
      <form @submit.prevent="guess">
        <div>
          <label>guess</label>
          <input v-model.trim="guessLetter" />
        </div>
        <button type="submit">guess</button>
      </form> <span v-for="(l, index) of lettersToShow" :key="index">
        {{ l }}
      </span>
    </div>
    <div v-else>
      you lost
      <button type="button" @click="reset">reset</button>
    </div>
  </div>
</template><script>
const answer = "hangman";export default {
  name: "App",
  data() {
    return {
      guessLetter: "",
      answer,
      guesses: [],
    };
  },
  computed: {
    formValid() {
      const { guessLetter } = this;
      return /[a-z]{1}/.test(guessLetter);
    },
    lettersToShow() {
      const { answer, guesses } = this;
      return answer.split("").map((a) => {
        if (guesses.includes(a)) {
          return a;
        }
        return "_";
      });
    },
    guessesLeft() {
      const { answer, guesses } = this;
      return (
        6 -
        guesses.filter((g) => {
          return !answer.includes(g);
        }).length
      );
    },
    isWin() {
      const { answer, guesses } = this;
      const includedLetters = guesses.filter((g) => {
        return answer.includes(g);
      });
      return answer.split("").every((a) => {
        return includedLetters.includes(a);
      });
    },
  },
  methods: {
    guess() {
      if (!this.formValid) {
        return;
      }
      this.guesses.push(this.guessLetter);
      this.guessLetter = "";
    },
    reset() {
      this.guesses = [];
      this.guessLetter = "";
    },
  },
};
</script>
```

在模板中，我们检查的是`isWin`是`true`。

如果是，那么我们显示“你赢了”。

我们显示重置按钮，让用户重新开始游戏。

否则，如果`guessesLeft`大于 0，我们将显示一个带有表单的 div，让玩家猜字母。

这表明玩家仍然可以猜测。

该表单有一个猜测字段，让玩家输入一个字母来猜测。

我们用`v-model`将它绑定到`guessLetter`。

我们使用`trim`修改器来修剪空白。

我们用`@submit`指令和`guess`方法监听`submit`事件。

`prevent`让我们阻止服务器端表单提交，改为客户端提交。

在那下面，我们循环通过字母来显示。

否则，我们会向玩家显示一条“你输了”的消息，因为已经没有其他的猜测了。

我们在 div 上显示重置按钮，让玩家重置游戏。

在`script`的顶部有一个`answer`变量。

`guessLetter`有信。

`guesses`有一个猜测数组，是单个字母的字符串。

我们确保输入值是带有`formValid`计算属性的单字母字符串。

`lettersToShow`有目前猜测到的字母。

如果用`guess.includes(a)`检查，我们返回猜测正确的字母。

`answers`有正确的字符串，所以我们可以用`includes`检查其中的字母，看看我们是否有正确的字母。

否则，我们返回一个下划线。

`guessesLeft`还有猜测的次数。

它是 6 减去不正确猜测的次数，由以下公式确定:

```
guesses.filter((g) => {
  return !answer.includes(g);
}).length
```

`isWin`决定玩家是否获胜。

我们通过获取存储在`includedLetters`变量中的正确字母来确定这一点。

并且我们调用拆分成数组的`answer`字符串上的`every`来查看`answer`中的每个字母是否都包含在`includedLetters`中。

现在我们添加`guess`方法让玩家输入猜测。

根据`formValid`变量，我们只接受表单是否有效的猜测。

如果是`true`，那么我们将`guessLetter`推至`this.guesses`，之后重置`guessLetter`的值。

`reset`方法重置`guesses`和`guessLetter`值。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建一个刽子手游戏。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容看* [***说白了***](https://plainenglish.io/)