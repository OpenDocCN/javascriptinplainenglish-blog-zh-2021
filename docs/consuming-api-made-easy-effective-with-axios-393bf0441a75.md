# 使用 Axios 消费 API

> 原文：<https://javascript.plainenglish.io/consuming-api-made-easy-effective-with-axios-393bf0441a75?source=collection_archive---------10----------------------->

![](img/0c135ea9ce7ccd8d34f111fc343735fa.png)

Photo by [Thomas Tastet](https://unsplash.com/@thomast_404?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

随着项目的增长，在使用 API 的过程中做所有手工重复的事情变得非常麻烦，比如给请求添加一个令牌，从响应中显示通知，从响应中处理错误等等……
此外，如果你想在流程中做一些改变，更新每个 API 对整个团队来说都是一场噩梦。让我们从一个例子开始:

```
// api-call.jstry {
  const res = await axios.post('http://myserver.com/post', {
    headers: {
      authorization: 'my secret token'
    }
  });
  const { success, data, message } = res.data;
  successNotification(message);

  doSomethingWithData(data);} catch (error) {
  errorNotification(error.response.data.message);
  doSomethingWithError(error);
}
```

对于您使用的每一个 API，我们都需要以这种方式编写大量重复的代码。现在，让我们看看更好的解决方案:

为此，首先我们需要收集我们想要处理的问题，举几个例子:
1:在请求头中自动嵌入令牌
2:处理来自响应的错误
3:来自响应的通知
4:使这一切易于管理

axios 中有一个特性，`interceptors`，我们可以使用它在 API 调用的基础上增加一层，处理所有提到的东西，我们只需要关注更重要的东西。这充当了所有使用的 API 的接口。
举例:

```
// api-interface.jsconst instance = axios.create({
headers: {
  Accept: 'application/json',
  'Content-Type': 'application/json',
  'Access-Control-Allow-Origin': '*',
  },
});instance.interceptors.request.use((*config*) => {
  // invoked before every API call config.headers.Authorization = 'my secret token';
  return config;}, (*error*) => {
  // invoked if error occurs in API call    return Promise.reject(error);
});instance.interceptors.response.use((*response*) => {
  // invoked after successful API response

  successNotification(response.data.message);
  return response.data;
}, (*error*) => {
  // invoked after error in API response errorNotification(error.response.data.message);
  doSomethingWithError(error); 
  return Promise.reject(error.response.data);
});export default instance;
```

在上面的代码片段中，我们用 **axios 拦截器**制作了一个`api-interface`，可以很容易地使用它来消费 API，它将通过定义的重复流程。这是 API 现在的样子:

```
// api-call.js
import api from 'api-interface';try {
  const res = await api.post('http://myserver.com/post');
  const { data } = res.data;

  doSomethingWithData(data);
} catch (error) {
  doSomethingWithError(error);
}
```

看，现在使用一个 API 是多么简单，使用这个接口就可以处理所有的任务，并把 API 的最终结果返回给我们。

这是我的完整文件的链接。你也可以检查回购，它的设计保持生产力，规模铭记。

 [## dhruv479/react-redux

### 在 GitHub 上创建一个帐户，为 dhruv479/react-redux 开发做贡献。

github.com](https://github.com/dhruv479/react-redux/blob/master/src/services/api.interface.js) 

*我希望你喜欢这篇文章，并发现它很有价值。可以关注我上* [*中*](https://dhruv479.medium.com) *和* [*推特*](https://twitter.com/dhruv479) *。感谢支持！*

*更多内容请看*[***plain English . io***](https://plainenglish.io/)