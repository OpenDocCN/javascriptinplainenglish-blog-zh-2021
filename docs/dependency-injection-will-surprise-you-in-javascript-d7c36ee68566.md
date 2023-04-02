# JavaScript 中的依赖注入会让你大吃一惊

> 原文：<https://javascript.plainenglish.io/dependency-injection-will-surprise-you-in-javascript-d7c36ee68566?source=collection_archive---------12----------------------->

## JavaScript 让事情变得不同，通常，要意识到这些不同

![](img/2eec6f6cf92cbfe0d22a1ddf8f059812.png)

[Sam Moqadam](https://unsplash.com/@itssammoqadam) via [Unsplash(CC0)](https://unsplash.com/photos/l9VjM-Pp7-M)

如果你打算用 C#或 Java 这样的面向对象编程语言来开发你的软件。总有一天，你必须考虑对元件进行去耦。打开谷歌搜索引擎，最终，你会发现一个术语叫做依赖注入，简称 DI。[1] [2]

# 为什么要使用依赖注入？

一个典型的例子是在现有的编码项目中必须改变的记录器或数据库组件。很明显，您希望尽可能少地做这件事，并且不愿意调整旧组件的实现来适应新组件。

通常，当组件完成相同的任务时，你可以很容易地改变它们，而不需要太多的努力来适应现有的代码库。但真正的问题是:

我/我们需要修改多少代码？

我打赌你过去听说过双容器。那是我们正在寻找的术语。他们负责基础的配置。管理依赖关系并将信息分发给每个请求者。

简单总结一下这个概念:这种技术用于使类独立于它们的依赖关系。在 C#中，你用新的操作符*创建一个对象。如果类 A 依赖于类 B，它通过调用构造函数并结合类 B 的 *new* 操作符来创建这个类。想象类 B 的状态被类 A 改变，而类 C 进入游戏。
C 类也需要 B 类的一个实例，如果已经创建了 B 的实例，C 如何获得 B 的实例？A 会创建 C 并传入已经创建的实例吗？C 是否创建了另一个实例？C 需要 B 的实例的改变后的状态吗？*

你意识到我们在这里遇到了麻烦。

因此，DI 使您能够替换依赖项，而不必改变使用它们的类。它还能够降低仅仅因为一个类的依赖关系发生变化而导致该类发生变化的风险。[3]

但真正的问题是:**JavaScript 有依赖注入的能力吗？**

# JavaScript 和依赖注入

![](img/b1d3033393fddf1a2491fcddd7cd75e3.png)

[Greg Rakozy](https://unsplash.com/@grakozy) via [Unsplash (CC0)](https://unsplash.com/photos/vw3Ahg4x1tY)

更改组件意味着定义一个接口来指定两个组件之间的交互契约。拥有接口意味着创建从接口推断的对象。当像这样而不是用具体的类编码时，您就达到了可交换性的点，因为两个组件都必须满足接口的契约，并且最终是可交换的。这意味着 DI 通过依赖契约(接口)而不是具体的类，将具体的类从依赖中分离出来。[3]

要做到这一点，你所使用的语言必须支持强类型系统，并允许你使用接口。成功的关键是在不知道具体类型的情况下请求契约(接口),以获得我们正在寻找的可互换性。

C#做到了，但是 JavaScript 呢？

这两个需求在 JavaScript 中都是半生不熟的。由于 ECMAScript 2015 是两个可用的关键字:*类*和*扩展*。但是与真正的面向对象相比，它们都不是一回事。隐藏 JavaScript 基于原型的继承更像是语法上的糖。

即使你要把这算作面向对象，JS 也没有接口。这导致了无法在 JavaScript 中进行面向对象的依赖注入的结论。

# 有解决办法吗？

如果我们不能在 JavaScript 中使用真正的依赖注入，我们应该首先考虑 DI 的背景和它所解决的问题。它解决了面向对象语言中由于使用静态类型系统而存在的问题。JavaScript 使用动态类型系统。[4]

依赖注入通常为类的可交换性建立基础，并通过接口来描述。这意味着每个传递给方法的对象都必须履行接口的契约，否则，程序就会崩溃。接口确保了契约和对象的完整性。
在 JavaScript 中把一个对象传入一个函数，调用那个对象的一个不存在，但应该到的函数，不会给我们带来崩溃。如果这个函数存在，它就被调用；如果不存在，这个调用就无效。

更进一步，JavaScript 不关心被传入对象的其他功能。只要满足所需的功能。我们称之为*鸭子打字*。[5]

> 当我看到一只像鸭子一样走路、像鸭子一样游泳、像鸭子一样嘎嘎叫的鸟时，我就把那只鸟叫做鸭子。— [詹姆斯·惠特科姆·雷利斯](https://de.wikipedia.org/wiki/James_Whitcomb_Riley)

因为这不是 JavaScript 中的一种方式，所以引用被大量转换为:

> 当我看到一只叫起来像鸭子的鸟看起来像狗，走路像猫的时候，我把那个叫做 JavaScript。—俗语

因此，您只需将一个匹配的对象传递给一个需要的组件，例如，一个日志记录器，只要它与任务匹配，它是否正式匹配预期的契约并不重要。因为 JavaScript 中的对象除了对象之外没有类型，因为缺少静态类型系统，所以它们不能匹配。

JavaScript 的这一特性使测试变得容易得多，因为您可以专门为手头的用例构造存根和模拟，而不需要依赖正式的系统，也不需要相应复杂的工具来这样做。

# 有没有实现依赖注入的方法？

当然，这留下了如何配置整个事情的问题——如何用 JavaScript 实现用 C#和阿迪容器解决的任务。一种简单的方法是将它需要的依赖项的函数作为参数传递，或者将组件注册在一个中心位置，然后可以从那里检索它们。这大致相当于服务定位器的开始，这在面向对象编程中经常被认为是一种不受欢迎的编码方式。最后，更简单、更实用的解决方案代表了经常被过度开发的 DI 容器。亲吻原则再次适用于此。

[](https://medium.com/next-level-source-code/do-you-follow-these-10-principles-for-good-programmers-1445727af447) [## 你遵循了优秀程序员的这 10 条原则吗？

### 从接吻和干燥到足球和 YAGNI 和聪明屁股代码的 10 个原则！

medium.com](https://medium.com/next-level-source-code/do-you-follow-these-10-principles-for-good-programmers-1445727af447) 

## 结构

![](img/94b8652e5a3d6b48d033bdf5ea10e467.png)

[Pat Whelen](https://www.pexels.com/@pat-whelen-2913248) via [Pexels (CC0)](https://www.pexels.com/photo/wood-light-city-sky-5579612/)

在 JavaScript 中，您有几个选项。 [Angular](https://angular.io/) 框架试图在这里模拟一个类似的构造，但是这需要惊人的(或者令人害怕的)高度复杂性和努力。它全部内置在 Angular 的[模块系统](https://angular.io/api/core/NgModule)中。当你启动你的应用程序时，你的根模块连接你在整个应用程序中需要的依赖关系，并允许你将一些依赖关系解析推迟到[功能模块](https://angular.io/guide/feature-modules)。在测试它们的时候，你可以用一个[测试床](https://angular.io/api/core/testing/TestBed)做同样的事情(这只是一个小规模的模块)，只提供运行测试所需的依赖关系。[6]

如果 Angular 不是你的菜或者你根本用不上它，还有一个框架叫做 [InversifyJS](https://inversify.io/) 。它提供了一种不同的方式来配置您的依赖项，但控制级别相同。[7]

为 DI 使用一个框架是一件好事，因为您可以减少需要编写的样板文件的数量。框架还支持您以更少的努力维护您的代码。

# 结论

依赖注入解决了静态类型、面向对象语言中的一个问题，如果它们不是静态类型系统，这个问题就不会存在。这个概念不是一个不惜任何代价实现的价值。通常情况下，最好先熟悉 JavaScript 语言，然后在适合自己的时候使用它——而不是采用 C#或其他语言中已知的模式，或多或少地一对一，期望两个世界以相同的方式工作。

## 进一步阅读

[](https://medium.com/next-level-source-code/naming-variables-and-methods-write-better-code-part-2-5707e54250f1) [## 命名变量和方法—编写更好的代码第 2 部分

### 如何编写表达自己的代码，以便更好地使用命名进行编码

medium.com](https://medium.com/next-level-source-code/naming-variables-and-methods-write-better-code-part-2-5707e54250f1) [](https://arnoldcode.medium.com/increase-annual-salary-with-these-3-simple-tactics-145f8bc03c60) [## 用这三个简单的策略增加年薪

### 成为他们梦寐以求的汽车！

arnoldcode.medium.com](https://arnoldcode.medium.com/increase-annual-salary-with-these-3-simple-tactics-145f8bc03c60) [](https://medium.com/agileinsider/comparison-of-scrum-vs-scrumban-vs-kanban-1d1d2b9a9fd5) [## Scrum、Scrumban 和看板的比较

### 挑选合适产品的快速指南！

medium.com](https://medium.com/agileinsider/comparison-of-scrum-vs-scrumban-vs-kanban-1d1d2b9a9fd5) 

# 参考

[1][https://stack overflow . com/questions/130794/what-is Dependency-injection](https://stackoverflow.com/questions/130794/what-is-dependency-injection)
【2】[https://stack overflow . com/questions/14301389/why-does-one-use-Dependency-injection/14301816](https://stackoverflow.com/questions/14301389/why-does-one-use-dependency-injection/14301816)
【3】[https://stack ify . com/Dependency-injection/#:~:text = Dependency % 20 injection % 20 is&text = That % 20 enables % 20 you % 20 to % 20 replace，one % 20 of % 20 its % 20 dependencies % 20 changed](https://stackify.com/dependency-injection/#:~:text=Dependency%20injection%20is%20a%20programming,class%20independent%20of%20its%20dependencies.&text=That%20enables%20you%20to%20replace,one%20of%20its%20dependencies%20changed)。
【4】[https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Data _ structures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)
【5】[https://www . html goodies . com/beyond/JavaScript/duck-Typing-In-JavaScript . html #:~:text = In % 20 duck % 20 Typing % 2C % 20 an % 20 objects，键入% 20 for % 20 our % 20
【6】](https://www.htmlgoodies.com/beyond/javascript/duck-typing-in-javascript.html#:~:text=In%20Duck%20Typing%2C%20an%20object's,Typing%20for%20our%20own%20objectives)[https://angular.io/](https://angular.io/)
【7】[https://inversify.io/](https://inversify.io/)