# 不重复 React 本地化的简单方法

> 原文：<https://javascript.plainenglish.io/the-simple-way-to-not-repeat-yourself-with-react-localization-f9bba4453c2b?source=collection_archive---------13----------------------->

*本地化经常会导致重复翻译——这里有一个处理它的好方法！*

![](img/f80728b0d5b2a47f972fd5857c90055d.png)

Photo by [Sigmund](https://unsplash.com/@sigmund?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果你正在读这篇文章，那么你可能不需要我向你推销**网络应用本地化**的好处。如果你正在构建任何可以在世界范围内访问的东西，那么本地化就不是“生活质量”的提高，而是一项必要的功能**。尽管一个好的用户界面可以不用文字来直观地解释它自己，但是你不需要向你的用户显示文本。**

# 本地化基础

在我正在做的一个项目中，我们在(恰当命名的) [react-localization](https://www.npmjs.com/package/react-localization) 库的帮助下解决了本地化问题。这是一个**超级简单的**库，让你的本地化自动化，不需要太多的思考能力。

用他们的例子；

```
import LocalizedStrings from 'react-localization';

let strings = new LocalizedStrings({
 en:{
   how:"How do you want your egg today?",
   boiledEgg:"Boiled egg",
   softBoiledEgg:"Soft-boiled egg",
   choice:"How to choose the egg"
 },
 it: {
   how:"Come vuoi il tuo uovo oggi?",
   boiledEgg:"Uovo sodo",
   softBoiledEgg:"Uovo alla coque",
   choice:"Come scegliere l'uovo"
 }
});
```

我们创建一个`strings` LocalizedStrings 对象，并在其中定义我们所有的 UI 字符串，并使用国家代码来提供翻译。现在，如果我们将这个对象导入一个组件并编写:

```
<p>{strings.how}</p>
```

*它会* *看起来不同，取决于我们的浏览器是英语还是意大利语。*

恭喜您，您的 web 应用程序现已本地化。任务完成。

# 嗯，工作完成了一半。

关于如何**组织您的翻译文件**，需要做出一个决定。这里有两个主要的选择:

![](img/4d16418d8a481c7b8ae575bf5f29f6c7.png)

1.  **集中的字符串文件** (1 个文件)
    优点
    -总是知道在哪里寻找字符串
    -将所有文件放在一个文件中被认为是“更整洁”
    缺点
    -文件长度是一个巨大的问题-想象你有 1k 个翻译并且你支持 8 种语言
    -很容易在编辑一些语言时出错而忘记其他语言
    -我提到文件大小了吗？它真的不漂亮，而且破坏了任何智能 IDE 自动完成的建议。
2.  **每个组件/文件夹 1 个文件** (n 个文件)
    优点
    -只有组件相关的字符串与该文件相关联
    -人类实际上是可读的
    -可用的 IDE 自动完成建议
    缺点
    -你最终会得到很多额外的文件，有些在
    中很少-很容易在不同的文件中重复字符串(不是很枯燥)

对于我们的项目，我们采用选项 2。这似乎进行得很顺利，但是我们构建的 UI 越多，翻译文件中出现的相同字符串就越多。有些词或短语会出现在用户界面的不同部分，比如“返回”、“提交”、“取消”等等。这些看起来并不是什么大问题，但是它们累积起来就是你在 8 个不同的地方翻译“电子邮件”这个词。为什么这样不好？**D-R-Y——不要重复自己**(我在之前提到的一个*)。那么答案是什么呢？这是我的方法。*

# 把常用的单词放在…一个普通的文件里

据我所知，这并不是一个突破性的想法，但确实有效。我们可以识别经常使用的单词并把它们转移到一个单独的“公共”翻译文件中，而不是让单词的副本在不同的翻译文件中浮动。然后我们需要做的就是包装我们的翻译文件，使它们也包含 common。这是一个如何做到这一点的示例代码片段；

```
//commonStrings.tslet common = new LocalizedStrings({
 en:{
   common: "This is a common string!"
 }
}); export function includeCommon<Type>(strings: Type): Type & typeof ***commonStrings*** {
    return {
        ...strings,
        ...***common*** }
}//uniqueStrings.tslet uniqueStrings = new LocalizedStrings({
 en:{ 
   unique: "This is a unique string!"
 }
});export default includeCommon<typeof uniqueStrings>(uniqueStrings);//TestComponent.tsximport strings from "./uniqueStrings"console.log(strings.common) ---> "This is a common string!"
console.log(strings.unique) ---> "This is a unique string!"
```

希望您可以从底部的 2 个控制台日志中看到，包装我们的

![](img/e570391a4e63507505b1623269683ea0.png)

使用 common 的特定翻译使我们能够访问我们的常用词库。这意味着不再有重复和浪费时间翻译相同的东西！这也意味着我们可以使用 IDE auto completes 来查看我们是否需要翻译一些东西。例如，如果我们正在创建一个具有字符串“Enter”的按钮，我们可以编写`strings.e..`并查看 IDE 是否试图自动完成到`strings.enter`的操作。如果是的话，我们就可以使用这个字符串了。如果没有，那么我们知道我们实际上需要花时间去翻译。不管怎样，我们都做出了正确的决定，这是一个生产力双赢的局面。

# 包扎

本地化对于 web 开发人员来说是一个重要的概念，谢天谢地，像 react-localization 这样的包使得实现起来很简单。然而，最简单的实现并不总是最好的，如果你在开始时投入一点额外的时间，并以一种明智的方式设置它，未来的你会感谢你自己。在配置上花一点时间，在重复上就会节省很多时间。

如果您喜欢这篇文章或觉得它有用，请随意操作。或者，你可以在 Medium [*这里*](https://jamesmbrightman.medium.com/membership) *支持我或者给我买一杯* [*咖啡*](https://ko-fi.com/jamesbrightman) *！非常感谢所有的支持。*

*更多内容请看*[***plain English . io***](http://plainenglish.io/)