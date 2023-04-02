# 在 Vue 应用程序 Vuefire 和 Vuexfire 中使用 Firebase

> 原文：<https://javascript.plainenglish.io/using-firebase-in-a-vue-app-vuefire-and-vuexfire-ab5083db112f?source=collection_archive---------19----------------------->

![](img/ab434d16c46af383bb57162beb84bc27.png)

Photo by [Birmingham Museums Trust](https://unsplash.com/@birminghammuseumstrust?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vuefire 库允许我们直接从我们的 Vue 应用程序添加 Firebase 数据库操作功能。

在本文中，我们将了解如何使用 Vuefire 和 Vuexfire 将对云 Firestore 数据库操作的支持添加到我们的 Vue 应用程序中。

# 地理点

我们可以用`GeoPoint`构造函数添加一个地点的纬度和经度。

这仅受 CloudFirestore 支持。

例如，我们可以写:

```
<template>
  <div>
    <button @click="add">add city</button>
    <div v-for="c of cities" :key="c.id">{{c}}</div>
  </div>
</template>
<script>
import { db, GeoPoint } from "./db";
export default {
  data() {
    return {
      cities: []
    };
  },
  mounted() {
    this.$bind("cities", db.collection("cities"));
  },
  methods: {
    async add() {
      await db.collection("cities").add({
        name: "London",
        location: new GeoPoint(51.3, 0)
      });
    }
  }
};
</script>
```

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

我们用一个`GeoPoint`实例调用了`add`方法来保存位置的纬度和经度。

那么我们应该得到这样的结果:

```
{ "name": "London", "location": { "latitude": 51.3, "longitude": 0 } }
```

得救了。

# 时间戳

另外，我们可以用 Vuefire 保存时间戳。

我们使用`Timestamp.fromDate`方法来创建我们的时间戳。

例如，我们可以写:

```
<template>
  <div>
    <button @click="add">add event</button>
    <div v-for="e of events" :key="e.id">{{e}}</div>
  </div>
</template>
<script>
import { db, Timestamp } from "./db";
export default {
  data() {
    return {
      events: []
    };
  },
  mounted() {
    this.$bind("events", db.collection("events"));
  },
  methods: {
    async add() {
      await db.collection("events").add({
        name: "event",
        date: Timestamp.fromDate(new Date("2029-07-14"))
      });
    }
  }
};
</script>
```

我们将一个`Date`实例传递给了`Timestamp.fromDate`。

然后我们会得到这样的结果:

```
{ "name": "event", "date": { "seconds": 1878681600, "nanoseconds": 0 } }
```

结果得救了。

# 武菲尔

我们可以使用 Vuefire 从 Firebase 数据库中获取和设置数据，并将数据库的状态存储在我们的 Vuex 存储中。

要使用它，我们通过运行以下命令来安装所需的软件包:

```
yarn add vuex vuexfire vuefire firebase
```

或者

```
npm i vuex vuexfire vuefire firebase
```

现在，我们可以创建我们的 Vuex 存储，并通过编写以下代码将我们的存储绑定到 Firebase 数据库:

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

我们像往常一样用`Vuex.Store`构造函数创建我们的商店。

但是我们进口`vuefireMutations`并把它放在我们的商店里。

同样，我们的动作是用`fireStoreAction`函数创建的。

我们调用`context.bindFirestoreRef`方法来获取我们的商店数据并将其设置为状态。

第一个参数是州名，第二个参数是我们希望绑定到具有给定名称的州的集合。

此外，我们有一个 getter 来获取`books`状态。

在`App.vue`中，我们将动作和 getters 分别映射到方法和计算属性。

完成之后，我们可以调用映射到方法的`this.bindBooksRef`动作来填充`books`状态。

那么我们的模板应该显示`books`数据。

# 结论

我们可以用 Vuefire 添加地理位置和时间戳数据。

此外，Vuexfire 库让我们可以轻松地将 Firebase 数据库绑定到我们的 Vuex 存储。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**