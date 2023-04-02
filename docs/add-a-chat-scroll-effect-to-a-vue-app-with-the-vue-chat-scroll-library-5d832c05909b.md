# 使用 vue 聊天滚动库为 Vue 应用程序添加聊天滚动效果

> 原文：<https://javascript.plainenglish.io/add-a-chat-scroll-effect-to-a-vue-app-with-the-vue-chat-scroll-library-5d832c05909b?source=collection_archive---------10----------------------->

![](img/515598346cab360d55423b1b95b53942.png)

Photo by [JESHOOTS.COM](https://unsplash.com/@jeshoots?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

要在 Vue 应用中添加类似聊天应用中滚动的滚动效果，我们可以使用 vue-chat-scroll 库。

在本文中，我们将看看如何使用 vue-chat-scroll 库来添加聊天滚动效果。

# 装置

我们可以通过运行以下命令来安装该库:

```
npm i vue-chat-scroll
```

我们还可以添加带有脚本标签的库:

```
<script src="https://cdn.jsdelivr.net/npm/vue-chat-scroll/dist/vue-chat-scroll.min.js"></script>
```

# 添加聊天滚动效果

我们可以用`v-chat-scroll`指令添加聊天滚动效果。为此，我们写道:

```
<template>
  <div id="app">
    <ul class="messages" v-chat-scroll>
      <li class="message" v-for="(n, i) in messages" :key="i">{{ n }}</li>
    </ul>
    <form @submit.prevent="addMessage">
      <input v-model="message">
      <input type="submit">
    </form>
  </div>
</template><script>
export default {
  name: "App",
  data() {
    return {
      message: "",
      messages: [
        "Lorem",
        "ipsum",
        "dolor",
        "sit",
        "amet,",
        "consectetur",
        "adipiscing",
        "elit.",
        "Praesent",
        "facilisis",
        "justo"
      ]
    };
  },
  methods: {
    addMessage() {
      this.messages.push(this.message);
      this.message = "";
    }
  }
};
</script>
```

现在，当我们在框中输入内容并提交时，`v-chat-scroll`指令会滚动到列表的底部。

我们有一个表单，我们提交添加到`this.messages`数组。

# 当用户向上滚动时防止向下滚动并平滑滚动

我们可以通过将`always`属性设置为`false`来防止用户向上滚动时的向下滚动效果。

我们可以添加平滑滚动，将`smooth`属性设置为`true`:

```
<template>
  <div id="app">
    <ul class="messages" v-chat-scroll="{always: false, smooth: true}">
      <li class="message" v-for="(n, i) in messages" :key="i">{{ n }}</li>
    </ul>
    <form [@submit](http://twitter.com/submit).prevent="addMessage">
      <input v-model="message">
      <input type="submit">
    </form>
  </div>
</template><script>
export default {
  name: "App",
  data() {
    return {
      message: "",
      messages: [
        "Lorem",
        "ipsum",
        "dolor",
        "sit",
        "amet,",
        "consectetur",
        "adipiscing",
        "elit.",
        "Praesent",
        "facilisis",
        "justo"
      ]
    };
  },
  methods: {
    addMessage() {
      this.messages.push(this.message);
      this.message = "";
    }
  }
};
</script>
```

我们只能为更新添加平滑滚动，而不能在第一次加载时使用`notSmoothOnInit`属性:

```
<template>
  <div id="app">
    <ul class="messages" v-chat-scroll="{smooth: true, notSmoothOnInit: true}">
      <li class="message" v-for="(n, i) in messages" :key="i">{{ n }}</li>
    </ul>
    <form [@submit](http://twitter.com/submit).prevent="addMessage">
      <input v-model="message">
      <input type="submit">
    </form>
  </div>
</template><script>
export default {
  name: "App",
  data() {
    return {
      message: "",
      messages: [
        "Lorem",
        "ipsum",
        "dolor",
        "sit",
        "amet,",
        "consectetur",
        "adipiscing",
        "elit.",
        "Praesent",
        "facilisis",
        "justo"
      ]
    };
  },
  methods: {
    addMessage() {
      this.messages.push(this.message);
      this.message = "";
    }
  }
};
</script>
```

我们还可以添加`scrollonremoved`属性来确保在元素加载指示器被移除后发生滚动:

```
<template>
  <div id="app">
    <ul class="messages" v-chat-scroll="{always: false, smooth: true, scrollonremoved:true}">
      <li class="message" v-for="(n, i) in messages" :key="i">{{ n }}</li>
      <li v-if="loading">...</li>
    </ul>
    <form [@submit](http://twitter.com/submit).prevent="addMessage">
      <input v-model="message">
      <input type="submit">
    </form>
  </div>
</template><script>
export default {
  name: "App",
  data() {
    return {
      message: "",
      messages: [
        "Lorem",
        "ipsum",
        "dolor",
        "sit",
        "amet,",
        "consectetur",
        "adipiscing",
        "elit.",
        "Praesent",
        "facilisis",
        "justo"
      ],
      loading: false
    };
  },
  methods: {
    addMessage() {
      this.loading = true;
      setTimeout(() => {
        this.messages.push(this.message);
        this.message = "";
        this.loading = false;
      }, 1000);
    }
  }
};
</script>
```

我们在提交消息时将`this.loading`设置为`true`，在添加消息时将其设置为`false`。

拥有`scrollonremoved`属性确保了当加载指示器消失时，滚动将会发生。

# 结论

vue-chat-scroll 库让我们可以在 vue 应用程序中轻松滚动到文本列表的底部。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**