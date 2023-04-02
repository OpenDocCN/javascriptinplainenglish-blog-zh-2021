# 不要陷入这三个常见的类型脚本陷阱

> 原文：<https://javascript.plainenglish.io/dont-fall-for-these-3-common-typescript-pitfalls-43dd597fc723?source=collection_archive---------3----------------------->

## 我打赌你以前遇到过这 3 种类型脚本/JavaScript 陷阱…

![](img/3d0f51d61d57c72bc830a2f4bfe8d969.png)

当然，TypeScript 并不完美。这是因为它向后兼容 JavaScript。因此，有些事情可能无法解决，正如你所想的那样。

有些东西是“不幸”设计的，不得不拖着走。你可以称之为遗留问题，如果不破坏已经存在的代码库，这些问题是不容易消除的。

我说重要的是不要只涵盖 TypeScript 的好的部分，还要涵盖不好的部分。只有这样，你才能以专业的方式处理语言。这篇文章给你带来了三个陷阱，最好不要上当。

# 1.数组不是数组，你知道吗？

JavaScript 中的数组只不过是一个对象。一种对象，其上定义了一些方法，并自动分配其键。数组和对象几乎是相同的。证据:JavaScript 的 *typeof* 操作符在数组中使用时会返回*对象*。

特别是，数组和对象在某些地方有相同的行为。在 TypeScript 中的使用可能会导致问题，或者至少会导致意外和不希望的行为。当你想到 OOP 语言中对象遵循的规则集时，这一点就变得很清楚了。但在 JavaScript 中并非如此:它们与面向对象编程中的对象概念几乎没有任何共同之处。因为几乎没有传统面向对象的所有属性。相反，它们类似于所谓的字典或关联数组。

要在 JavaScript 中定义一个对象，试着想想可以用它做些什么。基本上，你是在运行时添加、修改、删除等等。这更像是字典中的键值对，不是吗？但在 JavaScript 中，这是对象的定义。如果将类型简单地称为字典而不是对象，JavaScript 中就会少一个绊脚石。

每当你试图处理一个不存在的键时:正常的行为会导致一个编译器错误。您甚至不能编译访问不存在的属性的代码。但在 JavaScript 中，严格来说，我们甚至没有对象，而是字典。所以键下是否有条目的问题不能在编译时回答，只能在运行时回答。因此，当访问对象的未设置属性时，JavaScript 只返回未定义的值。

数组也不像其他语言中的经典数组。主要的区别是它的变量大小。在 C#中，你需要一个泛型类型，比如集合或列表，大小是可变的。数组必须在写入任何值之前定义其大小。JavaScript 对数组没有这种限制。它可以在运行时动态放大/缩小。JavaScript 也知道所谓的稀疏数组，其中只有实际使用的值才占用内存。与 C 语言相比，数组的内部表示的结构非常不同。

这些收集到的差异对 TypeScript 产生了影响。TypeScript 确实不得不以同样的方式处理这些事情:

否则，将失去与 Java 脚本的向后兼容性，而这正是 TypeScript 想要不惜一切代价保留的。

我们来看看如何在 TypeScript 中定义数组

这确保了它是一个数字数组，因此，下面的调用是有效的:

尝试使用 number 之外的类型的调用会导致编译器错误:

读访问的行为如何？人们会认为访问索引 0 会返回 number 类型的值。正如对函数 *toFixed* 的调用所证明的，这是完全相同的，只在这个数据类型上定义:

当访问一个没有设置值的索引时会发生什么？事实上，如上所述，JavaScript 返回未定义的*，这就是类型应该考虑这一点的原因:可能返回的数字取决于索引，但也可能是未定义的。作为一名优秀的开发人员，您当然会意识到这一点，并努力将它考虑在内:*

*事实上，TypeScript 编译器现在抱怨说，与未定义的进行比较是不必要的——毕竟， *someStack* 属于类型*编号*。这显然是错误的，因为类型也可能是未定义的。这意味着以下内容的数组定义:*

*不应该导致数组中的每个元素都是类型 *number* ，而是类型 *number | undefined* 。这可能是正确的，但这正是 TypeScript 没有做到的！*

*当然，这个问题可以通过相应地定义数组来轻松解决:*

*不得不为每个阵列手动执行这一操作很烦人，事实证明并没有这样做。在这种情况下，应该始终注意类型系统会假装一种虚假的安全感。*

# *2.对象不是对象？{}是记录？等等什么？*

*正如我提到的，JavaScript 中的对象最终是包含键值对的字典，其条目可以改变。但是如何正确地输入它们呢？*

*一个明显的例子是当对象被认为表现得像一个经典对象时的场景。如果它有一组定义良好的属性和方法(如果需要的话),那么它就是真的。然后可以定义一个类或一个接口来描述对象:*

*为了类型安全，这两种情况具有相同的效果。类型为*字符*的对象——不管*字符*是如何定义的——现在总是具有属性*昵称*和*比赛*，这正是这里要确保的。*

*当我们故意把一个物体当作字典使用时，情况就不同了。属性的数量和名称在运行时会有所不同。可以肯定的是，这可能是一个“*对象*”。空对象是一种极端情况，人们可能倾向于简单地指定 *{}* 作为类型。*

*不幸的是 *{}* 作为类型规范并不意味着*空对象*。它的意思是任何非空值。然后你可以简单地切换到*对象*，但这也不是选项。事实上，如果你用*对象*键入它，你的意思是拥有一个任意值，它不对应于*空值*。*

*那么*物体*就适合了，对吗？(注意，*对象*，不是*对象*)嗯，这种类型也有问题，说到用法。不可能检查或确保某个密钥是否存在。它只描述了一个空的对象。*

