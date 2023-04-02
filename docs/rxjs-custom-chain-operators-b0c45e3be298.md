# 如何创建 RxJS 自定义运算符链

> 原文：<https://javascript.plainenglish.io/rxjs-custom-chain-operators-b0c45e3be298?source=collection_archive---------7----------------------->

![](img/fcab7a7c5e79c45eb631e3bd492598b0.png)

*先决条件:Javascript，Typescript，RxJs 操作符，RxJs 管道，可观察，订阅。*

RxJs 提供了强大的功能和简单的 javascript 反应式编程方法。它有很多内置的操作符，但是有时候，你只需要创建自己的操作符。

通过使用一些内置的操作符，比如 filter，很容易创建一个简单的操作符。我们将从简单的开始，然后我们将创建一个更复杂的，不使用内置的操作符，只是从零开始。

**使用内置运算符创建运算符**

让我们从一个流中创建一个乘 2 操作符。这很简单，因为我们可以使用现有的 map 操作符并返回一个新的可观察值。

```
function doubleTheValues() { return function<T>(source: Observable<T>) { return source.pipe(map(value => value * 2));}
```

为了使用它，我们将遵循与使用内置操作符相同的原则。考虑一个可观察的:

```
import { interval } from 'rxjs';import { map } from 'rxjs/operators';const myIntervalObservable = interval(200);
```

要使用我们的新运算符，只需:

```
myIntervalObservable.pipe( doubleTheValues()).subscribe();
```

但是，正如您所看到的，如果我们需要更复杂的逻辑或不同的条件，仅仅使用现有的操作符会变得非常困难。

比方说，我们需要两个操作符，根据流中的对象返回不同的值。

让我们以用户流为例。用户对象有一个属性，表明用户是否是管理员，我们称之为`isAdmin`。

```
class User {
    name: string;
    email: string;
    isAdmin: boolean;
}
```

基于`isAdmin`属性，我们要做出不同的逻辑。如果没有自定义操作符，我们可以通过以下方式实现:

```
myUserObservable: Observable<User>;
constructor() {
    this.myUserObservable.subscribe((user) => {
        if (user.isAdmin) {
 *// do some admin logic*        } else {
 *// do some non admin logic*        }
 *// do logic regardless user is admin or not*   })
}
```

但是，正如你所看到的，这很烦人，因为我们必须使用 if / else 表达式，如果将来`isAdmin`必须改变，我们将需要在每个使用该属性的文件中改变。

相反，我们可以创建两个自定义操作符并使用它们。让我们看看怎么做。

对于管理员用户，我们会这样做:

```
export function *userIsAdmin*(callback: (user: User) => void) { return (source) => {
        return new Observable((subscriber: Subscriber<User>) => {
          return source.subscribe({
            next(user: User) {
              if (user.isAdmin) {
                 try {
                    callback(user);
                 } catch (e) {
                    console.error(e);
                 }
              }
              subscriber.next(user);
           },
           error(err) {
             subscriber.error(err);
           },
           complete() {
             subscriber.complete();
          }
       })
    })
  }
}
```

这里我们可以看到我们的函数正在接收一个回调函数，它接收一个用户并返回 void。我们的函数只需要接收观察对象，订阅它，检查用户是否是管理员，调用回调函数并返回与接收到的观察对象相同的观察对象。

我们需要返回接收到的可观察值，因为在我们的链管道中，如果用户不是管理员，我们希望移动到下一个操作符。

对于非管理员用户:

```
export function *userIsNotAdmin*(callback: (user: User) => void) {return (source) => {
        return new Observable((subscriber: Subscriber<User>) => {
          return source.subscribe({
            next(user: User) {
              if (!user.isAdmin) {
                 try {
                    callback(user);
                 } catch (e) {
                    console.error(e);
                 }
              }
              subscriber.next(user);
           },
           error(err) {
             subscriber.error(err);
           },
           complete() {
             subscriber.complete();
          }
       })
    })
  }
}
```

现在，我们的逻辑看起来更清晰，也更容易理解和扩展。

```
this.myUserObservable.pipe(
 *userIsAdmin*((user: User) => {
 *// do admin user logic*    }),
 *userIsNotAdmin*((user: User) => {
 *// do non admin user logic*    })
  ).subscribe((user: User) => {
 *// do logic regardless user is admin or not* })
```

这就是我们如何创建自定义操作符，并在我们的项目中使用它们，以使代码更加简洁和易于扩展。

**PS:** 如果你需要一个正常运行时间监控工具，只需检查 [RoboMiri](https://robomiri.com) 。最好的免费正常运行时间监测服务。