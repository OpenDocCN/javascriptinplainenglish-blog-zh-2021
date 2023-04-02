# 虚拟化—表格

> 原文：<https://javascript.plainenglish.io/vuetify-tables-ccd954717858?source=collection_archive---------20----------------------->

![](img/0679f8af380ec567c9ad572dd3891aa9.png)

Photo by [Abel Y Costa](https://unsplash.com/@abelycosta?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vuetify 是一个流行的 Vue 应用程序 UI 框架。

在本文中，我们将了解如何使用 Vuetify 框架。

# 桌子

我们可以添加一个带有`v-simple-table`组件的表格。

例如，我们可以这样写:

```
<template>
  <v-simple-table height="300px">
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-left">Name</th>
          <th class="text-left">Calories</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in desserts" :key="item.name">
          <td>{{ item.name }}</td>
          <td>{{ item.calories }}</td>
        </tr>
      </tbody>
    </template>
  </v-simple-table>
</template>
<script>
export default {
  name: "HelloWorld",
  data: () => ({
    desserts: [
      {
        name: "Yogurt",
        calories: 159,
      },
      {
        name: "Ice cream sandwich",
        calories: 237,
      },
      {
        name: "Eclair",
        calories: 262,
      }
    ],
  }),
};
</script>
```

我们有了带有缺省槽的`v-simple-table`组件，槽中填充了表行。

我们只是使用`v-for`将数组条目渲染成行。

# 固定标题

将`fixed-header`和`height`支撑在一起，让我们将割台固定在桌面上。

例如，我们可以写:

```
<template>
  <v-simple-table height="150px" fixed-header>
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-left">Name</th>
          <th class="text-left">Calories</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in desserts" :key="item.name">
          <td>{{ item.name }}</td>
          <td>{{ item.calories }}</td>
        </tr>
      </tbody>
    </template>
  </v-simple-table>
</template>
<script>
export default {
  name: "HelloWorld",
  data: () => ({
    desserts: [
      {
        name: "Yogurt",
        calories: 159,
      },
      {
        name: "Ice cream sandwich",
        calories: 237,
      },
      {
        name: "Eclair",
        calories: 262,
      },
    ],
  }),
};
</script>
```

使表格可滚动并使标题始终在顶部。

# 密集表

要添加表的密集版本，我们可以使用`dense`道具。

例如，我们可以写:

```
<template>
  <v-simple-table dense>
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-left">Name</th>
          <th class="text-left">Calories</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in desserts" :key="item.name">
          <td>{{ item.name }}</td>
          <td>{{ item.calories }}</td>
        </tr>
      </tbody>
    </template>
  </v-simple-table>
</template>
<script>
export default {
  name: "HelloWorld",
  data: () => ({
    desserts: [
      {
        name: "Yogurt",
        calories: 159,
      },
      {
        name: "Ice cream sandwich",
        calories: 237,
      },
      {
        name: "Eclair",
        calories: 262,
      },
    ],
  }),
};
</script>
```

这些行将比默认版本短。

# 黑暗主题

`dark`道具让我们将桌子切换到黑暗主题:

```
<template>
  <v-simple-table dark>
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-left">Name</th>
          <th class="text-left">Calories</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in desserts" :key="item.name">
          <td>{{ item.name }}</td>
          <td>{{ item.calories }}</td>
        </tr>
      </tbody>
    </template>
  </v-simple-table>
</template>
<script>
export default {
  name: "HelloWorld",
  data: () => ({
    desserts: [
      {
        name: "Yogurt",
        calories: 159,
      },
      {
        name: "Ice cream sandwich",
        calories: 237,
      },
      {
        name: "Eclair",
        calories: 262,
      },
    ],
  }),
};
</script>
```

现在，该表将有一个黑色背景。

# 结论

我们可以用 Vuetify 的`v-simple-table`组件添加一个简单的表。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**