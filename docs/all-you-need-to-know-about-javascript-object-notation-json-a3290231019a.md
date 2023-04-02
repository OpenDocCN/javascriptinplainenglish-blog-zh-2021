# 关于 JavaScript 对象表示法(JSON ),您需要知道的是

> 原文：<https://javascript.plainenglish.io/all-you-need-to-know-about-javascript-object-notation-json-a3290231019a?source=collection_archive---------19----------------------->

## 了解关于 JSON 的一切

![](img/c552962103041b5db335c726396fafed.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JSON 是 JavaScript 对象符号的首字母缩写。它是最流行的数据表示和交换格式之一。

JSON 非常受欢迎，在某个时候，您可能已经听说过或使用过它。

JSON 令人难以置信的迷人之处在于它以一种更可读和更有效的方式表示数据。JSON 也是轻量级的，因此效率更高。

除此之外，许多工具都支持 JSON，包括大多数现代编程语言和技术。

## **JavaScript 对象符号(JSON)类型**

我们将看看 JSON 支持的一些数据类型。JSON 支持大多数数据表示类型，例如:

数字:— 70，29

数组:[ 'Hello '，' World '，' JavaScript']

对象:{'hello '，' world '，' key '，' value'}

布尔:对还是错

空:空

字符串 Unicode 字符串:“Hello World”

## **创建一个 JSON 文件**

JSON 文件在。json 文件，我们可以拥有 JSON 支持的所有数据表示类型，正如我们在上面看到的。

在里面。json 文件，我们可以有下面的 JSON 文件例子。

```
{
 “database”: { “host”: “localhost”, “port”: 3306, “user”: “root”, “password”: “12345”, “admin”: false
 }
}
```

## **JSON 语法规则**

JSON 实现了键和值对的使用。例如，对于包含的每个键，我们必须有一个表示该键的相关值。

使用 JSON 时，我们必须在双引号内包含密钥

## **JSON 的用例**

JSON 已经被其他编程语言广泛采用，尽管它听起来好像只适用于 JavaScript。

## **传输数据**

JSON 可以用来在系统之间传输数据。一个明显的例子是，当您想让一个用户使用 Google 的 API 服务登录您的应用程序时。首先，您将看到 JSON 格式的用户信息。类似地，您也可以使用 JSON 格式将用户信息发送给 Google 进行验证。

## **配置文件**

JSON 主要用于存储库和框架的配置文件。大多数常见的框架和库都实现了 JSON 在存储配置文件中的使用。

## **存储数据/信息**

JSON 以数组和对象的形式表示数据，可以用来存储各种类型的数据。例如，我们可以用它存储一些信息，如下所示。

```
{“name”: “John Philip”,“age”: 21,“email”: “[johnphilip@test.com](mailto:johnphilip@test.com)”, “street”: “2 broadway” “city”: “New York” “zip”: 11029 “state”: NY}
```

谢谢你到目前为止阅读这个故事，我希望你发现它有帮助。如果你有问题，我很乐意在评论区听到。

## **更多阅读:**

[](/the-fascinating-story-behind-the-birth-of-vue-js-a-documentary-97d353688c2) [## Vue.js 诞生背后的迷人故事

### 揭开创建 Vue.js 框架背后的故事。

javascript.plainenglish.io](/the-fascinating-story-behind-the-birth-of-vue-js-a-documentary-97d353688c2) [](/vue-js-best-practices-you-should-adopt-3f3b3a8abace) [## Vue.js 您应该采用的最佳实践

### 使用 Vue.js 时的最佳实践

javascript.plainenglish.io](/vue-js-best-practices-you-should-adopt-3f3b3a8abace) 

*更多内容看*[***plain English . io***](http://plainenglish.io/)