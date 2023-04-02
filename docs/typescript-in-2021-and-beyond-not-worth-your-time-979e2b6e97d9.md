# 打字稿被浪费的潜力

> 原文：<https://javascript.plainenglish.io/typescript-in-2021-and-beyond-not-worth-your-time-979e2b6e97d9?source=collection_archive---------0----------------------->

## 帮助您从 TypeScript 项目中获得最大类型安全性的一些模式

![](img/393931a1ecc9acec927498fe9551f671.png)

Photo of someone covered in TypeScript runtime errors, by [jesse orrico](https://unsplash.com/@jessedo81?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

**免责声明:**本文经过大量编辑，语气有所变化。请注意，标题不再是“TypeScript 不值得您花费时间”，而是“以下是从 TS 项目中提取更多价值的方法。”

TypeScript 不是免费的。它带来了严重的开发时损失和最低限度的安全保证，同时保留了 JavaScript 最糟糕的方面。

TypeScript 使得 JavaScript 更难编写，开发时间更长，测试难度更大*，并让您产生一种错误的类型安全感。太多的时候人们忘记了写打字稿是 ***打假装*** *。*您正在参与一个类型 ***提示*** 系统，而不是一个类型系统。您得不到运行时好处或安全保证，以及最少的类型推断。TypeScript 增加的任何价值都基于这样一个假设，即您用准确的类型来修饰您编写的所有内容。

TypeScript 的许多缺点可以被看作是脱离了它们的目标，即 TypeScript 是一种“非二进制”语言选择；首先是 JavaScript 互操作和逐步采用 TypeScript，这种语言对您编写的代码类型不做任何假设。

这种缺乏远见的做法使得 JavaScript(现在是 TypeScript)社区陷入了一些相当严重的反模式，比如使用类进行依赖注入、使用继承进行代码重用以及基于异常的错误处理。

TypeScript 已经明确表明他们愿意添加修改运行时行为的构造，即在 decorators 和 constructor 属性中——为什么不进一步考虑类型安全呢？为什么不劝阻[类&继承](https://medium.com/javascript-scene/how-to-fix-the-es6-class-keyword-2d42bb3f4caf)？为什么不强制[空值声明和处理](https://www.nickknowlson.com/blog/2013/04/16/why-maybe-is-better-than-null/)？为什么[不阻止异常](https://softwareengineering.stackexchange.com/questions/150837/maybe-monad-vs-exceptions)？为什么不鼓励使用类型来封装行为？

# 我希望包括什么

## 用结果类型进行优雅的错误处理

大多数语言，包括 Javascript 和 Typescript，都使用基于**控制流**的错误处理。例外情况。

这意味着当一个函数到达不能继续的状态时，它**抛出**一个错误，这个错误由调用它的函数和调用那个函数的函数再次抛出，直到希望有人捕捉到它。

这对 JS 来说可以，但对 TypeScript 就不行了。最大的问题是**你不能从它的类型签名**判断一个函数是否可能失败。这意味着您看到的任何 TypeScript 函数签名都有可能是谎言。

这个函数 ***说*** 它返回一个数字，但是如果你传递一个分母为 0 的值，它会抛出一个错误。

## 输入`Result<T, E>`

Result(有时也称为要么)是一种特殊的类型，它表示“**要么**运行正常，您得到一个 T，要么有一个错误，您得到一个 e。”

最小的定义可能是这样的:

请注意，这并不完美，更健壮的实现可以使用`[purify-ts/Either](https://gigobyte.github.io/purify/adts/Either)`或`[fp-ts/Either](https://gcanti.github.io/fp-ts/modules/Either.ts.html)`。

这意味着上面的`divide`函数可以重写为:

这有一些很大的好处:

*   我们可以流畅地处理错误(就像我们与数组交互一样；一般有`Result.map`、`Result.bind`、`Result.isOk` / `isErr`)
*   类型签名表示“我可以失败！”
*   `divide` **的调用者必须**检查结果是否正确，以便提取值，从而编译类型脚本
*   这个错误不会在调用栈中冒泡，直到有人发现它

## 使用选项进行优雅的空值处理

如果您启用了严格模式并使用了 null-coalesce 操作符，那么这就没什么价值了，但仍然很有价值。

与 Result 类似，我们可以使用类型来封装值是否存在:

请注意，这并不完美，更健壮的实现可用作`[purify-ts/Maybe](https://gigobyte.github.io/purify/adts/Maybe)`或`[fp-ts/Option](https://gcanti.github.io/fp-ts/modules/Option.ts.html)`。

*   我们可以流畅地处理空值(就像我们处理数组一样；一般有`Option.map`、`Option.bind`、`Option.isSome` / `isNone`)
*   类型签名说“我可能什么也不返回！”(你已经可以用`Nullable`做到这一点)
*   `Option` s **的接收者有**来确保该值是某个值，以便从选项中获取它

## 合成而非继承

在一种致力于成为另一种语言的超集的语言中，这种情况有点难以想象。在 TS 中有 3 种声明类型的方法；`type`、`interface`和`class`。`type`和`interface`类似，允许你声明一个函数类型但不实现它。`class`允许你混合类型定义和实现。

将数据建模为类的一个常见示例是形状；如`Triangle`、`Quadrilateral`。这个例子通常是因为每个形状都是从一个叫做`Shape`的基类中派生出来的。

这个模型的问题是，如果你使用一个基类来共享接口和实现，你已经把`Shape`和子类耦合得非常紧密了。

更好的模式是使用复合——将脚本从“`Triangle`是一个`Shape`”翻转为“`Triangle`有`Area`”和“`Triangle`有`Sides`”

通过用多个单一用途的接口替换基类，我们已经根据每个形状所具有的品质组合了各个形状。这意味着每一个都可以在不影响其他的情况下被扩展或改变。

在 Rust 和 Haskell 等语言中，复合模式发挥到了极限，它们用复合(如上)和代数数据类型完全取代了类和继承。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)