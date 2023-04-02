# 以下是我实际想要使用的类型脚本枚举

> 原文：<https://javascript.plainenglish.io/typescript-enums-i-want-to-actually-use-3ec989ea1158?source=collection_archive---------15----------------------->

![](img/37635c6cf1280fc63d393f3b41d6ee39.png)

自从我第一次了解 TypeScript，我就知道有一件事我会一直讨厌:*枚举*。如此不优雅，如此老派，如此为什么你污染我的运行时间。

我错了。我现在用枚举。至少是其中的一部分。

让我展示给你看。

# 什么是 TypeScript 中的枚举？

首先，让我们快速地谈谈什么是枚举器，或简称枚举器。

TypeScript 中的枚举是有限数量的事例的明确集合。也就是说，我们写下所有的可能性，不允许其他的。

枚举的意义在于，在代码中你只需要处理这几种情况，并且你可以确保处理所有的情况。如果您忘记处理一个或多个。

下面是一些常见的枚举示例，可以让您更好地理解:

*   方向:`North`、`South`、`East`、`West`
*   卡位:`Ace`、`King`、`Queen`、`Jack`、`10`、`9`、`8`、`7`、`6`、`5`、`4`、`3`、`2`
*   日期格式:`Unix`、`ISO`、`Email`

在本文中，我将使用我的应用程序支持的国家作为例子。这是在 TypeScript 中编写枚举的方式:

```
enum Country {
  Germany,
  Sweden,
  USA,
}
```

它几乎就像一个简单的物体。注意没有等号，这不是赋值。该定义看起来类似于接口的定义。

枚举有一个有趣的特性:它定义了类型和值。在这里看到一些用途:

```
enum Country {
  Germany,
  Sweden,
  USA,
}const setActiveCountry = (country: Country) => {
  //                               ^^^ this is a type // do something
}setActiveCountry(Country.Sweden)
//               ^^^ this is a value// @ts-expect-error
setActiveCountry('SE')
```

