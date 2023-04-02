# 如何保护 Angular 中的路由免受未经授权的访问

> 原文：<https://javascript.plainenglish.io/how-to-protect-routes-in-angular-from-unauthorized-access-52a131610266?source=collection_archive---------6----------------------->

## 了解如何使用 AuthGuard 保护 Angular 中的路线

![](img/24f0c9751ca1dd280025a2f270c3f893.png)

[https://unsplash.com/photos/ieic5Tq8YMk](https://unsplash.com/photos/ieic5Tq8YMk)

在本教程中，我们将看到，如何使用 Angular 来保护页面/路径免受未经授权的访问。我们可以轻松地创建一个组件，并为该组件创建一条路线。默认情况下，任何人都可以访问 **Angular** 中的所有路线。但是当我们开发 ERP、CRM 等应用时。，这些应用程序必须只能由授权人员访问。

在使用 Angular 之前，HTML 代码与服务器端代码混合在一起。所以我们之前有一个会话概念来限制用户访问页面。用户登录后，将为特定用户创建会话。每当用户访问新页面时，都会在每次请求页面时验证会话。这就是我们如何使用会话概念来限制用户访问。

现在我们使用 **REST API** 来获取数据。Angular 完全独立于服务器端代码。我们使用的是无状态 REST API。所以我们不能使用 Angular 中的会话概念来验证用户。因此，每个 Angular 开发人员都会想到这个问题。

*我们如何保护页面免受未授权用户的访问？*

Angular 为我们提供了解决这个问题的终极方案。那叫 **AuthGuard** 。AuthGuard 用于保护路由免受未经授权的访问。

## 【AuthGuard 如何工作？

AuthGuard 有许多生命周期事件。最常用的生命周期事件之一是 **canActivate** 。canActivate 就像一个构造函数。它将在访问路线之前被调用。canActivate 必须返回 true 才能访问页面。如果它返回 false，我们就无法访问该页面。我们可以在 canActivate 函数中编写我们的用户授权和认证逻辑。

## **创建授权卫士**

我们可以在您的终端上使用下面的命令创建一个 AuthGuard。使用终端在 Angular 项目中执行下面的代码。

```
ng g guard services/auth
```

我已经在 services 文件夹中创建了 AuthGuard。AuthGuard 名称为 auth。你可以用任何名字。获得下面的 AuthGuard 的完整代码。

这里，在 canActivate 内部，我从登录服务调用了 verify()函数。我使用 JWT 令牌来授权用户。因此 verify()函数从 cookies 中获取 JWT 令牌，并每次使用 HTTP 请求在服务器中验证它。您可以在这里实现自己的逻辑。

## **将 AuthGuard 包含到路由中**

将创建的 AuthGuard 包含到您的路线中，如下所示。

仅此而已。现在，对于路由的每个请求，将调用 verify()函数，如果 verify()函数返回 true，那么只有我们可以访问特定的路由。如果它返回 false，我们就无法访问它。

这就是我们如何限制未经授权的用户访问路由。

## **结论**

在本教程中，您学习了如何创建一个 **AuthGuard** 以及如何将 AuthGuard 添加到您的路线中以防止未经授权的用户访问。本教程对于试图创建使用认证和授权的应用程序的初学者来说非常有用。对于来自会话概念的开发人员，本文将帮助他们使用 Angular 实现访问限制。

Angular 完全独立于服务器。我们使用无状态 REST API 来获取数据。所以使用 AuthGuard 来保护路由免受未授权的访问。

感谢您阅读这篇文章。

延伸阅读。

[](/angular-routing-and-navigation-example-998d14c01f8e) [## 角度路由和导航示例

### 创建组件并创建路线，然后导航到路线

javascript.plainenglish.io](/angular-routing-and-navigation-example-998d14c01f8e) [](/implement-jwt-based-authorization-using-nodejs-and-angular-9f75ab5904ac) [## 使用 NodeJS 和 Angular 实现基于 JWT 的授权

### 如何使用 NodeJS，MySQL 创建 JWT 授权的完整示例，并使用 Angular

javascript.plainenglish.io](/implement-jwt-based-authorization-using-nodejs-and-angular-9f75ab5904ac) [](/create-rest-api-using-nodejs-and-mysql-from-scratch-d1844601e21) [## 从头开始使用 NodeJS 和 MySQL 创建 REST API

### 从头开始使用 MySQL 的 CRUD 示例

javascript.plainenglish.io](/create-rest-api-using-nodejs-and-mysql-from-scratch-d1844601e21) 

*更多内容尽在*[***plain English . io***](https://plainenglish.io/)