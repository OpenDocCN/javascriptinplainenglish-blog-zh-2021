# 用途:使用 Axios 的反作用挂钩

> 原文：<https://javascript.plainenglish.io/useaxios-a-react-hook-for-using-axios-c798762d1a13?source=collection_archive---------2----------------------->

## 如何为使用 Axios 创建自定义钩子

![](img/5ce2eca6da43e36f989900e857adaee9.png)

在几乎每个前端应用程序中，我们都进行 API 调用。发出 HTTP 请求的两种最流行的方法是使用 Fetch API 或 Axios 库。如果您没有看过我对 [Axios 和](/stop-using-the-fetch-api-in-javascript-f3ac14aca026?source=friends_link&sk=2316643e6f6abca6308832c7beece8ae)Fetch 的比较，请一定要看看。

在本文中，我将解释如何在 reactor 中为 Axios 编写一个自定义钩子。通过遵循这个方法，我们可以避免代码在多个地方重复。以下是实现它的步骤。

# 1.在组件中进行 API 调用

通常，应用程序的所有 API 都有相同的基本 URL。在这里，我们为 Axios 设置一个基本的网址，这样我们就可以重用它们了。如果你使用一个以上的基本 URL，Axios 通过创建实例来支持它。

首先，让我们在应用程序中安装`axios`包，然后暂时将它们导入我们的`App.js`文件中，直到我们将它们移动到另一个文件中。

在上面的代码片段中，我创建了一个方法`fetchData()`，它使用 Axios 发出 GET 请求。请注意，我在这里使用了`axios.default.baseURL`，因为我的应用程序只需要指向一个端点。如果需要使用多个端点，可以创建不同的实例。

# 2.添加状态变量来保存数据、错误和加载状态

现在让我们保存响应数据，错误并通过使用`useState()`钩子检查它是否加载。渲染时，我只是临时添加了代码，以便渲染内容。

# 3.将逻辑移到一个单独的文件中，创建一个自定义的反作用钩子

既然我们知道它在工作，那么让我们把获取逻辑移到一个单独的文件**usexios . js**中，并创建一个自定义的 React hook。

现在你的`App.js`文件可以这样重构了。

# 4.让钩子充满活力

到目前为止，我们只使用它来获取帖子，让我们通过将选项传递给钩子来使它更具动态性，这样它就可以根据我们的要求发出请求。为此，让我们将请求参数传递给钩子，并在钩子内使用`axios.request(params)`。

现在，因为我们只得到一个对象作为响应，让我们调整`App.js`文件。

这是这个应用程序的最终工作版本。

# 结论

我希望创建这个自定义挂钩非常容易。如果您愿意，还可以在此基础上添加定制。您还可以创建 Axios 的自定义实例，如果您有一个用例来访问不同的端点，就可以使用它们。这里可以引用，创建多个实例。我希望这篇文章对你有所帮助。感谢阅读！

## 参考

[](https://github.com/axios/axios) [## axios/axios

### 基于 Promise 的浏览器和 node . js HTTP 客户端新的 axios docs 网站:单击此处从…

github.com](https://github.com/axios/axios) [](/stop-using-the-fetch-api-in-javascript-f3ac14aca026) [## 停止在 JavaScript 中使用 Fetch API

### 这就是 Axios 更好的原因

javascript.plainenglish.io](/stop-using-the-fetch-api-in-javascript-f3ac14aca026) 

*更多内容尽在*[***plain English . io***](http://plainenglish.io)