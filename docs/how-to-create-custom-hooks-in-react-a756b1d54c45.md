# 如何在 React 中创建自定义挂钩

> 原文：<https://javascript.plainenglish.io/how-to-create-custom-hooks-in-react-a756b1d54c45?source=collection_archive---------15----------------------->

## 了解如何在 React 中创建第一个自定义钩子。

![](img/a43124cb8529eabc263010944c18eefc.png)

Image created with ❤️️ By author.

钩子在反应时非常有用。现在每个人都在使用它们，因为与使用类组件相比，它们有更简单的语法。

因此 React 附带了许多钩子，我们可以使用它们来轻松地为我们的组件创建功能。但是，您仍然可以选择创建自己的定制挂钩。

自定义钩子只是一个可重用的函数，它调用其他钩子来为组件创建特定的功能。因此，这是一种为组件创建功能的方式，并且能够在不同的地方使用它，而不必为该功能重复代码。您只需导入自定义挂钩，并在任何您想使用的地方使用它。

在本文中，我们将学习如何在 React 中创建我们的第一个自定义钩子。所以让我们开始吧。

# 没有自定义挂钩的示例

让我们来看一个简单的例子，在这个例子中，我们将从一个假的 API 获取数据，在页面上显示一个用户名列表。我们可以使用钩子`useState`、`useEffect`和 fetch API 来实现。

下面是一个例子:

```
//App.jsimport React,{useState, useEffect} from "react";const App = () => {
  const [users, setUsers] = useState([])**const getUsers = async ()=>{
    const response = await fetch(**"https://jsonplaceholder.typicode.com/users"**)
    const userdata = await response.json()
    setUsers(userdata)
  }** **useEffect(()=>{
    getUsers()
  },[])** return (
    <div className="container">
      <ul>
        {users.map(user => <li key={user.id}>**{user.name}**</li>)}
      </ul>
    </div>
  )
};export default App;
```

如您所见，这就是我们在 React 中获取数据的方式。但是如果我们想在不同的组件中获取数据呢？嗯，我们将需要复制和粘贴所有这些不同的组件上面相同的功能。这不是一个好的做法。

这就是定制挂钩发挥作用的原因。它们允许您轻松地将该功能调用到不同的组件中，而不必复制和粘贴所有内容。

所以对于上面的情况，我们需要创建一个自定义的钩子，允许我们获取数据。

# 创建自定义挂钩

为了创建我们的定制钩子，我们必须做的第一件事是创建一个新文件。我将称它为`useFtech.js`,因为它将是一个获取数据的钩子。

在该文件中，我们必须创建一个函数来放置功能。该函数将是自定义挂钩本身。还有，要记住函数的名字必须以`use`开头，否则就不行。所以我将调用这个函数`useFetch()`。

您还需要给函数一个参数。在我们的例子中，它将是`url`，因为我们将不得不从 API URL 获取数据。然后我们将不得不使用钩子`useState`和`useEffect`来添加抓取功能。

下面是一个例子:

```
//useFetch.jsimport {useState, useEffect} from 'react'//don't forget to give a url parameter for the function.
const **useFetch** = (url)=>{
  const [data, setData] = useState([]) const getData = async ()=>{
    const response = await fetch(url)
    const userdata = await response.json()
    setData(userdata)
  } useEffect(()=>{
    getData()
  },[url]) //return data that we will need in other components.
  **return {data};** }export default useFetch;
```

正如您所看到的，在创建了自定义钩子函数并在其中编写了抓取功能之后。您还需要在函数中返回获取的数据。因为 JavaScript 中的每个函数都需要返回一些东西，我们需要这些数据在其他组件中使用。

之后，我们只需导出自定义钩子函数，并将其导入另一个组件，这样我们就可以使用获取功能。

下面是一个在 App 组件中使用我们的定制钩子`useFetch`的例子:

```
//App.jsimport React from "react";
**import useFetch from './useFetch'**const App = () => {
  const API_URL = 'https://jsonplaceholder.typicode.com/users'; const {**data**} = **useFetch(**API_URL**)** return (
    <div className="container">
      <ul>
        {**data**.map(user => <li key={user.id}>{user.name}</li>)}
      </ul>
    </div>
  )
};export default App;
```

你所要做的就是导入自定义钩子，并像使用其他已有的钩子一样使用它。正如您在上面看到的，我们将 API URL 传递给钩子`useFetch`,因为它已经接受了一个 URL 参数。现在一切正常，我们的用户列表将会显示出来。

这就是如何创建一个获取数据的自定义钩子。您可以应用相同的方法来创建不同的定制挂钩。

# 结论

如您所见，创建定制挂钩并不困难。它们非常有用，可以让你不再重复。这也是一个让你的代码更整洁的好方法，因为你不必在不同的组件中重复相同的功能。

感谢您阅读这篇文章。希望你觉得有用。

**更多阅读**

[](/10-useful-javascript-coding-techniques-that-you-should-use-e8e7960e08ed) [## 您应该使用的 10 种有用的 JavaScript 编码技术

### 实现编程任务的有用 JavaScript 技术。

javascript.plainenglish.io](/10-useful-javascript-coding-techniques-that-you-should-use-e8e7960e08ed) [](/6-important-tips-to-write-clean-react-code-5ef29d6a73a6) [## 编写干净的 React 代码的 6 个重要技巧

### 作为 React 开发人员，编写干净代码的技巧。

javascript.plainenglish.io](/6-important-tips-to-write-clean-react-code-5ef29d6a73a6) 

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)