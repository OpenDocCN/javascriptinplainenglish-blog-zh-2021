# 用 Vue 3 和 JavaScript 创建一个井字游戏

> 原文：<https://javascript.plainenglish.io/create-a-tic-tac-toe-with-vue-3-and-javascript-3cbf7ad6c7cf?source=collection_archive---------17----------------------->

![](img/22c3799b57c77341077ab32a52d26247.png)

Photo by [Micheile Henderson](https://unsplash.com/@micheile?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个井字游戏。

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
vue create tic-tac-toe
```

并选择所有默认选项来创建项目。

# 创建井字游戏

为了创建井字游戏，我们编写:

```
<template>
  <div v-if="xWins || oWins">
    <div v-if="xWins">x wins</div>
    <div v-if="oWins">o wins</div>
    <button @click="restart">restart</button>
  </div>
  <form v-else>
    <div v-for="i in 3" :key="i">
      <span v-for="j in 3" :key="j">
        <input v-model.trim="board[i - 1][j - 1]" style="width: 20px" />
      </span>
    </div>
  </form>
</template><script>
const board = [[], [], []];export default {
  name: "App",
  data() {
    return {
      board,
    };
  },
  computed: {
    xWins() {
      return this.isWinner("x");
    },
    oWins() {
      return this.isWinner("o");
    },
  },
  methods: {
    restart() {
      this.board = [[], [], []];
    },
    isWinner(player) {
      const { board } = this;
      return (
        (board[0][0] === player &&
          board[0][1] === player &&
          board[0][2] === player) ||
        (board[1][0] === player &&
          board[1][1] === player &&
          board[1][2] === player) ||
        (board[2][0] === player &&
          board[2][1] === player &&
          board[2][2] === player) ||
        (board[0][0] === player &&
          board[1][0] === player &&
          board[2][0] === player) ||
        (board[0][1] === player &&
          board[1][1] === player &&
          board[2][1] === player) ||
        (board[0][2] === player &&
          board[1][2] === player &&
          board[2][2] === player) ||
        (board[0][0] === player &&
          board[1][1] === player &&
          board[2][2] === player) ||
        (board[0][2] === player &&
          board[1][1] === player &&
          board[2][0] === player)
      );
    },
  },
};
</script>
```

在模板中，我们有一个显示游戏结果(如果有的话)的 div。

如果 x 或 o 赢了，我们显示谁赢了。

另外，我们添加了一个重启按钮，这样游戏就可以重启了。

否则，我们显示游戏板。

我们使用`v-for`来呈现 3 个输入。

我们渲染输入让玩家输入值。

我们用`v-model`将输入的值绑定到`board`嵌套数组条目。

`trim`修饰符让我们修剪输入值的开头和结尾空白。

在脚本标签中，我们有一个`board`数组，我们用它作为`board`反应属性的初始值。

然后我们用`xWins`和`oWins`计算属性来决定谁赢。

获胜者由`isWinner`方法决定，该方法检查是否有任何`player`在棋盘上有对角、垂直或水平的标记。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建一个井字游戏。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)