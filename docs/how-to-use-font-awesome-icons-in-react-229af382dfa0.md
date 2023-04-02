# 如何在 React 中使用字体出色的图标

> 原文：<https://javascript.plainenglish.io/how-to-use-font-awesome-icons-in-react-229af382dfa0?source=collection_archive---------23----------------------->

## 了解如何在 React 中使用字体出色的图标。

![](img/1b9ef6f1a0985b4b215347d9284602ff.png)

Photo by [Moritz Kindler](https://unsplash.com/@moritz_photography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是最流行的前端框架之一。React 的架构和易用性令人惊叹。

我们经常不得不将字体融入到我们的项目中，而 font awesome 是一款时尚简洁的字体。

在本文中，我们将学习如何在 React 项目中使用字体非常棒的图标。

## **安装**

首先，我们需要使用 npm 在我们的项目中安装 font-awesome

打开您的开发人员终端，根据您首选的包管理器运行以下命令。

## **NPM**

```
 npm i --save [@fortawesome/fontawesome-svg-core](http://twitter.com/fortawesome/fontawesome-svg-core) npm install --save [@fortawesome/free-solid-svg-icons](http://twitter.com/fortawesome/free-solid-svg-icons) npm install --save [@fortawesome/react-fontawesome](http://twitter.com/fortawesome/react-fontawesome)
```

## **纱线**

```
 yarn add [@fortawesome/fontawesome-svg-core](http://twitter.com/fortawesome/fontawesome-svg-core) yarn add [@fortawesome/free-solid-svg-icons](http://twitter.com/fortawesome/free-solid-svg-icons) yarn add [@fortawesome/react-fontawesome](http://twitter.com/fortawesome/react-fontawesome)
```

这将在安装后直接将 font-awesome 安装到我们的项目文件中。

## **使用图标**

现在我们需要将字体很棒的图标直接导入到我们的工作文件中，这样我们就可以很容易地在应用程序中实现它们。

第一次导入将允许我们将字体 awesome 导入到我们的文件中。

第二次导入将使我们能够访问我们希望在项目中使用的各个图标。

这里是我们声明要在应用程序中使用的图标的地方。例如，如果我们想在项目中加入搜索图标，我们可以使用术语 ***faSearch*** 来实现。

我们使用 **fa** 后跟图标名称，并记住使用**大写字母**作为图标名称的首字母，否则 react 会抛出一些错误。

我们可以根据需要在应用程序中选择任意多的图标。

## **使用图标**

我想现在你已经知道如何在我们的应用程序中导入图标了。现在，我们将看看如何在应用程序中使用图标，并使它们在组件 UI 中可见。

为了使用图标，我们将它们包括在内，如下所示。

这就是我们如何在 React 中轻松实现使用字体出色的图标。

## **走之前**

感谢您阅读本文到目前为止。希望对你有帮助。

如果你觉得其他人可能会从这篇文章中受益，如果你分享它，对我来说意义重大。

## **更多内容:**

[](/how-to-perform-data-binding-in-vue-js-c22934f7721a) [## 如何在 Vue.js 中进行数据绑定

### Vue.js 中的数据和输入绑定，并附有示例。

javascript.plainenglish.io](/how-to-perform-data-binding-in-vue-js-c22934f7721a) [](/how-to-secure-environment-variables-with-dotenv-c534fe46c8a) [## 如何用 Dotenv 保护环境变量

### 使用 dotenv 保护环境变量的分步指南。

javascript.plainenglish.io](/how-to-secure-environment-variables-with-dotenv-c534fe46c8a) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)