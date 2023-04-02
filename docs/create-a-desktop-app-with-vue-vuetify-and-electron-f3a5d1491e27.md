# 使用 Vue、Vuetify 和 Electron 创建桌面应用程序

> 原文：<https://javascript.plainenglish.io/create-a-desktop-app-with-vue-vuetify-and-electron-f3a5d1491e27?source=collection_archive---------7----------------------->

![](img/6a1d833b96ff910dacbbc73da3c8ee75.png)

Photo by [Paul Gilmore](https://unsplash.com/@paulgilmore_?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Electron 是一个应用程序框架，让我们可以构建基于 web 应用程序的桌面应用程序。

Vuetify 让我们用材料设计建立一个网络应用程序。

我们可以使用[vue-CLI-plugin-electronic-builder](https://github.com/nklayman/vue-cli-plugin-electron-builder)生成器来构建一个基于 Vue.js 的电子 app

在本文中，我们将了解如何使用 Vuetify 和 electronic 构建一个简单的电子 Vue 应用程序。

# 入门指南

我们可以通过运行以下命令来创建我们的 Vue 项目:

```
npx vue create .
```

进入我们的项目文件夹后。

我们按照说明创建 Vue 项目。

然后在项目文件夹中，我们运行:

```
vue add electron-builder
```

完成后，我们通过运行以下命令将 Vuetify 添加到我们的 Vue 应用程序中:

```
vue add vuetify
```

现在已经为我们添加了所有的样板代码。

然后我们运行:

```
npm run electron:serve
```

或者

```
yarn electron:serve
```

预览我们的应用程序。

# 编写代码

现在可以使用 Vuetify 创建我们的应用程序。

我们可以通过向`App.vue`添加以下内容来创建一个简单的应用程序:

```
<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        /> <span class="mr-2">App</span>
      </div>
    </v-app-bar> <v-main>
      <v-form v-model="valid" @submit.prevent="add">
        <v-container>
          <v-row>
            <v-col cols="12" md="6">
              <v-text-field v-model="title" :rules="rule" label="book title" required></v-text-field>
            </v-col> <v-col cols="12" md="6">
              <v-text-field v-model="author" :rules="rule" label="book author" required></v-text-field>
            </v-col>
          </v-row>
          <v-row>
            <v-col cols="12">
              <v-btn text type="submit" color="primary">add</v-btn>
            </v-col>
          </v-row>
        </v-container>
      </v-form> <v-simple-table>
        <template v-slot:default>
          <thead>
            <tr>
              <th class="text-left">title</th>
              <th class="text-left">author</th>
              <th></th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(b, i) in books" :key="b.id">
              <td>{{ b.title }}</td>
              <td>{{ b.author }}</td>
              <td>
                <v-btn text color="primary" @click="remove(i)">remove</v-btn>
              </td>
            </tr>
          </tbody>
        </template>
      </v-simple-table>
    </v-main>
  </v-app>
</template><script>
import { v4 as uuidv4 } from "uuid";export default {
  name: "App",
  data: () => ({
    title: "",
    author: "",
    rule: [(v) => !!v || "required"],
    valid: false,
    books: [],
  }),
  methods: {
    add() {
      if (!this.valid) {
        return;
      }
      const { title, author } = this;
      this.books.push({
        id: uuidv4(),
        title,
        author,
      });
    },
    remove(index) {
      this.books.splice(index, 1);
    },
  },
};
</script>
```

我们创建了一个带有表单和表格的图书应用程序。

`v-app-bar`是最上面的 app 栏。

`v-main`拥有 app 的主要内容。

`v-form`创建表单。

表单上的`v-model`属性具有表单验证状态。

`@submit.prevent`指令监听要发出的提交事件。

`prevent`隐式调用`preventDefault`。

在表单内部，我们使用了`v-text-field`来添加文本字段。

`v-model`绑定到模型状态。

`rules`属性具有表单验证规则。

规则是用一组函数定义的，输入的值作为参数。

该表是用`v-simple-table`组件创建的。

我们用常规的表元素填充`default` 槽。

在`methods`对象中，我们有`add`方法让我们向`this.books`添加条目。

我们用`this.valid`属性检查表单数据的有效性。

使用`uuid`包为每个条目生成一个唯一的 ID。

我们需要表格中的`key`道具的唯一 ID，以便正确呈现项目。

我们通过运行以下命令来安装它:

```
npm i uuid
```

此外，我们使用了`remove`方法来根据索引删除条目。

现在我们应该能够随意添加和删除项目了。

# 构建我们的应用

为了将我们的应用程序构建成可执行文件，我们运行:

```
yarn electron:build
```

用纱线或:

```
npm run electron:build
```

和 NPM 一起。

# 结论

我们可以用 Vuetify、Vue 和[Vue-CLI-plugin-electronic-builder](https://github.com/nklayman/vue-cli-plugin-electron-builder)代码生成器创建一个好看的 Vue 桌面应用。