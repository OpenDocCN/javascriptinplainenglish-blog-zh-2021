# JavaScript:‘一切都是对象’，是吗？

> 原文：<https://javascript.plainenglish.io/javascript-everything-is-an-object-or-is-it-2f1092403dc3?source=collection_archive---------10----------------------->

## 快速浏览数据和结构类型。

![](img/d5390b8db7a0b390c9b94c6cf14d667f.png)

Photo by [Ash Edmonds](https://unsplash.com/@badashproducts?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

你听说过“JavaScript 中的一切都是一个*对象*”这句话吗？当我第一次学习 JS 的时候，我有一个老师对我说了这句话，我一直记在心里。当你第一次开始时，它确实给你这种轻松感和一种安全感，但我一直在想，这个通用短语并不完全正确。事实上，我敢说，这是误导。

这个想法是在我潜心研究 JS 的基础知识时产生的，目的是发现我在熨斗学校的旋风时期可能错过的一些小事实。我上周写了关于[编写循环](https://jmhero05.medium.com/javascript-loops-there-is-more-than-for-9ecda7e784d6)的不同方法，更多的是语法上的分解，而不是其他，我本周的思路引导我到值，也就是数据类型。当我对 JS 中的各种值使用`typeof`操作符时，我偶然发现了`typeof({});`。如你所料，如果你了解这种语言的话，`“object”`又回到了控制台。出于某种原因，这让我想到了“JavaScript 中的一切都是一个*对象*”这句话。如果 JS 中的一切都是对象，那么为什么`typeof(2)`不返回`“object”`而返回`“number”`？

现在，从大的方面来看，坚持“JavaScript 中的一切都是对象”这一说法不会让人们转过头来嘲笑你(嗯，也许有些人会，但你没有这样的人会更好#goodvibesonly)。当我开始学习 JS 时，它确实帮助了我，并且我继续把许多不同的数据/结构类型看作对象，这取决于我如何使用它们。但是，这不再是开始，我已经长大了。那么，在处理面向对象编程时，我们如何区分什么是“对象”，什么不是呢？

简单回答？[‘对象是指包含数据和处理数据的指令的数据结构。’](https://developer.mozilla.org/en-US/docs/Glossary/Object)

对象是包含数据的数据结构。它们可以是一个简单的键/值对，也可以是一个复杂的嵌套键/值对系统，代表一个用户及其所有帖子、喜欢、朋友、评论、个人数据等。它们可以将多个值存储为属性。现在，我可以继续深入下去，试着给出一个完整的，包罗万象的解释，关于什么是对象，就像数组也是对象一样，但是你得到了要点。事实上，我现在明白为什么我最初被告知“JavaScript 中的一切都是一个*对象*”。这是一个复杂的话题。也许讨论原始值更好，为什么它们不是对象。

JavaScript 包含七种原始数据类型:

> **未定义** ( `undefined`)，用于无意遗漏的值。
> 
> **Null** ( `null`)，用于故意缺失值。
> 
> **布尔值** ( `true`和`false`)，用于逻辑运算。
> 
> **数字** ( `-100`、`3.14`等)，用于数学计算。
> 
> **字符串** ( `"hello"`、`"abracadabra"`等)，用于文本。
> 
> **符号**(不常用)，用于隐藏实现细节。
> 
> **BigInts** (生僻新)，用于大数的数学。
> 
> 丹·阿布拉莫夫

*(快速旁注:* `null` *使用* `typeof()` *运算符时，技术上返回* `*‘object’*` *。当我知道那是因为最初版本的 JavaScript* *中的一个* [*错误时，我已经岁了。放心，* `null` *是基元值，不是对象。)*](https://2ality.com/2013/10/typeof-null.html)

我认为原始数据类型的一种方式是，它们被认为是快速和“轻量级”的。对象由于持有如此多不同的原始类型而陷入困境，变得相当“沉重”。然而， [Brendan Eich](https://en.wikipedia.org/wiki/Brendan_Eich) 知道 JavaScript 的用户想要以不同的方式访问这些原始类型。引入[原始包装对象](https://developer.mozilla.org/en-US/docs/Glossary/Primitive#primitive_wrapper_objects_in_javascript)。

用 JS 开发原始包装器对象为我们的一些原始数据类型提供了不同的方法。我找到了一个很好的资源来解释这个问题，比我在下面所能解释的要好得多:

> 这个解决方案看起来有点尴尬，但事实就是这样:
> 
> 1.原语还是原语。单个值，根据需要。
> 2。该语言允许访问`Strings`、`Numbers`、`Booleans`和`Symbols`的方法和属性。
> 3。为了让它工作，一个提供额外功能的特殊的“对象包装器”被创建，然后被销毁。
> 
> 每个原语类型的“对象包装器”是不同的，分别称为:`String`、`Number`、`Boolean`和`Symbol`。因此，它们提供了不同的方法集。
> 
> 例如，有一个字符串方法 [str.toUpperCase()](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/String/toUpperCase) 返回一个大写的`str`。
> 
> 它是这样工作的:
> 
> `let str = "Hello";
> alert( str.toUpperCase() ); // HELLO`
> 
> 简单吧？下面是在`str.toUpperCase()`中实际发生的事情:
> 
> 1.字符串`str`是一个原语。所以在访问它的属性时，创建了一个特殊的对象，它知道字符串的值，并且有有用的方法，比如`toUpperCase()`。
> 2。该方法运行并返回一个新字符串(如`alert`所示)。
> 3。特殊对象被销毁，只剩下原语`str`。
> 
> 所以原语可以提供方法，但是它们仍然是轻量级的。

我的朋友们，这也是你在这里提到“JavaScript 中的一切都是一个对象”的原因之一。从技术上讲，这是一个错误的说法。在 JavaScript 中不是所有的东西都是对象。也许这句话应该是“JavaScript 中的一切*都可以表现为*一个对象”？谁能说呢？我所知道的是，最初的短语可能会误导人，但它确实对我的 JS 努力有所帮助。

你认为什么是更好的短语？让我知道这是否有帮助！

快乐编码🤓

**来源:**

[1]丹·阿布拉莫夫。“[就 JavaScript] 02。JavaScript 宇宙”(电子邮件，2021 年 2 月 17 日)[就 JavaScript](https://justjavascript.com/) 。