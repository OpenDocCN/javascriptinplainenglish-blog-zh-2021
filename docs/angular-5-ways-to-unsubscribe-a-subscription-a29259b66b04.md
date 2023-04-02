# 通过 5 种方式取消订阅 Angular

> 原文：<https://javascript.plainenglish.io/angular-5-ways-to-unsubscribe-a-subscription-a29259b66b04?source=collection_archive---------5----------------------->

## 取消订阅

在这篇文章中，我们将探索 5 种不同的方法来取消 Angular 的可观察订阅

![](img/a96a01b6d5a2f805b73514ee2abb7ff2.png)

unsubscribing an subscription in Angular

**什么是有角的可观测值？** 可观察的是希望观察并采取行动的事物。Angular 使用观察者模式，这意味着—可观察对象被注册，其他对象观察它们(在 Angular 中使用 subscribe 方法),并在可观察对象以某种方式受到作用时采取行动。
可观察到的东西与承诺相似，但可观察到的东西和承诺之间还是有一些区别的。可观察的在事件发生后继续观察。我们可以在运行时取消观察。而承诺是不能取消的，因为我们只执行承诺一次。
要使用 observable，我们必须从名为**反应式扩展(RxJS)的第三方库中导入它。**

```
import { Observable } from 'rxjs/Observable';
```

**为什么我们需要取消订阅一个可观察的？** 正如我们所知，可观测量是事件，它拥有一些内存，我们需要在订阅发出值后从系统中释放这些内存。
一个可观察的订阅有一个 **unsubscribe()** 函数来释放资源/内存或者取消可观察的执行。

以下是在 Angular 中订阅的 4 种不同方式

**方法 1:通过使用 Unsubscribe 方法** Angular 已经公开了一个生命周期钩子 **ngOnDestroy()，**，它在组件被销毁之前被调用。我们可以通过调用 **unsubscribe()** 方法，用 **ngOnDestroy()** 生命钩子来清理订阅。请查看下面的例子:

```
import { Component,OnInit,OnDestroy } from ‘[@angular/core](http://twitter.com/angular/core)’;
import {Subscription} from ‘rxjs’;[@Component](http://twitter.com/Component)({
 selector: ‘app-root’,
 templateUrl: ‘./app.component.html’,
 styleUrls: [‘./app.component.scss’]
})
export class AppComponent implements OnInit, OnDestroy {
 $subscription: Subscription 
 ngOnInit () {
 var observable = Rx.Observable.interval(1000);
 this.$subscription = observable.subscribe(x => console.log(x));
 }
 ngOnDestroy() {
 this.$subscription.unsubscribe()
 }
}
```

在上面的例子中，如果你看到我们已经创建了 **$subscription** 对象，并且在 **ngOnDestroy()中调用了 **unsubscribe()** 方法。**如果您有多个订阅，那么您必须在 **ngOnDestroy()中调用 unsubscribe()方法两次。**请看下面的例子:

```
import { Component,OnInit,OnDestroy } from ‘[@angular/core](http://twitter.com/angular/core)’;
import {Subscription} from ‘rxjs’;
[@Component](http://twitter.com/Component)({
 selector: ‘app-root’,
 templateUrl: ‘./app.component.html’,
 styleUrls: [‘./app.component.scss’]
})
export class AppComponent implements OnInit, OnDestroy {
 $subscriptionOne: Subscription
 $subscriptionTwo Subscription 
 ngOnInit () {
 var observable = Rx.Observable.interval(1000);
 this.$subscriptionOne = observable.subscribe(x => console.log(x));
 this.$subscriptionTwo = observable.subscribe(x => console.log(x));
 }
 ngOnDestroy() {
 this.$subscriptionOne.unsubscribe();
 this.$subscriptionTwo.unsubscribe();
 }
}
```

我们可以将所有的订阅聚集在一个数组中，然后逐个取消订阅()。请参见下面的例子:

```
 import { Component,OnInit,OnDestroy } from ‘[@angular/core](http://twitter.com/angular/core)’;
import {Subscription} from ‘rxjs’;
[@Component](http://twitter.com/Component)({
 selector: ‘app-root’,
 templateUrl: ‘./app.component.html’,
 styleUrls: [‘./app.component.scss’]
})
export class AppComponent implements OnInit, OnDestroy {
 $subscriptionOne: Subscription;
 $subscriptionTwo Subscription;
 $subscriptions: Subscription[] = [] 
 ngOnInit () {
 var observable = Rx.Observable.interval(1000);
 this.$subscriptionOne = observable.subscribe(x => console.log(x));
 this.$subscriptionTwo = observable.subscribe(x => console.log(x));
 this.subscriptions.push(this.$subscriptionOne)
 this.subscriptions.push(this.$subscriptionTwo)
 }
 ngOnDestroy() {
 this.subscriptions.forEach((subscription) => subscription.unsubscribe())
 }
}
```

在上面的例子中，我们有多个订阅()。我们将它们存储在一个 subscription()数组中，并在 ngOndestroy()中逐个取消订阅()，如上例所示。
RxJs Observables subscribe()方法返回 RxJs 的订阅类型的对象。
该订购代表可任意使用的资源。我们可以使用 subscription()的 add()方法将它们分组。add()
方法会将一个子订阅附加到当前订阅。当您取消订阅()某个订阅时，它的所有子代都将被取消订阅。

