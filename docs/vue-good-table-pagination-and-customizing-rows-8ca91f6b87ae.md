# vue-good-table —分页和定制行

> 原文：<https://javascript.plainenglish.io/vue-good-table-pagination-and-customizing-rows-8ca91f6b87ae?source=collection_archive---------12----------------------->

![](img/1428a03c8508978e2851449ef2a21c29.png)

Photo by [Gift Habeshaw](https://unsplash.com/@gift_habeshaw?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

从头开始创建表是一件痛苦的事情。

这也是为什么有很多表格插件让我们轻松添加表格的原因。

在本文中，我们将了解如何使用 vue-good-table 插件将表格添加到 Vue 应用程序中。

# 分页选项

我们可以用`vue-good-table`组件添加分页。

为了添加它，我们添加了`pagination-options`道具:

```
<template>
  <div>
    <vue-good-table
      :columns="columns"
      :rows="rows"
      :pagination-options="{
        enabled: true,
        mode: 'records',
        perPage: 3,
        position: 'top',
        perPageDropdown: [3, 7, 9],
        dropdownAllowAll: false,
        setCurrentPage: 2,
        nextLabel: 'next',
        prevLabel: 'prev',
        rowsPerPageLabel: 'Rows per page',
        ofLabel: 'of',
        pageLabel: 'page', 
        allLabel: 'All',
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
        { id: 3, name: "Mary", age: 16, birthDay: "2004-10-30" },
        { id: 4, name: "James", age: 18, birthDay: "2002-10-30" }
      ]
    };
  }
};
</script>
```

我们添加了`pagination-options`道具，并将其值设置为一个具有某些属性的对象。

`enabled`表示我们是否要启用分页。

`mode`可以是`'records'`也可以是`'pages'`。

让我们跳到任何一页。

`perPage`是每页的项目数。

`position`是分页栏的位置。

`perPageDropdown`是一页中项目数的数值。

`dropdownAllowAll`表示我们是否要在分页下拉列表中显示“全部”选项。

`setCurrentPage`让我们设置当前页面。

`nextLabel`是转到下一页按钮的标签。

`prevLabel`是转到上一页按钮的标签。

`rowsPerPageLabel`是每页的行数。

`ofLabel`是分页显示中“of”字的标签。

`pageLabel`是我们显示页面的单位。

`allLabel`让我们更改“全部”选项的显示方式。

# 自定义

我们可以使用 vue-good-table 应用各种定制。

其中之一是定制行。

为此，我们可以填充`tabler-row`插槽。

例如，我们可以写:

```
<template>
  <div>
    <vue-good-table :columns="columns" :rows="rows">
      <template slot="table-row" slot-scope="props">
        <span v-if="props.column.field == 'age'">
          <span style="font-weight: bold;">{{props.row.age}}</span>
        </span>
        <span v-else>{{props.formattedRow[props.column.field]}}</span>
      </template>
    </vue-good-table>
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

使用`table-row`插槽，我们可以定制单元格的显示方式。

在我们的例子中，我们检查字段是否是`'age'`。

如果是，我们加粗文本。

否则，我们用`formattedRow`属性正常显示它。

`props.row`有行数据。

`props.column.field`有现场数据。

# 结论

我们可以自定义行的显示方式，并用 vue-good-table 添加分页。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**