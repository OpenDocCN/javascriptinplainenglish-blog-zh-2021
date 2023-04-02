# 在带有 Vuexfire 的 Vue 应用程序中使用 Firebase 添加文档和当前时间戳

> 原文：<https://javascript.plainenglish.io/using-firebase-in-a-vue-app-with-vuexfire-add-document-and-current-timestamp-ed51a752ed09?source=collection_archive---------12----------------------->

![](img/6fc61e174745308276dea51de2ba9ab2.png)

Photo by [Aditya Joshi](https://unsplash.com/@adijoshi11?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vuefire 库允许我们直接从我们的 Vue 应用程序添加 Firebase 数据库操作功能。

在本文中，我们将了解如何使用 Vuefire 和 Vuexfire 将对云 Firestore 数据库操作的支持添加到我们的 Vue 应用程序中。

# 向集合中添加文档

我们可以用`add`方法将文档添加到集合中。

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
    addBook: firestoreAction(async ({ state }, book) => {
      await db.collection("books").add(book);
      console.log("book added");
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
    <button @click="addBook">add book</button>
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
    addBook() {
      this.$store.dispatch("addBook", { title: "qux" });
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

我们有`bindBookRef`动作来同步 Firebase `books`集合和`books`状态。

此外，我们还有`addBook`动作，它调用`add`将我们的`book`对象添加到`books`集合中。

然后在`App.vue`中，我们调用`this.$store.dispatch`方法，用我们想要添加的对象调度`addBook`动作。

当我们点击按钮时，按钮运行`addBook`方法。

所以当我们点击它时，条目被添加。

# 当前时间戳

我们可以在创建或更新时添加当前时间戳。

为此，我们可以使用`firebase.firestore.FieldValue.serverTimestamp`方法。

例如，我们可以写:

`App.vue`

```
<template>
  <div>
    <button @click="addBook">add book</button>
    <div>{{books}}</div>
  </div>
</template>
<script>
import { mapGetters, mapActions } from "vuex";
import firebase from "firebase/app";export default {
  data() {
    return {};
  },
  methods: {
    ...mapActions(["bindBooksRef"]),
    addBook() {
      this.$store.dispatch("addBook", {
        title: "qux",
        createdAt: firebase.firestore.FieldValue.serverTimestamp()
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

我们只是在任何想要添加时间戳的地方使用它。

然后我们会得到这样的结果:

```
{ "createdAt": { "seconds": 1598895154, "nanoseconds": 675000000 }, "title": "qux" }
```

添加到`books`收藏中。

# 结论

Vuexfire 为我们提供了使用我们的 Vue 应用程序和 Firebase 添加文档和当前时间戳的方法。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**