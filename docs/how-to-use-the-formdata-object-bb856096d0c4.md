# 如何使用 FormData 对象

> 原文：<https://javascript.plainenglish.io/how-to-use-the-formdata-object-bb856096d0c4?source=collection_archive---------4----------------------->

## 解释什么是 FormData 对象以及如何在现有的 HTML 表单中使用它。

![](img/080cc24d095db3e82a174f92d8ece3f8.png)

Photo by [Christopher Gower](https://unsplash.com/@cgower?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 什么是 FormData 对象？

要理解什么是 FormData 对象，我们首先应该知道它们来自哪里。表单数据对象是从[表单数据](https://developer.mozilla.org/en-US/docs/Web/API/FormData)接口构建的。这个 FormData 接口让我们能够用 [FormData 构造函数](https://developer.mozilla.org/en-US/docs/Web/API/FormData/FormData)创建键、值对，来表示我们表单的字段和值。

# 在 JavaScript 中使用 FormData

为了演示如何用 Javascript 实现 FormData 对象，我们将在示例中使用这个表单。

![](img/82ab06868eae61d998d94b7ede950f22.png)

让我们看看这个新闻稿表单的 HTML 是什么样子的。

这里需要注意的一点是，我们已经包含了 [name](https://www.w3schools.com/tags/att_name.asp) 属性。不要忘记这一点，因为只有包含 name 属性的输入字段才能使用 FormData 对象。

现在我们已经看到了表单是如何设置的，让我们来看看 javascript 文件并编写代码。

在这里，您可以看到我们是如何第一次听到表单被提交的。一旦提交事件被触发，我们就创建一个 FormData 对象的新实例，传递从 DOM 中获取的表单元素。这将表单中的所有内容与 name 属性捆绑在一起，使我们能够访问提交的输入数据。

创建 FormData 对象后，我们使用`[.get()](https://developer.mozilla.org/en-US/docs/Web/API/FormData/get)`方法从输入中获取值(确保从输入中传递 name 属性值，而不是类名或 id)。在这一步之后，如果这是一个真实的应用程序，我们很可能会用一个获取请求将表单数据发送到某个服务器。出于演示的目的，我们将保持简单，并向用户呈现一条消息，让他们知道他们已经注册了。

既然我们已经设置好了一切，那就让我们试一试我们的时事通讯表格吧。

![](img/74c6cf65eb249a293189a9f3bfb96d5f.png)

现在，如果我们单击“注册”,我们所有的表单数据都将被提交，我们应该会得到一个弹出消息，让我们知道我们已经注册了。

![](img/9c51a16835436d7e389b5eaee845ffbe.png)

# 结论

FormData 对象是处理 HTML 表单的一个很好的工具。它们允许您轻松地访问表单中的所有内容，而不必逐个获取和存储每个元素或输入值。

只需从 FormData 构造函数中创建一个新对象，传递给表单元素，并利用提供的 [FormData 方法](https://developer.mozilla.org/en-US/docs/Web/API/FormData)。

*更多内容看*[***plain English . io***](http://plainenglish.io)