# 用 Vue 3 和 JavaScript 创建待办事项列表

> 原文：<https://javascript.plainenglish.io/create-a-to-do-list-with-vue-3-and-javascript-4ab7e3462c9d?source=collection_archive---------12----------------------->

![](img/718986db421689b12fd069b18df6b86c.png)

Photo by [Markus Winkler](https://unsplash.com/@markuswinkler?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个待办事项应用程序。

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
vue create todo-list
```

并选择所有默认选项来创建项目。

我们还需要`uuid`包来为我们的待办事项生成唯一的 id。

为此，我们运行:

```
npm i uuid
```

# 创建待办事项列表

为了创建待办事项列表，我们写下:

```
<template>
  <div>
    <form @submit.prevent="add">
      <input v-model="todo" />
      <button type="submit">Add</button>
    </form> <div v-for="(todo, index) of todos" :key="todo.id">
      {{ todo.todo }}
      <button @click="deleteTodo(index)">delete</button>
    </div>
  </div>
</template><script>
import { v4 as uuidv4 } from "uuid";export default {
  name: "App",
  data() {
    return {
      todo: "",
      todos: [],
    };
  },
  methods: {
    add() {
      const { todo } = this;
      this.todos.push({
        id: uuidv4(),
        todo,
      });
      this.todo = "";
    },
    deleteTodo(index) {
      this.todos.splice(index, 1);
    },
  },
};
</script>
```

我们有带`@submit`指令的表单，让我们提交表单。

`prevent`修饰符让我们在客户端而不是服务器端提交表单。

然后我们添加`v-for`来渲染待办事项。

将`key`属性设置为`id`属性，这是待办事项的唯一 ID。

我们在每一行中都有一个按钮，用`deleteTodo`方法删除给定索引处的一个条目。

在 component 对象中，我们有`todo`react tive 属性，它被绑定到带有`v-model`的输入。

`todos`有一系列待办事项。

`add`方法调用`push`方法向`this.todos`数组追加一个项目。

我们调用`uuidv4`函数来返回我们用于待办事项的唯一 ID。

然后我们将`this.todo` reactive 属性设置为空字符串来清除输入。

在`deleteTodo`方法中，我们用`index`和 1 调用`splice`来删除给定索引处的待办事项。

# 结论

我们可以使用 Vue 3 和 JavaScript 轻松创建待办事项列表。