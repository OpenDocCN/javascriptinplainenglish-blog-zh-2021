# 如何在 Angular 中实现客户端认证

> 原文：<https://javascript.plainenglish.io/how-to-implement-client-side-authentication-in-angular-d6dc30920f98?source=collection_archive---------8----------------------->

## 采用行业标准的最佳实践

![](img/646e7629df4232c82acf0b47064dd8c5.png)

Photo by [Chepe Nicoli](https://unsplash.com/@nicoli_?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在我们开始之前，区分客户端和服务器端身份验证是很重要的，并注意生产就绪的应用程序必须同时包含这两者。

服务器端身份验证控制谁有权访问单个 API 端点，进而控制应用程序数据的范围。

应用程序的安全性依赖于服务器，而不是客户端。服务器是将数据发送到客户端的最后一道防线。请记住，用户可以在没有用户界面的情况下访问服务器。

客户端身份验证在保护应用程序方面没有什么分量。它在保护用户不访问他们不应该访问的路线或组件方面确实举足轻重。

概括地说，服务器端身份验证主要提高安全性，客户端身份验证主要改善用户体验。说到这里，让我们开始吧。

# 安装

让我们用 routing 初始化一个 Angular 项目。这个演示项目将被称为“认证”

```
ng new auth --routing
```

让我们服务应用程序，看看我们的变化。

```
ng serve -o
```

# 组件

让我们生成两个组件:未经身份验证的用户的登录页面和经过身份验证的用户的主页。

```
ng generate component components/login
ng generate component components/home
```

# 路线

让我们用下面的内容替换**app.component.html**的内容。

```
<router-outlet></router-outlet>
```

登录页面和主页将分别与路线**/登录**和**/主页**相关联。我们还希望将基本 URL 重定向到主页。让我们将这些路线及其各自的组件添加到 **app-routing.module.ts** 中。

```
const routes: Routes = [
  {
    path: ‘login’,
    component: LoginComponent,
  },
  {
    path: ‘home’,
    component: HomeComponent,
  },
  {
    path: ‘’,
    pathMatch: 'full',
    redirectTo: 'home',
  },
];
```

现在， **/login** 显示登录组件， **/home** 显示 home 组件。基础 URL **重定向到 **/home** 。**

# 服务

让我们生成一个服务来检索当前用户和用户的模型。

```
ng generate services/authng generate interface models/User model
```

我们将修改 **user.model.ts** 如下:

```
*export* interface User {
  name: string;
}
```

在 **auth.service.ts** 中，我们添加一个 getter 函数来检索当前用户。如果用户已经登录，该函数将返回一个**用户**对象，否则返回 null。

```
get user$(): Observable<User | null> {
  return of({
    name: 'Bob',
  });
}
```

# 警卫

最后，我们需要一个路线守卫。Angular 提供了一个接口， [CanActivate](https://angular.io/api/router/CanActivate) ，决定用户是否可以激活一条路线。警卫将与认证服务通信以确定用户是否被认证。那么，有三种可能的结果:

1.  用户通过了身份验证，但被导航到登录页面。在这种情况下，守卫会将用户重定向到主页。
2.  该用户未经身份验证，但导航到了主页。在这种情况下，守卫会将用户重定向到登录页面。
3.  用户通过身份验证并导航到主页，或者用户未经身份验证并导航到登录页面。在任何一种情况下，警卫都会允许进入该路线。

让我们生成这个守卫。

```
ng generate guard guards/auth
# select CanActivate
```

让我们将从我们的服务中观察到的**用户$** 引入 **auth.guard.ts** 。我们还可以引入 Angular router 服务来为用户导航正确的路线。

```
user$: Observable<User>;constructor(authService: AuthService, private router: Router) {
  this.user$ = authService.user$;
}
```

我们希望通过 RxJS 地图操作符运行可观察的**用户$** 。我们将把用户对象转换成布尔值，并检查当前路由是否是登录路由。有了这些信息，我们就可以决定用户是否有权访问该路线。

如果用户试图访问他们无权访问的路线，我们将返回一个 URL 树。在 Angular 中，这告诉路由器用户无权访问路由，并相应地重定向他们。

在 **canActivate** 函数中，我们添加以下代码。

```
*return* *this*.user$.pipe(
  map((user) => {
    const isAuthorized = !!user;
    const isLoginRoute = state.url.includes('login');
    const hasAccess = isLoginRoute ? !isAuthorized : isAuthorized;
    const redirect = isLoginRoute
      ? *this*.router.createUrlTree([''])
      : *this*.router.createUrlTree(['login']);
    *return* hasAccess ? true : redirect;
  })
);
```

这是我们认证逻辑的核心。

让我们在 **app-routing.module.ts** 中通过向数组中的两个 route 对象添加键值对`canActivate: [AuthGuard]`来为两个 route 添加保护，如下所示。

```
 {
    path: ‘login’,
    component: LoginComponent,
    canActivate: [AuthGuard], },
  {
    path: ‘home’,
    component: HomeComponent,
    canActivate: [AuthGuard],
  },
```

现在，当我们转到位于 **/login** 的登录组件时，我们将被重定向到位于 **/home** 的 home 组件。如果我们去**/家**，我们就呆在那里。

让我们在 **auth.service.ts** 中更改我们的认证服务，以返回一个空用户来表示该用户已注销。

```
get user$(): Observable<User | null> {
  return of(null);
}
```

当我们转到位于 **/home** 的 home 组件时，我们将被重定向到位于 **/login** 的 login 组件。如果我们路由到**/登录**，我们就呆在那里。

Angular 总结了我们的客户端身份验证指南。您可以在这里找到这个演示的代码。

[](https://github.com/charlielevine/angular-auth) [## charlielevine/angular-auth

### 此项目是使用 Angular CLI 版本 11.1.4 生成的。为开发服务器运行 ng serve。导航到…

github.com](https://github.com/charlielevine/angular-auth) 

如果您觉得这很有用，请在 Medium ( [Charlie Levine](https://medium.com/u/6da6b651e31a?source=post_page-----d6dc30920f98--------------------------------) )上关注我，我每周都会在这里发布角度、编程和技术相关的文章。非常感谢您的支持，一如既往，非常感谢您的阅读！