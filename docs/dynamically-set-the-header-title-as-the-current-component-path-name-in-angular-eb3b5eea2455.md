# 将标题动态设置为角度中的当前组件路径名

> 原文：<https://javascript.plainenglish.io/dynamically-set-the-header-title-as-the-current-component-path-name-in-angular-eb3b5eea2455?source=collection_archive---------3----------------------->

## 如何在 Angular 中动态设置头标题为当前组件路径名

![](img/83eb471b395d75589a4e963e3656be45.png)

Photo by [Kelly Sikkema](https://unsplash.com/@kellysikkema?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 第一步:

创建带布线的角度项目。

`ng new header-title - — routing`

## 第二步:

创建组件。在这里，我用内联样式和模板创建最少的组件文件。

`ng g c components/**home** — skip-tests --inline-style - — inline-template --flat`

`ng g c components/**dashboard** — skip-tests --inline-style - — inline-template --flat`

`ng g c components/**profile** --skip-tests --inline-style - — inline-template --flat`

`ng g c components/**edit-profile** —-skip-tests --inline-style - — inline-template --flat`

`ng g c components/**select-products** — skip-tests --inline-style - — inline-template --flat`

## 第三步

将组件添加到`app-routing.module.ts`

app-routing.module.ts

## 第四步

创建标题组件。

`ng g c components/header --skip-tests --inline-style --inline-template --flat`

在`<router-outlet>`上方添加表头组件。现在它出现在每个组件路由上。

```
<app-header> </app-header><router-outlet> </router-outlet>
```

创建一个`header`元素并对其进行样式化。

header.component.ts

我们将在下一步分配标题变量。

## 第五步

在`app.component.ts`中添加用于导航到每条路线的按钮。

app.component.html

现在，在`router-outlet`上添加`(activate)`事件，该事件在每次路由器导航到新路径并且组件被实例化时发出，

`<router-outlet (activate)=”setHeader()”></router-outlet>`

在`setHeader()`中，我们将从路由器中读取当前组件路径。

如果您的路径有空格或任何特殊字符，使用`decodeURIComponent` 。

app.component.ts

## 第六步

将`title`传递到割台`component`。

`<app-header [title]=”title”></app-header>`

在`header.component.ts`中添加`@Input` 以接受该值。

`@Input() title: string = '';`

我们已经将`title` 绑定到了`header`上。所以当路线改变时，`title`值被更新。

最终的代码应该是这样的。

app.component.html

header.component.ts

# 结论

*   如果您有多个组件，并且想要将组件名称设置为标题，请使用`router-outlet`上的`(activate)`事件来检测组件更改。从`Router.`获取当前路径
*   使用`router-outlet`上方的`header`组件，使其出现在每个组件页面上。
*   将从`Router` 获取的路径名传递给`header` 组件。

这是一个工作的堆栈。

仅此而已！希望这篇文章有用。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)