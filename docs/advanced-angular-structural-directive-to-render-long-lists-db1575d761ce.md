# 呈现长列表的高级角度结构指令

> 原文：<https://javascript.plainenglish.io/advanced-angular-structural-directive-to-render-long-lists-db1575d761ce?source=collection_archive---------2----------------------->

## 本文向您展示了如何创建一个类似于 Angular 自己的 ngFor 的高级结构指令，并使用渐进式渲染概念来渲染一个长列表。

![](img/9b0354044f51748c93416140665b9833.png)

## 先决条件

对 JavaScript 和 Angular 有基本的了解。

## 设置和简要结构指令复习。

我们计划在我们的组件中使用这样的指令。

```
<ul>
  <li *ngxtFor="
      let item of longList; 
      itemsAtOnce: 500;
      intervalLength: 50">
   Item - {{item.id}}
  </li>
</ul>
```

指令中的“*”语法基本上是告诉 angular 将元素包装在 ngTemplate 中，而不是立即呈现它。然后，我们可以通过注入`TemplateRef`和`ViewContainer`服务来访问指令中的模板，并使用我们的定制逻辑来呈现模板。

`itemsAtOnce`和`intervalLength`将是输入，指定一次应该渲染多少个项目，以及在渲染之前应该等待多长时间。

接下来，在我们的应用程序组件中，我们创建一个包含 50000 个项目的列表。

```
ngOnInit() {
   const longList = [];
   for (let i = 0; i < 50000; i++) {
     longList.push({ id: i });
   }
   this.longList = longList;
}
```

这就是我们应用组件的全部内容。接下来让我们开始创建我们的指令。我们将首先从没有任何逻辑的基本结构开始。

`ngxtForOf`输入中的`of`让我们可以在指令中使用`let items of items`语法。其他输入也必须以指令的选择器为前缀，以便在第一个代码片段中显示的语法中使用。

如果你对结构指令完全陌生，你可以在这里参考[关于结构指令的角度指南](https://angular.io/guide/structural-directives)

# 介绍 iterable differents `angular service.`

此时，我们可以使用`ngOnInit`处理程序中的`viewContainer.createEmbeddedView`方法来获取项目并呈现它们，但是如果项目被添加到列表中或者被从列表中移除，这将不起作用。这就是`[IterableDiffers](https://angular.io/api/core/IterableDiffers)`出现的原因。它为我们提供了一种不同的策略，使用这种策略，我们可以在列表中添加或删除项目时处理场景，而不必自己编写逻辑。让我们把它加到我们的指令里。

如上所述，当我们接收到条目时，我们正在创建一个`IterableDiffer.`的实例，这是我们在列表中添加/删除条目时将使用的。

`IterableDiffers.find(items)`将检查 Angular 是否有一个为传递给它的项目提供不同策略的`IterableFactory`。在我们的例子中，`items`是可迭代的，Angular 有一个工厂。所以会被退回。然后我们调用工厂上`create`来获得`IterableDiffer`的实例，它可以用来区分列表。

需要注意的重要一点是`forEachAddedItem`和`forEachRemovedItem`在`[IterableRecord](https://angular.io/api/core/IterableChangeRecord)`对象上迭代。除了列表项本身之外，它们还包含许多附加信息。我们将使用`currentIndex`属性来确保从正确的索引中添加/删除模板引用。

想了解更多关于 Angular 中`IterableDiffers`的信息，请参考这篇[精彩文章](https://netbasal.com/getting-to-know-angular-differs-60cd68f4bd8f)

# 最后一步:添加逐步呈现列表的逻辑。

现在我们已经把所有的部分都整合在一起了。`progressiveRender`方法获取`IterableChangeRecord`对象的数组，并根据输入将它传递给`renderItems`方法，每次传递固定数量的项。该方法使用`createEmbeddedView`方法在 DOM 上创建它们，您可能已经在简单的结构化指令中见过这种方法。

注意`createEmbeddedView`的第三个参数。这个`index`参数确保当列表项被移除或替换时，项目被呈现在正确的位置。

`viewRefsMap`是一个私有映射，指令使用它来存储对嵌入式视图对象的引用。当处理列表项时，它会被填充。当视图项目从我们的应用程序组件的列表中删除时，这个映射在`ngDoCheck`中被用来删除视图项目

# 请参见 stackblitz 上的这条指令。

当使用我们的自定义指令和内置的`ngFor`指令呈现一个大的列表时，您可以看到性能上的差异。

# 参考

我从这篇由[詹卡洛·布姆普利斯科](https://medium.com/@.gc?source=post_page-----9f4dcb9b65--------------------------------)写的文章中得到了渐进渲染的想法

[](https://blog.bitsrc.io/3-ways-to-render-large-lists-in-angular-9f4dcb9b65) [## 在 Angular 中呈现大列表的 3 种方法

### 使用角度呈现大型项目列表的可用技术概述

blog.bitsrc.io](https://blog.bitsrc.io/3-ways-to-render-large-lists-in-angular-9f4dcb9b65) 

感谢 Yoni Amishav 撰写了关于如何构建我自己的 ngFor 指令的精彩文章。

[](https://www.talkinghightech.com/en/create-ngfor-directive/) [## 如何创建自己的 NgFor 指令？说话的高科技

### 学习 Angular 框架的内部有时会经历一些基本概念，有时会经历大部分…

www.talkinghightech.com](https://www.talkinghightech.com/en/create-ngfor-directive/) 

# 结论

在本文中，我们已经讨论了许多高级主题。我希望阅读这篇文章的每个人都觉得它很有用，并能从中受益。这是我写的第一篇关于媒体的文章，我写得很开心。如果你喜欢，那么请在 [Medium](https://medium.com/@sanjaylbhavnani) 上关注我，因为我计划继续写更多关于 Angular、TypeScript 和 JavaScript 的文章。

*更多内容尽在*[***plain English . io***](http://plainenglish.io)