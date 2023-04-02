# 如何用 Vue.js 处理注册表单

> 原文：<https://javascript.plainenglish.io/how-to-handle-registration-forms-with-vue-js-da3cdeb659e?source=collection_archive---------13----------------------->

## 用 Vue.js 向 API 端点发送用户信息。

![](img/a3813dee98acc4c932d7a01d9727f3a8.png)

Photo by [Pankaj Patel](https://unsplash.com/@pankajpatel?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在某个时间点，您必须在应用程序中执行某种形式的创建、读取、更新和删除。作为前端开发人员，向服务器或特定的 API 端点发送信息是一项基本技能。

处理来自用户的信息是需要了解的重要技能之一，特别是当作为一名前端开发人员工作时，Vue.js 对于那些在前端工作的人来说是非常令人惊讶的。

在本教程中，我们将看看如何使用 API 将用户数据发送到后端。我们将研究 fetch 和 Axios 在向后端服务器 API 发送用户数据时的两种不同方式。

对于本教程，我们将假设您已经配置了 backed，允许发送带有各种验证的请求。我们将利用与后端配置相关的各种 API 端点。假设在注册过程的本教程中，我们将利用上面的 API 端点，假设我们有—[***http://localhost:3000/API/user/register***](http://localhost:3000/api/user/register)。

## **用 fetch API 发送用户信息。**

在本教程的这一部分，我们将捕获用户信息，并将其发送到我们上面看到的端点。

在这一部分，我们将使用 fetch 方法发送用户输入的信息。

创建一个文件，命名为***registration . vue***

如果您检查我们的模板组件和表单数据，您会看到我们附加了一些指令。

**@ submit . prevent = " register user "**我们附加的这个指令将确保每次我们点击提交按钮时都运行 **registerUser** 方法。同理，**。prevent** 指令将确保当点击提交表单按钮时页面不会加载。

另外，要注意的是，我们已经将各自的 v-model 指令附加到数据中。这确保我们在提交表单时获得状态数据的更新版本。我们还可以确保这种状态与 refs 的反应性，以及与 Vue.js 3 中捆绑的 composition-API 的反应性。

Out **registerUser** 方法是应用程序的所有功能以及前端和后端应用程序之间的通信发生的地方。

registerUser 方法只是一个收集用户信息并通过 POST 方法将其发送到下面专门的 API 端点的函数。

对于 fetch 方法，我们首先必须提供信息将被发送到的 URL 端点，然后我们提供其他方法，比如声明发送用户信息的方法，比如我们的例子中的任一 POST。

然后我们仍然将我们的头发送给 application/JSON。之后，我们提供包含用户信息的主体，我们将把用户信息发送到服务器进行身份验证。在我们的例子中，将以 JSON 格式发送主体数据。记住与状态数据同步，以确保我们拥有状态的更新版本。

## **用 AXIOS 发送用户信息。**

如果我们使用 Axios，我们首先必须将它安装到我们的应用程序开发中。要安装 Axios，您可以使用下面显示的命令，这取决于您最喜欢的软件包管理器。

**NPM**

```
npm install axios
```

**纱线**

```
yarn add axios
```

然后，您必须将它导入到您想要实现它的各自的应用程序组件中。检查如下所示的代码片段:

对于 Axios，它将设置所有的默认头，因此我们只需链接我们想要实现的方法，比如我们的例子中的 POST。

然后，我们将提供我们的资源主体，在这种情况下，我们将发送我们的姓名、电子邮件和密码。这就是我们如何将用户信息发送到后端配置的服务器 API 端点。

## **最终想法**

感谢您通读这篇文章，希望对您有所帮助。请不要犹豫与他人分享它。

## **更多内容:**

[](/the-ugly-side-of-being-a-programmer-they-dont-tell-you-about-1a40a26fc39f) [## 作为一名程序员，他们不告诉你的丑陋一面

### 拥抱他们，让他们成为更好的整体开发者。

javascript.plainenglish.io](/the-ugly-side-of-being-a-programmer-they-dont-tell-you-about-1a40a26fc39f) [](/everything-you-need-to-know-about-null-and-undefined-in-javascript-a119aa192d9d) [## 关于 JavaScript 中的 Null 和 Undefined，你需要知道的一切

### JavaScript 中的 null 和 undefined 数据类型有什么区别和相似之处？解释为…

javascript.plainenglish.io](/everything-you-need-to-know-about-null-and-undefined-in-javascript-a119aa192d9d) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)