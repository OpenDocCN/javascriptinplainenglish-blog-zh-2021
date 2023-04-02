# vue-good-Table-表格样式

> 原文：<https://javascript.plainenglish.io/vue-good-table-table-styling-4c5c3ddec13b?source=collection_archive---------23----------------------->

![](img/56beb8b72e2f92dcbaa65b719de11add.png)

Photo by [Amanda Vick](https://unsplash.com/@amandavickcreative?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

从头开始创建表是一件痛苦的事情。

这也是为什么有很多表格插件让我们轻松添加表格的原因。

在本文中，我们将了解如何使用 vue-good-table 插件将表格添加到 Vue 应用程序中。

# 。vgt-表。有斑纹的

我们可以用`striped`类添加行分条。

例如，我们可以写:

```
<template>
  <div>
    <vue-good-table :columns="columns" :rows="rows" styleClass="vgt-table striped"></vue-good-table>
  </div>
</template>
<script>
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
        { id: 3, name: "Mary", age: 16, birthDay: "2004-10-30" }
      ]
    };
  }
};
</script><style>
.vgt-table {
  border: 1px solid red !important;
}
</style>
```

现在这些行是条纹状的。

# 。vgt-表。有边的

我们可以让表格行以`bordered`类为边界。

例如，我们可以写:

```
<template>
  <div>
    <vue-good-table :columns="columns" :rows="rows" styleClass="vgt-table bordered"></vue-good-table>
  </div>
</template>
<script>
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
        { id: 3, name: "Mary", age: 16, birthDay: "2004-10-30" }
      ]
    };
  }
};
</script>
```

我们添加了`bordered`类来为行和列添加边框。

# 浓缩表

为了使表更简洁，我们可以添加`condensed`类:

```
<template>
  <div>
    <vue-good-table :columns="columns" :rows="rows" styleClass="vgt-table condensed"></vue-good-table>
  </div>
</template>
<script>
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
        { id: 3, name: "Mary", age: 16, birthDay: "2004-10-30" }
      ]
    };
  }
};
</script>
```

# 厚颜无耻

我们可以通过编写以下代码来导入 vue-good-table 库提供的 SASS 样式:

```
<template>
  <div>
    <vue-good-table :columns="columns" :rows="rows" styleClass="vgt-table condensed"></vue-good-table>
  </div>
</template>
<script>
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
        { id: 3, name: "Mary", age: 16, birthDay: "2004-10-30" }
      ]
    };
  }
};
</script><style lang="scss">
@import "../node_modules/vue-good-table/src/styles/style.scss";
</style>
```

`@import`指令允许我们将样式导入到我们的应用程序中。

# 结论

我们可以用 vue-good-table 插件用各种方法添加样式。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**