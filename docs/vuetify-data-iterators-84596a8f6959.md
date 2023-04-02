# Vuetify —数据迭代器

> 原文：<https://javascript.plainenglish.io/vuetify-data-iterators-84596a8f6959?source=collection_archive---------11----------------------->

![](img/e7b015ee1ee719db823857b3af1c79da.png)

Photo by [Stephen Dawson](https://unsplash.com/@srd844?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vuetify 是一个流行的 Vue 应用程序 UI 框架。

在本文中，我们将了解如何使用 Vuetify 框架。

# 数据迭代器—扩展项目

我们可以用`v-data-iterator`组件展开和折叠项目。

例如，我们可以写:

```
<template>
  <v-container fluid>
    <v-data-iterator
      :items="items"
      item-key="name"
      :items-per-page="4"
      :single-expand="expand"
      hide-default-footer
    >
      <template v-slot:default="{ items, isExpanded, expand }">
        <v-row>
          <v-col v-for="item in items" :key="item.name" cols="12" sm="6" md="4" lg="3">
            <v-card>
              <v-card-title>
                <h4>{{ item.name }}</h4>
              </v-card-title>
              <v-switch
                :input-value="isExpanded(item)"
                :label="isExpanded(item) ? 'Expanded' : 'Closed'"
                class="pl-4 mt-0"
                [@change](http://twitter.com/change)="(v) => expand(item, v)"
              ></v-switch>
              <v-divider></v-divider>
              <v-list v-if="isExpanded(item)" dense>
                <v-list-item>
                  <v-list-item-content>Calories:</v-list-item-content>
                  <v-list-item-content class="align-end">{{ item.calories }}</v-list-item-content>
                </v-list-item>
                <v-list-item>
                  <v-list-item-content>Fat:</v-list-item-content>
                  <v-list-item-content class="align-end">{{ item.fat }}</v-list-item-content>
                </v-list-item>
              </v-list>
            </v-card>
          </v-col>
        </v-row>
      </template>
    </v-data-iterator>
  </v-container>
</template>
<script>
export default {
  name: "HelloWorld",
  data: () => ({
    itemsPerPage: 4,
    items: [
      {
        name: "Yogurt",
        calories: 159,
        fat: 6.0,
      },
      {
        name: "Ice cream sandwich",
        calories: 237,
        fat: 9.0,
      },
      {
        name: "Donuts",
        calories: 262,
        fat: 16.0,
      },
      {
        name: "Cupcake",
        calories: 305,
        fat: 3.7,
      },
    ],
  }),
};
</script>
```

我们从`default`插槽中获取`isExpanded`函数，根据条目是否扩展来设置不同的样式。

如果我们点击`v-switch`，插槽中的`expand`功能可以让我们展开或折叠条目。

# 过滤项目

我们可以对项目进行排序、过滤和分页。

例如，我们可以写:

```
<template>
  <v-container fluid>
    <v-data-iterator
      :items="items"
      :items-per-page.sync="itemsPerPage"
      :page="page"
      :search="search"
      :sort-by="sortBy.toLowerCase()"
      :sort-desc="sortDesc"
      hide-default-footer
    >
      <template v-slot:header>
        <v-toolbar dark color="blue darken-3" class="mb-1">
          <v-text-field
            v-model="search"
            clearable
            flat
            solo-inverted
            hide-details
            prepend-inner-icon="search"
            label="Search"
          ></v-text-field>
          <template v-if="$vuetify.breakpoint.mdAndUp">
            <v-spacer></v-spacer>
            <v-select
              v-model="sortBy"
              flat
              solo-inverted
              hide-details
              :items="keys"
              prepend-inner-icon="search"
              label="Sort by"
            ></v-select>
            <v-spacer></v-spacer>
            <v-btn-toggle v-model="sortDesc" mandatory>
              <v-btn large depressed color="blue" :value="false">
                <v-icon>mdi-arrow-up</v-icon>
              </v-btn>
              <v-btn large depressed color="blue" :value="true">
                <v-icon>mdi-arrow-down</v-icon>
              </v-btn>
            </v-btn-toggle>
          </template>
        </v-toolbar>
      </template> <template v-slot:default="props">
        <v-row>
          <v-col v-for="item in props.items" :key="item.name" cols="12" sm="6" md="4" lg="3">
            <v-card>
              <v-card-title class="subheading font-weight-bold">{{ item.name }}</v-card-title> <v-divider></v-divider> <v-list dense>
                <v-list-item v-for="(key, index) in filteredKeys" :key="index">
                  <v-list-item-content :class="{ 'blue--text': sortBy === key }">{{ key }}:</v-list-item-content>
                  <v-list-item-content
                    class="align-end"
                    :class="{ 'blue--text': sortBy === key }"
                  >{{ item[key.toLowerCase()] }}</v-list-item-content>
                </v-list-item>
              </v-list>
            </v-card>
          </v-col>
        </v-row>
      </template> <template v-slot:footer>
        <v-row class="mt-2" align="center" justify="center">
          <span class="grey--text">Items per page</span>
          <v-menu offset-y>
            <template v-slot:activator="{ on, attrs }">
              <v-btn dark text color="primary" class="ml-2" v-bind="attrs" v-on="on">
                {{ itemsPerPage }}
                <v-icon>mdi-chevron-down</v-icon>
              </v-btn>
            </template>
            <v-list>
              <v-list-item
                v-for="(number, index) in itemsPerPageArray"
                :key="index"
                @click="updateItemsPerPage(number)"
              >
                <v-list-item-title>{{ number }}</v-list-item-title>
              </v-list-item>
            </v-list>
          </v-menu> <v-spacer></v-spacer> <span class="mr-4 grey--text">Page {{ page }} of {{ numberOfPages }}</span>
          <v-btn fab dark color="blue darken-3" class="mr-1" @click="formerPage">
            <v-icon>mdi-chevron-left</v-icon>
          </v-btn>
          <v-btn fab dark color="blue darken-3" class="ml-1" @click="nextPage">
            <v-icon>mdi-chevron-right</v-icon>
          </v-btn>
        </v-row>
      </template>
    </v-data-iterator>
  </v-container>
</template>
<script>
export default {
  name: "HelloWorld",
  data: () => ({
    itemsPerPageArray: [1, 2],
    search: "",
    filter: {},
    sortDesc: false,
    page: 1,
    itemsPerPage: 1,
    sortBy: "name",
    keys: ["Name", "Calories", "Fat"],
    items: [
      {
        name: "Yogurt",
        calories: 159,
        fat: 6.0,
      },
      {
        name: "Ice cream sandwich",
        calories: 237,
        fat: 9.0,
      },
      {
        name: "Donuts",
        calories: 262,
        fat: 16.0,
      },
      {
        name: "Cupcake",
        calories: 305,
        fat: 3.7,
      },
    ],
  }),
  computed: {
    numberOfPages() {
      return Math.ceil(this.items.length / this.itemsPerPage);
    },
    filteredKeys() {
      return this.keys.filter((key) => key !== `Name`);
    },
  },
  methods: {
    nextPage() {
      if (this.page + 1 <= this.numberOfPages) this.page += 1;
    },
    formerPage() {
      if (this.page - 1 >= 1) this.page -= 1;
    },
    updateItemsPerPage(number) {
      this.itemsPerPage = number;
    },
  },
};
</script>
```

我们有文本字段来搜索`header`插槽中的项目。

如果我们在标题的文本字段中输入内容，就会设置`search`状态。

`v-btn-toggle`组件让我们在正向和反向排序之间切换。

当我们点击按钮时，我们切换`sortDesc`状态。

此外，我们有一个设置`sortBy`状态的下拉菜单，让我们按照给定的键自动对项目进行排序。

所有状态都被用作`v-data-iterator`组件中的属性值。

然后所有的排序、分页和搜索逻辑将由`v-data-iterator`负责。

我们还有一个`v-select`让我们用`updateItemsPerPage`方法改变每页的项目数。

内容被填充到`default`槽中。

`props.items`属性包含了我们想要渲染到卡片中的项目。

# 结论

我们可以用带有一些道具的`v-data-iterator`组件添加排序、分页和搜索。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**