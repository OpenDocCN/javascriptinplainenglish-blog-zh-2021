# 每个 TypeScript 开发人员都应该知道的 7 种实用工具类型

> 原文：<https://javascript.plainenglish.io/7-utility-types-that-every-typescript-developer-should-know-788fe73421f1?source=collection_archive---------3----------------------->

![](img/0f7006b3f8b93fc8f23638ea9a7ee440.png)

Photo by [Martin Adams](https://unsplash.com/@martinadams?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

TypeScript 中的类型系统非常强大。它为 JavaScript 程序提供了类型安全和文档，并允许它们轻松快速地伸缩。虽然类型系统如此有用和受欢迎，但如果我们不计划和设计类型和接口，它也会使我们的代码变得混乱。

# **仿制药**

无论我们从避免代码重复中获得什么好处，我们也可以从创建可重用类型中获得。很像为重复逻辑创建函数，*泛型*是一个类型脚本特性，允许我们编写可重用的类型。

让我们看一个例子:

通过将正确的类型放入 Add 的泛型中，它可以用于描述两个数字的求和或两个字符串的串联。我们只需要用泛型做一次，而不是为每个函数写一个类型。它不仅节省了我们的努力，而且使我们的代码更干净，更不容易出错。

# 实用程序类型

TypeScript 本身提供了几个有用的实用工具类型来帮助我们进行一些常见的类型转换。这些实用程序类型是全球可用的，它们都利用了泛型。

下面是每个 TypeScript 开发人员都应该知道的 7 种功能强大但易于使用的实用程序类型。

# **1。点选<类型，按键>**

Pick 实用程序类型通过从*类型*中挑选一组属性*键*来创建一个新类型，这些键可以是一个字符串或字符串的并集。*键*的值必须是*类型*的键，否则 TypeScript 编译器会报错。当您希望通过从具有大量属性的对象中拾取某些属性来创建较轻的对象时，该工具类型特别有用。

# 2.省略

省略实用程序类型与 Pick 相反。 *Keys* 没有说明要保留什么属性，而是指要省略的一组属性键。当您只想从对象中删除某些属性并保留其他属性时，它会更有用。

# 3.部分

分部实用程序类型构造了一个类型，其中*类型*的所有属性都设置为可选。当我们编写一个对象的更新逻辑时，它会非常有用。

# 4.必需的

所需的实用程序类型与 Partial 相反。它构造了一个类型，其中*类型*的所有属性都设置为 required。它可用于确保类型中不出现可选属性。

# 5.只读

Readonly 实用程序类型构造了一个类型，其中类型的所有属性都设置为只读。为其变量和属性重新分配新值将导致 TypeScript 警告。

# 6.记录

记录实用程序类型用属性键从*键*和类型*类型*的值构造一个对象类型。

# 7.ReturnType

ReturnType 实用工具类型从函数类型的返回类型构造类型。当我们处理来自外部库的函数类型并希望基于它们构建自定义类型时，这是非常有用的。

除了上面提到的，还有其他的工具类型可以帮助 TypeScript 开发人员编写更干净和“更简洁”的类型。关于实用程序类型的 TypeScript 文档的链接可以在[这里](https://www.typescriptlang.org/docs/handbook/utility-types.html)找到。

# 结论

实用工具类型是 TypeScript 提供的非常有用的功能。开发人员应该利用它们来避免硬编码类型。

*更多内容看* [***说白了。***](https://plainenglish.io/)

*报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) ***。***

***对缩放您的软件启动感兴趣*** *？检查出* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。*

# 进一步阅读

[](/typescript-made-easy-a-guide-to-your-first-type-safe-app-with-next-js-wundergraph-and-prisma-e197a59e2b30) [## 轻松编写类型脚本:使用 Next.js、WunderGraph 和 Prisma 编写第一个类型安全应用程序的指南

### 是时候抛开恐惧，学习 TypeScript 了。让我们给你第一次“发现！”瞬间通过建立一个完整的…

javascript.plainenglish.io](/typescript-made-easy-a-guide-to-your-first-type-safe-app-with-next-js-wundergraph-and-prisma-e197a59e2b30)