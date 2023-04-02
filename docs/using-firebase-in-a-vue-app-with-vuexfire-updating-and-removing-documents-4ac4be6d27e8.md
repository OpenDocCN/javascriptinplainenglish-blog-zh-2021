# 在带有 Vuexfire 的 Vue 应用程序中使用 Firebase 更新和删除文档

> 原文：<https://javascript.plainenglish.io/using-firebase-in-a-vue-app-with-vuexfire-updating-and-removing-documents-4ac4be6d27e8?source=collection_archive---------5----------------------->

![](img/52119c11f619018d11a80ca602e6762b.png)

Photo by [Hayden Scott](https://unsplash.com/@hayden?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vuefire 库允许我们直接从我们的 Vue 应用程序添加 Firebase 数据库操作功能。

在本文中，我们将了解如何使用 Vuefire 和 Vuexfire 将对云 Firestore 数据库操作的支持添加到我们的 Vue 应用程序中。

# 更新文档

我们可以用`update`方法更新文档。

例如，我们可以写:

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
import { db } from "./db";
Vue.use(Vuex);
Vue.use(firestorePlugin);
Vue.config.productionTip = false;
const store = new Vuex.Store({
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
    }),
    updateBook: firestoreAction(async ({ state }, { bookId, title }) => {
      await db.collection("books").doc(bookId).update({ title });
      console.log("book updated");
    })
  },
  getters: {
    books: (state) => {
      return state.books;
    }
  }
});
new Vue({
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
import { mapGetters, mapActions } from "vuex";
export default {
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

我们有`bindBooksRef`动作来同步`books` Firebase 集合和`books`状态。

此外，我们有`updateBook`动作来更新数据库中`books`集合中的文档。

`doc`方法通过 ID 获取`books`文档。

`update`让我们通过传递一个对象来更新一个文档，该对象带有我们想要更新的键和值。

# 删除文档

我们可以用`delete`或`remove`方法删除文档。

例如，我们可以写:

`main.js`

```
import Vue from "vue";
import App from "./App.vue";
import { firestorePlugin } from "vuefire";
import { vuexfireMutations, firestoreAction } from "vuexfire";
import Vuex from "vuex";
import { db } from "./db";
Vue.use(Vuex);
Vue.use(firestorePlugin);
Vue.config.productionTip = false;
const store = new Vuex.Store({
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
    }),
    deleteBook: firestoreAction(async ({ state }, bookId) => {
      await db.collection("books").doc(bookId).delete();
      console.log("book updated");
    })
  },
  getters: {
    books: (state) => {
      return state.books;
    }
  }
});
new Vue({
  store,
  render: (h) => h(App)
}).$mount("#app");
```

`App.vue`

```
<template>
  <div>
    <button @click="deleteBook">delete book</button>
    <div>{{books}}</div>
  </div>
</template>
<script>
import { mapGetters, mapActions } from "vuex";
export default {
  data() {
    return {};
  },
  methods: {
    ...mapActions(["bindBooksRef"]),
    deleteBook() {
      this.$store.dispatch("deleteBook", "ei4jIGJjcmS7eSRKUxsw");
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

我们有由`firestoreAction`函数创建的`deleteBook`动作。

回调获取`bookId`有效负载并调用`delete`删除具有给定 ID 的`book`文档。

在`App.vue`中，我们添加了用`'deleteBook'`动作调用`this.$store.dispatch`的`deleteBook`方法。

第二个参数是有效载荷。

# 结论

我们可以用 Vuexfire 的几行代码创建 Vuex 动作来更新和删除文档。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**