**方法 2:通过使用异步** '|' **管道** **aysnc**管道是一个不纯的管道，它从它发出的可观察或承诺返回最新的值。当发出新值时，异步管道标记要检查的组件。当组件被破坏时，异步管道也取消订阅。请参见下面的例子:

```
import { Component,OnInit,OnDestroy } from ‘[@angular/core](http://twitter.com/angular/core)’;
import {Subscription} from ‘rxjs’;
[@Component](http://twitter.com/Component)({
 selector: ‘app-root’,
 styleUrls: [‘./app.component.scss’]
 template: `
 <div>
 Interval: {{observable$ | async}}
 </div>
 `
})
export class AppComponent implements OnInit {
 observable$
 ngOnInit () {
 this.observable$ = Rx.Observable.interval(1000);
 }
}
```

**方法 3:通过使用 RxJs take*运算符** 我们可以使用 RxJs **take*** 族运算符来取消订阅()angular 项目中的一个 subscriptons。以下是我们可以用来取消订阅 RxJs 订阅的 take*系列运算符:

1.  **取(n)运算符:**

取(n)个操作符执行' **n** '次源订阅排放。take(n)运算符将在我们传递 1 时生效，它将只执行一个源订阅发射并取消订阅。

在下面的例子中，我们将 1 传递给了 take(n)操作符，它将只执行一次源订阅，并在执行后取消订阅。

一旦发出第一个值，订阅将被取消订阅，即使在 app-component 被销毁后，订阅也不会被销毁。所以建议用**ngOnDestory()**life hooks 退订订阅。

```
[@Component](http://twitter.com/Component)({
selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']

})
export class AppComponent implements OnInit {
    subscription$
    ngOnInit () {
        var observable$ = Rx.Observable.interval(1000);
        this.subscription$ = observable$.pipe(take(1)).
        subscribe(x => console.log(x))
     }
}
```

**方法 4:通过使用自定义装饰器**

我们可以创建一个自定义装饰器来自动取消订阅 Angular 应用程序。请看下面的例子，我写了 **ngUnsub()** 自定义指令来取消订阅 Angular 应用程序。它保存 **ngonDestroy()** 并将其添加到类中。当一个类将要销毁时，它将扫描订阅。如果存在任何订阅，它将销毁所有订阅。

```
function ngUnsub() {
    return function(constructor) {
        const _autoUnsub = constructor.prototype.ngOnDestroy
        constructor.prototype.ngOnDestroy = function() {
            for(const prop in this) {
                const ngprop = this[prop]
                if(typeof ngprop.subscribe === "function") {
                    ngprop.unsubscribe()
                }
            }
            _autoUnsub.apply()
        }
    }
}[@ngUnsub](http://twitter.com/ngUnsub)()
[@Component](http://twitter.com/Component)({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})
export class AppComponent implements OnInit {
    observable$
    ngOnInit () {
        this.observable = Rx.Observable.interval(1000);
        this.observable$.pipe(first())
        .subscribe(x => console.log(x));
    }
}
```

**方法 5:通过使用 TS lint** 我们可以通过向 TS lint 添加一个自定义规则来清理订阅，如果 ngOnDestroy() lifehooks 没有添加到组件中，我们会警告用户。

```
// ngOnDestroyRule.tsimport * as Lint from "tslint"import * as ts from "typescript"import * as tsutils from "tsutils"export class Rule extends Lint.Rules.AbstractRule {public static metadata: Lint.IRuleMetadata = {ruleName: "ng-on-destroy",description: "Give Warning ngOnDestory hook on a ts classes",optionsDescription: "ngOnDestroy",options: null,type: "style",typescriptOnly: false}public static WARNING_STRING = "ngOnDestroy should be present in a ts class";public apply(sourceFile: ts.SourceFile): Lint.RuleFailure[] {return this.applyWithWalker(new NgOnDestroyWalker(sourceFile, Rule.metadata.ruleName, void this.getOptions()))}}class NgOnDestroyWalker extends Lint.AbstractWalker {visitClassDeclaration(node: ts.ClassDeclaration) {this.validateMethods(node)}validateMethods(node: ts.ClassDeclaration) {const methodNames = node.members.filter(ts.isMethodDeclaration).map(m => m.name!.getText());const ngOnDestroyArr = methodNames.filter(methodName => methodName === "ngOnDestroy")if (ngOnDestroyArr.length === 0)this.addFailureAtNode(node.name, Rule.WARNING_STRING);}}
```

在上面的例子中，我们已经创建了一个定制的 tslint 规则，如果 Angular 中的组件/指令/管道中没有 ngOnDestroy()生命挂钩，它将抛出一个异常。
如果我们有一个角度组件类，并且不存在 ngOnDestroy() lifehooks，那么将抛出 below lint 错误。

```
$ ng lint
Error at app.component.ts 12: ngOnDestroy should be present in a ts class
```

***在本文中，我们讨论了在 Angular 应用中取消订阅的不同方式，以及如何在订阅执行后释放内存。***

***亲爱的读者，感谢您的支持和您宝贵的时间。我希望这是有用的，并有助于发现角度应用的基础。如果你喜欢这篇文章并在评论中留下你的想法，请鼓掌。***

***请关注我并成为会员上*** [***中***](https://medium.com/@technicadil_001/membership) ***获取更多文章。干杯！***

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，*[*不和*](https://discord.gg/GtDtUAvyhW) ***。***

***有兴趣缩放你的软件启动*** *？检查出* [***电路***](https://circuit.ooo/?utm=publication-post-cta) *。*