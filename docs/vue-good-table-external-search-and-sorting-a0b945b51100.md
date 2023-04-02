# vue-good-table —外部搜索和排序

> 原文：<https://javascript.plainenglish.io/vue-good-table-external-search-and-sorting-a0b945b51100?source=collection_archive---------9----------------------->

![](img/a4ba77a83a6a13c815532cacdb004432.png)

Photo by [Anthony Martino](https://unsplash.com/@amartino20?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

从头开始创建表是一件痛苦的事情。

这也是为什么有很多表格插件让我们轻松添加表格的原因。

在本文中，我们将了解如何使用 vue-good-table 插件将表格添加到 Vue 应用程序中。

# 外部搜索

我们可以将`externalQuery`属性添加到`search-options`对象来搜索阿布模型值。

例如，我们可以写:

```
<template>
  <div>
    <input type="text" v-model="searchTerm">
    <vue-good-table
      :columns="columns"
      :rows="rows"
      :search-options="{
        enabled: true,
        externalQuery: searchTerm 
      }"
    />
  </div>
</template><script>
export default {
  data() {
    return {
      searchTerm: '',
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

我们添加了自己的输入框，这样我们就可以用它来搜索表格。

`v-model`绑定到我们设置为`externalQuery`的值的`searchTerm`来进行搜索。

# 排序选项

此外，我们可以用 vue-good-table 更改排序选项。

为此，我们设置了`sort-options`道具。

例如，我们可以写:

```
<template>
  <div>
    <vue-good-table
      :columns="columns"
      :rows="rows"
      :sort-options="{
        enabled: true,
        initialSortBy: {field: 'name', type: 'desc'}
      }"
    />
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
        { id: 3, name: "Mary", age: 16, birthDay: "2004-10-30" }
      ]
    };
  }
};
</script>
```

我们添加了`sort-options`属性，并将其值设置为具有`enabled`和`initialSortBy`属性的对象。

`enabled`设置为`true`启用初始装载时的分类。

`field`设置作为排序依据的属性名称。

并且`type`让我们改变排序顺序。

# 多列排序

我们可以按多列排序。

为此，我们只需将`initialSortBy`设置为一个对象数组:

```
<template>
  <div>
    <vue-good-table
      :columns="columns"
      :rows="rows"
      :sort-options="{
        enabled: true,
        initialSortBy:[
          {field: 'name', type: 'asc'},
          {field: 'age', type: 'desc'}
        ]
      }"
    />
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
        { id: 3, name: "Mary", age: 16, birthDay: "2004-10-30" }
      ]
    };
  }
};
</script>
```

使用我们传递到`initialSortBy`数组中的对象数组，我们对`name`和`age`列进行排序。

# 结论

我们可以使用带有`vue-good-table`组件的`sort-options` prop 轻松地对表格中的项目进行排序。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**