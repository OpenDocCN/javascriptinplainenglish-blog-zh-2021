# 如何获得 RxJS 主题或可观察对象的当前值

> 原文：<https://javascript.plainenglish.io/how-to-get-the-current-value-of-an-rxjs-subject-or-observable-b5eb666b20f6?source=collection_archive---------0----------------------->

## 获取 RxJS 可观察值的当前值——每日角度提示、技巧和最佳实践

![](img/76bbfc57152f38706e81e8e8cebbbdd2.png)

Photo by [Sharon McCutcheon](https://unsplash.com/@sharonmccutcheon?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

作为开发人员，学无止境。我们总是需要与时俱进的技术，以及即将到来的或当前的市场趋势特征。

最近，我在寻找优化我的角度代码的最佳方法。我读过很多文章，我们都知道这是无限的。然后我想到了合并清单，为 Angular 编写更干净的代码，这对我有帮助，也可能对其他人有帮助。

这些小文章不仅能帮助你编写更好的 TypeScript 或 JavaScript 代码，还能理清前端技术的概念。这将有助于你建立强大的基础，并能在即将到来的前端面试中帮助你。

> 让我们进入我们的主要讨论

前端开发中最基本的主题之一是 RxJS 的正确使用，它有助于同步我们的代码。我们在日常生活中确实会大量使用 Observables，比如使用后端服务或在不同组件之间进行通信。想到的基本问题是我们如何得到可观测值的当前值。

我在 [Simon_Weaver](https://stackoverflow.com/users/16940/simon-weaver) 的回答中找到了最好的参考之一。

# 一般的规则是，你只能用`subscribe()`从一个可观测值中得到一个值

*(或异步管道，如果使用角形)*

**BehaviorSubject:** 当我们一订阅它，BehaviorSubject 就会保存之前的值，它会发送之前的值或者初始化它的值。

```
[@Component](http://twitter.com/Component)({
    selector: 'my-app',
    providers: [],
    template: `
    <h3>Accessing BehaviorSubject's Value</h3><input [(ngModel)]="currentValue" type="text"> 
    <br>
    <br>current Value is: <b>{{currentValue}}</b>
  `,
})
export class AppComponent {
    subject = new BehaviorSubject('default');get currentValue() {
        return this.subject.value;
    }set currentValue(v) {
        this.subject.next(v);
    }
}
```

# 方法:1

更好的方法总是使用`subscribe`来获取一个值。

```
//emit 1,2,3,4,5const source = of(1, 2, 3, 4, 5);//take the first emitted value then completeconst example = source.pipe(take(1));//output: 1const subscribe = example.subscribe(val => console.log(val));
```

运筹学

```
const source = from([1, 2, 3, 4, 5]);//no arguments, emit first valueconst example = source.pipe(first());//output: "First value: 1"const subscribe = example.subscribe(val => console.log(`First value: ${val}`));
```

如果流已经完成，这两个实体之间的差异`first()`将产生错误**；如果流已经完成或者没有立即可用的值，则**将不会发出任何可观察到的结果。

# 方法:2

不要试图访问你的函数中的值，**而是考虑一个函数，它创建了一个新的可观测值，甚至没有订阅它！**

通过保持一切都是可观察的，并使用`switchMap`来做决定，你可以创造新的可观察的事物，这些事物本身可以成为其他可观察事物的来源。

```
bear$: Observable<string> = of('Beary');
lion$: Observable<string> = of('Liony');
zooOpen$: Observable<boolean> = of(true);getZooReport() {return this.data$.pipe(switchMap(zooOpen => {if (zooOpen) {return combineLatest(this.bear$, this.lion$).pipe(map(([bear, lion] => {// this is inside 'map' so return a regular string
                 return "Welcome to the zoo! Today we have a bear called ' + bear + ' and a lion called ' + lion;
              }
          );
      }
      else {// this is inside 'switchMap' so *must* return an observable
         return of('Sorry the zoo is closed today!');
      }});
 }
```

**来源:**

[](https://stackoverflow.com/questions/37339016/get-current-value-from-observable-without-subscribing-just-want-value-one-time) [## 从不订阅的可观察值中获取当前值(只需要一次值)

### 我只想要一次当前值，而不是新值，因为它们正在到来…您仍将使用 subscribe，但是…

stackoverflow.com](https://stackoverflow.com/questions/37339016/get-current-value-from-observable-without-subscribing-just-want-value-one-time) 

## 如果你喜欢并想获得更多这样的内容，请做[订阅](https://medium.com/@patel_ap/membership)

# 延伸阅读:

[](/a-guide-to-the-20-best-vscode-extensions-for-frontend-developers-f75a5d716091) [## 面向前端开发人员的 20 个最佳 VSCode 扩展指南

### 面向前端开发的 VSCode 最有用扩展的综合指南

javascript.plainenglish.io](/a-guide-to-the-20-best-vscode-extensions-for-frontend-developers-f75a5d716091) [](/top-100-questions-you-must-prepare-for-to-ace-your-next-angular-interview-10-20-c3f5ab854be) [## 为赢得下一次面试，你必须准备的 100 个问题(10-20)

### 最常见的角度面试问题 2021

javascript.plainenglish.io](/top-100-questions-you-must-prepare-for-to-ace-your-next-angular-interview-10-20-c3f5ab854be) [](/33-javascript-useful-shorthands-cheat-list-2021-e08b46a1a688) [## 33 JavaScript 有用的速记作弊清单:2021

### 使用现代速记技术、技巧和诀窍优化您的 JavaScript 代码。

javascript.plainenglish.io](/33-javascript-useful-shorthands-cheat-list-2021-e08b46a1a688) 

*更多内容看*[***plain English . io***](http://plainenglish.io/)