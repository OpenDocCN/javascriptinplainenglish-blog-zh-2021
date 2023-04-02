# 学习使用 React Query 进行服务器状态数据管理

> 原文：<https://javascript.plainenglish.io/learn-to-use-react-query-for-server-state-data-management-abb4acf0694e?source=collection_archive---------12----------------------->

## React 的下一件大事。

![](img/da153db43f7ebf813faaa65edc849b6d.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

使用预配置的 React 查询库恢复您对服务器状态数据同步的信心。看看如何使用本教程中介绍的简单自动化挂钩将获取、缓存和更新逻辑变成几行容易理解的代码。

# 为什么它是下一个大事件？

![](img/cf6b56df1dec7ffb17c3dce52a0aab57.png)

Photo by [Karsten Winegeart](https://unsplash.com/@karsten116?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

这是 React 缺少的部分，有助于服务器状态数据管理。忘记把一切都保持在一个标准的全局状态，因为大多数库只是为了处理客户机状态而创建的，而服务器状态是完全不同的。

服务器数据是异步的。由于它没有存储在你的应用程序中，它可能会在一瞬间过时。所以你应该想出一个建立缓存的方法。坏消息是，这是编程中最难的事情之一。但是好消息是 React Query 可以处理您的获取、缓存、同步和更新服务器状态。

# 为什么用 React Query 开始一个项目很酷？

一行程序时间——它将把你的应用程序带到一个新的水平。但是真的，考虑下面的例子。

# React 查询的主要优势

![](img/42f47a210a6ff0586359e7be14ad02d8.png)

Photo by [Matt Artz](https://unsplash.com/@mattartz?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

*   窗口焦点重新提取——当用户离开你的应用选项卡时，React Query 会将数据标记为“陈旧”,并在用户返回时重新提取。
*   请求重试-您可以为任何请求设置重试次数，以防止随机错误。
*   预取-如果您的应用程序在更新请求后需要新数据，您可以使用特定的键预取查询，React Query 将在后台更新它。
*   乐观更新——当您编辑或删除列表中的项目时，您可以发布列表的乐观更新。

# 启动 React 查询引擎

![](img/5f491a70ca6783534169689df7f95b9f.png)

Photo by [Kaspars Eglitis](https://unsplash.com/@kasparseglitis?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

下面是基本配置。

```
import { QueryClient, QueryClientProvider } from 'react-query' const queryClient = new QueryClient() <QueryClientProvider client={queryClient}>  <App /></QueryClientProvider>
```

假设我们有一个基本的`axios`函数，它为我们的文章返回数据。

```
async function createFetchArticles() {  
 const { data } = await axios.get('/api/articles')  
 return data
}import React from 'react'
import { useQuery } from 'react-query' 
export const Articles = () => {  
const { data, error, isError, isLoading } = useQuery(['articles'], createFetchArticles)   
if (isLoading) {    
 return <span>Loading...</span>  
}   
if (isError) {    
 return <span>Error: {error.message}</span>  
}   
return (    <ul>      {data.map(article => (        <li key={article.id}>{article.title}</li>      ))}    </ul>  )
}
```

# 抓取现在更好了

为什么它比使用`useEffect`模式的普通抓取要好？当您使用带有相同的`projects`键的查询时，React Query 首先返回以前获取的数据，然后再次获取它。

当第二个数据集与第一个数据集相同时，React Query 将两个数据集都作为引用，而不强制重载。这是 UX 工作的巨大进步。

# 更新挂钩如何工作

因此您知道如何更容易地获取数据。我们来看看怎么更新吧。

```
async function createPostArticle(id) {  
await axios.post(`/api/article/${id}`)
} 
export const AddArticle = () => {  
const [title, setTitle] = React.useState('')  
const {isLoading, isError, error, mutate} = useMutation(createPostArticle)   
return (    <div>      <input        value={title}        onChange={(e) => setTitle(e.target.value)}        disabled={isLoading}      />      <button        onClick={() => {          mutate({ title })        }}        disabled={isLoading || !title}      >        Add Article      </button>      <div>        {isLoading          ? "Saving..."          : isError          ? error.message          : "Saved!"}      </div>    </div>  )
}
```

React Query 有一个`useMutation`钩子，可以用来更新/创建/删除数据。`useMutation`让你可以访问 mutate 函数，我们可以向它传递必要的参数。然后，它返回关于 API 调用状态的信息。状态可以是:

*   `idle`为空闲或刷新/复位状态
*   `loading`对于当前正在运行的突变
*   `error`当我们遇到一个
*   当一切正常且我们的数据可用时

您可以从 status 变量中访问状态信息，或者对于那些喜欢布尔状态的人来说，可以通过以下变量访问它们。

*   `isIdle`
*   `isLoading`
*   `isError`
*   `isSuccess`

如你所见，超级好用。由于有更多的选项可以传递给`useMutation`，React Query 可以成为您最强大的开发工具之一。

# 这才是真正的力量

当设备在发送数据时离线一会儿会发生什么？React Query 有一个解决方案！

![](img/c6547c341cd7befdc49d4655a405d4ba.png)

Photo by [Courtnie Tosana](https://unsplash.com/@courtniebt13?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 使用请求重试

您可以通过`retry`选项传递重新连接后查询应该重试变异的次数。

```
const mutation = useMutation(addArticle, { retry: 3 })
```

# 摘要

React Query 确实帮助我们解决了异步数据处理的问题。生活曾经更艰难。开发人员需要一堆其他库，他们最终会将服务器数据放入一个全局存储中。不是个好主意。为什么？正如我前面提到的，将异步服务器数据保存在全局存储中给我们的代码增加了不必要的复杂性。

还有更多。该查询还有助于减少样板代码的数量(比如将每次提取保存在`useEffect`钩子中)。如果使用得当，它会改善用户体验，但也会破坏用户体验。所以要小心，先试着去了解这个库。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)