# JavaScript 中“Enter”键的键盘事件

> 原文：<https://javascript.plainenglish.io/keyboard-events-in-javascript-for-the-enter-key-7fb454061a98?source=collection_archive---------8----------------------->

![](img/cdb6621b90893bf6cd403ee8f842c5f3.png)

Photo by [Raphael Nogueira](https://unsplash.com/@phaelnogueira?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我正致力于让键盘上的回车键代替按键来显示我正在开发的[天气应用](https://lujianna.github.io/weather-app/)中的今天天气。通常，应该有一个点击键盘上的 Enter/Return 的选项，以给出与按下提交按钮类似的效果。

对于我的项目，我只有几个需求:

*   在应用程序中包含键盘事件
*   能够从输入中获取位置
*   该页面应该显示指定位置的天气

为了做到这一点，我一头扎进了 [**MDN 文档**](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent) 。

通过检查开发人员工具中的键事件，我了解到每个键都有一个键码。通过获取回车键或代码或 keyCode 13，我们能够在按键时提取输入值，并使用它来调用特定的 JSON 值。

***注意:*** 对于大多数按键来说，调度是按如下按键事件顺序进行的:

*   当键被第一次按下时,‘keydown’事件首先被发送，
*   然后发送“按键”事件，
*   然后，当用户释放该键时，发送“keyup”事件。

## [**让我们看看 MDN 示例**](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent)

使用 MDN 文档中的这个例子，在三个事件之间切换，“keydown”、“keypress”和“keyup”。

由于使用键的顺序，我们使用“keyup”事件。

下面的代码是我想出来的:

***注意:*** 这个在移动设备上不行。仅桌面键盘事件。

在这篇文章之后，我将通过一个视频教程来一步一步地展示这一点，以防有些步骤在翻译过程中丢失。

感谢阅读。

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费每周简讯***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。***