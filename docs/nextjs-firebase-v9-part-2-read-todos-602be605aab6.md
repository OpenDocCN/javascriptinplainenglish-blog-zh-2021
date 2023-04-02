# Next.js Firebase v9:阅读 ToDos

> 原文：<https://javascript.plainenglish.io/nextjs-firebase-v9-part-2-read-todos-602be605aab6?source=collection_archive---------6----------------------->

## 第 2 部分:导入 onSnapshot、orderBy、collection 和 query 函数。

在本文中，我们将使用 Firebase Firestore 中的 onSnapshot、orderBy、collection 和 query 函数来读取文档。

![](img/31d044bf9e8fa72a153d135d2ab09e6b.png)

[视频教程](https://youtu.be/A-Ce4YyHMGk)和[源代码](https://www.udemy.com/course/complete-nextjs-firebase-firestore-course/?couponCode=FREESOURCE)

转到配置文件 **firebase.js** ，导入 getFirestore，并创建 db。最后，我们导出数据库。

```
// Import the functions you need from the SDKs you needimport { initializeApp } from "firebase/app";**import { getFirestore } from "firebase/firestore";**const firebaseConfig = {apiKey: "AIzaSyCCKSzdjGpZUj9Gf2sEa2kCR_gAgrELUb0",authDomain: "nextjs-firebase-61239.firebaseapp.com",projectId: "nextjs-firebase-61239",storageBucket: "nextjs-firebase-61239.appspot.com",messagingSenderId: "122363745629",appId: "1:122363745629:web:02de623d92474cd594c4b4"};// Initialize Firebaseconst app = initializeApp(firebaseConfig);**const db = getFirestore()****export {db}**
```

现在我们转到根文件夹，创建“components”文件夹。在这个文件夹下，创建 **TodoList.js** 。

![](img/b5df8a7ea2a5c7d008bf8a18444eab9e.png)

我们添加 useEffect 来获取按时间戳排序的 ToDos 集合。使用 onSnapshot 功能收听 Firestore 中的变化。我们还将文档 id 添加到 ToDo 对象中，并且我们还需要对时间戳对象进行转换。

为了让 JavaScript 理解 Firestore 时间戳，我们需要使用`doc.data().timestamp?.toDate().getTime()`。我们加上“？”以防还没有添加时间戳。

```
import { db } from "../firebase";import { onSnapshot, collection, orderBy, query } from "firebase/firestore";import { useEffect, useState } from "react";const TodoList = () => {const [todos, setTodos] = useState([])useEffect(() => {const collectionRef = collection(db, "todos")const q = query(collectionRef, orderBy("timestamp", "desc"));const unsubscribe = onSnapshot(q, (querySnapshot) => {setTodos(querySnapshot.docs.map(doc => ({ ...doc.data(), id: doc.id, timestamp: doc.data().timestamp?.toDate().getTime() })))});return unsubscribe;}, [])return (<div>{todos.map(todo => <p key={todo.id}>{todo.title}</p>)}</div>)}export default TodoList
```

## 呈现待办事项列表

为了呈现 ToDo 列表，我们需要将 ToDo list 组件导入到 **index.js** 中。

```
import { Container } from '@mui/material'import TodoList from '../components/TodoList'export default function Home() {return (<Container><TodoList /></Container>)}
```

![](img/0a5586ce2313444e29caa792bed471cd.png)

the todos are rendered inside the web

# 关注我们: [YouTube](https://www.youtube.com/channel/UCu4-4FnutvSHVo9WHvq80Ww?sub_confirmation=1) ， [Medium](https://ckmobile.medium.com/) ， [Udemy](https://www.udemy.com/user/cyruschan2/) ， [Linkedin](https://www.linkedin.com/company/ckmobi/) ， [Twitter](https://twitter.com/ckmobilejavasc1) ， [Instagram](https://www.instagram.com/ckmobile8050) ， [Gumroad](https://app.gumroad.com/ckmobile)

*更多内容请看*[***plain English . io***](http://plainenglish.io/)