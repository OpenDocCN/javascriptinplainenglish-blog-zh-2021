# 用 Vue 3 和 JavaScript 创建一个 Notes 应用程序

> 原文：<https://javascript.plainenglish.io/create-a-notes-app-with-vue-3-and-javascript-ca5eeb7e250f?source=collection_archive---------13----------------------->

![](img/ebe214ce3331d951eb99ed3bcf537d7c.png)

Photo by [Kelly Sikkema](https://unsplash.com/@kellysikkema?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个 notes 应用程序。

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
vue create notes-app
```

并选择所有默认选项来创建项目。

我们还需要`uuid`包来为我们的笔记生成唯一的 id。

为此，我们运行:

```
npm i uuid
```

# 创建 Notes 应用程序

为了创建 notes 应用程序，我们编写:

```
<template>
  <form @submit.prevent="add">
    <h1>add note</h1>
    <div>
      <label>title</label>
      <input v-model="title" />
    </div>
    <div>
      <label>description</label>
      <input v-model="description" />
    </div>
    <button type="submit">add</button>
  </form> <form>
    <h1>search</h1>
    <div>
      <label>keyword</label>
      <input v-model="keyword" />
    </div>
  </form> <div v-for="(note, index) of filteredNotes" :key="note.id">
    <h2>{{ note.title }}</h2>
    <p>{{ note.description }}</p>
    <button type="button" @click="remove(index)">remove</button>
  </div>
</template><script>
import { v4 as uuidv4 } from "uuid";export default {
  name: "App",
  data() {
    return {
      title: "",
      description: "",
      keyword: "",
      notes: [],
    };
  },
  computed: {
    filteredNotes() {
      const { keyword } = this;
      if (!keyword) {
        return this.notes;
      }
      return this.notes.filter(({ title, description }) => {
        return title.includes(keyword) || description.includes(keyword);
      });
    },
  },
  methods: {
    add() {
      const { title, description } = this;
      this.notes.push({
        id: uuidv4,
        title,
        description,
      });
      this.title = "";
      this.description = "";
    },
    remove(index) {
      this.notes.splice(index, 1);
    },
  },
};
</script>
```

第一个表单让我们添加一个注释条目。

我们用`@submit`指令添加了`submit`事件监听器。

`prevent`让我们阻止服务器端提交。

输入有`v-model`指令，让我们绑定到反应属性，这样我们就可以在组件对象中使用它们。

然后我们有一个`type`设置为`submit`的提交按钮，让我们在单击它时提交表单。

在那下面，我们有另一个表单让我们搜索笔记。

我们有一个输入绑定到带有`v-model`的`keyword`反应属性。

在此之下，我们用`v-for`指令将`filterNotes`呈现为 HTML。

我们呈现了`title`和`description`属性。

此外，我们需要将`key`属性设置为`id`属性，以便它接收一个惟一的 ID。

这样，Vue 3 可以正确地跟踪项目。

在组件对象中，我们使用了`data`方法来返回一个具有反应属性的对象，以及它们的初始值。

此外，我们使用`filteredNotes` computed 属性来获取由`keyword`过滤的注释。

然后我们添加`add`方法，用`id`将`title`和`description`放入一个对象，并调用`this.notes.push`将其推入`this.notes`数组。

`remove`方法让我们用`splice`通过`index`删除一个条目。

# 结论

我们可以使用 Vue 3 和 JavaScript 轻松创建一个 notes 应用程序。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)