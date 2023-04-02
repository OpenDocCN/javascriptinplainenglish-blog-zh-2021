# 用 Vue 3 和 JavaScript 创建一个问答游戏

> 原文：<https://javascript.plainenglish.io/create-a-quiz-game-with-vue-3-and-javascript-5e6467b3b779?source=collection_archive---------12----------------------->

![](img/23509057b29f9746d1a82a6e0fed11aa.png)

Photo by [Shubham Sharan](https://unsplash.com/@shubhamsharan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个问答游戏。

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
vue create quiz-game
```

并选择所有默认选项来创建项目。

# 创建问答游戏

为了创建测验应用程序，我们编写:

```
<template>
  <form>
    <div v-if="questionIndex < questions.length">
      <label>{{ question.question }}</label>
      <div v-for="c of question.choices" :key="c">
        <input type="radio" name="choice" v-model="answer" :value="c" />
        {{ c }}
      </div>
    </div>
    <div v-else>
      <button type="button" @click="restart">restart</button>
    </div>
    <button type="button" @click="submit">check</button>
  </form>
  <p>score: {{ score }}</p>
</template><script>
const questions = [
  {
    question: "What is American football called in England?",
    choices: ["American football", "football", "Handball"],
    rightAnswer: "American football",
  },
  {
    question: "What is the largest country in the world?",
    choices: ["Russia", "Canada", "United States"],
    rightAnswer: "Russia",
  },
  {
    question: "What is the 100th digit of Pi?",
    choices: [9, 4, 7],
    rightAnswer: 9,
  },
];
export default {
  name: "App",
  data() {
    return {
      questions,
      score: 0,
      questionIndex: 0,
      question: questions[0],
      answer: "",
    };
  },
  methods: {
    submit() {
      const { answer, question, questions, questionIndex } = this;
      if (answer === question.rightAnswer) {
        this.score++;
      } if (questionIndex < questions.length) {
        this.questionIndex++;
        this.question = { ...questions[this.questionIndex] };
      }
    },
    restart() {
      this.question = questions[0];
      this.answer = "";
      this.questionIndex = 0;
      this.score = 0;
    },
  },
};
</script>
```

我们有一个带有 div 的表单元素来显示问题。

只有当`questionIndex`小于`questions.length`时，我们才显示一个问题。

如果`questionIndex`等于`questions.length`，那么我们就没有问题可以显示了。

为了显示这个问题，我们在标签中呈现了`question.question`。

我们在它下面的 div 中呈现了`question.choices`条目。

我们通过将`type`设置为`radio`来呈现单选按钮。

`name`属性都被设置为`choice`，这样浏览器就知道它们在同一个组中。

这意味着我们只能选择其中之一。

`v-model`也绑定到相同的值，因此所选的选择被绑定到`answer`反应属性。

否则，我们显示重启按钮，这样当我们点击它时会调用`restart`方法。

我们在下方显示提交按钮，以提交答案。

我们在下面显示分数。

在`script`标签中，我们有带`chocies`和`rightAnswer`的问题条目。

`data`具有我们所有无功属性的初始值。

`submit`方法是我们检查答案的地方。

我们得到`answer`并将其与`question.rightAnswer`进行比较。

`question`有当前的疑问。

如果它们相同，我们将`score`增加 1。

如果`questionIndex`小于`questions.length`，我们将`questionIndex`加 1，进入下一个问题。

然后我们把`this.question`设置为之后的新问题。

一旦我们完成了所有的问题，`restart`就运行了。

我们只是将反应变量重置为初始值。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建一个问答游戏。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)