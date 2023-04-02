# 改进 RxJS 调试

> 原文：<https://javascript.plainenglish.io/improve-rxjs-debugging-35c83b815a0c?source=collection_archive---------13----------------------->

![](img/04785dd3165812e1d7ba2a9d5567515b.png)

前端 Web 开发中的反应式编程是有意义的，因为它是一种专注于对事件做出反应的范式。用户与广播事件的 DOM 交互。

[RxJS](https://rxjs.dev/) 是无功编程的瑞士军刀。它为我们提供了一种基于推送的模式，允许我们对用户创建的事件做出响应。

😱但是有一个主要问题。调试 RxJS 流可能是一场噩梦！

本文将向您介绍一个新的社区拥有的 RxJS 操作符，旨在帮助简化调试，并提供一些额外的健壮调试技术。

# `debug()`操作员

这个神奇的算子是什么？它是`debug()`操作符*(你可以在这里找到更多的*[](https://github.com/Coly010/rxjs-debug-operator)**)*并且可以非常容易地安装:*

*NPM:*

*`npm install rxjs-debug-operator`*

*纱线:*

*`yarn add rxjs-debug-operator`*

*它也很容易使用！只需将它通过管道传输到您已经建立的任何流中:*

```
*obs$.pipe(debug());*
```

# *但是它有什么用呢？*

*简而言之，它帮助您找出 RxJS 流哪里出错了，哪里对了。*

*默认情况下，它只是将值记录到控制台。*

*[https://gist . github . com/coly 010/59 cef FD 69 cc 72 f 334 f 61 a 08d 4 DFB 0f](https://gist.github.com/Coly010/59ceffd69cc72f334f61a08d4dfbd0f0)0*

*然而，它比这灵活得多，可以成为诊断问题甚至报告可能对业务产生负面影响的用户路径中的关键错误的强大工具！*

# *怎么才能充分利用呢？*

*您可以利用无数的用例来利用这个操作符。*

*一种常见的方法是查看流中一系列操作的值是如何变化的。*

*由于有了方便的`label`选项，这可以变得更加容易操作:*

*[https://gist . github . com/coly 010/39 c 63 e 50 be 855 b 12 CD 3 f 792346751 DD](https://gist.github.com/Coly010/39c63e50be855b12dcd3f792346751dd)*

*下面我们来看一些更具体的用例！*

# *例子*

*希望这些例子能派上用场，展示操作者的力量！*

# *简单日志记录*

***无标签***

*[https://gist . github . com/coly 010/56de 91 ef 29 f 67 c 504725 ba F3 c 776 ad 0 c](https://gist.github.com/Coly010/56de91ef29f67c504725baf3c776ad0c)*

***带标签***

*[https://gist . github . com/coly 010/2574 AFE EAC 5266 b 0454d 028195 c15 a9 a](https://gist.github.com/Coly010/2574afeeac5266b0454d028195c15a9a)*

*您甚至可以更改每个通知的内容:*

*[https://gist . github . com/coly 010/e 64 a3 d6b 61419 dfca 5 be 2c 51 cfae b 712](https://gist.github.com/Coly010/e64a3d6b61419dfca5be2c51cfaeb712)*

# *仅在开发模式下记录*

*您也只能在开发模式下进行记录。*

*有两种方法可以做到这一点，一种是对所有的`debug()`实例进行全局处理，另一种是根据具体情况进行局部处理。*

***全球***

*[https://gist . github . com/coly 010/9e 1704 f 6 BD E3 ee ebf 636 ced 32 fff 69 CD](https://gist.github.com/Coly010/9e1704f6bde3eeebf636ced32fff69cd)*

***本地***

*[https://gist . github . com/coly 010/03 a5 ab 6 f 10 c 6208171016 cc 7 ebcd 9 E0 a](https://gist.github.com/Coly010/03a5ab6f10c6208171016cc7ebcd9e0a)*

# *衡量一组操作员的表现*

*现在来看一些可能非常酷的东西。我们可以使用 debug 操作符和定制的`next`通知处理程序来测量一组到流的管道操作的性能/时间。*

*下面的例子显示了它被用来测量一个`switchMap`对一个网络请求所花费的时间，然而，这种方法可以用于任何一组操作符。*

*[https://gist . github . com/coly 010/a4ff 124763 CB 88 b 508 f 05 D5 a3 bbfeb 08](https://gist.github.com/Coly010/a4ff124763cb88b508f05d5a3bbfeb08)*

# *远程记录以提高可观察性*

*`rxjs-debug-operator`有一个全局配置，也允许您更改所使用的记录器。*

*因此，您可以使用类似于 [Winston](https://github.com/winstonjs/winston) 的东西作为您的日志记录器！*

# *结论*

*这一切都是从一个笑话开始的:“*开发者* `*tap(console.log)*` *用 RxJS 多少次？”**

*但它已经繁荣成如此之多！希望这篇文章展示了使用这样一个简单的操作符可以做些什么，我期待看到开发人员开始用它做些什么奇怪而奇妙的事情！*

*如果您注意到任何问题或有功能要求，请在回购[https://github.com/Coly010/rxjs-debug-operator](https://github.com/Coly010/rxjs-debug-operator)上打开问题！*

*有问题请在下面提问或者在 Twitter 上联系我: [@FerryColum](https://twitter.com/FerryColum) 。*

**原载于 2021 年 3 月 23 日*[*https://dev . to*](https://dev.to/coly010/improve-rxjs-debugging-3iph)*。**