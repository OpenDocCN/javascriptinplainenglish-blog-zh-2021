# Next.js Firebase v9:切换到不同的页面

> 原文：<https://javascript.plainenglish.io/nextjs-firebase-v9-part-17-switch-to-different-pages-f04969a480c1?source=collection_archive---------16----------------------->

## 第 17 部分:使用 React useContext 返回当前用户信息

在前一篇文章中，我们已经创建了一个 Google 登录。登录后我们可以看到令牌，如果用户没有登录，我们还会看到“no users”消息。

所以我们想针对不同的情况返回一个合适的页面。回到 **Auth.js** 。

![](img/20ac1c8a4dfd3be60d910c2a7bb3312d.png)

观看[视频系列](https://www.youtube.com/watch?v=Sdv3bw2rIuQ&list=PLC5vixW_4xSKqwpgaPEcLj7O3SvUNqC9L)和[源代码](https://www.udemy.com/course/complete-nextjs-firebase-firestore-course/?referralCode=50C342DE4DD73B4428F4)

首先，我们需要创建两个状态，一个是`currentUser`，另一个是`loading`。因为在一天结束的时候，我们需要输出`currentUser`的信息，所以整个 app 都可以得到。

```
const [currentUser, setCurrentUser] = useState(null)const [loading, setLoading] = useState(true)
```

如果没有用户，则将当前用户设置为 null，并将 loading 设置为 false。否则将当前用户设置为用户并停止加载。

对于渲染页面，如果 loading 为真，则返回`<Loading>`组件。如果最后没有用户，返回`<Login>`组件。

如果用户确实存在，则返回待办事项列表。

```
import { useEffect,createContext, useState } from "react";import { getAuth } from 'firebase/auth';import nookies from 'nookies';import Login from "./components/login";import Loading from "./components/Loading";const AuthContext = createContext({});export const AuthProvider = ({children})=>{const [currentUser, setCurrentUser] = useState(null)const [loading, setLoading] = useState(true)useEffect(() => {const auth = getAuth()return auth.onIdTokenChanged(async(user)=>{if (!user) {console.log('no user');nookies.set(undefined,"token","",{});**setCurrentUser(null);****setLoading(false);**return;}const token = await user.getIdToken();nookies.set(undefined,"token",token,{});**setCurrentUser(user);****setLoading(false);**console.log('token', token);console.log('user', user);})}, [])**if (loading) {****return (<Loading type="bubbles" color="yellowgreen"/>)****}****if(!currentUser) {****return <Login/>****}else{****return (****<AuthContext.Provider value={{currentUser}}>****{children}****</AuthContext.Provider>****)**}}export const useAuth = () =>useContext(AuthContext)
```

最后，记得在`AuthProvider`将`currentUser`对象作为一个值返回。从 React 导入`useContext`，然后导出 const useAuth。

```
import { useEffect,createContext, useState, useContext } from "react";export const useAuth = () =>useContext(AuthContext)
```

# 关注我们: [YouTube](https://www.youtube.com/channel/UCu4-4FnutvSHVo9WHvq80Ww?sub_confirmation=1) ， [Medium](https://ckmobile.medium.com/) ， [Udemy](https://www.udemy.com/user/cyruschan2/) ， [Linkedin](https://www.linkedin.com/company/ckmobi/) ， [Twitter](https://twitter.com/ckmobilejavasc1) ， [Instagram](https://www.instagram.com/ckmobile8050) ， [Gumroad](https://app.gumroad.com/ckmobile)

*更多内容请看*[***plain English . io***](http://plainenglish.io/)