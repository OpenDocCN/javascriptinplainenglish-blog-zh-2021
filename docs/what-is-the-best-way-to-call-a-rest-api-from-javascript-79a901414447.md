# 从 JavaScript 调用 REST API 的最佳方式是什么？

> 原文：<https://javascript.plainenglish.io/what-is-the-best-way-to-call-a-rest-api-from-javascript-79a901414447?source=collection_archive---------5----------------------->

![](img/aa2dcff32e08cd55d68a080480e52f3f.png)

您有没有想过进行 JavaScript REST API 调用的最佳且干净的方式是什么？在一个大项目中，你会做上百个这样的东西？

在我的项目中，这个问题问得太晚了，因为已经写了很多代码。最好早点知道选择哪种方法，这样你以后就不会那么头疼了。

您可能知道，从 JavaScript 调用 API 有很多选项。其中有 **XMLHttpRequest** 、 **jQuery** 、 **fetch** 等等一个。我将在这里讨论 **fetch** 方法，因为它在我们的代码中看起来更干净。

使用**获取**非常简单。http 请求通常如下所示:

```
fetch(‘[https://jsonplaceholder.typicode.com/todos/1](https://jsonplaceholder.typicode.com/todos/1)’)
  .then(response => response.json())
  .then(json => console.log(json));
```

如您所见，发出 get 请求非常简单。但是当我们想要发出一个 **post** 请求时会发生什么呢？让我们看看:

```
fetch(‘[https://jsonplaceholder.typicode.com/todos/1](https://jsonplaceholder.typicode.com/todos/1)’,
    {method: “POST”, body: JSON.stringify(data)})
  .then(response => response.json())
  .then(json => console.log(json));
```

事情已经开始变得相当糟糕了。类似的，**放**和**删除**的方法看起来也会一样。

好吧，我们需要做点什么。首先，让我们假设我的基础 rest api url 类似于[*https://my-URL/v1/*](https://my-url/v1/)，如果我想从服务器获取所有用户，我必须调用[*https://my-URL/v1*](https://my-url/v1/)*/users*。如你所见，我在代码中会一直使用[*https://my-URL/v1/*](https://my-url/v1/)。所以，如果我必须发出数百个请求，我的代码就会被这个字符串污染。

此外，如果将来我要对我的应用程序进行升级，并且我也需要将我的 rest 基本 url 从 *v1* 升级到 *v2* 会发生什么？我将不得不在应用程序中到处搜索并替换那些字符串。

## **第一选项**

我的第一个选择是创建一个 *main.js* ，我将在每个*中导入它。在这个文件中，我将声明我的基本 url 字符串。让我们看看它会是什么样子:*

*main.js*

```
const baseUrl = ‘[*https://my-url/v1/*](https://my-url/v1/)’;
```

*users.js*

```
fetch(baseUrl + ‘users’)
  .then(response => response.json())
  .then(json => console.log(json));
```

它现在看起来更好，但我仍然会重复代码，并会有*。然后(…)* 和 *baseUrl* 常量在我的项目中随处可见。所以，我想做一些更普通的事情。另外，如果我想在我的请求中添加一些身份验证头，会发生什么呢？代码将如下所示:

```
const baseUrl = ‘[*https://my-url/v1/*](https://my-url/v1/)’;const authHeaders = {Authorization: ‘Bearer ‘ +
  $.cookie(‘jwtToken’), ‘Content-Type’: ‘application/json’};fetch(baseUrl + ‘users’, {method:’GET’, headers: authHeaders)
  .then(response => response.json())
  .then(json => console.log(json));
```

如你所见，当我需要更多的选项时，代码会很快变得令人讨厌。

## **最佳选项**

对我来说最好的选择是下面这个。在我的 *main.js* 文件中，我将为 **put、post、get** 和 **delete** 定义四个方法，并在我的代码中的任何地方将它们直接用于*窗口*对象。因此，在我的 *main.js* 文件中，我会有以下内容:

```
const urlLocation =’[*https://my-url/v1/*](https://my-url/v1/)’;const authHeaders = {Authorization: ‘Bearer ‘ +
  $.cookie(‘jwtToken’), ‘Content-Type’: ‘application/json’};window.postJson = function (url, data) {
  return fetch(urlLocation + url, {method: “POST”, headers:
    authHeaders, body: JSON.stringify(data)}).then((res) => res.json());}window.getJson = function (url) { 
  return fetch(urlLocation + url, {method: “GET”, headers: authHeaders})
    .then((res) => res.json()); 
  }window.deleteJson = function (url) { 
  return fetch(urlLocation + url, {method: “DELETE”, headers: authHeaders})
    .then((res) => res.json()); 
  }window.putJson = function (url) { 
  return fetch(urlLocation + url, {method: “PUT”, headers: authHeaders})
    .then((res) => res.json()); 
  }
```

在我的项目中，如果我需要发出一个 get 调用来获得所有用户，我所要做的就是:

```
const alUsers = await getJson(allUsers+'users').then( (res) => { return res; } );
```

正如您所看到的，这是一种更干净、更易于维护的 rest api 调用方式。现在，我把所有的逻辑都放在一个地方，我可以很容易地改变我的基本 url 位置或者添加/删除标题。

**PS:** 如果你曾经需要一个运行时间监控工具，只需检查 [RoboMiri](https://robomiri.com) 。最好的免费正常运行时间监测服务。