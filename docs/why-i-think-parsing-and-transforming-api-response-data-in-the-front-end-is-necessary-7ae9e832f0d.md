# 为什么我认为在前端解析和转换 API 响应数据是必要的

> 原文：<https://javascript.plainenglish.io/why-i-think-parsing-and-transforming-api-response-data-in-the-front-end-is-necessary-7ae9e832f0d?source=collection_archive---------2----------------------->

所以，你有一个 API，你想在前端使用它。您如何处理响应数据？我们可以在`fetch`之后加上`JSON.parse`吗？

我见过许多前端项目只是直接使用 API 返回的任何内容，而没有进一步处理，我会说这并不理想——在我看来，解析和转换 API 响应数据是必要的，我将解释为什么。

# 主要原因:运行时类型安全

让我们从我从别处偷来的一句话开始:

> “东西会碎”——丹·阿布拉莫夫

![](img/a6d0126307ecc9ee509f5759ff46c41d.png)

[Error & frustrated man Vectors by Vecteezy](https://www.vecteezy.com/vector-art/629015-error-frustrated-man)

我以前是后端开发者。我学到的最重要的一条规则是“**永远不要相信来自前端的输入**”。这很公平，因为我们都知道恶意用户可以绕过客户端验证来发送携带畸形/危险负载的请求，客户端代码也可能会出现导致错误请求负载的问题。

反过来，作为前端开发人员，我们应该仅仅相信后端通过 API 提供给我们的任何东西吗？绝对不会——我们可能会收到潜在的意外 API 响应数据，并且我们应该尽最大努力使我们的前端对此具有弹性(除非我们想随时解决更多问题)。

直接使用从 API 返回的数据会出什么问题？以下是一些例子:

## 我们期望有一个`number`，但却收到一个`string`

```
{
  "aNumber": "1"
}
```

想象一下，我们要从`+1`到`aNumber`，会发生什么？

结果是 11，不是 2！

## 我们期望有一个`Array`，但是收到一个`null`

```
{
  "anArray": null
}
```

想象一下，我们要访问`anArray`的`length`，会发生什么？

我们会得到`Uncaught TypeError: Cannot read property ‘length’ of null`

这些意外的 API 响应背后有许多原因:

*   后端代码中的一个错误
*   数据库中存储了错误的数据
*   后端做出的更改没有通知前端
*   等等

不幸的是，我不认为我们能消除它们，因为我们不能仅仅抱着“没有人为错误”的信念——再说一次，“东西会坏掉”:)

## **引入类型脚本/流并不能解决整个问题**

当然，我们有 TypeScript/Flow 来执行静态类型检查，但这只是针对编译时，而不是运行时。也就是说，即使我们显式地输入了从 API 接收的数据，我们仍然会遇到类型问题，因为拥有类型定义不会影响运行时行为——我们输入为`number`的`string`仍然是`string`，我们输入为`Array`的`null`(或者非空值)仍然是`null` —没有什么可以真正阻止它们发生。

虽然在 TypeScript/Flow 中定义可选类型可能会提醒我们在代码中进行空检查(老实说，我更喜欢尽可能提供有意义的默认值，而不是将某些内容保留为`null`或`undefined`)，但这并不能解决所有潜在的情况——我们仍然有一些误报(例如`number`对`string`)。

那我们该怎么办？我们应该到处写类型检查/强制转换代码吗？嗯，这是一个解决方案，但是可能会有许多重复，我们很容易忘记检查/更改 10 个地方中的 1 个。

## 终极解决方案:解析和转换 API 响应数据

在开发原生移动应用程序(Obj-C/Swift、Java/Kotlin)时，解析 API 响应数据并将其转换为模型对象是非常常见的——很少看到移动项目只是使用 API 返回的数据。

我认为可能有两个主要原因:

1.  JSON(或 JavaScript 对象)并不是这些编程语言本身支持的数据类型
2.  在移动应用上没有运行时类型安全的成本比 web 高得多——发布周期长得多，崩溃的感觉真的很糟糕

在基于 JavaScript 的 web 项目中，即使 JSON 是本机支持的，发布周期也可以短得多，只要我们关心运行时类型安全，我们也应该这样做。

我的建议是 ***在内部和外部*之间建立一个门:让我们解析和转换从 API 接收的数据，在将它们提供给系统的其他部分之前，使它们真正是类型安全的，包括在运行时。**

换句话说，如果我们想要某种数据类型，在试图从其他地方访问它之前，让我们确保我们确实拥有它。一种可能的方法是使用`lodash`提供的转换函数:

```
import get from "lodash/get";
import toInteger from "lodash/toInteger";
import toString from "lodash/toString";const parseData = (json: any): IData => {
  return {
    id: toInteger(get(json, "id")),
    name: toString(get(json, "name"))
  }
}
```

# 加分点:R **eshaping 数据的灵活性**

来自后端的响应负载可能并不总是我们在前端想要的:

*   它可能使用不同的命名约定:`a_snake_case_variable`与`aCamelCaseVariable`
*   它可能缺少我们进行数据规范化所必需的信息:有效负载中可能省略了关系键/ id
*   同一类型实体的数据可能以不同的形状从不同的 API 端点返回

通过添加一个解析和转换层，我们可以减轻上面列出的所有问题，并且知道在访问数据时我们所拥有的正是我们希望从 API 响应中得到的。

# 概述

在前端解析和转换 API 响应数据是必要的，因为这有助于我们确保数据在运行时可以安全使用，并且数据的形状正是我们想要的。

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)