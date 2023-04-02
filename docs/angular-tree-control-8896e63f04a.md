# 如何在 Angular 中创建树控件

> 原文：<https://javascript.plainenglish.io/angular-tree-control-8896e63f04a?source=collection_archive---------10----------------------->

## 这篇文章将向你展示如何使用角度模板和内容投影来编写一个可定制的树控件。

![](img/6fe2fe2e8b3dda9999d36b6095818222.png)

# 设置

让我们首先定义组件使用的模型。

```
export interface TreeItem {
  children?: TreeItem[];
  expanded?: boolean;
}
```

接下来，让我们定义我们的组件

如上所述，我们在 TypeScript 中使用泛型来定义我们的组件与任何扩展`TreeItem`接口的数据结构一起工作。

它还期望我们投射一个`TemplateRef`。在我们的 html 中，这不过是`ng-template`。

# 让我们构建模板

这看起来有点棘手，但实际上非常简单。`treeTemplate`模板只是定义了树的一个层次。如果它有孩子，它会重复自己，但是上下文设置为`item.children`

`nodeTemplate`是模板的消费者传入的模板。这使得用户可以完全控制每个节点的外观。

如果您以前没有使用过带有`let`语法的`ng-template`，这里有一个快速概述。

1.  您可以使用`*ngTemplateOutlet`结构指令实例化一个`ng-template`。
2.  这样做时，您可以使用`context`对象将数据传递给模板。
3.  要访问上下文中传递的任何属性，必须使用 let 语法。因此，如果您的上下文是`{name: 'John'}`，要访问模板中的`name`，您必须这样做`<ng-template let-firstname="name">{{firstname}}</ng-template>`
4.  您可以删除正在访问的`$implicit`属性。所以如果上下文是`{$implicit: 'John'}`，那么你可以使用`<ng-template let-firstname>{{firstname}}</ng-template>`

# 让我们看看如何消费这个组件。

首先让我们定义我们的应用程序组件

接下来，我们将使用应用程序组件 html 中的组件。

这里，我们定义了自己的接口，它扩展了我们在一开始定义的`TreeItem`接口。

在 app 组件中，我们只是将节点的`treeData`和`ng-template`传递给树组件。它负责递归地呈现你传入的模板。

# 工作样本(Stackblitz)

# 额外小费

如果你想支持一个包含大量条目的树控件，那么你可以用自定义的`*ngxtFor`指令替换树控件中的`*ngFor`，我在[这篇文章](https://sanjaybhavnani.medium.com/advanced-angular-structural-directive-to-render-long-lists-db1575d761ce)中展示了这个指令。它使用渐进渲染概念。

你也可以尝试将它与 cdk 虚拟滚动结合起来，但我没有尝试过，所以我不能说实现它有多容易或多困难。

*更多内容尽在*[***plain English . io***](http://plainenglish.io)