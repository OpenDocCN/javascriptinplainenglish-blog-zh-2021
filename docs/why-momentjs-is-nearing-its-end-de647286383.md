# 停止使用 MomentJS。下面是您应该使用的方法

> 原文：<https://javascript.plainenglish.io/why-momentjs-is-nearing-its-end-de647286383?source=collection_archive---------2----------------------->

## *时刻接近尾声*

![](img/fe1a36e480d93efea80aaa73ecd91dfb.png)

Photo by [Ocean Ng](https://unsplash.com/@oceanng?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/clock?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

# 介绍

[MomentJS](https://momentjs.com/) 是一个广泛使用的时间和日期格式化和计算库。但它在成为长期最佳后，正慢慢接近它的终点。例如，如果没有 MomentJS 之类的库，我甚至无法格式化和使用所有的日期格式。

所以我在网上搜索了一下，在 MomentJS 网站上我看到了一些有趣的东西。

![](img/64b805c0bce4575f09c25d36d05235a5.png)

From the official MomentJS site

如果你在他们的网站上进一步搜索，你实际上可以看到一些替代方案，以及为什么这些方案会更好。

JavaScript 后来添加了`Intl`对象。而 MomentJS 用的是`Date`。对于一些项目来说，这根本不是问题，直到 MomentJS 消失还需要一段时间，但尽快检查替代方案是个好主意。

使用新的`Intl`物体的替代物之一是 [Luxon](https://moment.github.io/luxon/) 。这似乎是开始使用新 Javascript 函数的好地方。

# Luxon vs MomentJS

Luxon 与 Moment 有一些不同之处，值得注意。首先，Luxon 对象不像 Moment 对象那样是可变的。

```
let m1 = moment(); 
let m2 = m1.add(3, 'minutes'); 
m1.valueOf() === m2.valueOf(); // -> true
```

如果使用`.add()`更新日期或时间，对象本身将立即改变。这就是为什么`m1`和`m2`在使用力矩的情况下是相同的。

```
let l1 = DateTime.local(); 
let l2 = l1.plus({ minutes: 3}); 
l1.valueOf() === l2.valueOf(); // -> false
```

但是在卢克逊，这些物品将会不同。`l1`此处增加 3 分钟后不变。也不是语法上的区别。

此外，语法上也有一些小的变化，比如用函数代替变量来获取数据。`time.year()`而不是`time.year`。

# 使用 Luxon

Luxon 可以在各种项目中以各种方式使用。最简单的方法是用`npm`或`yarn`安装。为了浏览器兼容性，你可能需要 polyfills，但是对 MS Edge 等新的浏览器的[支持相当不错。](https://moment.github.io/luxon/docs/manual/matrix.html)

正如你所料，创建一个新的 Luxon 对象很容易。`DateTime.local()`。

将字符串解析成 Luxon 比在 Moment 中要难一些，我们必须使用函数名来指定格式。

例如使用`DateTime.fromISO(String)`或`DateTime.fromRFC2822(String)`。但是也有使用你自己的格式的`.fromFormat(str, str)`。

您可以使用`.isValid`检查日期是否正确，这不是 Moment 中的功能。以及使用`.year`或`.second`获得特定的日期值。

## 转变

改变日期对象，比如添加几天，可以使用`.plus()`、`.minus()`等等来实现。与 Moment 不同，这些函数需要对象，而不是字符串和数字的混合。

```
dateObj.plus({ months: 3, days: 2 })
```

使用`toLocal()`将 date 对象设置为当前本地时间，我可以想象如果您的应用程序需要支持多个时区，这将非常有用。

## 询问

就像在 Moment 中一样，您可以查询当前日期是否早于、晚于您在参数中给出的日期。

以`dateObj.isBefore(dateObj2)`、`dateObj.isBetween(d1, d2)`为例。这对于日历等应用程序非常有用。

## 输出

将您到目前为止制作的数据输出到任何其他可用的格式是非常重要的。您的数据库可能支持另一种格式，而不是您想要使用的格式，或者您可能需要为人类格式化它。

`.toString()`是最简单的，这个格式在 ISO 8601。但是您可以指定格式，如`.toISO()`、`.toFormat(str)`、`.toJSDate()`等等。

但是你可能想显示一个倒计时。谢天谢地，Luxon 也给出了一个简单的方法来做到这一点。瞬间的`fromNow`是卢克森的`toRelative()`。`toNow`从瞬间起就是`DateTime.local().toRelative({ base: this })`在鲁迅。这不是最短的语法，但是它很有效，而且非常有意义。

虽然 Luxon 仍在开发中，但我们可以说它会一直存在下去。至少暂时如此。由于有更多的选项使用新的 Javascript 函数，我认为 Luxon 更胜一筹，因为它已经开发了很长时间。

# 结论

时刻还没有完全过去。但在他们的网站上，他们建议你不要只看瞬间，除非你陷入了特定的用例。

就目前而言，Luxon 似乎是未来时刻的最大替代品。技术发展得非常快，所以谁知道一两年后会用上什么。

我希望这篇文章对一些人有用。非常感谢你的阅读，祝你有美好的一天。