# 如何检测输入()值在角度上的变化

> 原文：<https://javascript.plainenglish.io/how-to-detect-when-an-input-value-changes-in-angular-5872c77517fc?source=collection_archive---------2----------------------->

## 角度基础 2021

## 检测输入值何时改变角度

![](img/82f7a1097e73476dee353fb651d2f70a.png)

Photo by [Elena Koycheva](https://unsplash.com/@lenneek?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 angular 应用程序中，我们主要处理父子组件关系，但有时会发生这样的情况，我们的父组件做了一些更改，但子组件不会直接通知或更改值。**我们如何通知孩子或直接更新输入值？**

## 1.使用 ngOnChanges()生命周期方法

当组件中的任何输入值发生变化时，调用 ngOnChanges 方法。这个方法有一个 **SimpleChanges** 对象，从中我们可以比较当前和以前的值。

```
@Input() testId: string;

    ngOnChanges(changes: SimpleChanges) {

        this.doSomething(changes.testId.currentValue);
        // 

    }
```

## 2.使用输入设置器和 Getter 属性

我们可以创建 getter 和 setter 方法，这样做的好处是无论何时发生变化，setter 都会设置值，而我们得到更新后的值。

```
private _testId: string;[@Input](http://twitter.com/Input)() set testId(value: string) {this._testId= value;
    this.changeHappened(this._testId);}get testId(): string {return this._testId;}
```

## 3.我们可以使用异步管道。

```
[@Component](http://twitter.com/Component)({
    selector: 'child-component',
    template: `<p>{{ data }}</p>`,
})
export class SubComponent implements OnInit {
    [@Input](http://twitter.com/Input)() data: string;ngOnInit() {
        console.log('received data', this.data);
    }
}[@Component](http://twitter.com/Component)({
    selector: 'Parent-app',
    template: `
    <h1>Hello {{name}}</h1>
    <sub-component [data]="data$ | async"></sub-component>
  `
})
export class ParentCOmponent {
    data$ = Observable.of('Values').delay(1000);
}
```

异步管道执行以下任务。

*   `async`管道订阅`Observable` 并返回最新发出的值。
*   当我们得到新的变化时，这个管道将只检查变化
*   这将有助于避免任何内存泄漏。

## 您应该使用哪种方法？

如果您需要检查以前的值和当前的值，并对多个输入一起进行一些检查，那么最好使用 ngOnChanges()，因为我们需要在 setter 和 getter 中处理多个东西。

最有效的方法是使用异步管道，因为它有助于取消订阅，最终有助于不写或不关心取消订阅。

## 在某些情况下，角度变化检测可能不会触发

通常，每当父组件更改它传递给子组件的数据时，setter 和 ngOnChanges 的更改检测都会触发，**假设数据是 JS 原语数据类型(字符串、数字、布尔)**。但是，在下面的场景中，它不会启动，我们需要小心。

1.  如果我们使用一个嵌套的对象或数组，可能会发生变化检测不会自己通知，因为我们可能需要创建一个新的数组或对象，就像这样`data= {...data};`
2.  如果您在外部更改数据，angular 将不会知道这些更改。我们需要在组件中使用 ChangeDetectorRef 或 NgZone 来使 angular 意识到外部变化，从而触发变化检测。

**参考文献:**

# 进一步阅读

*更多内容请看*[***plain English . io***](http://plainenglish.io)