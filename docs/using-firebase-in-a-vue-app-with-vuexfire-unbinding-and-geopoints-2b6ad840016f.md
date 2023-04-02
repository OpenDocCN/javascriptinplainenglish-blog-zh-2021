# 在带有 Vuexfire 的 Vue 应用程序中使用 Firebase 解除绑定和地理点

> 原文：<https://javascript.plainenglish.io/using-firebase-in-a-vue-app-with-vuexfire-unbinding-and-geopoints-2b6ad840016f?source=collection_archive---------16----------------------->

![](img/5f50c9d15a9dc29d6f47bf6ec8009a89.png)

Photo by [Jean-Philippe Delberghe](https://unsplash.com/@jipy32?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vuefire 库允许我们直接从我们的 Vue 应用程序添加 Firebase 数据库操作功能。

在本文中，我们将了解如何使用 Vuefire 和 Vuexfire 将对云 Firestore 数据库操作的支持添加到我们的 Vue 应用程序中。

# 解开

我们可以用`unbindFirestoreRef`方法停止将集合或文档的状态同步到我们的 Vuex 存储。

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
    books: []
  },
  mutations: {
    ...vuexfireMutations
  },
  actions: {
    bindBooksRef: firestoreAction((context) => {
      return context.bindFirestoreRef("books", db.collection("books"));
    }), unbindBooksRef: firestoreAction(({ unbindFirestoreRef }) => {
      unbindFirestoreRef("books");
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

我们添加了`unbindBookRef`动作，该动作用集合名称字符串调用`unbindFirestoreRef`。

默认情况下，当我们解除集合绑定时，Vuex 存储状态将重置为初始值。

`unbindFirestoreRef(“books”);`与`unbindFirestoreRef(“books”, true);`相同。

如果我们不想在解除绑定时重置状态，我们可以传入`false`作为第二个参数:

```
unbindFirestoreRef("books", false);
```

如果我们传入一个返回我们想要重置的值的函数，我们也可以将状态重置为我们想要的值:

```
unbindFirestoreRef('books', () => [{ title: 'foo' }])
```

如果我们重置文档，那么它将被重置为`null`:

```
unbindFirestoreRef('book')
```

# 地理点

我们可以用`GeoPoint`构造函数将地理位置数据保存到 Firebase 文档中。

这仅适用于 Cloud Firestore。

例如，我们可以这样使用它:

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
    cities: []
  },
  mutations: {
    ...vuexfireMutations
  },
  actions: {
    bindCitiesRef: firestoreAction((context) => {
      return context.bindFirestoreRef("cities", db.collection("cities"));
    })
  },
  getters: {
    cities: (state) => {
      return state.cities;
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
  <div>{{cities}}</div>
</template>
<script>
import { mapGetters, mapActions } from "vuex";
import { db, GeoPoint } from "./db";export default {
  data() {
    return {};
  },
  methods: {
    ...mapActions(["bindCitiesRef"])
  },
  computed: {
    ...mapGetters(["cities"])
  },
  async mounted() {
    this.bindCitiesRef();
    await db.collection("cities").add({
      name: "Paris",
      location: new GeoPoint(48.9, 2.3)
    });
  }
};
</script>
```

我们只需调用`add`将条目添加到我们的 Firestore 集合中。

`GeoPoint`构造函数返回一个具有`latitude`和`longitude`属性的对象。

这些也是构造函数的参数。

由于我们调用了`bindCitiesRef`方法，集合的文档会自动与 Vuex 存储同步。

我们调用了`mapGetters`来将`cities` getter 映射到我们的组件，所以我们将在模板中看到文档。

# 结论

我们可以从我们的存储中解除绑定，并将`GeoPoint`实例添加到我们的集合中，并立即看到更新。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**