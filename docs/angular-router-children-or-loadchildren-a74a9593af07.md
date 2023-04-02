# 角路由器:孩子还是 LoadChildren？

> 原文：<https://javascript.plainenglish.io/angular-router-children-or-loadchildren-a74a9593af07?source=collection_archive---------0----------------------->

![](img/48de4f982e8d4d9be2e70ae8202816a0.png)

Photo by [Jannis Brandt](https://unsplash.com/@jannisbrandt?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

*(本文假设基本了解路由器和路由器 API。如需深入了解，请参考* [*棱角文档*](https://angular.io/guide/router) *)*

**Angular Router** 是 Angular 生态系统中最有用的包之一。但是，如果您是 Angular 的新手，并且刚刚开始使用路由器，您的目标可能是设置一些基本路由。此外，对于新的开发人员，我通常会看到许多关于 **children** 和 **loadChildren** 属性的问题。因此，本文将只关注这两个属性之间的区别以及何时使用什么。

## **角度路线界面**

```
export interface Route {path?: string;
component?: Type<any>;children?: Route[];loadChildren?: LoadChildren;... few other properties}
```

让我先快速解释一下路由接口的上述四个属性(在本文的范围之内):

*   **路径**:路由器 API 将整个 URL 分解成单独的片段。路径属性可以对应于这些片段的组合。它主要用于标识应该在父路由器出口中实例化和加载的角度组件。
*   **组件**:该属性是指应该为该路径实例化的角度组件。
*   **Children** :这个属性定义了嵌套的路径，angular 会提前加载它们。
*   **LoadChildren** :也用于定义嵌套路由，但是 Angular Router 会延迟加载。你看到这里的优势了。

现在我们已经定义了相关的路由属性，让我们看看什么时候应该在`children`和`loadChildren`之间进行选择。

# 使用儿童:

*   添加嵌套路由。
*   Angular 将预先加载所有子组件。
*   确保为嵌套路由表中定义的每个组件导入所有 NgModules。否则，您的代码将无法工作。
*   为了提高代码的可读性和可维护性，如果路由表的嵌套太长，请避免使用该属性。我个人的偏好是< 3 级最高。
*   简单路线的理想选择。
*   代码示例:

```
const routes = [
  {
    path: '',
    component: ApplicationFrameComponent,
    children: [
    {
      path: 'home',
      component: HomeDashboardComponent,
      children: [
        {
           path: 'api-dashboard',
           component: ApiHomeDashboardComponent
        }]
    },
    {
      path: 'api-list',
      component: ApiListComponent,
      children: [
        {
           path: 'internal',
           component: InternalApisListComponent
        },
        {
           path: 'external',
           component: ExternalApisListComponent
        }]
    }]
  }];
```

# 使用 LoadChildren:

*   对于懒加载。当用户导航到与当前路由路径匹配的特定 URL 时，使用此属性将只加载嵌套的路由子树，从而优化应用程序的性能。
*   这有助于保持嵌套路由表的独立性。
*   您必须为 loadChildren 指定一个路由模块。此模块必须定义路线，并应导入所有相关的 ng 模块
*   如果您使用`import(<module-path>).then(module => module.<routing-module>)`，Angular 将创建一个单独的 js 包，只有当一个子路径被激活时才会被加载。您将获得更好的性能、代码可读性和可维护性。
*   如果您使用`() => <routing-module>`，angular 将不会创建一个单独的 js 包，但是 routes 表将保持独立。结果是更好的代码可读性和可维护性。性能将与`children`方法相同。
*   代码示例:

```
const rootRoutes = [
  {
    path: '',
    component: ApplicationFrameComponent,
    children: [
    {
      path: 'home',
      loadChildren: () => HomeDashboardRoutingModule
    },
    {
      path: 'api-list',
      loadChildren: @import('./api-list.module').then(module => module.ApiListRoutingModule)
    }]
  }];// In HomeDashboardRoutingModuleconst homeRoutes = [
  {
    path: '',
    component: HomeDashboardComponent,
    children: [
      {
         path: 'api-dashboard',
         component: ApiHomeDashboardComponent
      }]
  }]; // In ApiListRoutingModule
const apiListRoutes = [
{
   path: '',
   component: ApiListComponent,
   children: [
     {
        path: 'internal',
        component: InternalApisListComponent
     },
     {
        path: 'external',
        component: ExternalApisListComponent
     }]
}];
```

我希望这篇文章是有帮助的！一个**给我的观众的小问题**。如果我们为带有 **loadChildren** 属性的路由传递一个`component`会发生什么？

```
{
  path: 'home',
  component: HomeDashboardComponent,
  loadChildren: () => HomeDashboardRoutingModule
},
```

请在下面的评论区回复好吗？

*更多内容请看*[***plain English . io***](http://plainenglish.io/)