[游乐场链接](https://www.typescriptlang.org/play?#code/KYOwrgtgBAwg9mEAXATgTygbwFBSgcWBQgEMQ0AaXKAZQHdgATUKvAVRoEEqBfavAYLzYAxnBABnJFAnAknEUgCWAN2DxEqDAF4oACjGb0ALlgJk6AJRRtAPizUA9I6Gu37oQD1vUJAAslCShAqBJfNAAHYGonF0Y4GTgIOQCQAHNsPmxZeUVVdXMtPQ0LNAA6eiZQS1iPQW9PXwCgkLCVEgAbMGjsZygAASQJAFpgAA8oxVGUFDgUbLkFZTUSooByGgBRNcsgA)

> 注意*:我在代码示例中用* `*@ts-expect-error*` *来标记下一行有打字错误。这也抑制了错误，所以你不会在操场上看到它。删除该行以查看报告的错误。*

# Enums 怎么了？

对，听起来不错，有什么问题吗？

有三个要点，我从第一天起就反对 Enums。

## 1.枚举引入了(丑陋的)运行时代码

如果您希望有一个可用的值，这意味着该值必须在运行时存在。这意味着枚举是极少数(也可能是唯一经常使用的)类型脚本构造之一，可以在生成的 JavaScript 中生成一些代码。

通常，当目标是当前 ECMAScript 时，所有类型定义和注释都将被删除。这是因为 JavaScript 中的所有其他结构(如对象文字、函数或类)都与 TypeScript 中的相同。

看看上面定义的`Country`枚举是如何结束的:

```
var Country;
(function (Country) {
    Country[Country["Germany"] = 0] = "Germany";
    Country[Country["Sweden"] = 1] = "Sweden";
    Country[Country["USA"] = 2] = "USA";
})(Country || (Country = {}));
```

## 2.默认情况下，枚举是基于数字的

你看到那个代码了吗？你看到那些数字 0，1 和 2 了吗？

这是分配给国家的实际值。所以当你使用好听的名字时，它们会被转换成数字。

生成的代码实际上相当于下面的 dictionary 对象。

```
const Country = {
  Germany: 0,
  Sweden: 1,
  USA: 2,
};
```

所以当你想调试你的代码并记录你的函数接收到的国家时，你会得到一个神秘的数字。然后，您需要去查看 TypeScript 中源代码的相关版本，从顶部开始数那个数字，然后您就有了您最初实际想要的名称。啊，真糟糕。

另一个问题是，你可以在期望`Country`类型的地方传递一个数字。一个令人头疼的维护问题即将自行出现。但是，您实际上可以传递任何数给*，不管它是否在 Enum 中定义。这两个调用[都将通过类型检查](https://www.typescriptlang.org/play?target=99&strict=true#code/KYOwrgtgBAwg9mEAXATgTygbwFBSgcWBQgEMQ0AaXKAZQHdgATUKvAVRoEEqBfbbAMZwQAZyRQRwJJwFIAlgDdg8RKgwBeKAAohq9AC5YCZOgCUUdQD4s1APS2ojOBLgQpACzkgA5tj7ZJaVlFZWM1LQBGUwCpGXklFRM0SIAGFNMgA):*

```
setActiveCountry(1)   // 1 for Sweden
setActiveCountry(100) // 100 for ???
```

当然，枚举应该是唯一的值。开发人员不应该关心运行时值，而应该将枚举视为不透明的。然而，对数字的整体翻译感觉非常老派，提醒人们记忆是昂贵的，数字被用作节省记忆的手段。

我知道有一个字符串枚举的解决方案(我们稍后会谈到)。然而，我不明白为什么这些值不能等同于已经是唯一的标签。或者，当目标是 ES2015+时，值可以是符号，在创建它们的地方使用它们。

## 3.TypeScript 中不需要枚举

在 TypeScript 中必须使用枚举吗？

不，还有其他方法来键入有限数量的案例。

我看到人们用许多方法避免枚举。不管是有意还是出于习惯。当然，你不需要*他们来编写好的代码。*

在我向您展示我现在如何使用 Enums 以便对它们感到舒适之前，让我们探索这些常见的替代方法并讨论它们的优缺点。

# 枚举的替代

## 文字类型的不相交并集

一个相当简单的选择是定义一个由所有允许的实际字符串(或其他值)组成的类型。这被称为不相交或有区别的联合；参见打字稿文档中的[区别工会](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes-func.html#discriminated-unions)。

```
type Country = 'DE' | 'SE' | 'US'const setActiveCountry = (country: Country) => {
  // do something
}setActiveCountry('SE')// @ts-expect-error
setActiveCountry('CZ')
```

[游乐场链接](https://www.typescriptlang.org/play?#code/C4TwDgpgBAwg9gVwHbAE4igXigcgCICiOUAPrgMpGm4Cq5OAUFMy6ywwMZxIDOwUPCMACCHYAEsAbhHjI0GbAAouc9AC5YiFOgCUWAHxQA3kygB6M1AAmcAXAC2QgBbikAcwYBfBg0EixUjJa8oo4lDg6PhZQAALAPAC0EAAekGJJqKhwqL5CohLSstogoTAAWhFAA)

正如您所看到的，这种方法可以正确地键入函数。问题是到处都是“魔法”线。当然，对于我的例子，字符串实际上有点不言自明。但是让我们想象一下，我们将使用[ISO 3166–1 数字](https://en.wikipedia.org/wiki/ISO_3166-1_numeric)国家代码来代替[ISO 3166–1](https://en.wikipedia.org/wiki/ISO_3166-1)两个字母的国家代码:

```
type Country = '276' | '752' | '840'const setActiveCountry = (country: Country) => {
  // do something
}setActiveCountry('752')// @ts-expect-error
setActiveCountry('203')
```

[游乐场链接](https://www.typescriptlang.org/play?#code/C4TwDgpgBAwg9gVwHbAE4igXigcgEwDsAbDlAD64ECsepFOAHACwAMOAUFF9z9+wMZwkAZ2BRhEYAEF+wAJYA3CPGRoM2ABSDV6AFyxEKdAEosAPigBvTlAD0tqABM44uAFtJACzlIA5uwBfdnYJaVlFZUM1DRxqWmNg+ygAAWBhAFoIAA9IWUzUVDhUEMkZeSUVIxAYvBYAZhxjIA)

虽然在技术上与之前的版本相当，但现在完全不可读且容易出错。

## 常数项类型的不相交并集

我们能做些什么来移除那些“魔法”线？让我们将这些值保存为常数:

```
const GERMANY = '276'
const SWEDEN = '752'
const USA = '840'
const CZECHIA = '203'type Country = '276' | '752' | '840'const setActiveCountry = (country: Country) => {
  // do something
}setActiveCountry(SWEDEN)// @ts-expect-error
setActiveCountry(CZECHIA)
```

[操场链接](https://www.typescriptlang.org/play?#code/MYewdgzgLgBA4gUQEoFkCCA5AmjAvDAcgCYB2ANgIChRJYBlAdQQBEEM9CSBWIqm6GAFU6aDgQAcAFgAMfcAIDCALQQKAEgElR+YtIDMVSlACeABwCmMBSACuYKACdjY0hRgAfTjwIfCU2ZQwQcEhwdTysBDmUGjAUACWAG7m1naOzvgAFKBpTgBcVrb2TgCUeAB8MADegTAA9HUwACYgMBAgALbRABbxYADmlAC+lJRRMXFJKUXpmYwsbCWjDTAAAlAQALTmAB4WcdsODiAOY9GxCcmpxcaZyqqaaCVAA)

现在，这肯定更好。常量的名称告诉开发人员他们使用的是什么。

事实上，这是 Redux 社区中流行的一种 Redux 动作方式(或者，我应该说[很流行](https://phryneas.de/redux-typescript-no-discriminating-union)？).

尽管如此，我们还是能发现问题。首先，没有什么强迫你使用这些常数。因此，如果它逃过了通常一丝不苟的审查者的眼睛，您可能会得到一种混合的方法:常数和神奇的字符串。第二，代码不是很优雅，我们要么必须在类型定义中重复值，要么使用看起来很奇怪的`typeof`操作符。无论哪种方式，增加或删除都意味着两个地方的变化。

## 常数字典

嗯，也许有一种方法可以把它们合二为一。当我们查看为 Enum 生成的代码时，我们可能会想:我们可以首先使用那个字典吗？

这个管用。它非常接近 Enum:

```
const Country = {
  Germany: 'DE',
  Sweden: 'SE',
  USA: 'US',
} as consttype Country = typeof Country[keyof typeof Country];const setActiveCountry = (country: Country) => {
  // do something
}setActiveCountry(Country.Sweden)// @ts-expect-error
setActiveCountry('CZ')
```

[游乐场链接](https://www.typescriptlang.org/play?ssl=16&ssc=23&pln=1&pc=1#code/MYewdgzgLgBAwiArmKAnAnjAvDA3gKBhgHEBTVAWwEMx0AuGAcgBEBRRgGkJgGUB3UgBNSYBox7suRAKo8AgmNmd8AXxhUIMUJCj58UdAAdS8JCgzYYB4yABmp5GnQBtANal0dq0dJeEjjABdAG5uInCIonxtaBgIUig5YCgASwA3Un9zTBwAClAA+gdsgEpsAD48bgB6aphBEDiQCgSACxSwAHNVPXjE5PTMsydcrKcAOn4hERK9WpgAASgIAFpSAA9jZLXUVBBUfD6k1IyxjFzGOAAtRhKgA)

Weel，这并不可怕。但是也不是很棒。

让我回顾一下需要记住的几点。

1.  字典必须声明为`[as const](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-4.html#const-assertions)`。这防止了类型引擎将类型推断为通用字典`Record<string, string>`。这是可以的。
2.  `Country`字典是一个值而不是类型。我们需要单独定义类型。这是一个神秘的命令，我总是不得不谷歌一下——不太好。幸运的是，类型可以和字典一样命名，所以从现在开始它就和 Enum 一样了，对吗？嗯，没有。
3.  与前一种情况一样，没有任何东西真正将字典与函数参数联系起来。调用`setActiveCountry('SE')`不会产生错误。最终,`Country`类型只是另一个不相交的 iteral 类型的并集。好处是只在一个地方做改变。这是 Boo(或者至少是 Meh)。

# 枚举正确的方式我的方式

多年来，我一直使用以前的技术来避免枚举。

然后有一天，一位公关人员问:“为什么？”。

我正在回答的时候，我决定核实一些事实，然后……我发现我错了。枚举有两个重要的属性，这使得它们比其他任何东西都优越。即使对于那些担心有一天会回到普通 JavaScript 的人来说。

## 字符串枚举

不用依赖源代码顺序来定义枚举中选项的值，您可以自己定义它。

下面的代码非常接近上面的字典示例，只是更简洁。

```
enum Country {
  Germany = 'DE',
  Sweden = 'SE',
  USA = 'US',
}const setActiveCountry = (country: Country) => {
  // do something
}setActiveCountry(Country.Sweden)// @ts-expect-error
setActiveCountry('CZ')// @ts-expect-error
setActiveCountry('SE')
```

[游乐场链接](https://www.typescriptlang.org/play?ssl=1&ssc=1&pln=18&pc=1#code/KYOwrgtgBAwg9mEAXATgTygbwFBSgcWBQgEMQMBeKAcgBEBRagGlygGUB3YAE1CiuptGLPAFU2AQX41xzbAF9WeZSrzYAxnBABnJFG3AkE9UgCWAN2DxEqSlAAUmm+gBcsBMnQBKfgD4srAD0gVDccPpwEIYAFqYgAOYK2NgGRiYWVh629taeaAB0nDygXsnBUAACSNoAtMAAHgAOwCZ1KChwKCmGxmaWudnUMABa1KXY5VW1Dc2tRB1dqb0ZA+j2goylQA)

同样，让我们讨论一些或多或少显而易见的观察结果:

1.  它使用相等的符号，而不是冒号。不要问我为什么。尽管如此，它非常接近于对象字面量。
2.  这些值必须都是字符串。不支持其他值。(技术上可以用数字，但是没有带来优势。坚持弦乐。)
3.  你必须在任何需要枚举值的地方使用枚举值(例如`Country.Sweden`)。传递同一个字符串是不行的(比如`'SE'`)。这使得重构成为一个轻松的过程。并且您的代码库保持一致。
4.  不过，也不全是独角兽和彩虹。生成的代码 a)仍然存在，b)仍然(有点)难看。

“你到底想怎么改进，罗宾，”你可能会问

你会享受到一顿美餐。

## 常量，字符串枚举

第二个帮助我跨越枚举卢比孔河的改进(“类型是强制转换的！”，不好意思，不好意思，我只好)是 constant Enum 或者简称 [const Enum](https://www.typescriptlang.org/docs/handbook/enums.html#const-enums) 。

它看起来怎么样？

```
const enum Country {
  Germany = 'DE',
  Sweden = 'SE',
  USA = 'US',
}const setActiveCountry = (country: Country) => {
  // do something
}setActiveCountry(Country.Sweden)// @ts-expect-error
setActiveCountry('CZ')// @ts-expect-error
setActiveCountry('SE')
```

[游乐场链接](https://www.typescriptlang.org/play?#code/MYewdgzgLgBApmArgWxgYRIsUBOBPGAbwCgYYBxOHZAQzAIF4YByAEQFFmAaUmAZQDucACYIYTZn048yAVT4BBcS3ndiAX15ltOssVCRYEOFAXAoASwBucDFlyMYAClD38ALnSZs+AJTiAPiJeAHoQmGEQGAgQZBMACwswAHMNYmJjU3NrW28HJzsfPAA6QREEX3SwmAABKAgAWjgADwAHOHMmnBwQHAyTM0sbQvzmNAAtZkriarrGlvbOqh6+zMGckfwnSU5fIA)

等等，等等，我没有骗你。

除了在`enum`前面增加了`const`之外，它是前面代码的完全复制。

功能也完全相同。看上面的列表项:1。是一样的，2。是一样的，3。是一样的，4。就是……不一样！

没有为 const 枚举生成代码。这是前面代码的输出:

```
const setActiveCountry = (country) => {
    // do something
}setActiveCountry('SE' /* Sweden */)
```

是的，现在所有的值都在使用的地方内联了。没有线索表明曾经有过枚举。也许除了有用的评论。

最后，结果与我们讨论的第一种选择相同:文字类型的分离联合。然而，它更容易使用，在各方面都更安全。

总而言之，使用常量字符串枚举，您可以获得字符串枚举的所有好处(类型检查、可调试、不可由字符串替换)以及直接编写它的好处(无需额外的代码)。

## 不断枚举是一条单行道

在我们继续之前，我需要提醒你注意常量。他们不是每次都是顺带替换的。

有什么问题？没有办法获得一个值的标签。你看，没有字典，根本没有生成代码。因此，如果您有值，比如说`'SE'`，并且您想要它的标签用于日志记录，在本例中是`Sweden`，您将不能。

这是一个小小的不便，你应该记住。

此外，如果您需要访问日志以外的标签，这可能意味着 Enum 不适合您。枚举标签应该只对开发人员有意义。

## 常量枚举可能很大

我发现常量枚举的一个很好的用例是，你不关心一个枚举中的项数。可能有一个世界上所有国家的 const string 枚举，如果你只在那里使用，那么只有这三个会进入生产代码。其余的就会消失。代码自动完成仍然没有问题。

在我们的服务代码中，我们现在有一个包含所有现有 HTTP 响应代码的共享常量字符串枚举(摘录):

```
export const enum Success {
  OK = '200',
  Created = '201',
  // …
}export const enum ClientError {
  BadRequest = '400',
  Unauthorized = '401',
  PaymentRequired = '402',
  Forbidden = '403',
  NotFound = '404',
  // …
}// …export type HttpStatusCode =
  | InformationalResponse
  | Success
  | Redirection
  | ClientError
  | ServerError
```

# 什么是伟大的枚举？

常量字符串枚举。

就是这样。

这就是我现在到处使用的东西。

在提交之前，我确保每个枚举满足以下两个条件:

1.  所有枚举选项都有一个定义的自定义字符串值。
2.  枚举被声明为`const`。

我认为这结合了 TypeScript 的好处和纯 JavaScript 的雄辩。对结果几乎没有影响的卓越开发人员体验。

## 结论

感谢您的阅读。我希望你已经发现这是有用的。你在代码中使用枚举吗？你会避免 ECMAScript 没有考虑的语言特性吗？请务必在评论中让我们知道。

*更多内容尽在*[***plain English . io***](https://plainenglish.io/)