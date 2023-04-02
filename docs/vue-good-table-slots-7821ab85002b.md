# vue-good-table-插槽

> 原文：<https://javascript.plainenglish.io/vue-good-table-slots-7821ab85002b?source=collection_archive---------26----------------------->

![](img/dbb27dd2aed9fa077c25ce4c67aa9d84.png)

Photo by [Aysha Begum](https://unsplash.com/@aysha_be?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

从头开始创建表是一件痛苦的事情。

这也是为什么有很多表格插件让我们轻松添加表格的原因。

在本文中，我们将了解如何使用 vue-good-table 插件将表格添加到 Vue 应用程序中。

# 表格动作槽

我们可以用自己的内容填充插槽。

例如，我们可以写:

```
<template>
  <div>
    <vue-good-table :columns="columns" :rows="rows">
      <div slot="table-actions">top slot.</div>
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
        { id: 2, name: "Jane", age: 24, birthDay: "2011-10-31" },
        { id: 3, name: "Susan", age: 16, birthDay: "2011-10-30" }
      ]
    };
  }
};
</script>
```

我们将`slot`属性设置为`table-actions`来填充`table-actions`插槽。

内容将显示在表格标题的上方。

# 空状态槽

我们也可以在桌子空着的时候展示一些东西。

例如，我们可以写:

```
<template>
  <div>
    <vue-good-table :columns="columns" :rows="rows">
      <div slot="emptystate">Nothing to show</div>
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
      rows: []
    };
  }
};
</script>
```

当`rows`为空时，我们填充`emptystate`槽来显示一些东西。

内容将代替行单元格显示。

# 方式

我们可以将`mode`设置为`remote`,以便允许由服务器端而不是客户端来支持排序和过滤:

```
<template>
  <div>
    <vue-good-table :columns="columns" :rows="rows" mode="remote"/>
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

# 紧凑模式

我们可以添加`compactMode`道具以紧凑模式显示表格。

例如，我们可以写:

```
<template>
  <div>
    <vue-good-table :columns="columns" :rows="rows" compactMode/>
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

现在，当我们的屏幕很窄时，这些列将被堆叠起来。

# 结论

我们可以填充各种插槽，在表格顶部显示内容，或者在没有内容时显示内容。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**