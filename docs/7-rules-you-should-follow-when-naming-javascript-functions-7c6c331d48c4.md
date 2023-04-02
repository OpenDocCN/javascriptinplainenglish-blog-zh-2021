# 命名 JavaScript 函数时应该遵循的 7 条规则

> 原文：<https://javascript.plainenglish.io/7-rules-you-should-follow-when-naming-javascript-functions-7c6c331d48c4?source=collection_archive---------9----------------------->

下面是命名函数时要遵循的简单规则，这样代码就能保持清晰易懂。用一些快速的解释来帮助记住它们。

![](img/8b90d090c2b841cd3292b7f7cb0c4b98.png)

Photo by [Gita Krishnamurti](https://unsplash.com/@ramm_?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 1.不要撞东西

避免使用相同范围内其他事物的名称。偏爱有助于这一点，但是棉绒也有帮助。覆盖功能会导致错误和混乱。这是 JavaScript 中可能发生的事情，程序员必须保持警惕。

![](img/e346690e74eab6bfb37aaac6ba7515aa.png)

Photo by [Romain Vignes](https://unsplash.com/@rvignes?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 2.使用描述性动词

功能是要做的动作，要计算的计算，以及在编程中要出现的新对象。这有助于让代码看起来像简单的英语(或者团队使用的任何语言)，这有助于使事情变得简单。确保动词与函数的功能相匹配。动词可以是先行词，但通常要尝试用动词作为函数名的开头。

![](img/5367f3ee000ecd422dd5a8b731256902.png)

Photo by [UX Indonesia](https://unsplash.com/@uxindo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 3.避免名称空间描述符

避免用同一个词来描述一组功能所交互的事物。相反，创建一个类或模块，并删除常见的形容词。

![](img/ad1b033407962ea749fbe868973e0cbd.png)

Photo by [Alice Donovan Rouse](https://unsplash.com/@alicekat?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 4.使用一致的格式

如果程序的大部分是 camelcase，没有一个是外部 API，避免使用`_`(下划线)作为分隔符，而使用 camelcase。或者反之亦然，作为一个团队来决定。

遵循更漂亮的文件(如果有的话),或者在与团队讨论之后将一个文件添加到项目中。

![](img/195b5246b0cbdcb17da32f8259e6b437.png)

Photo by [Tim Mossholder](https://unsplash.com/@timmossholder?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 5.没有悬挂下划线

不要在函数名的开头加下划线。这不会像在其他语言中那样对 JavaScript 函数产生影响。一些棉短绒将呼吁这一点。如果你希望一个函数是私有的，考虑一下为什么你认为另一个程序员会看到这个函数并试图使用它。然后改变设计，也许用一个关闭。

![](img/f2e400297e3358efb33fe8b0eef8a8b6.png)

Photo by [Braden Collum](https://unsplash.com/@bradencollum?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 6.准备出发

对于 JavaScript `class` 中的 Setters & Getters，使用`get functionName`和`set functionName`，这样可以编写专注于功能主题的代码，避免命名中的冗余。

![](img/918a923df9c7e34d4ccae114089ddabd.png)

Photo by [Felicia Buitenwerf](https://unsplash.com/@iamfelicia?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 7.使用简单的英语

越少搜索以了解正在发生的事情越好。使用简单的英语，避免多音节短语，尽量减少行话。保持内容易于阅读。记住代码是一种语言，不仅仅是执行命令。函数的名字对计算机来说几乎不起任何作用。这是试图向阅读代码的人传达信息。

# 结论

这里有七个简单的规则来命名函数，这样代码就清晰易懂了。我希望您发现这很有用！感谢您的阅读。