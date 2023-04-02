# 使用 Firebase 向 Nuxt 应用程序添加身份验证

> 原文：<https://javascript.plainenglish.io/adding-authentication-to-a-nuxt-app-with-the-firebase-cb9739583a2f?source=collection_archive---------7----------------------->

![](img/4b7d5fe42ba827a4edf3c13161525c53.png)

Photo by [Félix Lam](https://unsplash.com/@feliixlam?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

使用 Nuxt Auth 模块，我们可以轻松地将身份验证添加到我们的 Nuxt 应用程序中。

一种方法是用 Firebase 添加身份验证。

在本文中，我们将了解如何向服务器端呈现的 Nuxt 应用程序添加 Firebase 身份验证。

# 安装软件包

我们必须添加一些包来将 Firebase 添加到我们的 Nuxt 应用程序中。

为此，我们运行:

```
npm i @nuxtjs/firebase @nuxtjs/pwa firebase firebase-admin
```

添加所需的包。

# 配置

我们必须向我们的 Nuxt 应用程序添加配置，以便我们可以在加载页面时获取用户。

在`nuxt.config.js`中，我们写道:

```
export default {
  /*
  ** Nuxt rendering mode
  ** See https://nuxtjs.org/api/configuration-mode
  */
  mode: 'universal',
  /*
  ** Nuxt target
  ** See https://nuxtjs.org/api/configuration-target
  */
  target: 'server',
  /*
  ** Headers of the page
  ** See https://nuxtjs.org/api/configuration-head
  */
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
  /*
  ** Global CSS
  */
  css: [
  ],
  /*
  ** Plugins to load before mounting the App
  ** https://nuxtjs.org/guide/plugins
  */
  plugins: [
  ],
  /*
  ** Auto import components
  ** See https://nuxtjs.org/api/configuration-components
  */
  components: true,
  /*
  ** Nuxt.js dev-modules
  */
  buildModules: [
  ],
  /*
  ** Nuxt.js modules
  */
  modules: [
    // Doc: https://axios.nuxtjs.org/usage
    '@nuxtjs/axios',
    '@nuxtjs/pwa',
    [
      '@nuxtjs/firebase',
      {
        config: {
          apiKey: "api-key",
          authDomain: "project-id.firebaseapp.com",
          databaseURL: "https://project-id.firebaseio.com",
          projectId: "project-id",
          storageBucket: "project-id.appspot.com",
          messagingSenderId: 'message-sender-id',
          appId: "BookDb"
        },
        services: {
          auth: {
            persistence: 'local',
            initialize: {
              onAuthStateChangedMutation: "SET_USER",
              onAuthStateChangedAction: 'onAuthStateChangedAction',
            },
            ssr: {
              serverLogin: {
                sessionLifetime: 60 * 60 * 1000,
                loginDelay: 50
              }
            }
          }
        }
      }
    ]
  ],
  /*
  ** Axios module configuration
  ** See https://axios.nuxtjs.org/options
  */
  axios: {},
  /*
  ** Build configuration
  ** See https://nuxtjs.org/api/configuration-build/
  */
  build: {
  },
  firebase: {
    services: {
      auth: {
        ssr: true
      }
    }
  },
  pwa: {
    meta: false,
    icon: false,
    workbox: {
      importScripts: [
        '/firebase-auth-sw.js'
      ],
      dev: true
    }
  }
}
```

我们添加了带有许多选项的`@nuxtjs/firebase`模块。

`config`属性有 Firebase 配置选项。

`services`配置`auth`服务来持久化用户。

`onAuthStateChangeMutation`动作是保存认证用户数据的 Vuex 动作。

`ssr`有保留用户数据多长时间的选项。

`sessionLifetime`属性具有会话生存期。

而`loginDelay`是成功登录后保存用户数据的延迟。

# Vuex 商店

我们必须创建一个 Vuex 商店来存储数据。

为此，我们创建一个`store/index.js`文件并编写:

```
export const state = () => ({
  authUser: {}
})export const actions = {
  async onAuthStateChangedAction({ commit }, { authUser, claims }) {
    const { uid, email, emailVerified, displayName, photoURL } = authUser commit('SET_USER', {
      uid,
      email,
      emailVerified,
      displayName,
      photoURL,
      isAdmin: claims.custom_claim
    })
  },
  async nuxtServerInit({ dispatch, commit }, { res }) {
    console.log(res.locals)
    if (res && res.locals && res.locals.user) {
      const { allClaims: claims, idToken: token, ...authUser } = res.locals.user
      await dispatch('onAuthStateChangedAction', {
        authUser,
        claims,
        token
      })
      commit('ON_AUTH_STATE_CHANGED_MUTATION', { authUser, claims, token })
    }
  }
}export const mutations = {
  ON_AUTH_STATE_CHANGED_MUTATION(state, { authUser, claims }) {
    const { uid, email, emailVerified, displayName, photoURL } = authUser state.authUser = {
      uid,
      displayName,
      email,
      emailVerified,
      photoURL: photoURL || null,
      isAdmin: claims.custom_claim
    }
  },
  SET_USER(state, payload) {
    console.log(payload)
    state.authUser = payload;
  }
}
```

`onAuthStateChanged`动作由`nuxtServerInit`调用，以在页面加载时设置认证用户的数据。

页面加载时运行`nuxtServerInit`。

`ON_AUTH_STATE_CHANGED_MUTATION`是保存`authUser`状态的突变。

`SET_USER`设置`authUser`状态。

当我们运行`this.$fireAuth.signInWithEmailAndPassword`方法时，通过正确的凭证验证运行成功，那么动作和突变将会运行。

还将设置`nuxtServerInit`中的`res.locals.user`属性，以便我们在页面加载时拥有当前登录用户的数据。

# 登录表单

最后，我们需要一个登录表单，以便我们可以登录。

我们创建一个`login.vue`文件并添加:

```
<template>
  <div class="container">
    <form @submit="signIn">
      <div>
        <label>Username</label>
        <input type="text" v-model="login.email" />
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
  data() {
    return {
      login: {},
    };
  },
  methods: {
    async signIn() {
      try {
        const { email, password } = this.login;
        await this.$fireAuth.signInWithEmailAndPassword(email, password);
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>
```

我们创建一个登录表单，如果我们使用正确的电子邮件和密码登录，就会运行 Vuex 操作来设置数据。

这是因为 Nuxt Firebase 自带的`static/assets/firebase-auth-sw.js`服务人员会在后台为我们工作。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**