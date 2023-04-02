# 用 Vue 3 和 JavaScript 创建一个问题跟踪器

> 原文：<https://javascript.plainenglish.io/create-an-issue-tracker-with-vue-3-and-javascript-140ee7f6d79d?source=collection_archive---------11----------------------->

![](img/97cee1dd93dc02c7252c82db1d7f9f59.png)

Photo by [Mika Baumeister](https://unsplash.com/@mbaumi?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个问题跟踪器。

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
vue create issue-tracker
```

并选择所有默认选项来创建项目。

我们还需要安装`uuid`包，这样我们就可以为每个成绩条目生成唯一的 id。

要安装它，我们运行:

```
npm i uuid
```

# 创建问题跟踪器

为了创建问题跟踪器，我们写道:

```
<template>
  <form @submit.prevent="addIssue">
    <div>
      <label>description</label>
      <input v-model="issue.description" />
    </div> <div>
      <label>priority</label>
      <select v-model="issue.priority">
        <option>low</option>
        <option>medium</option>
        <option>high</option>
      </select>
    </div> <div>
      <label>assignee</label>
      <input v-model="issue.assignee" />
    </div>
    <button type="submit">add issue</button>
  </form>
  <div v-for="(issue, index) of issues" :key="issue.id">
    <p>description: {{ issue.description }}</p>
    <p>priority: {{ issue.priority }}</p>
    <p>assignee: {{ issue.assignee }}</p>
    <button type="button" @click="deleteIssue(index)">delete issue</button>
  </div>
</template><script>
import { v4 as uuidv4 } from "uuid";export default {
  name: "App",
  data() {
    return {
      issue: {
        description: "",
        priority: "low",
        assignee: "",
      },
      issues: [],
    };
  },
  computed: {
    formValid() {
      const { description, priority, assignee } = this.issue;
      return description && priority && assignee;
    },
  },
  methods: {
    addIssue() {
      if (!this.formValid) {
        return;
      }
      const { description, priority, assignee } = this.issue;
      this.issues.push({ id: uuidv4(), description, priority, assignee });
    },
    deleteIssue(index) {
      this.issues.splice(index, 1);
    },
  },
};
</script>
```

我们有一个带有`@submit`指令的表单来监听提交事件，当我们点击带有`type` `submit`的按钮时会发出这些事件。

`prevent`修饰符让我们在客户端而不是服务器端提交表单。

在表单中，我们输入了任务的描述和任务负责人。

我们有一个选择下拉菜单，用于选择优先级。

我们将所有这些值绑定到带有`v-model`的`issue`反应属性的属性。

在字段下方，我们有一个提交表单的“添加问题”按钮。

在那下面，我们有 div 来呈现我们添加的问题。

`key`属性被设置为`id`属性，它是每个`issues`条目的唯一 ID。

我们显示属性并显示“删除问题”按钮，让用户删除问题。

在组件对象中，我们有返回反应属性的`data`方法。

`formValid` computed 属性检查每个字段是否都已填充。

`addIssue`方法使用`formValid`计算属性来检查字段的有效性。

如果它们都有效，这意味着`formValid`是`false`，那么我们调用`this.issues.push`将发布对象推入数组。

`deleteIssue`方法接受一个`index`并调用`this.issues.splice`来删除带有给定`index`的条目。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建一个简单的问题跟踪器。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)