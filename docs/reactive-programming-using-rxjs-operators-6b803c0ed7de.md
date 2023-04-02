# 反应式编程—使用 RxJS 运算符

> 原文：<https://javascript.plainenglish.io/reactive-programming-using-rxjs-operators-6b803c0ed7de?source=collection_archive---------10----------------------->

## RxJS 操作符可以帮助简化您的 web 应用程序开发。

![](img/05c76230dba368b1ddb8f67e6e675968.png)

Image by [Pashminu Mansukhani](https://pixabay.com/users/1137303-1137303/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=835340) from [Pixabay](https://pixabay.com/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=835340)

在我目前的工作中，我一直在使用反应式编程范式进行编码——我从中获得了很多乐趣。我已经知道这个范例是基于观察者设计模式的。然而，在我旅程的早期，我经历了一个陡峭的学习曲线。诚然，在阅读了文档之后，我的收获是如何创建一个可观察对象(主体)和一个观察者。我在通读操作员之后不知何故迷路了。

您可以使用的可用运算符的数量可能会非常多。文档写得很好。然而，我认为这是你需要付诸实践才能更深入理解的概念之一。或者更好的是，找到可以用 RxJS 操作符解决的现有问题。

在这篇文章中，我将带你浏览到目前为止我认为有用的 RxJS 操作符。代码示例将使用用 TypeScript 编写的 RxJS 版本 6.6.7。

您会注意到，我故意让我的示例代码尽可能地详细:

*   我正在指定可观察的类型。指定类型使我们在初始化一个可观察对象时变得清晰。
*   在箭头函数中明确使用了 return 语句。JSFiddle 中似乎有一个 bug，使用 arrow 函数快捷方式进行 return 语句不起作用。
*   有一些我们可能不需要做的变量赋值。然而，我将一些可观察的变量赋值给一个变量，这样它们更容易理解。
*   我将美元符号($)附加到可观测量上，这是标准做法。

# RxJS 的基础

在我们跳到操作符之前，让我们快速回顾一下基础知识。

如果你已经知道如何在 RxJS 中使用 Observable、Observer 和 Subject，你可以跳过这一节。

## 可观察的和观察者

来自 [RxJS 单据](https://rxjs-dev.firebaseapp.com/guide/overview)。

> 可观察的:表示未来值或事件的可调用集合的概念。
> 
> Observer:是一个回调集合，它知道如何监听可观察对象传递的值。

让我们首先创建一个用一组值和一个 *setTimeout* 函数初始化的*可观察对象*。

```
const observable$: rxjs.Observable = new rxjs.Observable(observer => {
  observer.next(1);
  observer.next(2);
  observer.next(3);
  observer.next(3.5);
  setTimeout(() => {
    observer.next(4);
    observer.complete();
  }, 1000);
});
```

接下来，我们将为一个观察者订阅*可观察的*。Observable 中的下一个调用将执行我们的 observer 中的回调函数。

```
observable$.subscribe({
  next(x): void { console.log('got value ' + x); },
  error(err): void { console.error('something wrong occurred: ' + err); },
  complete(): void { console.log('complete'); }
});
```

当观察者执行完可观察集合中的内容后，就会调用 *complete* 函数。

代码示例将按如下方式运行:

1.  按顺序打印“获得值”——1、2、3 和 3.5。
2.  打印“仅在订阅后”
3.  打印“获得值 4”
4.  打印“完成”

Code snippet by the author.

上面的代码示例让我们了解了可观察对象和观察者的概念。在反应式编程中，任何东西都可以是流。让我们探索几个例子，看看如何在我们的 Web UI 中实现这些概念。

## 科目

简单来说，*主题*是*可观察对象*和*观察者*的包装。

```
const subject$ = new rxjs.Subject();
```

我们可以方便地使用*主题*同时创建一个*可观察的*和*观察者*。然后通过实例化的*主题*对象在代码中的任何地方访问它们。

```
subject$.subscribe(x => console.log('Subscriber A: ' + x));
subject$.next(1);
subject$.next(2);
```

当我们运行该代码时，它将打印出以下内容。

```
"Subscriber A: 1"
"Subscriber A: 2"
```

我们可以为我们的*可观察对象*订阅另一个*观察对象*，该观察对象打印“订户 b”

```
subject$.subscribe(x => console.log('Subscriber B: ' + x));
subject$.next(3);
```

从这条线开始，我们现在有两个可用的观察者。

```
"Subscriber A: 1"
"Subscriber A: 2"
"Subscriber A: 3"
"Subscriber B: 3"
```

如果我们想阻止新订阅我们的可观察对象，我们可以使用*完成*方法*来阻止新订阅方法的静默调用*。

```
subject$.complete();
```

否则，我们可以使用*取消订阅*来抛出错误。

```
subject$.unsubscribe();
```

Code snippet by the author.

# 1.拿

它从一系列发射值中取出 *n* 个值。

当我们有一系列发射值时，我们可以使用 take，我们只想取第一个 *n 个*发射值。该方法对于捕获前几个单击事件或从值列表中取样非常有用。

我们有一系列发射值 1、2、3、4 和 5。

```
const emittedValues$: rxjs.Observable = rxjs.of(1, 2, 3, 4, 5);
```

我们可以使用 *take* 运算符，通过取第一个 *n 个*值来转换可观察对象的发射值。

注意我们是如何将 *take* 操作符传递给 *pipe* 方法的。

> 可管道操作符是一个函数，它将一个可观察值作为其输入，并返回另一个可观察值。这是一个纯粹的操作:之前的可观察值保持不变。— [rxjs-dev](https://rxjs-dev.firebaseapp.com/guide/operators)

```
const takeValues$: rxjs.Observable = emittedValues$.pipe(rxjs.operators.take(2));
```

然后，我们可以使用转换后的发射值订阅该可观察值。

```
takeValues$.subscribe(x => {console.log(x)});
```

我们的代码将打印前两个发出的值。

```
1
2
```

*使用下面的示例代码试验 take 操作符。*

Code snippet by the author.

# 2.过滤器

当我们希望根据我们设定的条件过滤掉由我们的可观察对象发出的值时，我们可以使用 filter 操作符。一个简单的例子是过滤出偶数或奇数的值。

让我们重用上一个例子中相同的发射值。

```
const emittedValues$: rxjs.Observable = rxjs.of(1, 2, 3, 4, 5);
```

我们可以使用带有回调的*过滤器*操作符来过滤模 2 等于零的数字，从而过滤出偶数。

```
// filter even numbers
const evenNumbers$: rxjs.Observable = emittedValues$.pipe(
 rxjs.operators.filter(x => {return x % 2 == 0})
);console.log('even numbers');
evenNumbers$.subscribe(x => {console.log(x)});
```

我们将回调改为只过滤奇数— *模二不等于零*。

```
// filter odd numbers
const oddNumbers$: rxjs.Observable = emittedValues$.pipe(
 rxjs.operators.filter(x => {return x % 2 != 0})
);console.log('odd numbers');
oddNumbers$.subscribe(x => {console.log(x)});
```

尝试你能想到的其他过滤操作回调。

Code snippet by the author.

# 3.地图

给定一系列从可观察对象发出的值，如果我们想为每个发出的值附加字符串“take:”会怎么样？我们可以使用*映射*操作符将函数应用于每个来自可观测值的发射值。

```
const emittedValues$: rxjs.Observable = rxjs.of(1, 2, 3, 4, 5);
```

让我们使用一个 map 操作符函数，该函数接受一个回调，该回调将字符串“take:”附加到每个值上。

```
const mappedValues$: rxjs.Observable = emittedValues$.pipe(
 rxjs.operators.map(x => {return 'take: ' + x})
);
```

让我们给我们的 *$mappedValues* 订阅一个回调。回调将打印我们的 map 函数返回的值。

```
mappedValues$.subscribe(x => {console.log(x)});
```

我们将获得以下输出。

```
"take: 1"
"take: 2"
"take: 3"
"take: 4"
"take: 5"
```

*使用你能想到的其他 map operator 回调。*

Code snippet by the author.

# 4.合并地图

当我们想同时处理两个不同的观测值时, *mergeMap* 操作符很有用。

一个具体的例子是，如果我们希望执行一个 API 调用来检索用户 id，并执行另一个 API 调用来检索每个用户 id 的用户配置文件信息。

*被模仿的 API 调用来检索用户 id。*

```
// mock a userIDs API call
const getUserIds$: rxjsObservable = () => { 
 const userIds$: rxjs.Observable = rxjs.of(1, 2, 3, 4, 5);
  return userIds$;
}
```

*被模仿的 API 调用来检索用户配置文件。*

```
// mock a user profile API call
const getUserProfile$: rxjs.Observable = (userId) => {
 const userProfiles$: rxjs.Observable = rxjs.of('a', 'b', 'c', 'd', 'e');
  return userProfiles$;
};
```

检索用户 ID 的 API 调用将是我们的“外部可观察对象”，检索每个用户 ID 的用户配置文件的 API 调用将是我们的“内部可观察对象”我们可以将这个示例应用于任何数据集，而不仅仅是用户，也就是说，您必须从一个 API 中检索 id 或键，然后使用它们或键从另一个 API 中检索另一条信息。

```
const retrievedUsers$: rxjs.Observable = getUserIds$().pipe(
  rxjs.operators.mergeMap(userId => {
    return getUserProfile$(userId).pipe(rxjs.operators.map(userProfile => {
      return userId + userProfile;
    }))
  }),
);retrievedUsers$.subscribe(x => { console.log('retrieved user: ' + x) });
```

从这个例子中，我们可以看到 *mergeMap* 如何帮助组合两个不同的结果集，或者将外部可观察的结果映射到内部可观察的结果。

*使用下面的示例代码作为参考，自己尝试不同的数据集。*

Code snippet by the author.

# 5.开关图

> `switchMap`和其他展平算子的主要区别是抵消效果。在每次发射时，先前的内部可观测值(您提供的函数的结果)被取消，新的可观测值被订阅。你可以通过短语**切换到一个新的可观察对象**来记住这一点。- [learnrxjs.io](https://www.learnrxjs.io/learn-rxjs/operators/transformation/switchmap)

*switchMap* 操作符有助于 typeahead 实现。例如，在用户在我们的 typeahead 搜索的文本输入中输入一个新字符后，我们希望放弃前面的 API 请求。

我们可以通过将点击事件作为我们的“外部可观察”和将*间隔*作为我们的“内部可观察”来证明这一点点击事件观察将发出点击事件，当然，当它被点击时。可观测区间每秒会发出一个从零开始的数字。

```
const clickEvent$: rxjs.Observable = rxjs.fromEvent(document, 'click');
```

将我们的 *clickEvent$* 作为我们的“外部可观察”，将 *interval* 可观察作为我们的“内部可观察”

```
rxjs.interval(1000)
```

这个可观测区间将重置为零，因为我们每次点击按钮都会切换到一个新的可观测区间。“外部可观察的”是包裹着我们的“内部可观察的”

```
clickEvent$.pipe(
  rxjs.operators.switchMap(() => { 
    return rxjs.interval(1000)
  })
).subscribe(console.log);
```

下面输出中的零表示按钮被单击的时间；因此，它切换到一个新的可观测区间。

```
5
6
0
1
2
0
1
```

使用下面的示例代码，尝试切换到不同类型的可观察对象。

Code snippet by the author.

# 结论

您可以学习许多其他的操作符。到目前为止，这些是我发现有帮助的几个。随着我逐渐使用更多 RxJS 将提供的东西，我使用的运算符工具箱可能会增加。您的学习之旅将与我的不同，因此我建议尝试您可以在 RxJS 文档中找到的新操作符。

*更多内容看*[***plain English . io***](https://plainenglish.io/)