# 使用 vue-good-table 插件在 Vue 应用程序中添加表格

> 原文：<https://javascript.plainenglish.io/add-tables-in-a-vue-app-with-the-vue-good-table-plugin-6fd4f935746c?source=collection_archive---------16----------------------->

![](img/6d44cd313f0fa10eafbdddc0e1e3bdd6.png)

Photo by [Abel Y Costa](https://unsplash.com/@abelycosta?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

从头开始创建表是一件痛苦的事情。

这也是为什么有很多表格插件让我们轻松添加表格的原因。

在本文中，我们将了解如何使用 vue-good-table 插件将表格添加到 Vue 应用程序中。

# 入门指南

我们可以从安装包开始。

为此，我们运行:

```
npm install --save vue-good-table
```

然后我们可以通过编写以下代码将插件添加到`main.js`:

```
import Vue from "vue";
import App from "./App.vue";
import VueGoodTablePlugin from "vue-good-table";
import "vue-good-table/dist/vue-good-table.css";Vue.use(VueGoodTablePlugin);Vue.config.productionTip = false;new Vue({
  render: (h) => h(App)
}).$mount("#app");
```

添加样式和插件。

我们还可以使用以下命令将其导入到我们的组件中:

```
import 'vue-good-table/dist/vue-good-table.css'
import { VueGoodTable } from 'vue-good-table';//...
components: {
  VueGoodTable,
}
```

现在我们可以通过编写以下内容来添加一个简单的表:

```
<template>
  <div>
    <vue-good-table :columns="columns" :rows="rows"/>
  </div>
</template><script>
export default {
  data() {
    return {
      columns: [
        {
          label: "Name",
          field: "name"
        },
        {
          label: "Age",
          field: "age",
          type: "number"
        },
        {
          label: "Birthday",
          field: "birthDay",
          type: "date",
          dateInputFormat: "yyyy-MM-dd",
          dateOutputFormat: "MMM do yy"
        }
      ],
      rows: [
        { id: 1, name: "John", age: 20, birthDay: "2000-01-20" },
        { id: 2, name: "Jane", age: 24, birthDay: "1996-10-31" },
        { id: 3, name: "Susan", age: 16, birthDay: "2004-10-30" }
      ]
    };
  }
};
</script>
```

我们用`columns` pro【】添加列定义。

`label`是显示的标题。

`field`是要显示的字段的属性名。

`dateInputFormat`是表格中日期行对象的格式。

`dateOutputFormat`是显示的日期输出格式。

`rows`道具有一个显示为行的对象数组。

# 表格选项

我们可以用 vue-good-table 更改许多选项。

其中之一是最大高度。

这可以用`max-height`道具改变:

```
<template>
  <div>
    <vue-good-table :columns="columns" :rows="rows" max-height="300px"/>
  </div>
</template><script>
export default {
  data() {
    return {
      columns: [
        {
          label: "Name",
          field: "name"
        },
        {
          label: "Age",
          field: "age",
          type: "number"
        },
        {
          label: "Birthday",
          field: "birthDay",
          type: "date",
          dateInputFormat: "yyyy-MM-dd",
          dateOutputFormat: "MMM do yy"
        }
      ],
      rows: [
        { id: 1, name: "John", age: 20, birthDay: "2000-01-20" },
        { id: 2, name: "Jane", age: 24, birthDay: "1996-10-31" },
        { id: 3, name: "Susan", age: 16, birthDay: "2004-10-30" }
      ]
    };
  }
};
</script>
```

我们可以用`fixed-header`支柱固定割台:

```
<template>
  <div>
    <vue-good-table :columns="columns" :rows="rows" fixed-header/>
  </div>
</template><script>
export default {
  data() {
    return {
      columns: [
        {
          label: "Name",
          field: "name"
        },
        {
          label: "Age",
          field: "age",
          type: "number"
        },
        {
          label: "Birthday",
          field: "birthDay",
          type: "date",
          dateInputFormat: "yyyy-MM-dd",
          dateOutputFormat: "MMM do yy"
        }
      ],
      rows: [
        { id: 1, name: "John", age: 20, birthDay: "2000-01-20" },
        { id: 2, name: "Jane", age: 24, birthDay: "2011-10-31" },
        { id: 3, name: "Susan", age: 16, birthDay: "2011-10-30" }
      ]
    };
  }
};
</script>
```

# 结论

我们可以使用 vue-good-table 插件轻松地将表格添加到 Vue 应用程序中。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**