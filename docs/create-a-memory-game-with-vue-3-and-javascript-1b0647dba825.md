# 用 Vue 3 和 JavaScript 创建一个记忆游戏

> 原文：<https://javascript.plainenglish.io/create-a-memory-game-with-vue-3-and-javascript-1b0647dba825?source=collection_archive---------15----------------------->

![](img/094b49b6b183c155be7f9f0fe2ddca8e.png)

Photo by [Soragrit Wongsa](https://unsplash.com/@invictar1997?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个记忆游戏。

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
vue create memory-game
```

并选择所有默认选项来创建项目。

我们还需要`uuid`包来让我们为瓦片生成唯一的 id。

为此，我们运行:

```
npm i uuid
```

# 创造记忆游戏

为了创建记忆游戏，我们写道:

```
<template>
  <div class="container">
    <div v-for="a of answer" :key="a.id" class="tile" @click="onClick(a.id)">
      <div v-if="a.open">
        {{ a.value }}
      </div>
      <div v-else>&nbsp;</div>
    </div>
  </div>
</template><script>
import { v4 as uuidv4 } from "uuid";
const answer = [1, 1, 2, 2, 3, 3, 4, 4, 5, 5]
  .map((n) => {
    return {
      id: uuidv4(),
      open: false,
      value: n,
    };
  })
  .sort(() => Math.random() - 0.5);export default {
  name: "App",
  data() {
    return {
      answer,
      itemIds: []
    };
  },
  methods: {
    onClick(id) {
      if (!this.itemIds.length < 2 && !this.itemIds.includes(id)) {
        this.itemIds.push(id);
      }
      const index = this.answer.findIndex((a) => a.id === id);
      this.answer[index].open = true;
      if (this.itemIds.length === 2) {
        const item1Index = this.answer.findIndex(
          (a) => a.id === this.itemIds[0]
        );
        const item2Index = this.answer.findIndex(
          (a) => a.id === this.itemIds[1]
        );
        if (this.answer[item1Index].value !== this.answer[item2Index].value) {
          this.answer[item1Index].open = false;
          this.answer[item2Index].open = false;
        }
      }
      if (this.itemIds.length === 2) {
        this.itemIds = [];
      }
    },
  },
};
</script><style scoped>
.container {
  display: flex;
}.tile {
  border: 1px solid black;
  width: 20vw;
  height: 50px;
}
</style>
```

我们有一个包含类`container`的 div，它是一个 flex 容器。

在里面，我们有可以点击的瓷砖。

如果两个单幅图块具有相同的值，则它们保持显示。

否则，我们再次使它们都为空白。

如果`a.open`是`true`，我们显示该值。

否则，我们显示一个空的 div。

在脚本标签中，我们用数字数组创建了`answer`数组。

我们用`map`方法把它们毛到物体上。

每个对象都有一个`id`和`open`值。

然后我们用`sort`方法对它们进行随机排序，回调函数返回一个介于-0.5 和 0.5 之间的随机数。

在`data`方法中，我们返回一个具有反应属性的对象。

`answer`是反应性的，这样我们可以在模板中渲染它。

`itemId`拥有我们点击的图块对象的 id。

接下来，我们添加`onClick`方法，该方法接受一个`id`,如果我们的条目少于 2 个，并且条目还不在`itemIds`数组中，我们就把它放入`itemIds`反应数组中。

接下来，我们用给定的`id`值获取项目的`index`，并将其`open`属性设置为`true`来翻转它。

如果我们有两个项目，如`this.itemIds.length === 2`所示，那么我们比较这两个项目，看它们是否具有相同的值。

如果没有，那么我们将每个项目的`open`设置回`false`。

在最后一个`if`语句中，如果`itemIds`中已经有 2 个条目，我们将`itemIds`设置回空。

现在，当我们单击两个匹配的图块时，我们看到它们与值一起显示。

否则，我们会看到瓷砖回到一个空瓷砖。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建一个记忆游戏。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)