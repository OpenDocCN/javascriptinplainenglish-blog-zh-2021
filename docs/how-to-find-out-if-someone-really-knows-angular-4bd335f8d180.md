# 如何发现某人是否真的了解 Angular

> 原文：<https://javascript.plainenglish.io/how-to-find-out-if-someone-really-knows-angular-4bd335f8d180?source=collection_archive---------1----------------------->

## 5 个高级面试问题

![](img/13e162f4e8d26501af48b962d96a1da0.png)

Photo by [Charles Deluvio](https://unsplash.com/@charlesdeluvio?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

作为企业 Angular 项目的技术负责人，我的职责之一是旁听潜在候选人的面试。招聘人员主要瞄准那些提到“棱角分明”这个词的简历。然而，我和我的团队寻找已经精通流行的 Google 框架的有经验的开发人员。这是我用来帮助揭示一个开发人员是否像他们声称的那样资深的五个问题。

# Angular 中有哪些不同的变化检测策略？

Angular 的前身 AngularJS 的一个常见问题是它通过摘要循环和观察器进行变化检测的策略。这对于较小的应用程序很好，但是随着指令和观察者数量的增加，对这些观察者的不当管理将导致内存泄漏，并使浏览器瘫痪。Angular 对框架进行了彻底的检查，远离了这些概念，并为组件引入了两种不同的[变更检测策略](https://angular.io/api/core/ChangeDetectionStrategy):Default 和 OnPush。

OnPush 是大型应用程序的首选方法，因为它更明确地说明了什么类型的事件将触发变更检测。

*   组件输入已更改
*   组件正在侦听的 DOM 事件被触发
*   异步管道接收到新值
*   已显式触发更改检测(detectChanges，markForCheck)

[](https://blog.angular-university.io/onpush-change-detection-how-it-works/) [## 角度 OnPush 变化检测-避免常见陷阱

### 你有没有尝试过在你的应用中使用 Angular OnPush 变化检测策略，但是遇到了一些很难…

blog.angular-university.io](https://blog.angular-university.io/onpush-change-detection-how-it-works/) [](https://www.tiny.cloud/blog/angular-change-detection-onpush-strategy/) [## 角度变化检测和 OnPush 策略

### 如果你是一个经常使用 Angular 构建应用程序的开发人员，你可能听说过…

www.tiny .云](https://www.tiny.cloud/blog/angular-change-detection-onpush-strategy/) 

这是 Angular 开发人员应该知道的基本主题之一，以防止他们的应用程序做不必要的工作。性能是企业应用的关键，所以如果这不是他们的首要考虑，这可能意味着他们没有太多复杂应用的经验。

# 2)你知道哪些 RxJS 变换运算符，你是如何使用它们的？

Angular 的核心是 RxJS。候选人应该对其可观测量和[管道操作员](https://rxjs.dev/guide/operators#piping)有丰富的经验。tap 和 map 等更常见的操作符应该是已知的，但熟练的开发人员应该对 concatMap、mergeMap、switchMap 或 exhaustMap 等更具挑战性的转换操作符有所了解。有几个教程和博客介绍了它们的区别。

[](https://blog.angular-university.io/rxjs-higher-order-mapping/) [## RxJs 映射:切换映射 vs 合并映射 vs 串联映射 vs 穷举映射

### 我们日常发现的一些最常用的 RxJs 运算符是 RxJs 高阶映射…

blog.angular-university.io](https://blog.angular-university.io/rxjs-higher-order-mapping/)  [## 合并映射 vs 穷举映射 vs 切换映射 vs 串联映射

### 参见 mergeMap(又名 flatMap)、exhaustMap、switchMap 和 concatMap 与大理石图的对比:

thinkrx.io](https://thinkrx.io/rxjs/mergeMap-vs-exhaustMap-vs-switchMap-vs-concatMap/) 

如果候选人可以用一个或多个转换操作符描述真实世界的情况——不像基本的间隔计时器示例——那么他们就有潜力。

# 3)你用过 AsyncPipe 吗，它的主要优点是什么？

Angular 的一个重要方面是处理 [RxJS 订阅](https://rxjs.dev/guide/subscription)。开发人员订阅可观察的对应物通常没有任何问题，但是当不再需要时，没有多少人能够熟练地正确移除它们。已经提出了几种方法来处理这种模式:

*   向订阅数组添加订阅，并在组件销毁时取消订阅每个数组
*   使用单个订阅对象并向其添加子订阅。当组件被销毁时，只需要对父订阅进行一次取消订阅。
*   使用带有 take(1)的管道运算符只订阅一次

所有这些都是有效的，但 Angular 提供的另一个选项是[异步管道](https://angular.io/api/common/AsyncPipe)。AsyncPipe 的要点是，它可以用来订阅一个可观察对象，并且当组件被销毁时会自动**取消订阅。这是一种更好的方法，可以避免您自己去管理订阅。也就是说，考生往往不知道这个技巧，因为它通常不包括在基础教程中。**

# 4)您是否使用过任何状态管理，如果没有，您在组件之间共享数据的其他方式是什么？

状态管理框架对 Angular 来说并不重要，但在开发 Angular 应用程序时，它至少应该是对话的一部分。我们目前使用的是 [NGXS](https://www.ngxs.io/) ，它类似于更流行的框架 [NGRX](https://ngrx.io) ，但是样板代码要少得多。如果开发人员有任何状态管理方面的经验，他们应该能够说出它的主要优势，即组件共享数据的单一来源。

在 Angular 中，组件共享数据更常见的方式是通过组件输入/输出，或者通过使用 RxJS [Subject](https://www.learnrxjs.io/learn-rxjs/subjects/subject) 或 [BehaviorSubject](https://www.learnrxjs.io/learn-rxjs/subjects/behaviorsubject) 类的服务类。这些都是可以接受的方法，但是在这两者之间，服务实现更加优雅，并且利用了非常有用的 RxJS observables。一个有经验的 Angular 开发人员讨论这些策略应该没有问题，但是如果他们能够与状态管理框架对话，那就更好了。

# 5)你做过单元测试吗，你熟悉 Jest 吗？

当利用 Angular CLI 生成 Angular 类时，总是会创建相应的等级库测试文件。这些意味着要详细阐述，并成为代码质量和回归测试的基本要素。开箱即用，Angular 使用 Jasmine 和 Karma test runner，它们足以对你的代码库进行压力测试。这些经验应该是任何 Angular 开发人员的标准。

[](https://jasmine.github.io/) [## Jasmine 文档

### 快速低开销，jasmine-core 没有外部依赖性。包括电池在内的所有产品都是开箱即用的…

茉莉. github.io](https://jasmine.github.io/) [](https://karma-runner.github.io/latest/index.html) [## Karma -壮观的 Javascript 测试运行程序

### 事情应该很简单。我们相信测试，所以我们想让它尽可能简单。因果报应的主要目标…

karma-runner . githum . io](https://karma-runner.github.io/latest/index.html) 

在我们的项目中，我们使用 Jest，它非常优秀。正如他们的文档中提到的，“Jest 附带了`jsdom`，它模拟了一个 DOM 环境，就像你在浏览器中一样。”

[](https://jestjs.io/) [## 笑话🃏愉快的 JavaScript 测试

### Jest 是一个 JavaScript 测试框架，旨在确保任何 JavaScript 代码库的正确性。它允许您…

jet js . io](https://jestjs.io/) 

这迎合了角度代码动态操作 DOM 的测试场景。Jest 随着 [React](https://reactjs.org) 变得更加流行，所以它在 Angular 开发者中并不知名。这是一个非常有用的工具，对于理解代码质量重要性的候选人来说，应该引起注意。

# 结论

我还没有找到一个能回答所有这些问题的候选人，但我也不会说这是一个硬性要求。我的建议是，更多地使用它们作为一种衡量标准，以帮助确定他们对 Angular 有什么样的体验。如果一个开发人员可以用真实的工作经验的例子来回答两到三个问题，那么他们就有潜力。如果他们能回答所有五个问题，那么你就中大奖了——请把他们寄给我。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)