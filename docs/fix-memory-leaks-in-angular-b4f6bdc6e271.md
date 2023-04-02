# 提高角度应用的性能

> 原文：<https://javascript.plainenglish.io/fix-memory-leaks-in-angular-b4f6bdc6e271?source=collection_archive---------2----------------------->

## 如何减少内存泄漏？

## 角度性能和优化清单

![](img/7a3424617241f7e459663e3f67de1658.png)

Angular 是功能强大、高性能的前端框架之一。随着应用程序的增长，它会变得越来越慢。如果你不知道如何优化应用程序，它会开始影响最终用户的体验。

要预先了解并修复性能，最好了解优化技术。我们有很多方法可以优化你的角度应用，这里我想讨论一些对我的开发很有帮助的技术。

让我们进入我们的主要讨论。

当“泄露”这个词出现在脑海中时，它意味着有些事情正在混乱地发生。有时很难找到问题所在，也很难解决问题。在软件开发中，写一个干净的代码，让你与众不同，是基本的事情之一。有时，当我们开发更大的应用程序时，随着时间的推移，它会随着代码的增长而变得缓慢。从一开始就知道让我们的应用程序更干净以减少包的大小并避免任何泄漏是非常重要的。

正如所讨论的，内存泄漏发生在每个应用程序中，让我们讨论如何影响 Angular 应用程序。在本文中，我们将在 Angular 应用程序中创建一个内存泄漏，并将解决和讨论解决它的不同方法。

当应用程序变慢时，我们通常会刷新或重新加载页面，从而释放内存，应用程序变得正常，但我们不知道后台实际发生了什么，直到我们深入了解它。

有一些原因有时会导致内存泄漏。

1.  长时间使用同一个应用程序。
2.  使用 ngIf 多次渲染应用程序，这取决于可观测量。
3.  在应用程序中调用多个观察值，并且在使用后不取消订阅。
4.  订阅诸如表单控件之类的侦听器，而不是在组件被破坏后取消订阅。
5.  当我们使用 shareReplay 但没有添加 unsubscribe 逻辑来处理它时。

让我们创建一些场景来讨论内存泄漏。

# 1.订阅/取消订阅可观察值

让我们看看与可观察到的问题相关的问题和解决方案。

让我们创建 **TestLeakChild** 和**testleakpanarcomponent**。

**TestLeakChild** 有一个计时器每秒运行一次，计时器的控制台以日期和时间启动。

**ParentLeakComponent** 有两个启动观察和停止观察按钮，分别运行定时器和停止定时器。

让我们来看看演示。

**观察:**

1.  我点击了**开始观察按钮**
2.  我点击了**开始观察**按钮，控制台正在打印计时器值
3.  我点击了 **stop observable** 按钮，控制台仍在打印。点击**停止可见**按钮不是应该停止吗？
4.  是的，你猜对了，我们已经成功地造成了内存泄漏。
5.  我们如何监控呢？

我们来看看这个。

> 首先，我们需要按照方法在浏览器中打开性能监视器。

让我们遵循相同的步骤，通过连续点击**开始可见**和**停止可见**按钮来检查 Chrome 性能监视器。

如果你在 GIF 中注意到了(抱歉有点模糊),我们可以看到 CPU 使用率和堆大小开始增加。

那么，我们应该如何解决这个问题呢？

# 解决办法

常见的解决方案是使用 unsubscribe 方法，在可观察对象被使用后将其取消订阅。

让我们通过创建 TestFixChildComponent 和 TestFixParentComponent 来检查解决方案。

让我们检查一下使用 unsubscribe 方法后的行为。

有多种方法可以清理 RXJS 订阅。我们将在本文的后面讨论它们。

你可以在这里和 stackblitz 一起玩。

