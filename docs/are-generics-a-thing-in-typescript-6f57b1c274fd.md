# 泛型是 Typescript 中的东西吗？

> 原文：<https://javascript.plainenglish.io/are-generics-a-thing-in-typescript-6f57b1c274fd?source=collection_archive---------10----------------------->

## 使用泛型意味着知道意想不到的事情！

![](img/0970581459c005e99c1dcafd441e4f4d.png)

[timJ](https://unsplash.com/@the_roaming_platypus) via [Unsplash](https://unsplash.com/photos/ots0EOYuGtU) (CC0)

在 Typescript 中创建堆栈需要完成什么任务？很少。我们只需要一个类作为数组的包装。出于简单的原因，我们将忽略错误处理。下面是堆栈的基本结构。

这是一个功能良好的常见堆栈。但是作为一个聪明人，你马上会发现 Typescript 中的这个堆栈根本不是类型安全的。这不是一个普通的。我打赌你通过发现 *any* 的用法猜到了这一点。[1]要想出一个快速而肮脏的解决方案，我们可以切换到未知的*类型。但是这能让事情变得更好吗？不完全是。只是避免不负责任地访问堆栈元素的任何属性。*

*更常见的需求是数字堆栈。为了满足这个要求，我们只需将*的类型任意*改为*号*。但是如果你需要一个文本类型的堆栈呢？当然只是复制粘贴代码，用*字符串*替换每次出现的*数字*。那么，其他类型甚至阶层呢？作为一个好的程序员意味着，你能够发现这是一个简单的违反[单一责任原则](https://medium.com/unity-hub/unity-solid-s-single-responsibility-6707d9569e73)和[干](https://medium.com/next-level-source-code/do-you-follow-these-10-principles-for-good-programmers-1445727af447)的法律(不要重复自己)。[2]*

*对另一种类型采取相同的行动？这难道不是仿制药的一个例子吗？对我来说，是的！*

# *仿制药拯救你*

*泛型人进入现场，让你意识到泛型的存在！*

*泛型是可参数化的数据类型。在某种程度上类似于正常变量，但能够收集不同类型的值。但是泛型有所谓的*类型变量*来保存它们现在服务的类型。知道了这一点，我们就可以用一种通用的方法来重新定义我们的堆栈。*

*T 代表该类应该处理的具体数据类型。尽管约定描述泛型类型应该有 T21，但这不是最好的选择。从另一个角度看实现揭示了真相。堆栈通过它保存的项目来定义自己。一个更好的名字应该是: *TItem**

*无论你按什么键，你都会得到和你弹出的键相同的类型。这导致了泛型类型的定义。但是像生活中的一切一样:*

> *每个故事都有两面性[…]——乔纳森·爱德华兹*

*这段引文让我们得出结论，我们需要为 *TItem* 传递一个类型。它只不过是一个变量。为数字创建一个堆栈意味着这样调用它:*

**标题*替换为*号*。实例的每个泛型方法也将拥有类型*号*。你还需要一个字符串堆栈吗？然后，您可以使用与创建数字堆栈相同的方式来完成此操作，但使用另一种类型，为创建传递:*

*你不能选择两个筹码吗？您也可以使用联合堆栈来实现，两者都接受:*

*关闭门，我们也可以做一个*任何*堆栈:*

*就是这样，我们又在跑圈了！但是现在我们已经从文章的开头获得了一个可配置的原始堆栈变体。*

*您可能需要一个默认的堆栈类型，因此也可以配置它。在这里，您可以创建它并根据您的需要定义 *TItem* 。*

# *在函数中键入参数*

*Typescript 允许我们对其他类型使用泛型。当然，您首先想到的是接口！这没什么不同。相反，它几乎是相同的，因此非常直观:*

*有趣的是，泛型和函数一起使用，而不是任何类或接口的一部分。如果这是您的愿望，您必须在泛型函数中定义类型参数:*

*上面的例子描述了传递的值的返回，没有改变，但是类型安全的。像这样调用函数:*

*因为能够从构造函数中读取函数的泛型类型，所以没有必要明确提及类型。*

# *Typescript 中的默认泛型*

*而不是使用您自己定义的泛型类型。Typescript 附带了一些现成的泛型。最常见的一种:*偏<T>。我打赌你这辈子已经见过一个了。如果没有，没时间担心，最好继续读下去。**

*这个简短的词将传递的类型的所有属性标记为可选，并允许您只初始化属性的子集。*

*常数只描述整个对象的一些属性，而不是整个属性列表。可以访问未定义的属性，但是正如我提到的，当用*Partial<T>创建一个对象时，没有必要定义它们。**

**挑<T>和*省略<T>是两个有趣的家伙。它们允许您构建必须定义了某些属性的类型，或者分配一些属性。***

*同样非常重要的是要知道*记录< Tkey，t value>。这定义了一个具有两种泛型类型的字典。例如:**

*你可以通过添加新的属性来扩展这个字典，只要它们遵循的排版是一对<*字符串，数字>* 。*

*如果你现在很好奇，想要更深入地了解泛型类型的完整列表，你可以通过阅读关于实用程序类型的 [Typescript 文档来实现你的愿望。[1]](https://www.typescriptlang.org/docs/handbook/utility-types.html)*

# *结论*

*通过使用泛型，您可以保持代码干净，避免冗余和重复。此外，您的代码是类型安全的。也包括单一责任原则和 DRY 法的保留。*

*说出你的泛型类型，而不仅仅是 *T* ，让它们变得容易理解，就像我用 *TItem* 例子向你展示的那样。如果您的代码充满了 *T* ，您将无法再识别差异。*

*与[变量命名](https://medium.com/next-level-source-code/naming-variables-and-methods-write-better-code-part-2-5707e54250f1)相同的规则对于泛型类型的创建是有效的。*

## *进一步阅读*

*[](https://medium.com/next-level-source-code/naming-variables-and-methods-write-better-code-part-2-5707e54250f1) [## 命名变量和方法-编写更好的代码第 2 部分

### 如何编写表达自己的代码，以便更好地使用命名进行编码

medium.com](https://medium.com/next-level-source-code/naming-variables-and-methods-write-better-code-part-2-5707e54250f1) [](https://arnoldcode.medium.com/increase-annual-salary-with-these-3-simple-tactics-145f8bc03c60) [## 用这三个简单的策略增加年薪

### 做他们梦想和噩梦的汽车！

arnoldcode.medium.com](https://arnoldcode.medium.com/increase-annual-salary-with-these-3-simple-tactics-145f8bc03c60) [](https://medium.com/agileinsider/comparison-of-scrum-vs-scrumban-vs-kanban-1d1d2b9a9fd5) [## Scrum 与 Scrumban、看板的比较

### 正确选择的快速指南！

medium.com](https://medium.com/agileinsider/comparison-of-scrum-vs-scrumban-vs-kanban-1d1d2b9a9fd5) 

## 参考

[1]泛型:[https://www.typescriptlang.org/docs/handbook/generics.html](https://www.typescriptlang.org/docs/handbook/generics.html)
[2]如何在类型脚本中使用泛型 https://www . digital ocean . com/community/tutories/type script-泛型-in-typescript
[3]实用程序类型:[https://www . typescripttlang . org/docs/manual/Utility-type . html](https://www.typescriptlang.org/docs/handbook/utility-types.html)*