*为了充分利用它，使用通用数据类型 *Record < TKey，TValue >* 。这内置于 TypeScript 中，描述了从键到值的映射。但是要注意，不要犯轻易填写带有*字符串*和*任意*的类型的错误。这样就会错过这个操作的最初原因。使用*未知的*代替。这迫使你在访问一个属性时进行适当的强制转换，就像任何一个属性一样。不幸的是，这里也有问题。当处理定义为接口的对象时，TypeScript 不允许您处理类型为 *<字符串、未知>* 的*记录*。*

*总结一下，在 Typescript 中有多种方法来描述表现为字典的对象。它们都不简单，或者不能很好地与语言的其他部分配合。这就像在生活中，你不能总是得到你想要的，这更像是一场你需要什么和什么最适合你的游戏。因此，明智地选择你的行动方式，你会得到回报。但是苦涩的余味总是存在，因为 *{}* 和*对象*的行为不一样，当然也不像预期的那样。*

# *3.for-in 和 for-of 有什么区别？*

*JavaScript 提供了几种循环类型，除了经典的计数循环*用于*之外，还有其他选项可供选择。[*for-in*迭代对象键，当然还有 *for-of* 迭代所有可迭代类型](https://bitsofco.de/for-in-vs-for-of/)。不要忘记 *forEach* 循环，它只在数组上可用。[4]*

*这些年来，你可能还注意到，你可以用 *for-of* 循环覆盖几乎所有的循环类型。正因为如此，linters 为此引入了一个规则。甚至有一个 ESLint 规则[1],每当它可以替换默认的 *for* 循环时，强制使用 *for-of* 循环。*

*与函数 *Object.keys* 、 *Object.values* 和 *Object.entries* 结合使用， *for-of* 循环可用于迭代对象的键、值或两者。没有理由再使用任何其他类型的循环。至少如果不使用 TypeScript 的话。如果使用以下构造，TypeScript 会报告一个错误:*

*该错误声明不确定一个键是否实际上是字符中的一个键——即使您正在遍历字符对象的键，因此它必须包含定义中的键！*

*通过使用 *Object.entries* 来防止这种情况，以避免手动解析密钥。这适用于读取权限。这种方式不包括写访问。例如用户定义的对象克隆功能。*

**for-in* 循环是唯一可以帮助你离开这里的循环。此外，还有一些副作用。因为它不仅返回并遍历给定对象的键，还迭代来自原型的键。因此，最好使用一个合适的[保护](https://medium.com/@scadge/if-statements-design-guard-clauses-might-be-all-you-need-67219a1a981a) - [子句](https://refactoring.com/catalog/replaceNestedConditionalWithGuardClauses.html)，它确实检查了 *hasOwnProperty* 以保持在给定对象的属性内。[2] , [3]*

*幸运的是，这种情况最终被 *for-of* 循环抛在了脑后，但是没有！打字稿偷偷带回来的。*

# *结论*

*TypeScript 中有些东西至少是不幸实现的。我们不能再期待改变了。这只会破坏与以前的 TypeScript 版本的兼容性。*

*使用 *for-of* 循环的例子很烦人也很麻烦，但是是可以解决的。例 1 和例 2 要严重得多。它们只能通过开销和不方便的方式来解决。例如，通过额外指定*未定义*来正确输入数组，或者对象被用作字典。*

*还有更多的设计缺陷，但我认为本文提出的这三个缺陷是 TypeScript 中最常见的误解。*

*不要忘记，Typescript 是一种很好的语言，可以用来编写轻量级和高效的代码。使用它很有趣，但主要是要确保知道你的工具的好与坏！*

*[***节省自己大量的时间，专注于重要的主题。***](https://arnoldcodeacademy.ck.page/26-web-dev-cheat-sheets)*

# *继续读*

*[](https://medium.com/agileinsider/is-kanban-just-putting-sticky-notes-onto-a-wall-1d8c3092213e) [## 看板只是把便签贴在墙上吗？

### 关于何时以及何时不使用看板的看板指南

medium.com](https://medium.com/agileinsider/is-kanban-just-putting-sticky-notes-onto-a-wall-1d8c3092213e) [](https://medium.com/front-end-weekly/html-dom-guide-for-everyone-ec07fdca93a1) [## 面向所有人的 HTML DOM 指南

### 关于 HTML 5 中的 DOM 您必须知道的一切

medium.com](https://medium.com/front-end-weekly/html-dom-guide-for-everyone-ec07fdca93a1) [](https://medium.com/javascript-in-plain-english/the-dark-side-of-typescript-try-catch-deeded18ba0d) [## TypeScript 中 Try/Catch 的黑暗面

### 用“unknown”转义 TypeScript 4.0 中的任何错误异常

medium.com](https://medium.com/javascript-in-plain-english/the-dark-side-of-typescript-try-catch-deeded18ba0d) 

## 资源

[1]ESLint rule For-of:[https://github . com/sindresorhus/ESLint-plugin-unicorn/blob/master/docs/rules/no-For-loop . MD](https://github.com/sindresorhus/eslint-plugin-unicorn/blob/master/docs/rules/no-for-loop.md)
【2】Guard-clause:[https://refactoring . com/catalog/replacenesteddconditionalwithguardluctions . html](https://refactoring.com/catalog/replaceNestedConditionalWithGuardClauses.html)
【3】Guard clause Medium 教程:[https://Medium . com/@ scadge/if-statements-design-design](https://medium.com/@scadge/if-statements-design-guard-clauses-might-be-all-you-need-67219a1a981a)*