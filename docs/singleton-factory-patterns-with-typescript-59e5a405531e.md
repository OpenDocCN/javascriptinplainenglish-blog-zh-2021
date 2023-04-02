# 使用 TypeScript 的单例模式和工厂模式

> 原文：<https://javascript.plainenglish.io/singleton-factory-patterns-with-typescript-59e5a405531e?source=collection_archive---------2----------------------->

## 用 TypeScript 实现的单例和工厂设计模式。用一个理发师和一个冰淇淋店的例子来解释。

![](img/186c171923395d14d3fafcded3eb8e04.png)

[Eisvogel](http://www.zentrale.ch/) — The best ice creams in Zürich

在我在工程学校学到的所有设计模式中，singleton 和 factory 可能是我在日常编程活动中使用最多的。有时我甚至把两者混合起来，让乐趣倍增😜。

在这篇博文中，我将向你展示如何用 [TypeScript](https://www.typescriptlang.org/) 实现这些模式。

# 一个

> 在软件工程中，单例模式是一种软件设计模式，它将类的实例化限制在一个“单个”实例中([源](https://en.wikipedia.org/wiki/Singleton_pattern))。

单身者可能就像你的理发师。当你需要理发时，你不想去沙龙找任何新的专业人士，即使她/他和你有同样的技能，但是，你确实想要你的，因为她/他已经知道你最喜欢的设置✂️.

这种模式可以通过将一个`class`的`constructor`定义为`private`，使其在类声明之外实际上不可访问，并且只提供一个已经被设为`static`的对象的实例来实现。

```
export class Hairdresser {
  private static *instance*: Hairdresser | undefined = undefined;

  private constructor() {}

  static *getInstance*(): Hairdresser {
    if (!Hairdresser.*instance*) {
      Hairdresser.*instance* = new Hairdresser();
    }

    return Hairdresser.instance;
  }
}
```

使用上面的片段，我们不能得到任何新的理发师。尝试实例化新对象会导致错误。

```
// TS2673: Constructor of class 'Hairdresser' is private and only accessible within the class declaration.
const hairdresser: Hairdresser = new Hairdresser();
```

相反，访问实例将总是返回第一个已初始化的对象。

```
const hairdresser: Hairdresser = Hairdresser.*getInstance*();
```

# 工厂

> 在基于类的编程中，工厂方法模式是一种创造性的模式，它使用工厂方法来处理创建对象的问题，而不必指定将要创建的对象的确切类。这是通过调用工厂方法而不是调用构造函数来创建对象来实现的( [source](https://en.wikipedia.org/wiki/Factory_method_pattern) )。

工厂模式就像 [Eisvogel](https://www.gaultmillau.ch/zuri-isst/eisvogel-das-beste-glace-zurich) ，我最喜欢的，当然也是苏黎世最好的冰淇淋店。他们每天出售手工制作的美味冰淇淋，每天有五种不同的新口味。

当你到了那里，你知道你要去买冰淇淋，但是你不知道是什么口味的。

换句话说，您可以使用一个工厂来获得共享一个预期行为的对象，但是可以以不同的方式实现。

首先，它或者需要一个`interface`或者一个`abstract`类，这个类描述了除了应该由工厂创建的预期对象的有效实现之外的公共行为。

同`interface`:

```
export interface IceCream {
  yummy(): boolean;
}

export class Strawberry implements IceCream {
  yummy(): boolean {
    return true;
  }
}

export class Chocolate implements IceCream {
  yummy(): boolean {
    return true;
  }
}
```

使用`abstract`(注意:使用修饰器`override`，这是在 TypeScript 4.3 中新引入的，表示一个方法覆盖了父定义):

```
export abstract class IceCream {
  abstract yummy(): boolean;
}

export class Strawberry extends IceCream {
  override yummy(): boolean {
    return true;
  }
}

export class Chocolate extends IceCream {
  override yummy(): boolean {
    return true;
  }
}
```

不考虑上面的实现，可以实现一个相关的工厂。它可以是一个`static`方法或者一个无状态`function`的形式。重要的是，根据参数创建并返回所需的实现。

用一种`static`方法:

```
export class Factory {
  static *getIceCream*(): IceCream {
    return Math.random() % 2 === 0 ? 
                new Strawberry() : new Chocolate();
  }
}
```

带着`function`:

```
export const getIceCream = (): IceCream =>
  Math.random() % 2 === 0 ? new Strawberry() : new Chocolate();
```

我使用了一个`random`数字来创建一个或另一个类型的对象。在实际应用中，变量通常是工厂的一个参数或另一个选项。

通过`static`方法或`function`请求一个对象将返回不同的对象。

```
// Static method call 
console.log(Factory.getIceCream().yummy());// Function call
console.log(getIceCream().yummy());
```

# 联合的；共同的

正如我在介绍中所说，有时我喜欢将乐趣加倍，并将两种模式结合起来。

例如，在 [DeckDeckGo](https://github.com/deckgo/deckdeckgo/) 中，我开发了这样一个概念，根据环境(“本地、登台或生产”)获得不同的服务。

应用到上面的`IceCream`片段，这意味着`factory`需要跟踪用`singleton`创建的对象。

```
export class SingletonFactory {
  private static *instance*: IceCream | undefined = undefined;

  static *getInstance*(): IceCream {
    if (!this.*instance*) {
      this.*instance* =
        Math.random() % 2 === 0 ? 
             new Strawberry() : new Chocolate();
    }

    return this.*instance*;
  }
}
```

# 摘要

有许多[模式](https://en.wikipedia.org/wiki/Software_design_pattern)但是，这些是我最常用的。下次我使用另一种类型时，我应该把它收藏起来，它可能值得我写一篇新文章😉。

与此同时，下次你去苏黎世的时候，请品尝一下美味的雪糕🍦。

到无限和更远的地方！

大卫

你可以通过推特[或我的](https://twitter.com/daviddalbusco)[网站](https://daviddalbusco.com/)联系我。

为您的下一个演示，尝试一下 [DeckDeckGo](https://deckdeckgo.com/) 。

[![](img/4bba41bd3bc0b4335e2a0e2b3caa967f.png)](https://deckdeckgo.com)

*更多内容请看*[***plain English . io***](http://plainenglish.io)