# 使用 Nuxt 验证模块向 Nuxt 应用程序添加验证

> 原文：<https://javascript.plainenglish.io/adding-authentication-to-a-nux-app-with-the-nuxt-auth-module-3ce290a829c2?source=collection_archive---------5----------------------->

![](img/72aab0a1307af3c574dc1f8e09ff5e82.png)

Photo by [Marta Bednarska](https://unsplash.com/@lorrenx?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

使用 Nuxt Auth 模块，我们可以轻松地将身份验证添加到我们的 Nuxt 应用程序中。

在本文中，我们将了解如何使用 Express 和 Nuxt Auth 模块向我们的 Nuxt 应用程序添加身份验证。

# 入门指南

我们必须添加 Axios 和 Nuxt 认证模块。

Nuxt Auth 使用 Axios 发送请求。

要安装它，我们运行:

```
yarn add @nuxtjs/auth @nuxtjs/axios
```

或者:

```
npm install @nuxtjs/auth @nuxtjs/axios
```

然后在`nuxt.config.js`中，我们添加:

```
const baseURL = "https://ReasonableRecursiveSupercollider--five-nine.repl.co";export default {
  mode: 'universal',
  target: 'server',
  head: {
    title: process.env.npm_package_name || '',
    meta: [
      { charset: 'utf-8' },
      { name: 'viewport', content: 'width=device-width, initial-scale=1' },
      { hid: 'description', name: 'description', content: process.env.npm_package_description || '' }
    ],
    link: [
      { rel: 'icon', type: 'image/x-icon', href: '/favicon.ico' }
    ]
  },
  css: [
  ],
  plugins: [
  ],
  components: true,
  buildModules: [
  ],
  modules: [
    '@nuxtjs/axios',
    '@nuxtjs/auth'
  ],
  axios: {
    baseURL
  },
  build: {
  }
}
```

我们将`baseURL`添加到`axios`属性来设置请求的基本 URL。

同样，我们将`'@nuxtjs/auth'`模块添加到`modules`数组中来添加模块。

在`store`文件夹中，我们必须添加`index.js`来使用 Nuxt auth 模块。

# 后端

我们使用 Express 作为应用程序的后端。

为了创建它，我们通过运行以下命令来安装 Express 和一些软件包:

```
npm i express body-parser cors
```

在项目文件夹中。

然后，我们在同一个文件夹中创建`index.js`,并添加:

```
const express = require('express');
const bodyParser = require('body-parser');
const cors = require('cors')
const app = express();
app.use(cors())
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));app.post('/api/auth/login', (req, res) => {
  res.json({});
});app.post('/api/auth/logout', (req, res) => {
  res.json({});
});app.get('/api/auth/user', (req, res) => {
  res.json({});
});app.listen(3000, () => console.log('server started'));
```

我们需要`cors`中间件来接受跨域请求。

路由是我们向其发送身份验证请求的端点。

我们应该添加逻辑来检查真实应用程序中的用户。

# 前端

在我们的 Nuxt 应用程序中，我们添加了一个`login.vue`组件，并添加了:

```
<template>
  <div class="container">
    <form @submit.prevent="userLogin">
      <div>
        <label>Username</label>
        <input type="text" v-model="login.username" />
      </div>
      <div>
        <label>Password</label>
        <input type="text" v-model="login.password" />
      </div>
      <div>
        <button type="submit">Submit</button>
      </div>
    </form>
  </div>
</template><script>
export default {
  middleware: "auth",
  data() {
    return {
      login: {},
    };
  },
  auth: {
    strategies: {
      local: {
        endpoints: {
          login: {
            url: `/api/auth/login`,
            method: "post",
            propertyName: "token",
          },
          logout: { url: `/api/auth/logout`, method: "post" },
          user: {
            url: `/api/auth/user`,
            method: "get",
            propertyName: "user",
          },
        },
      },
    },
  },
  methods: {
    async userLogin() {
      try {
        let response = await this.$auth.loginWith("local", {
          data: this.login,
        });
        console.log(response);
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>
```

它有一个输入用户名和密码的登录表单。

在组件选项中，我们使用`middleware: 'auth'`属性来启用`auth`中间件。

然后，我们通过添加`auth.strategies.local`属性来设置 auth 选项，以添加端点，我们将向。

`login`由`this.$auth.loginWith`方法用来发出请求。

`auth.strategies.local`可选`tokenRequired`和`tokenType`属性。

`tokenRequired: false`禁用所有令牌处理。

`tokenType`是要在 Axios 请求中使用的授权头名称。

`this.$auth.loginWith`使用`data`属性，将策略作为第一个参数，将数据作为第二个参数。

因此，当我们提交表单时，会调用`userLogin`方法，并使用请求有效负载中的用户名和密码向`https://ReasonableRecursiveSupercollider--five-nine.repl.co/api/auth/login`发出请求。

# 结论

我们可以用 Nuxt 添加一个登录表单，并使用 auth 模块来发出请求。