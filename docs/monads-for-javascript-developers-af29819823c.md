# JavaScript 开发人员的单子

> 原文：<https://javascript.plainenglish.io/monads-for-javascript-developers-af29819823c?source=collection_archive---------2----------------------->

## JavaScript Alpha 指南

## 什么是单子？你不必是范畴理论专家就能理解。你必须知道 JavaScript 的承诺。

![](img/7c0a83cba56a944cd267a73561816606.png)

像其他程序员一样，我想知道什么是单子。但是每次你在网上搜索单子，你都会被范畴理论论文淹没。而其他资源似乎也没多大意义。

为了了解单子是什么，我付出了艰辛的努力。我开始学习哈斯克尔。几个月后我才意识到，人们对单子太过重视了。如果您是一名 JavaScript 开发人员，那么您肯定每天都在使用它们。你只是没有意识到。

我们不会详细讨论范畴理论或 Haskell，但是有一件事你需要知道。当你在互联网上搜索单子时，你不能错过这个定义:

```
(>>=) :: m a -> (a -> m b) -> m b
```

这是 Haskell 中一个`bind`操作符的定义。不同的语言对此操作有不同的名称，但它们都表示相同的意思。一些替代的名字是`chain`、`bind`、`flatMap`、`then`、`andThen`。

# 一元语境

```
(>>=) :: m a -> (a -> m b) -> m bm    :: monadic context
a, b :: value inside the context (string, number, ..)
```

**一元上下文**只是一个盒子，它实现了这个盒子成为一元所需的所有东西。一个非常简单的(非一元的)盒子可能是这样的:

```
const Box = val => ({ val }); 
const foo = Box("John");
```

这是一个盒子——只是一个包装好的值。该框没有任何行为，因为它没有任何方法。

> 要使某物成为单子，你必须让它自己表现得像单子。

所以让我们回到`(>>=) :: m a -> (a -> m b) -> m b`。`(>>=)`用作中缀运算符:`m a >>= (a -> m b)`。并且`(>>=)`操作的结果是`m b`。

# 问题是

有没有注意到我们有`m a`，但是函数把`a`作为参数？这就是单子的意义。

`(>>=)`操作是关于在一元上下文`m a`中取一个值，展开它，所以我们只得到`a`并将它流水线化到函数`(a -> m b)`。这不是魔法。您必须自己编写该行为的代码。我们以后会看到的。

# JavaScript 承诺类似于单子

更好地说，他们有单子式的行为。对于要成为单子的东西，它还必须实现一个**函子**和**可应用的**接口。我提到这一点只是为了完整性，但我们不会更深入。

JavaScript **承诺**用`.then()`方法实现一元接口。让我们看看。

```
// p :: m a :: Promise { 42 }
const p = Promise.resolve(42);
```

这基本上创建了一个盒子。我们有一个值`42`，在**承诺**里面。☝️这是我们的`m a`。

然后我们有一个将一个数除以二的函数。输入没有包含在**承诺**中。但是返回的函数被包装在一个**承诺**中。

```
// divideByTwo :: (a -> m b)
const divideByTwo = val => Promise.resolve(val / 2);
```

☝️这是我们的`(a -> m b)`。

再次注意，我们在**承诺**中有一个值`42`，但是函数`divideByTwo`接受一个未包装的值。我们仍然可以把这些连接起来。

```
// p :: m a :: Promise { 42 }
const p = Promise.resolve(42);
// p2 :: m a :: Promise { 21 }
const p2 = p.then(divideByTwo);
// p3 :: m a :: Promise { 10.5 }
const p3 = p2.then(divideByTwo);
```

或者更明显的是:

```
// p :: m a :: Promise { 10.5 }
const p4 = p.then(divideByTwo).then(divideByTwo);
```

**这是单子最重要的特征。**

你有一个值在盒子里— `Promise { 42 }`。您有一个接受展开值的函数— `42`。类型不匹配— `m a` vs. `a`。您仍然可以将该函数应用于装箱后的值。

## 这怎么可能

因为**承诺**以那种方式实现了`then`方法。大多数时候，运行在**承诺**中的代码是异步的。但是 **Promise 的**单子式行为使得链接一系列函数成为可能。

**单子抽象掉辅助数据管理、控制流或副作用。**将可能复杂的功能序列转化为简洁的流水线。

# 自定义单子式类

我用 TypeScript 编写了一个非常简单的单子式类的例子。它不会产生任何副作用，但允许函数链接。

```
class Dummy<T> {
  constructor(private val: T) {} chain<TResult>(fn: (value: T) => Dummy<TResult>): Dummy<TResult> {
    return fn(this.val);
  } static unit<T>(val: T): Dummy<T> {
    return new Dummy(val);
  }
}const d = new Dummy(41);
d.chain(val => new Dummy(val + 1))
 .chain(val => new Dummy("The answer is: " + val));
```

# **单子定律**

有单子行为的类必须遵守一些法则。

*   左侧标识
*   正确的身份
*   结合性

你可以在网上了解更多。我将在这里放一段代码，证明虚拟类遵循这些规则。

```
const m = Dummy.unit(1);
const f = (val: number) => new Dummy(val + 1);
const g = (val: number) => new Dummy(val + 2);// 1\. left identity
Dummy.unit(1).chain(f) ==== f(1)// 2\. right identity
m.chain(Dummy.unit) ==== m// 3\. associativity
const m1 = Dummy.unit(1);
m.chain(f).chain(g) ==== m.chain(val => f(val).chain(g)
```

`==`或`===`在这里不起作用；对象引用不同。为此，我使用了不存在的`====`,但将其理解为比较单子对象的内部值。

# 包扎

我希望这能对单子是什么有所启发。如果您是 JavaScript 开发人员，那么您每天都在使用它们。将封装在**承诺**中的值提供给期望解包值的函数。并再次返回一个包装在**承诺**中的新值。

# 资源

*   (一)[https://en . Wikipedia . org/wiki/Monad _(functional _ programming)](https://en.wikipedia.org/wiki/Monad_(functional_programming))