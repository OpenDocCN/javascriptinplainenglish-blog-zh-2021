# 在带有 Vuexfire 的 Vue 应用程序中使用 Firebase 查询和替换文档

> 原文：<https://javascript.plainenglish.io/using-firebase-in-a-vue-app-with-vuexfire-querying-and-replacing-documents-f59ca56103a?source=collection_archive---------19----------------------->

![](img/d4ee516bc983b2a1ef47b00cbdfc51bc.png)

Photo by [Amy Humphries](https://unsplash.com/@amyjoyhumphries?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vuefire 库允许我们直接从我们的 Vue 应用程序添加 Firebase 数据库操作功能。

在本文中，我们将了解如何使用 Vuefire 和 Vuexfire 将对云 Firestore 数据库操作的支持添加到我们的 Vue 应用程序中。

# 查询数据库

我们可以查询数据库，用 Vuexfire 与 Vuex 商店同步。

# 整理

为了对我们从 Firebase 数据库中获得的数据进行排序，我们可以调用`orderBy`来对数据进行排序。

`db.js`

```
import firebase from "firebase/app";
import "firebase/firestore";
export const db = firebase
  .initializeApp({ projectId: "project-id" })
  .firestore();
const { Timestamp, GeoPoint } = firebase.firestore;
export { Timestamp, GeoPoint };
```

`main.js`

```
import Vue from "vue";
import App from "./App.vue";
import { firestorePlugin } from "vuefire";
import { vuexfireMutations, firestoreAction } from "vuexfire";
import Vuex from "vuex";
import { db } from "./db";Vue.use(Vuex);
Vue.use(firestorePlugin);
Vue.config.productionTip = false;const store = new Vuex.Store({
  state: {
    books: []
  },
  mutations: {
    ...vuexfireMutations
  },
  actions: {
    bindBooksRef: firestoreAction((context) => {
      return context.bindFirestoreRef(
        "books",
        db.collection("books").orderBy("title", "desc")
      );
    })
  },
  getters: {
    books: (state) => {
      return state.books;
    }
  }
});new Vue({
  store,
  render: (h) => h(App)
}).$mount("#app");
```

`App.vue`

```
<template>
  <div>{{books}}</div>
</template>
<script>
import { mapGetters, mapActions } from "vuex";export default {
  data() {
    return {};
  },
  methods: {
    ...mapActions(["bindBooksRef"])
  },
  computed: {
    ...mapGetters(["books"])
  },
  mounted() {
    this.bindBooksRef();
  }
};
</script>
```

在`bindBookRef`动作中，我们调用了`bindFirestoreRef`方法将`books`状态绑定到我们的`books`数据库集合。

`orderBy`方法按降序对`title`字段值进行排序。

然后`state.books`返回一个`books`对象的数组，其中`title`按降序排序。

因为我们调用了`mapGetters`来将 getters 映射到计算的属性，所以我们将看到它显示在模板中。

# 过滤

我们也可以用`where`方法过滤项目。

例如，我们可以写:

`main.js`

```
import Vue from "vue";
import App from "./App.vue";
import { firestorePlugin } from "vuefire";
import { vuexfireMutations, firestoreAction } from "vuexfire";
import Vuex from "vuex";
import { db } from "./db";Vue.use(Vuex);
Vue.use(firestorePlugin);
Vue.config.productionTip = false;const store = new Vuex.Store({
  state: {
    books: []
  },
  mutations: {
    ...vuexfireMutations
  },
  actions: {
    bindBooksRef: firestoreAction((context) => {
      return context.bindFirestoreRef(
        "books",
        db.collection("books").where("wordCount", ">", 200)
      );
    })
  },
  getters: {
    books: (state) => {
      return state.books;
    }
  }
});new Vue({
  store,
  render: (h) => h(App)
}).$mount("#app");
```

我们调用了`where`来只返回`wordCount`大于 200 的文档。

这就是我们在状态和吸气器中看到的。

# 写入数据库

我们必须使用 Firebase SDK 来写入我们的 Firebase 数据库。

例如，我们可以写:

`main.js`

```
import Vue from "vue";
import App from "./App.vue";
import { firestorePlugin } from "vuefire";
import { vuexfireMutations, firestoreAction } from "vuexfire";
import Vuex from "vuex";
import { db } from "./db";Vue.use(Vuex);
Vue.use(firestorePlugin);
Vue.config.productionTip = false;const store = new Vuex.Store({
  state: {
    books: [],
    book: {}
  },
  mutations: {
    ...vuexfireMutations
  },
  actions: {
    bindBooksRef: firestoreAction((context) => {
      return context.bindFirestoreRef("books", db.collection("books"));
    }), updateBook: firestoreAction(async ({ state }, { bookId, title }) => {
      const bookSnapshot = await db.collection("books").doc(bookId).get();
      const book = bookSnapshot.data();
      const newBook = { ...book, title };
      await db.collection("books").doc(bookId).set(newBook);
      console.log("book updated");
    })
  },
  getters: {
    books: (state) => {
      return state.books;
    }
  }
});new Vue({
  store,
  render: (h) => h(App)
}).$mount("#app");
```

`App.vue`

```
<template>
  <div>
    <button @click="updateBook">update book</button>
    <div>{{books}}</div>
  </div>
</template>
<script>
import { mapGetters, mapActions } from "vuex";export default {
  data() {
    return {};
  },
  methods: {
    ...mapActions(["bindBooksRef"]),
    updateBook() {
      this.$store.dispatch("updateBook", {
        bookId: "ei4jIGJjcmS7eSRKUxsw",
        title: "baz"
      });
    }
  },
  computed: {
    ...mapGetters(["books"])
  },
  mounted() {
    this.bindBooksRef();
  }
};
</script>
```

在 Vuex 商店中，我们有`updateBook`动作让我们通过它的`bookId`得到我们想要更新的书。

我们想用它来更新`title`。

为此，我们用`collection`方法获得了`books`集合。

根据 ID 获取文档。

`get`获取查询结果的快照。

然后`data`方法返回实际数据。

一旦我们这样做了，我们通过创建`newBook`对象来更新`title`。

一旦我们这样做了，我们就调用`set`来更新文档。

在`App`组件中，我们调用了`updateBook`方法中的`dispatch`来调度`updateBook` Vuex 存储动作来进行更新。

由于使用`bindFirestoreRef`将商店状态与收藏同步，更新的项目应该会自动显示。

# 结论

我们可以通过使用 Firebase SDK 中的方法来更新数据。

因为它是异步的，我们必须把代码放到动作中。

此外，当我们将集合绑定到状态时，我们可以对项目进行排序和过滤。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**