# 使用 Fetch 在 Vue 应用程序中发出 HTTP 请求

> 原文：<https://javascript.plainenglish.io/make-http-requests-in-a-vue-app-with-fetch-adb81884248a?source=collection_archive---------14----------------------->

![](img/aacbfc99dc332c79ee69fa0e38a0d89f.png)

Photo by [Mia Anderson](https://unsplash.com/@miaanderson?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Fetch API 是一个内置于现代浏览器中的 HTTP 客户端。

因此，我们可以用它来发出 HTTP 请求，而不需要安装任何东西。

在本文中，我们将了解如何在 Vue 应用程序中使用 Fetch API 发出请求。

# 提出请求

我们可以用`fetch`函数发出请求。

例如，我们可以写:

```
<template>
  <div id="app"></div>
</template>
<script>
export default {
  name: "App",
  async beforeMount() {
    const res = await fetch("https://jsonplaceholder.typicode.com/posts/1", {
      method: "GET",
      mode: "cors"
    });
    const data = await res.json();
    console.log(data);
  }
};
</script>
```

用`fetch`做一个简单的 GET 请求。

第一个参数是 URL。

第二个是具有`method`和`mode`属性的对象。

`method`属性是请求方法。

`mode`被设置为`'cors'`以允许我们进行跨原点请求。

要发出 POST 请求，我们可以:

```
<template>
  <div id="app"></div>
</template>
<script>
export default {
  name: "App",
  async beforeMount() {
    const res = await fetch("https://jsonplaceholder.typicode.com/posts", {
      method: "POST",
      headers: {
        "Content-Type": "application/json"
      },
      body: JSON.stringify({
        title: "foo",
        body: "bar",
        userId: 1
      })
    });
    const data = await res.json();
    console.log(data);
  }
};
</script>
```

我们设置`headers`属性来设置请求头。

`body`属性具有用于请求体的 stringified JSON 对象。

# 上传文件

要上传文件，我们可以写:

```
<template>
  <div id="app">
    <input type="file" @change="onChange">
  </div>
</template>
<script>
export default {
  name: "App",
  methods: {
    async onChange(ev) {
      const formData = new FormData();
      formData.append("username", "abc123");
      formData.append("avatar", ev.target.files[0]);
      const res = await fetch(
        "https://run.mocky.io/v3/c5189845-2a93-49aa-85c7-70bc64e8af90 ",
        {
          method: "PUT",
          body: formData
        }
      );      
      console.log(res);
    }
  }
};
</script>
```

我们有一个文件输入和一个更改事件监听器来监听文件选择的更改。

`onChange`方法是变更监听器。

在其中，我们创建了一个`FormData`实例，并用`ev.target.files[0]`文件对象将文件添加到其中。

然后，我们通过将`body`属性设置为`formData`对象来发出请求。

例如，我们可以写:

```
<template>
  <div id="app">
    <input type="file" @change="onChange" multiple>
  </div>
</template>
<script>
export default {
  name: "App",
  methods: {
    async onChange(ev) {
      const formData = new FormData();
      formData.append("username", "abc123");
      for (const file of ev.target.files) {
        formData.append("photos", file);
      }
      const res = await fetch(
        "https://run.mocky.io/v3/c5189845-2a93-49aa-85c7-70bc64e8af90 ",
        {
          method: "PUT",
          body: formData
        }
      );
      console.log(res);
    }
  }
};
</script>
```

我们使用 for-of 循环遍历`ev.target.files`对象，将所有文件从对象添加到请求体。

# 检查请求是否成功

我们可以通过捕捉错误来检查请求是否成功。

只会引发网络错误。这不包括带有 400 或 500 系列错误代码的已完成请求。

例如，我们可以写:

```
<template>
  <div id="app"></div>
</template>
<script>
export default {
  name: "App",
  async beforeMount() {
    try {
      const res = await fetch("https://picsum.photos/200");
      const data = await res.blob();
      console.log(data);
    } catch (error) {
      console.error(error);
    }
  }
};
</script>
```

用`catch`块捕捉错误。

# 结论

我们可以使用 Fetch API 在 Vue 应用程序中发出 HTTP 请求。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**