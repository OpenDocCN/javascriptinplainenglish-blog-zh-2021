# 比较 Vue.js 和 Vanilla JavaScript 中的自定义日期组件

> 原文：<https://javascript.plainenglish.io/comparing-a-custom-date-component-in-vuejs-and-vanilla-javascript-95d984485989?source=collection_archive---------19----------------------->

## 探索 Vue.js 和 Vanilla JavaScript 中自定义日期组件的差异。

最近，我们有理由返工我们如何收集生日(和其他日期在塞拉芬)。虽然默认的浏览器实现在开始时可以做到这一点，但我们面临着几个问题:

1.  并非所有浏览器的实现都是一致的。
2.  大多数浏览器打开的日历输入都聚焦于今天的日期，这让我们的用户很难输入他们的生日。

我们决定创建日期输入组件来解决这个问题(使用 Vuejs)。

虽然结果非常好，但它确实让我问自己，如果我们用普通的 Javascript 编写相同的行为，会有什么不同。

因此，这是本系列的第三篇比较 Vue.js 和普通 JavaScript 日期组件的文章。

在[第一部分](https://pablo-curell-mompo.medium.com/building-a-custom-date-input-component-in-vue-js-b5641b7b7c2b)中，我们探索了如何在 Vue.js 中构建自定义日期输入。

在[第二部分](https://pablo-curell-mompo.medium.com/bulding-a-custom-date-component-using-vanilla-javascript-4cb6e8f547a)中，我们探索了如何使用普通 JavaScript 构建自定义日期输入。

# 规格

我们的 DateInput 组件的规范表现为浏览器上的本地日期输入减去日历选择，即:

*   我们只能输入两位数来表示日和月。
*   我们只能输入四位数的年份。
*   这一天应该在 1 到 31 之间
*   月份应该在 1 到 12 之间
*   年份应该在 1900 年到 2100 年之间(这个是我们的，不是浏览器的)
*   我们需要通过直接输入数字或用箭头键上下移动来输入日期。
*   如果我们用箭头键输入日期，并达到上限或下限，显示的数字应该循环。
*   如果我们通过输入数字来输入日期，输入应该是有边界的(max(输入，高边界)或 min(输入，低边界)
*   我们应该以直观的方式让用户进入下一个领域。
*   我们应该证实日期是正确的。

![](img/98b80269b7fb04755756a70603004d95.png)

Photo by [Santiago Lacarta](https://unsplash.com/@lacarta?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/confrontation?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

# 先入为主的观念(假设)

在开始这个项目之前，我认为创建普通的 JavaScript 组件会有更多的麻烦和更糟糕的“开发者体验”。

我还认为页面的“反应性”在 Vue 上比在普通 JavaScript 上要好。

另一方面，我预计页面的总权重在 Vue 上更高(因此在较慢的连接或较差的手机上的性能也更高)。

# 调查的结果

## JavaScript 和 Vue.js 有类似的开发者体验

我没有努力用普通的 JavaScript 来工作，甚至可以更简洁地表达我想要的东西(尽管没有完全重构)。

以上也可能是因为我已经弄清楚了在做 Vue.js 组件时不同元素如何交互背后的逻辑。

两者都相对容易实现，尽管如果您喜欢默认的浏览器日期输入，它们可能会有点复杂。

## 反应性

我认为普通的 JavaScript 和 Vue.js 在满足用户需求方面非常被动。我能够相对容易地向两者添加错误类，并且当用户使用它时两者都流动。

## 重量/性能

就权重而言，Vue.js 组件的权重更大，但是它的执行速度更快。

对于我们的 Vue.js 组件，最高的成本来自于 2.54 MB 的 *chunk-vendors.js* ，总成本约为 2.66MB。

我们的普通 JavaScript 组件没有网络需求，一切都在 750 毫秒内执行(所有 DOM 事件都已运行完毕)。文件本身重 4.7 KB。

正如我们所看到的，这里的结论是 Vue.js 很好地优化了代码的执行(至少在这个规模上),但是在较差的连接或较差的机器上，性能可能会受到更大的影响。

## 其他备注

另一件值得指出的事情是，我的 Vue.js 组件比普通的 JavaScript 组件更容易理解。我相信这是因为 Vue.js 组件固有的组织方式。

这种固有的组织结构使它们比普通的 JavaScript 更容易导航(一旦你知道你在找什么)，但是我可能会做更多的努力来确保我的 Javascript 文件更易读。

最终，如果你有好的约定，JavaScript 可以像 Vue.js 一样简单，但是它需要开发者更多的训练。

最后，记住我是用 Vue 2 而不是 Vue 3 编码的。如果在更大的项目中使用复合 API，Vue 3 中的相同示例可能会有所不同。

# 结论

总之，我想你会问自己是应该使用 Vue.js 还是普通的 JavaScript。

我相信这主要是你的选择，以及你更喜欢使用的东西。如果你使用普通的 JavaScript，你对网络的需求可能会更少，但是 Vue.js 已经被很好的优化了。如果你对它更适应，你将拥有的生产力可能会打乱使用它的潜在成本。

我不是性能专家，无法准确地对此进行基准测试。正如你在这里看到的，在大多数情况下，一个框架永远不会像普通的 JavaScript 那样高性能，因为框架在 JavaScript 之上增加了层，从而让你一直加载更多的代码。

同样重要的是要注意，你可以通过更多的参与来提高臃肿的 Vue.js 应用的性能。