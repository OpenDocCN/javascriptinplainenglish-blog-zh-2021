# 如何用 JavaScript 计算感知温度(风冷)

> 原文：<https://javascript.plainenglish.io/how-to-calculate-the-perceived-temperature-windchill-with-javascript-5f52ec82f0ae?source=collection_archive---------17----------------------->

## 使用 JavaScript 计算感知温度指南。

![](img/ff79eb9fa304585423476cec317235ff.png)

Photo by [Denny Müller](https://unsplash.com/@redaquamedia?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

圣诞节快到了，圣诞老人正在做准备。最棘手的问题之一是设备。雪橇承受着巨大的压力，连驯鹿都要全力以赴。一夜之间，它们穿越了所有的气候。为了保护他们，圣诞老人会计算每个地方的温度。温度计测得的温度是不够的:他用的是感知的温度。

# 谜题:宝贝，❄️外面很冷

![](img/1a0bf082614b19d3d7cfcae41c85599e.png)

[开发降临节日历问题 18🎅](https://github.com/devadvent/puzzle-18)相当简单。我必须在知道风速和室外温度的情况下计算感知温度。结果可以是摄氏度或华氏度。

最难的是找到正确的公式。或者说，是最常见的公式。在网上搜索时，我发现了这篇文章:

[](https://sciencing.com/calculate-wind-chill-factor-5981683.html) [## 如何计算风寒因子

### 风寒因子是为有限的目的而设计的。它测量人体暴露区域的热量损失，如…

sciencing.com](https://sciencing.com/calculate-wind-chill-factor-5981683.html) 

我省略了所有的计算，只报告公式:

> 感知温度= 13.12+0.6215t—11.37(v⁰-⁶)+0.3965t(v⁰-⁶)

使用:

*   **T** :摄氏温度
*   **V** :风速，单位为千米每小时

我可以转换成 JavaScript 来得到这个函数:

使用英里和华氏温度:

> 感知温度= 35.75+0.6215t—35.75(v⁰-⁶)+0.4275t(v⁰-⁶)

使用:

*   **T** :华氏温度
*   V :风速，单位为英里/小时

在 JavaScript 中:

结合这两段代码，我得到了:

# 将数字从一种系统转换到另一种系统

这个问题很简单，但是从一种测量系统转换到另一种测量系统时会出现一些复杂情况。

我不打算写一篇完整的讨论。我将只报告一些转换函数

**转换公里和英里:**

**转换摄氏度和华氏度:**

今天到此为止。

感谢阅读！敬请关注更多内容。

***不要错过我的下一篇文章—报名参加我的*** [***中邮箱列表***](https://medium.com/subscribe/@el3um4s)

[](https://el3um4s.medium.com/membership) [## 通过我的推荐链接加入 Medium—Samuele

### 阅读萨缪尔的每一个故事(以及媒体上成千上万的其他作家)。不是中等会员？在这里加入一块…

el3um4s.medium.com](https://el3um4s.medium.com/membership) 

*原载于 2021 年 12 月 21 日 https://blog.stranianelli.com*[](https://blog.stranianelli.com/how-to-calculate-the-perceived-temperature-windchill/)**。**

**更多内容看* [*说白了. io*](http://plainenglish.io/) *。在这里注册我们的* [*免费周报*](http://newsletter.plainenglish.io/) *。**