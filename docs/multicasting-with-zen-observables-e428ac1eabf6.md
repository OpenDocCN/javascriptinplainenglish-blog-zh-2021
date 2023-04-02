# 具有 Zen 可观测量的多播

> 原文：<https://javascript.plainenglish.io/multicasting-with-zen-observables-e428ac1eabf6?source=collection_archive---------10----------------------->

## 因为你太贱了，用不了 RxJS

![](img/624e30d1f2d8b7d912849b04e31e3f82.png)

Photo by [Sergey Semin](https://unsplash.com/@feneek?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/observers?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

Zen Observables 是 RxJS 的一个很好的轻量级替代品。如果您使用的是 Apollo Client，那么您不会因为使用 Zen 而付出包大小的代价。不过，有一个问题是 Zen 不支持[多播](https://www.learnrxjs.io/learn-rxjs/operators/multicasting/multicast)。Github 有一个[问题已经开放了好几年来解决这个问题。如果您正在寻找一种快速而简单的方法来为多播提供最少的支持，我在下面的 TypeScript 中准备了一个例子。](https://github.com/tc39/proposal-observable/issues/66)

值得注意的是，我们使用 Ramda 来[组合](https://ramdajs.com/docs/#compose)我们的`register`和`emit`函数。这允许我们在功能代码中利用单例。我们还返回了一个自定义的`Subscription`，允许订阅者取消订阅事件流:

```
return {
  closed: false,
  unsubscribe() {
    const index = subscriberMap.get(event.type).indexOf(onNext);

    this.closed = true;
    // splice mutates the arra in
    subscriberMap.get(event.type).splice(index, 1);
  },
};
```

这保留了 Zen Onsersable 接口，其中 subscribe 调用返回一个`Subscription`实例。

我们使用一个`subscriberMap`来提供过滤，这使得通知过程更加有效。`interceptors`数组允许执行副作用，这确实有助于调试和进一步过滤。如果您不熟悉拦截器，请查看这篇[文章](https://en.wikipedia.org/wiki/Interceptor_pattern)。

我们多播的主要用例是中央应用程序事件总线。滥用事件总线有很多弊端，所以请阅读[链接文章](https://www.techyourchance.com/event-bus/)。该实现允许解耦的应用程序组件订阅中央事件总线，并接收应该触发应用程序行为或向订阅者发送通知的通知。

要执行验证，请使用下面的测试。

编码快乐！