[https://stackblitz.com/edit/angular-meomry-leak?file = src % 2f app % 2f test-leak % 2f test-leak-parent . ts](https://stackblitz.com/edit/angular-meomry-leak?file=src%2Fapp%2Ftest-leak%2Ftest-leak-parent.ts)

# 2.共享重播

首先，让我们了解什么是 ShareReplay。它返回 hot observable 并重放 N 个通知，因此一旦源完成，它就向订阅者重放，而无需再次调用源。

让我们来看看这个例子。

[https://stackblitz.com/edit/rxjs-warning-sharereplay?file=app/app.component.ts](https://stackblitz.com/edit/rxjs-warning-sharereplay?file=app/app.component.ts)

当我们看到上面的截图时，我们可以看到通过改变标签可以使堆的大小增加，并且计数器不会自己停止。

我们在这里错过了一件事。

# 解决方案:

共享重播的源代码

我们错过了属性 refCount: true，订阅将永远不会被取消订阅。

请查看下面的文章以了解更多信息。

> [*有角度有深度文章:ShareReplay 有什么变化*](https://blog.angularindepth.com/rxjs-whats-changed-with-sharereplay-65c098843e95) *。*

为了解决这个问题，让我们添加以下内容:

正如我们现在看到的，我们的内存泄漏已经消失了。

# 3.事件监听器

内存泄漏的另一个常见原因是 DOM 事件没有被注册，因此它将总是侦听一些事件。

让我们看一个常见的例子，在这个例子中，我们在主体上注册了一个事件，但从来没有取消注册。

这将在我们实例化 ScrollComponent 时造成内存泄漏。

# 解决办法

一旦我们销毁了组件，基本上我们需要注销侦听器以避免内存泄漏。

我们已经讨论了很多关于内存泄漏的问题，让我们检查一些常见的编码实践，以避免我们的 Angular 应用程序中的内存泄漏。

# 练习

## 1.使用`unsubscribe`方法

所有订阅都需要**取消订阅**才能释放或取消可观察的执行。

为了防止内存泄漏，一个常见的做法是捕获订阅中的可观察对象，并在 ngOnDestroy 钩子中取消订阅，一旦组件被销毁，这个钩子就会被调用。

为了防止这些内存泄漏，我们必须在完成订阅后取消订阅。我们这样做是通过调用`unsubscribe`可观察的方法。

正如我们所看到的，我们将 ngOnDestroy 添加到了 TestComponent 中，我们在订阅方法中捕获了可观察对象，并且取消了订阅。

如果组件中有多个订阅怎么办？让我们看看它是什么样子的。

TestComponent 中有两个订阅。它们都在 ngOnDestroy 钩子中被取消订阅，以防止内存泄漏。

我们可以在一个数组中收集它们的订阅，并在`ngOnDestroy`中取消订阅:

Observables subscribe 方法返回一个 RXJS subscription 对象，所以基本上，我们可以使用 **add** 方法将它们分组，这样当我们取消订阅一个主订阅时，所有子订阅都将被自己取消订阅。

让我们来看看这个例子:

当组件被销毁时，这将取消`this.subscripton1$`和`this.subscripton2$`的订阅。

## 2.使用异步`|`管道

异步管道订阅可观察对象，并返回最新发出的值。捕获新值后，异步管道标记组件会自行检查。异步管道自动取消订阅，以避免任何潜在的内存泄漏。

让我们看看异步管道的例子:

因此，异步管道的主要优点是我们不需要记住取消订阅 ngOnDestroy 方法中的可观察对象，因为它会自己处理。

## 3.使用 RxJS `take*`运算符

RXJS 确实有一些 take 操作符，可以用来取消订阅 Observables。

*   拿走
*   takeUntil(通知程序)
*   takeWhile(谓语)

## 拿走

该操作符确保订阅发生一次，或者基于数量 **n** 次(基于提到的数量)。

大多数情况下，它与 take(1)一起使用，以确保我们只接收一次可观察值，并在此之后完成。

当我们希望源 Observable 发出一次，然后直接从流中取消订阅时，这个操作符将是有效的。

在上面的例子中，data$在从服务中获得数据的第一个值后将取消订阅。

唯一的问题是，即使我们的组件被破坏，data$也不会退订，直到它获得价值。

因此，最好确保取消 ngOnDestroy 挂钩中的所有内容:

## takeUntil(通知程序)

该操作符发出由源可观察对象发出的值，直到通知者可观察对象发出一个值。

取消订阅可观察对象的一种常用方法是使用 takeUntil 操作符，它会一直等到我们从服务中获得数据。一旦我们得到数据，它将取消订阅数据美元。

当我们有多个订阅时，这种方法有助于只声明一次，并且只需要在 ngOnDestroy 钩子中编写一次代码来取消订阅。

## 4.使用 RxJS `first`运算符

该运算符类似于 take(1)和 takeWhile 的组合

如果它被调用时没有值，那么它将在第一个值时完成。如果用谓词函数调用它，它会发出源可观察对象的第一个值，该值通过了谓词函数的测试条件，并且是完整的。

如果间隔发出第一个值，数据$将完成。

# 5.使用 Decorator 自动退订

我们很有可能会忘记编写代码，或者有任何原因导致我们最终清理订阅。

我们可以创建自己的装饰器，这有助于避免一次又一次地编写代码。

下面是 npm 包名称 unsubscribe all 的一个实现。

【https://www.npmjs.com/package/unsubscribe-all 

通过这样做，我们只需要在每个类中编写 unsubscribe all()decorator，其他事情将由 decorator 负责。

## 6.使用`tslint`

有些可能需要`tslint`的提醒，在控制台中提醒我们，我们的组件或指令应该有一个 ngOnDestroy 方法，当它检测不到时。

我们可以向 tslint 添加一个自定义规则，以便在林挺和构建过程中，如果它在我们的组件中没有发现 ngOnDestroy 挂钩，就在控制台中向我们发出警告:

您可以按照本文来实现 lint 规则。

[](https://blog.bitsrc.io/6-ways-to-unsubscribe-from-observables-in-angular-ab912819a78f) [## 取消订阅 Angular Observables 的 6 种方法

### 回顾了在 Angular 中取消订阅 Observables 的不同方法

blog.bitsrc.io](https://blog.bitsrc.io/6-ways-to-unsubscribe-from-observables-in-angular-ab912819a78f) 

如果我们有这样一个没有 ngOnDestroy 的组件:

林挺 AppComponent 将警告我们丢失的 ngOnDestroy 钩子:

```
$ ng lint
Error at app.component.ts 12: Class name must have the ngOnDestroy hook
```

## 7.子链接

我们可以使用第三方库来实现这些功能。

使用 setter 使用`sink`属性收集订阅的示例。

**参考文献:**

[](https://trungk18.com/experience/angular-common-memory-leak-use-case-observable/) [## 了解并防止 Angular 应用程序中最常见的内存泄漏——订阅…

### TL；DR —记得清理您的 Rx 订阅。以我的经验来看，这是目前记忆最常见的原因…

trungk18.com](https://trungk18.com/experience/angular-common-memory-leak-use-case-observable/) [](https://itnext.io/angular-rxjs-detecting-memory-leaks-bdd312a070a0) [## Angular & RxJS:检测内存泄漏

### 我已经使用 RxJS 构建了一个示例 Angular 应用程序来模拟各种内存泄漏。这些技术中的大多数…

itnext.io](https://itnext.io/angular-rxjs-detecting-memory-leaks-bdd312a070a0) [](https://blog.bitsrc.io/6-ways-to-unsubscribe-from-observables-in-angular-ab912819a78f) [## 取消订阅 Angular Observables 的 6 种方法

### 回顾了在 Angular 中取消订阅 Observables 的不同方法

blog.bitsrc.io](https://blog.bitsrc.io/6-ways-to-unsubscribe-from-observables-in-angular-ab912819a78f) 

## 如果你喜欢并想获得更多这样的内容，请做[订阅](https://medium.com/@patel_ap/membership)

**你可以在这里查看我以前的文章:**

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)