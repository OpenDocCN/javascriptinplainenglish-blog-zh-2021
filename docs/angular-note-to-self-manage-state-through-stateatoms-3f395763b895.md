# 自我提醒:通过状态原子管理状态

> 原文：<https://javascript.plainenglish.io/angular-note-to-self-manage-state-through-stateatoms-3f395763b895?source=collection_archive---------5----------------------->

![](img/d92c77a2d2b90641e53ca7f4d3e9b460.png)

Photo by [Raphaël Biscaldi](https://unsplash.com/@les_photos_de_raph?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

当谈到 Angular 应用程序中的基本状态管理时，我是这样做的。除了 RxJS 之外，它不需要其他库。

## 状态原子

没找到更好的名字，就叫**态原子**。这是一个存储和跟踪单个值的类——一个原语、一个对象或一个数组。我们用一个`BehaviorSubject`来存储值，用一个`Observable`来通知变化。此外，很少有方便的类方法来更新和重置值。

Fig 1: State Atom class

只有状态原子不足以进行状态管理。相反，我们将编写一个助手服务来实现业务逻辑，同时消除复杂性，并使其易于对更改和加载数据做出反应。

## 国家服务

我喜欢让我的控制器瘦，服务胖。因此，例如，我将为`ArticleViewPageComponent`创建一个特定的服务`ArticleViewPageStateService`。`root`范围内不提供服务。相反，我将把它**注入到组件**中，因为这个服务应该和组件有相同的生命周期:

```
@Component({
    templateUrl: './view-article-page.component.html',
    styleUrls: ['./view-article-page.component.scss'],
    **providers: [ViewArticlePageStateService]**,
})
export class ViewArticlePageComponent implements OnInit {}
```

我为状态创建了一个接口，以确保正确的类型。仅仅为了这个例子，设想一个页面，其中显示了一篇文章，并且与该文章相关联的评论以分页的方式显示。每次我的页面获取数据和更新视图时，我都会显示一个加载指示器。因此，页面状态可能如下所示:

Fig 2: Page State interface and initial value

现在，在`ViewArticlePageStateService`中，我将介绍原子。原子需要一个初始状态。所以我将在`initialState`对象中定义的初始值传递给每个原子。

原子暴露了其存储值的可观察性。这意味着如果我们通过`combineLatest` RxJS 操作符收集所有原子的值，那么我们将总是得到最新的状态。

Fig 3: Building the state with atoms

我们可以跟踪特定的原子值是否被改变。基于此，我们可以更新状态的其他属性。这是使用副作用的最佳地方，比如从服务器加载数据。我们在页面状态服务的实例化过程中注册了`handleEffects()`触发器，它一直运行到服务被销毁。

Fig 4: Registering side effects

为了理解这里的机制，让我们考虑当任何一个`_start,_limit`或`_sort`查询参数改变时，我们想要加载注释。为此，我在效果处理器中点击`commentsPagination`流(通过`combineLatest`)。每当有新的值时，我们将它传递给`switchMap`操作符，并从`commentService`加载注释。SwitchMap 用于取消之前的呼叫。如果您认为由于您在效果处理程序中跟踪许多 atom 值而导致调用过多，那么您可以使用`debounceTime`操作符来最小化这个数量。最后，我更新了 subscribe 块中的状态。

这只是一个例子。您可以使用更多的处理程序来完成必要的副作用，例如从多个 REST 服务加载数据、进行计算等。

最后，我添加了更多的类方法来方便状态的操作，比如`reset(), getStateSnapshot(), updateXyz()`等。下面是整个 StateService 的样子:

Fig 5: StateService to be provided in the page component

我们已经完成了简单的状态管理器。让我们看看如何在页面组件中使用它。

这种国家服务提供了许多优势:

*   我可以安全地使用`OnPush`变更检测策略，而不用担心 bug。
*   所有的模板变量都位于`state$` observable 内部。在模板中使用 with `async` pipe 时，它会自动退订，让您高枕无忧。
*   架构变得干净，真正的反应。我更新状态原子，状态服务反映原子的变化。
*   数据单向流动，因此更容易调试。
*   我可以突然提高单元可测试性，因为服务中的方法更小了。组件控制器的责任很小。
*   我可以对多个组件使用相同的状态服务。

这种方法是托马斯·伯利森这篇伟大文章的略微修改版本:

[](https://thomasburlesonia.medium.com/push-based-architectures-with-rxjs-81b327d7c32d) [## 具有 RxJS 的基于推送的架构

### 你一直编码错误！

thomasburlesonia.medium.com](https://thomasburlesonia.medium.com/push-based-architectures-with-rxjs-81b327d7c32d) 

感谢阅读！