# 如何在 JavaScript 中使用第三方 API

> 原文：<https://javascript.plainenglish.io/how-to-call-and-use-third-party-apis-in-vanilla-javascript-with-a-full-example-da44b095da03?source=collection_archive---------2----------------------->

![](img/cfa7be49d4b63c24bbf7cc39a14c1a01.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

作为一名新的开发人员，寻找工作意味着通读一份需求清单，我注意到了常见的技能组合。第三方 API/REST 的使用似乎很流行，所以知道如何调用 API 和使用它的数据很重要。

***TL；dr***

## **什么是第三方 API？**

*“第三方 API 是由第三方提供的 API，通常是脸书、Twitter 或谷歌等公司，允许您通过 JavaScript 访问它们的功能并在您的网站上使用”——MDN*

从 API 调用数据的方法有很多，但我们只探讨最常见的几种:

我们将在示例中使用 JSONPlaceholder。

# 方法一。取得

```
**ES5**
var getData = fetch('https://jsonplaceholder.typicode.com/posts')
  .then(function(response) {
    return response.json();
  });
  .then(function(jsonObject) {
    return console.log(jsonObject);
  });**OR****ES6**
const getData = fetch('https://jsonplaceholder.typicode.com/posts')
  .then(response => response.json)
  .then(jsonObject => console.log(jsonObject))**Then call the function to view the data in the console**
getData()
```

# 方法二。Axios

请记住，axios 不像 fetch 那样内置在浏览器中，所以我们必须导入它。

```
**ES5** const getData = axios.get('https://jsonplaceholder.typicode.com/posts')
  .then(function(response) {
    console.log(response.data);
});**ES6** const getData = axios.get('https://jsonplaceholder.typicode.com/posts')
  .then(response => console.log(response.data));**Then call the function to view the data in the console**
getData()
```

## 用例示例

让我们来看一个数据的示例。将 URL 放入您的浏览器:`[https://jsonplaceholder.typicode.com/posts](https://jsonplaceholder.typicode.com/posts.)`

您应该得到这样的结果:

```
[
  {
    "userId": 1,
    "id": 1,
    "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
    "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
  },
  {
    "userId": 1,
    "id": 2,
    "title": "qui est esse",
    "body": "est rerum tempore vitae\nsequi sint nihil reprehenderit dolor beatae ea dolores neque\nfugiat blanditiis voluptate porro vel nihil molestiae ut reiciendis\nqui aperiam non debitis possimus qui neque nisi nulla"
  },
  {
    "userId": 1,
    "id": 3,
    "title": "ea molestias quasi exercitationem repellat qui ipsa sit aut",
    "body": "et iusto sed quo iure\nvoluptatem occaecati omnis eligendi aut ad\nvoluptatem doloribus vel accusantium quis pariatur\nmolestiae porro eius odio et labore et velit aut"
  },
....
]
```

让我们为 API 请求创建一个`service.js`文件:

```
const fetchPosts = axios.get('https://jsonplaceholder.typicode.com/posts')
  .then(response => console.log(response.data))
  .catch(error => console.error(error));fetchPosts();
```

让我们创建一个`index.html`文件

```
<!DOCTYPE html>
<html lang="en">
  <head>
  <meta charset="UTF-8">
    <title>Calling data from an API</title>
  </head>
  <body>
    <div>
      <h1></h1>
      <p></p>
   </div> <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
  <script src="script.js"></script>
  </body>
</html>
```

现在让我们更新我们的`fetchPosts`请求，映射我们在`script.js`文件中得到的数据。

```
const postTitle = document.querySelector('h1');
const postBody = document.querySelector('p');const fetchPosts = axios.get('https://jsonplaceholder.typicode.com/posts')
  .then(response => {
    const data = response.data;
    data.map(d => {
      postTitle.innerHTML(response.data.title)
      postBody.innerHTML(response.data.body)
    })}
    .catch(error => console.error(error));fetchPosts();
```

应该就是这样了。它缺乏风格，但它的作品！

# 结论

感谢阅读。我希望它有帮助。如果是的话，请在评论中告诉我。