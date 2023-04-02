# 为赢得下一次面试，你必须准备的 100 个问题(30-40)

> 原文：<https://javascript.plainenglish.io/top-100-questions-you-must-prepare-for-to-ace-your-next-angular-interview-30-40-6f195ed91de?source=collection_archive---------7----------------------->

## Angular 2021 面试问题

## 最常见的角度面试问题 2021

![](img/1291ea03b8bb92a2826f569ddf7ec23c.png)

Photo by [Christina @ wocintechchat.com](https://unsplash.com/@wocintechchat?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

最近，我试图为即将到来的面试做准备，在谷歌上搜索并打开链接却每次都看到相同的问题，这有点困难。所以，我想到了分享我的发现，以及如果一个人准备面试，他应该知道的最常见的问题是什么。

以下是最新角度面试中最常被问到的面试问题。这些有角度的面试问题和答案帮助有角度的开发人员准备从初级到高级的面试。此外，这篇文章涵盖了你在 2021 年必须准备的基本问题。

# 如果你错过了 1-10 个问题，请查看这篇文章。

[](/top-100-questions-you-must-prepare-for-your-next-angular-interview-1-10-3e13d5fefab9) [## 你必须为下一次角度面试准备的 100 个问题(1-10)

### 最常见的角度面试问题 2021

javascript.plainenglish.io](/top-100-questions-you-must-prepare-for-your-next-angular-interview-1-10-3e13d5fefab9) 

# 如果你错过了 10-20 个问题，请查看这篇文章。

[](/top-100-questions-you-must-prepare-for-to-ace-your-next-angular-interview-10-20-c3f5ab854be) [## 为赢得下一次面试，你必须准备的 100 个问题(10-20)

### 最常见的角度面试问题 2021

javascript.plainenglish.io](/top-100-questions-you-must-prepare-for-to-ace-your-next-angular-interview-10-20-c3f5ab854be) 

# 31.解释 Angular 中支持的不同防护装置。

这是角度应用中最常见的问题之一。

在 angular 有五个主要的守卫。它守卫着道路的入口。

*   `CanActivate`:会在去路由之前调用:*可以用来阻止路由到特定路径*
*   `CanActivateChild`:在转到子组件之前会被调用:*可以用来阻止子路径*的加载
*   `CanDeactivate`:在销毁组件之前会被调用:*可以用来处理浏览器事件*
*   `CanLoad`:在模块加载前调用:*可以用来阻止模块*的加载
*   `Resolve`:加载组件前调用:*可用于加载组件前预取数据*

***为了更好地理解这个概念，我们来检查一下实际代码。***

[https://stackblitz.com/edit/route-guard](https://stackblitz.com/edit/route-guard)

要了解实现，请参阅本文

[](https://medium.com/@ryanchenkie_40935/angular-authentication-using-route-guards-bf7a4ca13ae3) [## 角度认证:使用路由保护

### Angular 附带了许多内置特性，对处理身份验证非常有帮助。我想我的…

medium.com](https://medium.com/@ryanchenkie_40935/angular-authentication-using-route-guards-bf7a4ca13ae3) 

# 32.懒得加载组件的最好方法是什么？

当我们想要减少包的大小并避免一起加载所有模块时，延迟加载模块是最佳实践之一。

但是惰性加载组件呢？这意味着我们加载模块，但不加载组件，直到我们需要它们。它基本上根据需要创建动态组件，并在使用后立即销毁。

***让我们通过检查实际代码来更好地理解这个概念。***

[https://stackblitz.com/edit/ivy-lazy-loading-component](https://stackblitz.com/edit/ivy-lazy-loading-component)

下面的文章解释了我们如何在 angular 中延迟加载组件。

[](https://medium.com/angular-in-depth/lazy-load-components-in-angular-596357ab05d8) [## 以角度表示的惰性负载分量

### 用 Ivy 和 Angular 9 延迟加载 Angular 组件

medium.com](https://medium.com/angular-in-depth/lazy-load-components-in-angular-596357ab05d8) 

# 33.我们有什么办法可以用 Angular 显示 app 版本？

当我们处理大量部署时，最好显示应用程序版本，这有助于团队之间就变更进行沟通。

可以通过以下步骤实现。

1.  打开`/tsconfig.json`使 resolveJsonModule 为真。

```
"compilerOptions": {
      ...
      "resolveJsonModule": true
      ...
```

然后在组件中我们可以使用版本。

```
import { version } from '../../package.json';
    ...
    export class AppComponent {
      public version: string = version;
    }
```

也可以在您的 environment.ts 文件中执行步骤 2，这样就可以从那里访问版本信息。

# 34.ES6 中的发电机有哪些？

检验你的 ES6 技能的最佳问题之一。发电机有什么实际用途？

生成器可用于多次暂停和恢复。

它主要用于处理用户一次又一次点击查找按钮的查找场景，如果有多个搜索结果，用户可以一个接一个地移动到不同的记录。

默认情况下，生成器是异步的。

***为了更好地理解这个概念，我们来检查一下实际代码。***

[https://stackblitz.com/edit/es6-generators](https://stackblitz.com/edit/es6-generators)

# 35.解释应用程序中的错误机制。

所有应用程序都有其全局错误机制来处理错误并将其记录在 Splunk 或 new relic 上。团队的大多数成员都遵循全局错误机制，该机制会记录是否有任何问题出现，以便进行跟踪，并将用户重定向到特定的路线。

***为了更好地理解这个概念，我们来检查一下实际代码。***

[https://stackblitz.com/edit/global-error-handler](https://stackblitz.com/edit/global-error-handler)

如果你想了解我们如何实现全局错误机制，请查看这篇文章。

[](https://medium.com/angular-in-depth/expecting-the-unexpected-best-practices-for-error-handling-in-angular-21c3662ef9e4) [## 期待意外 Angular 中错误处理的最佳实践

### "期待意想不到的事情显示了完全现代的智慧."——奥斯卡·王尔德

medium.com](https://medium.com/angular-in-depth/expecting-the-unexpected-best-practices-for-error-handling-in-angular-21c3662ef9e4) 

# 36.angular 中的自举是什么？

大多数时候，当我们想到这个词的时候，我们会想到一个自举库，但自举不是初始化或加载我们的 Angular 应用程序的技术。

有时候面试官会问角度应用如何加载，或者一开始就解释角度应用加载。让我们检查一下答案。

**Angular 采取以下步骤加载我们的第一个视图。**

1.  Main.ts 应用程序入口点
2.  Index.html 负载
3.  角度、第三方库和应用程序负载
4.  应用模块
5.  应用程序组件
6.  app-root 将在其中添加组件 HTML

欲知详情见下文。

[https://www . tektutorialshub . com/angular/angular-Bootstrapping-application/#:~:text = Bootstrapping % 20 is % 20a % 20 technique % 20 of，to % 20 load % 20 our % 20 first % 20 view](https://www.tektutorialshub.com/angular/angular-bootstrapping-application/#:~:text=Bootstrapping%20is%20a%20technique%20of,to%20load%20our%20first%20view)。

# 37.什么是角元素？我们为什么使用它？

随着 Angular 的成长，它有了非常好的特性。如果你听说过微服务架构使应用程序更加健壮，Angular 也在做同样的事情。

使用 angular 元素，我们可以将 Angular 应用程序即插即用到其他前端框架。

[](https://netbasal.com/understanding-the-magic-behind-angular-elements-8e6804f32e9f) [## 🎩理解棱角元素背后的魔力

### 角形腹板部件

netbasal.com](https://netbasal.com/understanding-the-magic-behind-angular-elements-8e6804f32e9f) 

> 让我们继续回答更多的问题。

# 38.箭头函数和常规函数有什么区别？

我见过面试官开始问一些基本的 JavaScript 问题来测试应聘者的知识。

**候选人:**我知道箭头函数的语法比较简单，而常规函数的语法比较复杂。

面试官大多了解水有多深:)

**回答:**

***1。参数绑定*** :

箭头函数不支持参数绑定，而常规函数支持参数绑定(但是我们可以使用 spread 运算符在箭头函数中添加参数)

**②*。*本关键词:**

箭头函数不支持该关键字，而常规函数有自己的关键字支持。这个特性使得常规的函数使用工厂方法来创建对象。

***3。新增关键词:***

使用函数声明创建的常规函数是可构造的，并且可以使用 new 关键字调用。然而，箭头函数只能被调用而不能被构造，也就是说，箭头函数永远不能被用作构造函数。

***4。重复参数:***

常规函数允许重复参数，而箭头函数不允许重复参数。

# 39.函数式编程语言和面向对象编程语言的区别是什么？你更喜欢哪一个，为什么？

我见过一些面试官开始问这种问题，以获取求职者关于他们目前正在从事的编程语言的知识。

![](img/03b66457d542a6a23a6c2f862625bb95.png)

geeksforgeeks

函数式编程的优势和特点是:

*   **纯函数**
*   **功能组成**
*   **避免共享状态**
*   **避免突变状态**
*   **提供高阶函数**

# 40.JavaScript 和 TypeScript 有什么区别？

候选人:TypeScript 是 JavaScript 的超集。

我看到大多数候选人的答案很简单，因为他们不知道 angular 为什么使用 typescript 的许多优点。

你可以在这里找到最好的解释。

[https://www . geeks forgeeks . org/difference-between-TypeScript-and-JavaScript/#:~:text = TypeScript % 20 is % 20 known % 20 as % 20 object，JavaScript % 20 is % 20a % 20 scripting % 20 language。&text = TypeScript % 20 gives % 20 support % 20 for % 20 modules，JavaScript % 20 does % 20 not % 20 have % 20 interface](https://www.geeksforgeeks.org/difference-between-typescript-and-javascript/#:~:text=TypeScript%20is%20known%20as%20Object,JavaScript%20is%20a%20scripting%20language.&text=TypeScript%20gives%20support%20for%20modules,JavaScript%20does%20not%20have%20Interface)。

**使用 TypeScript 优于 JavaScript 的优势**

*   TypeScript 总是在运行时给出编译错误，因此在部署之前解决这个问题更容易
*   TypeScript 支持静态类型，这允许在编译时检查类型正确性。

# 第 1 部分是(1-10)个问题和答案

[](/top-100-questions-you-must-prepare-for-your-next-angular-interview-1-10-3e13d5fefab9) [## 你必须为下一次角度面试准备的 100 个问题(1-10)

### 最常见的角度面试问题 2021

javascript.plainenglish.io](/top-100-questions-you-must-prepare-for-your-next-angular-interview-1-10-3e13d5fefab9) 

# 第二部分是(10-20)个问题和答案

[](/top-100-questions-you-must-prepare-for-to-ace-your-next-angular-interview-10-20-c3f5ab854be) [## 为赢得下一次面试，你必须准备的 100 个问题(10-20)

### 最常见的角度面试问题 2021

javascript.plainenglish.io](/top-100-questions-you-must-prepare-for-to-ace-your-next-angular-interview-10-20-c3f5ab854be) 

# 第 3 部分是(20-30)个问题和答案

[](/top-100-questions-you-must-prepare-for-to-ace-your-next-angular-interview-20-30-5121828b4f91) [## 要在下一次面试中胜出，你必须准备的 100 个问题(20-30)

### 最常见的角度面试问题 2021

javascript.plainenglish.io](/top-100-questions-you-must-prepare-for-to-ace-your-next-angular-interview-20-30-5121828b4f91) 

# 第 4 部分是(30-40)个问题和答案

[](/top-100-questions-you-must-prepare-for-to-ace-your-next-angular-interview-30-40-6f195ed91de) [## 为赢得下一次面试，你必须准备的 100 个问题(30-40)

### 最常见的角度面试问题 2021

javascript.plainenglish.io](/top-100-questions-you-must-prepare-for-to-ace-your-next-angular-interview-30-40-6f195ed91de) 

# 其余的问题如下，我将在下一篇文章中提供答案。

1.  constructor 和 ngOnInit 有什么区别？
2.  组件和指令有什么区别？
3.  ElementRef、TemplateRef 和 viewContainerRef 有什么区别？
4.  ng-content、ng-template、ng-container 有什么区别？
5.  视图子级和内容子级的区别是什么？
6.  组件视图、主体视图和嵌入视图之间有什么区别？
7.  去抖时间和油门时间有什么区别？
8.  forEach 和 map 有什么区别？
9.  ng-content 和 ng-templateoutlet 有什么区别？
10.  forchild 和 forroot 有什么区别？
11.  为什么我们在 RXJS 中使用管道操作符。有什么用？
12.  在 Angular 应用程序中使用异步管道和订阅函数有什么区别？
13.  承诺和可观察的区别是什么？
14.  事件发射器和主体有什么区别？
15.  可观察和主体有什么区别？
16.  激活的路由和激活的路由快照有什么区别？
17.  讨论在您的角度应用中使用的不同类型的加载策略。
18.  什么是元数据？
19.  routerlinkActive 有什么用途？
20.  我们在 Angular 中使用泛型。
21.  外卡路线是什么？
22.  ngIf 和 hidden 有什么区别？
23.  什么是路由器插座？
24.  路由器状态是什么？
25.  什么是活动路由？
26.  以角度解释不同的注入。
27.  在 angular 中实现翻译的最好方法是什么？
28.  解释角度的不同布线参数。
29.  什么是 Angular 中的虚拟卷轴？
30.  路由参数和查询参数有什么区别？
31.  解释 Angular 中支持的不同防护装置。
32.  哪些 RXJS 运算符用于转换或操作数据？
33.  延迟加载组件的最佳方式是什么？
34.  我们有什么办法可以用 Angular 显示 app 版本？
35.  ES6 中的发电机有哪些？
36.  解释应用程序中的错误机制。
37.  angular 中的自举是什么？
38.  什么是角元素？我们为什么使用它？
39.  箭头函数和常规函数有什么区别？
40.  函数式编程语言和面向对象编程语言的区别是什么？你更喜欢哪一个，为什么？
41.  JavaScript 和 TypeScript 有什么区别？
42.  你对闭包了解多少？
43.  模板驱动表单和反应式表单有什么区别？
44.  Angular 中有哪些不同类型的绑定？
45.  您最常用哪些 RXJS 操作符来处理 HTTP 服务？
46.  mergemap/switchmap/concatmap 和 exhaustmap 有什么区别，我们可以在哪里使用它们？
47.  在 Angular 中讨论不同的装饰者。
48.  用 Angular 解释不同的生命周期方法。
49.  解释角度生命周期挂钩的层次。
50.  渲染器 2 是什么？
51.  渲染器和 ElementRef 有什么区别？
52.  Zone.js 是什么？
53.  Angular 中的竞争条件是什么？
54.  Angular 中的回调、承诺和异步/等待是什么？
55.  Angular 中的主机绑定和主机侦听器是什么？
56.  Angular 中的依赖注入是什么？
57.  以角度解释摘要周期/变化检测周期。
58.  markForCheck 和 detectchanges 有什么区别？
59.  克隆对象的方法有哪些？
60.  解释 Angular 应用程序如何加载/初始化。
61.  当一个 [@Input](http://twitter.com/Input) ()值发生角度变化时，如何检测非原语类型数据？
62.  Angular 中有哪些不同的封装策略？
63.  Angular 中的暗影 DOM 是什么？
64.  解释 Angular 中不同类型的指令。
65.  退订可观测的最好方法是什么？
66.  什么是有角度的语言服务？
67.  Angular 的 canLoad 和 canActivate 的区别？
68.  如何检查路线角度是否改变？
69.  用 Angular 解释不同的路由器事件。
70.  触发角度变化检测的手动方式有哪些？
71.  从角度讨论不同的管道。
72.  你在 Angular 中遵循的最佳安全实践是什么？
73.  提高角度性能的最佳方法是什么？
74.  你处理过检查错误后发生变化的表达式吗？
75.  如果已经加载了一个模块，该如何处理？
76.  你在 Angular 中创建了自定义库吗？
77.  你在应用中分析内存的方法有哪些？
78.  用 Angular 解释不同的路由器事件？
79.  Angular 中的数据类型有哪些？
80.  优化异步验证器的最好方法是什么？
81.  Angular 中的 Enums 是什么？
82.  JavaScript 中的 find 和 filter 有什么区别？
83.  防止在 Angular 中点击按钮时出现多个服务呼叫。
84.  如何在 Angular 中的组件之间传递数据？
85.  (change)和(ngModelChange)有什么区别？
86.  声明、提供者和导入之间有什么区别？
87.  如何在角元件库(比如角材)中覆盖 CSS？
88.  如何将组件中的字符串动态绑定到 HTML？
89.  如何在同一个元素上设置 ngFor 和 ngIf？
90.  你能举一个内置验证器的例子吗？
91.  什么是入门组件？
92.  什么是有角度的可观察和观察者？
93.  Angular 里的服务人员是什么？
94.  如何在 Angular 中用最新版本更新所有库？
95.  什么是拦截器？您如何配置您的应用程序/
96.  解释你的 Angular 应用的架构。
97.  解释一些你最常用的测试角度组件的方法。
98.  你在应用中使用了哪些不同的 SCSS 函数？
99.  OnPush 和默认变更检测有什么区别？
100.  如何将数据绑定到模板？
101.  takeWhile 和 takeUntil RXJS 运算符有什么区别？
102.  behavior Subject/Subject/replay Subject 和 Async Subject 有什么区别？
103.  解释 ng-temple、ng-content、ng-container 和 ng-templateOutlet 的实际用法。
104.  为什么我们在 route 中使用 forchild 和 forroot 方法？它的用法是什么？
105.  如何将所有角度库更新到最新版本？
106.  Angular 中的内容投影是什么，它是如何工作的？
107.  Angular 中的 APP _ INITILIZER 是什么，是用来做什么的？
108.  解释角度应用中的路由重用策略。
109.  Angular 中的服务器端渲染是如何工作的？
110.  Angular 里的服务人员是什么？如何使用它们？

# 请在评论中提供您的反馈，如果您想优先考虑一些问题。

# 如果你通过鼓掌和评论来支持我，我会带着接下来的 40-50 个问题来。

# 我真的需要你的帮助来获得动力。

*更多内容看*[***plain English . io***](http://plainenglish.io/)