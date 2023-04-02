# 在带有 Vuexfire 的 Vue 应用程序中使用 Firebase 添加数据

> 原文：<https://javascript.plainenglish.io/using-firebase-in-a-vue-app-with-vuexfire-adding-data-3afcbebf02b?source=collection_archive---------21----------------------->

![](img/aab3a01eb06d5eba70f7c5963608c0be.png)

Photo by [Element5 Digital](https://unsplash.com/@element5digital?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vuefire 库允许我们直接从我们的 Vue 应用程序添加 Firebase 数据库操作功能。

在本文中，我们将了解如何使用 Vuefire 和 Vuexfire 将对云 Firestore 数据库操作的支持添加到我们的 Vue 应用程序中。

# 时间戳

我们可以用`Timestamp.fromDate`方法给文档添加时间戳。

这仅在我们将 Vuexfire 与 Cloud Firestore 配合使用时可用。

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
import { db } from "./db";Vue.use(Vuex);
Vue.use(firestorePlugin);
Vue.config.productionTip = false;const store = new Vuex.Store({
  state: {
    events: []
  },
  mutations: {
    ...vuexfireMutations
  },
  actions: {
    bindEventsRef: firestoreAction((context) => {
      return context.bindFirestoreRef("events", db.collection("events"));
    })
  },
  getters: {
    events: (state) => {
      return state.events;
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
  <div>{{events}}</div>
</template>
<script>
import { mapGetters, mapActions } from "vuex";
import { db, Timestamp } from "./db";export default {
  data() {
    return {};
  },
  methods: {
    ...mapActions(["bindEventsRef"])
  },
  computed: {
    ...mapGetters(["events"])
  },
  async mounted() {
    this.bindEventsRef();
    await db.collection("events").add({
      name: "event",
      date: Timestamp.fromDate(new Date("2029-09-14"))
    });
  }
};
</script>
```

我们调用`Timestamp.fromDate`方法来添加时间戳。

我们调用了`bindEventsRef`来同步`events`集合和我们商店中的`events`状态。

然后我们用一个 getter 得到`events`状态。

那么我们的`events`状态大概是:

```
[ { "name": "event", "date": { "seconds": 1884038400, "nanoseconds": 0 } } ]
```

我们还可以调用`toDate`将`Timestamp`对象变回人类可读的日期:

```
<template>
  <div>
    <div v-for="e of events" :key="e.id">{{e.date.toDate()}}</div>
  </div>
</template>
<script>
import { mapGetters, mapActions } from "vuex";
import { db, Timestamp } from "./db";export default {
  data() {
    return {};
  },
  methods: {
    ...mapActions(["bindEventsRef"])
  },
  computed: {
    ...mapGetters(["events"])
  },
  async mounted() {
    this.bindEventsRef();
    await db.collection("events").add({
      name: "event",
      date: Timestamp.fromDate(new Date("2029-09-14"))
    });
  }
};
</script>
```

# 参考

我们可以在一个文档中存储另一个文档的引用。

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
      return context.bindFirestoreRef("books", db.collection("books"));
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
import { mapGetters, mapActions } from "vuex";
import { db } from "./db";export default {
  data() {
    return {};
  },
  methods: {
    ...mapActions(["bindBooksRef"])
  },
  computed: {
    ...mapGetters(["books"])
  },
  async mounted() {
    this.bindBooksRef();
    await db.collection("books").add({
      title: "foo",
      author: db.collection("authors").doc("james-smith")
    });
  }
};
</script>
```

我们只是用`db.collection`得到集合。

然后用它返回的内容，我们调用`doc`，用`authors`文档的 ID 作为参数来引用它。

# 结论

我们可以将文档添加到我们的 Firebase 数据库集合中，如果我们将 Vuex 状态绑定到我们的集合，它们将自动反映在我们的 Vue 应用程序中。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**