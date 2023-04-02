# 用 Vue 3 和 JavaScript 创建一个购物清单应用程序

> 原文：<https://javascript.plainenglish.io/create-a-grocery-list-app-with-vue-3-and-javascript-af2c30491df?source=collection_archive---------12----------------------->

![](img/91a3f460b3c9fbf13688db048c3023a2.png)

Photo by [Fikri Rasyid](https://unsplash.com/@fikrirasyid?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

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
vue create grocery-list
```

并选择所有默认选项来创建项目。

我们还需要`uuid`包来为我们的杂货清单项目生成唯一的 id。

为此，我们运行:

```
npm i uuid
```

# 创建购物清单应用程序

为了创建购物清单应用程序，我们编写:

```
<template>
  <div>
    <form @submit.prevent="add">
      <fieldset>
        <label>item</label>
        <input v-model="item" />
      </fieldset>
      <button type="submit">add item</button>
    </form> <div v-for="(item, index) of items" :key="item.id">
      {{ item.item }}
      <button @click="remove(index)">remove</button>
    </div>
  </div>
</template><script>
import { v4 as uuidv4 } from "uuid";
export default {
  name: "App",
  data() {
    return {
      item: "",
      items: [],
    };
  },
  methods: {
    add() {
      const { item } = this;
      this.items.push({
        id: uuidv4(),
        item,
      });
    },
    remove(index) {
      this.items.splice(index, 1);
    },
  },
};
</script>
```

我们有一个带有`@submit`指令的表单元素，让我们监听提交事件，当我们单击 add item 时会触发该事件。

`v-model`被绑定到`item`，这样我们就可以从`add`方法中获得输入的值。

使用`v-for`指令，我们呈现添加的项目。

`key`需要是一个惟一的 ID，这样 Vue 3 就可以跟踪呈现列表中的项目。

我们有移除按钮来移除项目。

在组件对象中，我们有`data`方法来定义我们想要添加的项目。

`items`拥有我们添加的物品。

在`add`中，我们调用`this.items.push`将一个项目添加到购物清单中。

我们用`uuidv4`函数为每个项目生成一个惟一的 ID。

在`remove`方法中，我们调用`this.items.splice`通过索引删除一个条目。

现在，我们可以分别使用 add item 按钮和 remove 按钮在杂货店中添加和删除商品。

# 结论

我们可以使用 Vue 3 和 JavaScript 轻松编写一个购物清单应用程序。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)