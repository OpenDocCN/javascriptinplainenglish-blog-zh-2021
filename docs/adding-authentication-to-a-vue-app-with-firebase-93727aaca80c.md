# 使用 Firebase 向 Vue 应用程序添加身份验证

> 原文：<https://javascript.plainenglish.io/adding-authentication-to-a-vue-app-with-firebase-93727aaca80c?source=collection_archive---------12----------------------->

![](img/fc159962e77b2b317d1cfe086e82ef3e.png)

Photo by [Smith Mehta](https://unsplash.com/@smithmehta?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Firebase 为我们提供了内置的身份验证功能。

我们可以用它来管理用户和认证他们。

在本文中，我们将了解如何在 Vue 应用程序中使用 Firebase 的 auth 功能。

# 创建基于密码的帐户

我们可以用几行代码创建基于密码的帐户。

为此，我们可以写:

`App.vue`

```
<template>
  <div>
    <form @submit.prevent="createUser">
      <input type="text" v-model="email" placeholder="email">
      <input type="password" v-model="password" placeholder="password">
      <input type="submit" value="create user">
    </form>
  </div>
</template>
<script>
import firebase from "firebase/app";
import "firebase/auth";
const firebaseConfig = {
  apiKey: "api-key",
  authDomain: "project-id.firebaseapp.com",
  databaseURL: "https://project-id.firebaseio.com",
  projectId: "project-id",
  storageBucket: "project-id.appspot.com",
  appId: "app-id"
};export default {
  data() {
    return {
      email: "",
      password: ""
    };
  },
  beforeMount() {
    firebase.initializeApp(firebaseConfig);
  },
  methods: {
    createUser() {
      const { email, password } = this;
      firebase
        .auth()
        .createUserWithEmailAndPassword(email, password)
        .then(() => alert("user creeated"))
        .catch(function(error) {
          console.log(error);
        });
    }
  }
};
</script>
```

我们用一个对象初始化 Firebase 来配置它。

`apiKey`有 API 密匙。

`authDomain`是 Firebase 应用的网址。

`dataBaseURL`有数据库的 URL。

`projectId`拥有 Firebase 项目 ID。

`storageBucket`是存储桶的 URL。

`appId`是应用的 ID。

在模板中，我们有一个接受电子邮件和密码的表单。

我们有`createUser`方法来创建用户。

`createUserWithEmailAndPassword`方法接受一个电子邮件和密码字符串，用该电子邮件和密码创建用户。

当用户创建成功时，调用`then`回调。

`catch`用户创建失败时调用回调。

`error`具有`code`和`message`属性来获取错误的来源。

# 使用电子邮件地址和密码登录用户

我们可以使用用户名和密码通过`signInWithEmailAndPassword`方法登录。

例如，我们可以写:

```
<template>
  <div>
    <form @submit.prevent="signIn">
      <input type="text" v-model="email" placeholder="email">
      <input type="password" v-model="password" placeholder="password">
      <input type="submit" value="sign in">
    </form>
  </div>
</template>
<script>
import firebase from "firebase/app";
import "firebase/auth";
const firebaseConfig = {
  apiKey: "api-key",
  authDomain: "project-id.firebaseapp.com",
  databaseURL: "https://project-id.firebaseio.com",
  projectId: "project-id",
  storageBucket: "project-id.appspot.com",
  appId: "app-id"
};export default {
  data() {
    return {
      email: "",
      password: ""
    };
  },
  beforeMount() {
    firebase.initializeApp(firebaseConfig);
  },
  methods: {
    signIn() {
      const { email, password } = this;
      firebase
        .auth()
        .signInWithEmailAndPassword(email, password)
        .then(() => alert("sign in successful"))
        .catch(error => {
          console.log(error);
        });
    }
  }
};
</script>
```

我们添加了与`createUser`方法基本相同的`signIn`方法。

# 使用 Google 登录

我们可以用谷歌添加登录。

首先，我们进入应用程序的身份验证部分。

然后，我们转到登录方法部分，将我们的应用托管的域添加到授权域列表中。

现在我们可以添加身份验证了。

例如，我们可以写:

```
<template>
  <div>
    <button @click="signIn">sign in with google</button>
  </div>
</template>
<script>
import firebase from "firebase/app";
import "firebase/auth";
const provider = new firebase.auth.GoogleAuthProvider();
const firebaseConfig = {
  apiKey: "api-key",
  authDomain: "project-id.firebaseapp.com",
  databaseURL: "https://project-id.firebaseio.com",
  projectId: "project-id",
  storageBucket: "project-id.appspot.com",
  appId: "app-id"
};export default {
  data() {
    return {};
  },
  beforeMount() {
    firebase.initializeApp(firebaseConfig);
  },
  methods: {
    signIn() {
      firebase
        .auth()
        .signInWithPopup(provider)
        .then(result => {
          const token = result.credential.accessToken;
          const user = result.user;
          console.log(token, user);
        })
        .catch(error => {
          console.log(error);
          // ...
        });
    }
  }
};
</script>
```

我们用`firebase.auth.GoogleAuthProvider`构造函数创建 Google auth provider。

我们添加了`signIn`方法，该方法使用我们的 auth provider 对象调用`signInWithPopup`方法来添加登录功能。

然后调用`then`回调来获取`user`和`token`。

`user`有用户数据。

`token`有 auth 令牌。

出现错误时会调用`catch`回调，它会向我们提供关于错误的信息，包括电子邮件、代码和消息。

# 结论

我们可以将 Firebase 轻松添加到 Vue 应用程序中。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**