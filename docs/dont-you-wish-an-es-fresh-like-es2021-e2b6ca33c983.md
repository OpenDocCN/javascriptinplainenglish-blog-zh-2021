# 所有 ES2021 已确认的 JavaScript 更改

> 原文：<https://javascript.plainenglish.io/dont-you-wish-an-es-fresh-like-es2021-e2b6ca33c983?source=collection_archive---------12----------------------->

![](img/a0de7fde43e2c30c43110240080fbf8c.png)

Image Credits: [moroioh.com](https://morioh.com/)

ES2020 的发布时间不长，但其他功能已经在开发中，只等发布。TC39 工作组负责将这些特性纳入 ECMAScript 标准的新版本。这篇文章为您带来了 TC39 第 4 阶段已经具备的特性。

TC39 提供以下阶段:

## **阶段 0:稻草人**

TC39 成员可以提出以前没有提出过的(或以前被完全否决的)任何想法、变化或补充。

## **第一阶段:提案**

TC39 成员创建了一个提案。它描述了一个具体的问题和相关的解决方案。

## **第二阶段:草稿**

提案的语法和语义用正式规范语言描述。

## **第三阶段:候选人**

提案的规范已经完成，审阅者已经批准了它。第 4 阶段—完成:提案可以包含在即将发布的 ECMAScript 版本中。

## **第四阶段:完成**

该提案可能会包含在即将发布的 ECMAScript 版本中。ES2021 大概会在 2021 年 6 月发布。

# 逻辑赋值运算符

逻辑赋值运算符组合了逻辑运算符和赋值表达式。它们使代码更短，并使变量和对象属性的条件值赋值更容易。ES2021 将引入三种新的逻辑运算符，每种运算符处理两个操作数。

```
||=  *// combines logical OR with ASSIGN* &&=  *// combines logical AND with ASSIGN* ??=  *// combines NULLISH with ASSIGN*
```

逻辑 OR 运算符`||=`是逻辑运算符`||`和赋值运算符的组合。如果右操作数的值为*false*(即测试结果为 false 的值)，并且是符号`a||(a=b)`的缩写形式，则将右操作数赋给左操作数。

逻辑 AND 赋值操作符`&&=`的工作方式相同，但它组合了逻辑`&&`操作符和赋值操作符，并且仅当第一个操作数具有*真值*时，才将右操作数赋给左操作数(即评估为真的值)。它是符号`a&&(a=b)`的简称。

逻辑*无效*赋值`??=`的操作符是符号`a??(a=b)`的缩写。只有当第一个操作数为空或未定义时，它才会将第二个操作数赋给第一个操作数。

新运算符对于对象属性的初始化非常方便。它们有助于在内部确保对象`person`的属性`firstName`用值`Commander`初始化，如果属性还没有被赋值的话。

我们很快就走完了老路:

使用 ES2021，您可以缩短整个结构:

总之，您只是缩短了为未初始化的变量分配默认值的方式。出发地:

```
person.firstName = person.firstName|| person.firstName='Commander';
```

收件人:

```
person.firstName ||= 'Commander';
```

***注意*** *:除此之外，旧的方法停止了对可能存在的 getter 方法的访问。另一种方法是调用底层的 getter，如果存在的话。*

# 字符串替换

当您替换字符串中所有出现的子字符串时，使用正则表达式是最好的方法。您还可以使用 polyfill 函数`replaceAllPolyfill()`，该函数将指定正则表达式的全局搜索应用于相应的字符串。

另一个选择是使用字符串方法`split()`来完成。这个方法在传递的子字符串出现的所有地方分割字符串，并将各个部分作为数组返回。在这个数组上调用`join()`,指定要插入的新字符串，将整个事情放回一起。

应该清楚的是，由于性能原因，这些方法效率较低。长字符串和频繁出现的搜索字符串会很快发现这一点。`replaceAll()`方法将来会简化这一切:它用指定为第二个参数的新字符串替换指定为第一个参数的子字符串的所有出现。

正如你现在看到的，我们可以优化一切，以编写更少的代码和更高的性能。

# 承诺

ES2020 已经有了一个通过`allSettled()`方法扩展承诺的特性。在 ES2021 我们会在这个团队中得到一个新的玩家，他就是`any()`。它期望得到一个可重复的承诺，并返回一个承诺，当一个承诺被实现时，这个承诺就被实现。每当所有通过的承诺被拒绝时，同样的行为对于拒绝也是有效的，并且`any()`返回一个被拒绝的承诺。在后一种情况下，用户可以通过`AggregateError`访问关于所有被拒绝承诺的相应错误的详细信息。

如您所见，当滚动异步解决/拒绝承诺示例时，`any()` 函数等待第一个解决的示例，然后才打印出`firstResolver`。当每个承诺都被拒绝时，它会为 try-catch 包装器触发一个错误。第三个例子清楚地说明了为什么`firstResolver`没有控制台打印。

# WeakRefs

我打赌你知道`WeakSet`和`WeakMap`。自 ES2015 年开始实施。WeakSet 是对象的集合。WeakMap 是键-值对的集合，其中每个键必须是一个对象。它们之间的联系是让对象被弱引用。这意味着，如果没有对这些对象的其他强引用，这些对象可以作为垃圾收集的一部分从内存中移除。因此，对对象的弱引用是一种不阻止垃圾收集器从内存中移除该对象的引用。相反，正常(或强)引用将对象保存在内存中。

ES2021 可以通过手动使用`WeakRef`对象来创建对`WeakSet`或`WeakMap`上下文之外的对象的弱引用。相应的建议警告您在使用`WeakRef`之前要小心。无论如何，检查它的使用是否合理。基本上，如果可能的话，应该避免使用。垃圾收集太复杂且依赖于系统，因此很难预测垃圾收集器的确切行为。

# 二进制、十六进制和 BIGINT 最终变得可读

阅读大数字容易吗？我介意的答案是:不！这同样适用于大整数、大二进制数和十六进制数。那么，为什么要等到 2021 年才引入大数值的可读格式呢？我不知道，因为其他语言也有(Java、Python、Perl、Ruby 和 C#)，但现在 JavaScript 也有了。数字分隔符的功能将帮助我们的眼睛保持清醒。

有了这个分隔符，我们只需将分隔符放在相应的数字组之间，就可以使数值更具可读性。分隔符适用于十进制记数法中的数字、二进制或十六进制记数法中的数字，并使用 ES2020 中引入的 BigInts。

***注意*** *:通过* `*===*` *运算符比较时，分隔符不影响数值。*

# 结论

Javascript 的标准一直在稳步发展。虽然发布还有几个月，但一些相当不错的功能已经完成，正在等待 2021 版的大发布。如果所有的特性都融入到新版本中，这将是 JavaScript 的又一次伟大的进步。在[https://github.com/tc39/proposals](https://github.com/tc39/proposals)上展示了当前状态的概述，在[https://github . com/tc39/proposals/blob/master/finished-proposals . MD](https://github.com/tc39/proposals/blob/master/finished-proposals.md)上提供了第四阶段功能的概述。[1], [2]

张贴支持表的图片是不够的，因为一旦我做了一个截图，该表几乎立即过时。点击[这里](https://kangax.github.io/compat-table/esnext/)查看对通用操作系统、服务器端 JavaScript 运行时环境(如 Node.js)和移动浏览器的支持。

为你自己节省大量的时间，专注于重要的主题。

**延伸阅读**

[](https://medium.com/javascript-in-plain-english/dont-fall-for-these-3-common-typescript-pitfalls-43dd597fc723) [## 不要陷入这三个常见的类型脚本陷阱

### 我打赌你以前遇到过这 3 种类型脚本/JavaScript 陷阱…

medium.com](https://medium.com/javascript-in-plain-english/dont-fall-for-these-3-common-typescript-pitfalls-43dd597fc723) [](https://medium.com/agileinsider/is-kanban-just-putting-sticky-notes-onto-a-wall-1d8c3092213e) [## 看板只是把便签贴在墙上吗？

### 关于何时以及何时不使用看板的看板指南

medium.com](https://medium.com/agileinsider/is-kanban-just-putting-sticky-notes-onto-a-wall-1d8c3092213e) [](https://medium.com/front-end-weekly/html-dom-guide-for-everyone-ec07fdca93a1) [## 面向所有人的 HTML DOM 指南

### 关于 HTML 5 中的 DOM 您必须知道的一切

medium.com](https://medium.com/front-end-weekly/html-dom-guide-for-everyone-ec07fdca93a1) 

**参考文献**

[1] TC39 提案[https://github.com/tc39/proposals](https://github.com/tc39/proposals)

[2] TC39 第四阶段功能[https://github . com/TC39/proposals/blob/master/finished-proposals . MD](https://github.com/tc39/proposals/blob/master/finished-proposals.md)。

[3]https://kangax.github.io/compat-table/esnext/ECMA 支持表