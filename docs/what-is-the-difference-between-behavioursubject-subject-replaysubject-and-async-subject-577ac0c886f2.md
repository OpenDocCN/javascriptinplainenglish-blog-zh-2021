# BehaviourSubject、Subject、ReplaySubject 和 Async Subject 有什么区别？

> 原文：<https://javascript.plainenglish.io/what-is-the-difference-between-behavioursubject-subject-replaysubject-and-async-subject-577ac0c886f2?source=collection_archive---------10----------------------->

## 每日角度提示、技巧和最佳实践

## 基本角度面试问题 2021

最近，我在寻找最好的技术来写干净和优化我的 angular 代码。我看了很多文章，我们知道，是无限的。然后我想到用不同的基本角度的主题来巩固清单，这些主题对我有帮助，将来也可能对别人有帮助。

![](img/2eb9b69236170a4e5eab30521bffe834.png)

[https://www.aviva.ie/insurance/home-articles/spot-the-difference/](https://www.aviva.ie/insurance/home-articles/spot-the-difference/)

这些小文章不仅能帮助你写出更好更干净的 Angular 代码，还能让你清楚前端技术的概念。这将有助于你建立强大的基础，并能在即将到来的前端面试中帮助你。

> 让我们先了解主题，然后再讨论它们的差异。

**Subject:**Subject observable 用于立即通知订阅者它发出的更新值。

*   它不跟踪旧值，即，如果一个主体可观察对象首先发出一个值，然后被订阅，那么订阅者将不会获得该值。
*   你可以把一个主题想象成一个实时更新/提要。从创建到订阅期间发出的旧值不会被保留；只能捕获在其订阅后发出的值。

```
const subject = new Subject < number > ();subject.subscribe({
    next: (val) => console.log(`Subject Value: ${val}`)
});subject.next(1);
subject.next(2);// Logs:
// Subject Value: 1
// Subject Value: 2
```

**behavior Subject**:behavior Subject 的行为就像一个普通的可观察主体，但它有一个额外的特性，即它保留了最后发出的值。

*   这意味着如果值是在 BehaviorSubject 之前发出的，并且如果订阅是在值发出之后添加的，那么订阅将给出最后发出的值。

```
const subject = new BehaviorSubject(0); // 0 is the initial valuesubject.subscribe({
    next: (v) => console.log(`Subject Value: ${v}`)
});subject.next(1);
subject.next(2);subject.next(3);// Logs
// Subject Value: 0
// Subject Value: 1
// Subject Value: 2
```

**replay subject**:replay subject 的行为“像”一个 **BehaviorSubject** 只是它提供了保存/重放/重复“n”个先前发出的值的灵活性。

*   它可以接受两个参数:第一个参数是“应该为将来的订阅保留多少最新发出的值”；第二个参数是“这些最新值应该有效多长时间(以毫秒为单位)”

```
const subject = new ReplaySubject(3); // buffer 3 values for new subscriberssubject.subscribe({
    next: (v) => console.log(`observer1: ${v}`)
});subject.next(1);
subject.next(2);
subject.next(3);
subject.next(4);subject.subscribe({
    next: (v) => console.log(`observer2: ${v}`)
});subject.next(5);// Logs:
// observer1: 1
// observer1: 2
// observer1: 3
// observer1: 4
// observer2: 2
// observer2: 3
// observer2: 4
// observer1: 5
// observer2: 5
```

*   **AsyncSubject** :一个 **AsyncSubject** 的行为更像一个 Subject，而不太像行为/重放 Subject，也就是说，在订阅之前发出的值不会被保留。
*   甚至订阅后发出的所有值都不会被保留。
*   AsyncSubject 是一个 Subject 变体，其中**仅将可观察执行的最后一个值**发送给其订户，并且**仅在执行完成时发送**

```
const subject = new AsyncSubject();subject.subscribe({
    next: (v) => console.log(`observer1: ${v}`)
});subject.next(1);
subject.next(2);
subject.next(3);
subject.next(4);subject.subscribe({
    next: (v) => console.log(`observer2: ${v}`)
});subject.next(5);
subject.complete();// Logs:
// observer1: 5
// observer2: 5
```

## 两者有什么区别？

让我们看一个简单的例子，并理解其中的区别。

[https://gfycat.com/cookedfavorableblacklab](https://gfycat.com/cookedfavorableblacklab)

**说明:**

1.  如您所见，受试者正在经历间隔，显示值为 0，1，2，3，4，5。主题不能包含任何值。
2.  接下来，行为主题以间隔开始，并显示值-1，0，1，2，3，4，5。在我们订阅观察者之前，行为主体可以保存一个初始值。
3.  对于控制台上的 Replay 主题，我们可以发现，当我们使用第二个以 2，3，4 开始的观察点时，第一个观察点获得了 1，2，3，4 值。这意味着我们可以在 Replay Subject 中缓冲一些值。
4.  对于异步主题，它将只显示值 5，因为它将只从流中获取最后一个值。

这里可以找到 stackblitz。

[https://stack blitz . com/edit/rxjs-angular-subject-vs-behavior-vs-replay-vs-async-5s rktn](https://stackblitz.com/edit/rxjs-angular-subject-vs-behavior-vs-replay-vs-async-x2vsap)

**来源:**

## 进一步阅读

*更多内容请看*[***plain English . io***](http://plainenglish.io)