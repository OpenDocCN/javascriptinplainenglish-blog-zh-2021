# 新手反应问题，以帮助你在面试中

> 原文：<https://javascript.plainenglish.io/beginner-react-questions-to-help-you-during-interviews-a5d6c56dc691?source=collection_archive---------13----------------------->

## 作为初级开发人员应该知道的有用的 React 问题。

![](img/724b794fbac5eaea15cfaaabae89e241.png)

Image created With ❤ ️️by the author.

如果你想找一份开发人员的工作，面试准备是非常重要的。准备会让你更有信心通过面试，得到你想要的工作。

如果你在寻找一个初级 React 开发人员的职位，总会有一些他们在面试时可能会问的常见技术问题。

这就是为什么在这篇文章中，我将回答一些作为初学者需要知道的常见 React 问题。所以让我们开始吧。

# 1.什么是反应？

React 是一个开源的 JavaScript 库，允许我们构建用户界面。这是一个基于组件的库，使得创建 web 应用程序更加容易。

React 于 2013 年由一名脸书软件工程师发布。该库拥有前端框架的所有功能。React 中有许多开源工具和软件包，可以让开发变得更容易、更高效。这也是 React 在开发者社区中人气不断增长的原因。

# 2.什么是 JSX？

JSX 是一种语法扩展，允许你用 JavaScript 轻松编写 HTML 代码。这是一种使代码更具可读性并在 HTML 中轻松使用 JavaScript 逻辑的方法。

JSX 类似于 HTML，但也有一些不同，尤其是在编写属性时。另外，记住 JSX 不是有效的 JavaScript，这就是为什么我们把它编译成 JavaScript。

```
*//JSX syntax.*<div>
  <h2 **className**="heading">This is a heading.</h2>
  <p>This is a paragraph;</p>
</div>
```

# 3.React 中的组件是什么？

组件只是 UI 的一部分，可能具有某些功能。React 中的组件以数据为道具，返回 JSX。组件的伟大之处在于，它们允许您分离代码，并在应用程序的不同部分重用它。

React 中有两种类型的组件:

*   类组件:我们使用 ES6 类语法创建它们。它们是有状态的，这意味着它们保存数据的状态。
*   功能组件:它们易于编写和管理。他们拿着道具争论，并返回 JSX。功能组件是无状态的，这意味着它们不持有状态。然而，有了 React 钩子，现在我们能够在功能组件中使用状态。

# 4.如何在 React 中创建组件？

说到功能组件，就很简单了。创建一个函数，将 props 对象作为参数传递，并从函数中返回 JSX。

这里有一个例子:

```
function Modal({text}) {
  return <h1>{text}</h1>;
}
```

我们可以使用一个类组件创建一个相同的组件:

```
class Modal extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      text: 'Modal text'
    }
  } render() {
    return <h1>{props.text}</h1>;
  }
}
```

此外，确保组件名称的第一个字母大写。如您所见，在 React 中有两种创建组件的方法。功能组件语法简单，可读性更强。除此之外，React 钩子允许我们在功能组件中使用状态。

# 5.如何在 React 中添加样式？

React 中有许多应用样式的方法:

*   你可以在 JSX 使用属性`style`:

要对 React 中的元素应用样式，可以使用属性`style`，该属性接受包含样式的对象。此外，请记住 CSS 属性必须是驼峰式的。

这里有一个例子:

```
function Modal({text}) { const headingStyle = {
   color: 'blue',
   backgroundColor: 'gray'
  }; return <h1 **style**={**headingStyle**}>{text}</h1>;
}
```

*   您可以将 CSS 文件导入到您的应用程序中以应用这些样式。
*   您也可以使用样式库，如样式组件、材质 UI 或任何其他 React 样式库。

# 6.如何创建一个简单的自定义钩子？

自定义挂钩只是一个允许您在项目的不同位置使用功能的函数。它允许您为组件创建特定的功能，并在应用程序中的任何地方使用它，而不必再次从头编写代码。

假设您想要创建一个自定义挂钩，允许您从 API 获取数据。为此，我们创建一个新文件，并在其中创建一个以`use`开头的函数(这是必须的)。在我们的例子中，因为我们想要获取数据，我们将称它为`useFetch()`。

该函数应该有一个参数，它是我们要从中获取数据的 URL。因此，它应该返回该 API 的数据。

下面是一个例子:

```
*//useFetch.js* import {useState, useEffect} from 'react'//give a url parameter for the function.
const **useFetch** = (**url**)=>{  
  const [data, setData] = useState([]) const getData = async ()=>{
    const response = await fetch(**url**)
    const userdata = await response.json()
    setData(userdata)
  }

 useEffect(()=>{
    getData()
  },[url])

  //return data that we will need in other components.
  **return {data};**
}export default useFetch;
```

现在我们只需要将这个定制钩子导入到其他组件中，并在那里使用它。

因为我们的定制钩子`useFetch`接受一个 URL 参数，所以当我们想要在应用程序的其他组件中获取数据时，我们可以将 API URL 传递给它。

这里有一个例子:

```
//App.js
import React from "react";//importing our custom hook that we created.
**import useFetch from './useFetch'**const App = () => {
  const API_URL = 'https://jsonplaceholder.typicode.com/users';

  //using our custom hook.
  const **{data} = useFetch(API_URL)**

  return (
    <div className="container">
      <ul>
        {data.map(user => <li key={user.id}>{user.name}</li>)}
      </ul>
    </div>
  )
};
export default App;
```

# 结论

如你所见，这些是每个初学者都应该知道的非常简单的问题。我们将在接下来的文章中尝试回答更多中级甚至高级的 React 问题。

感谢您阅读这篇文章。希望你觉得有用。

**更多阅读:**

[](/5-exciting-reactjs-projects-for-all-junior-frontend-developers-eb7f28098ab4) [## 所有初级开发人员都应该构建的 5 个 React 项目

### 作为一名前端开发人员，您应该构建令人敬畏的 React 项目。

javascript.plainenglish.io](/5-exciting-reactjs-projects-for-all-junior-frontend-developers-eb7f28098ab4) [](/7-awesome-apis-for-all-frontend-developers-a06c1057661) [## 面向所有前端开发人员的 7 款出色的 API

### 您的下一个项目可能需要的有用的 API。

javascript.plainenglish.io](/7-awesome-apis-for-all-frontend-developers-a06c1057661) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)