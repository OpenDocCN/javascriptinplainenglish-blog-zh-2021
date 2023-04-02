# 测试 JavaScript 用户界面的 5 个基本技巧

> 原文：<https://javascript.plainenglish.io/5-essential-tips-for-testing-javascript-uis-3cbf57d507e0?source=collection_archive---------7----------------------->

说到为(JavaScript)ui 编写测试，你要么喜欢，要么不喜欢。但是，如果你在一个要求一定测试覆盖阈值的公司里，或者你想要覆盖逻辑，你最终将不得不这样做。不管你的情况如何，我相信下面的五个建议会帮助你写出更好的测试。

![](img/d89e1301ea32fffb4cff50b2a29502f0.png)

Photo by [Annie Spratt](https://unsplash.com/@anniespratt?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

开始的时候，我在编写测试方面做了很多努力。这个概念非常简单——您编写代码来验证您编写的其他代码。但是，当时有些不对劲，起初我并不太喜欢它。一晃几年过去了，我现在对写作测试还算满意。我已经想好了。这些是我发现在日常编写 UI 测试中最有用的技巧。

# **1。测试行为，而不是实现**

对于一些人来说，遵循测试 UI 行为而不是实现的原则可能是很自然的。但是请相信我，有时候，在测试代码的深处，您可能会失去这个想法，并试图通过破解来摆脱测试。

如果你熟悉测试驱动开发( [**TDD**](https://en.wikipedia.org/wiki/Test-driven_development) )，还有行为驱动开发( [**BDD**](https://en.wikipedia.org/wiki/Behavior-driven_development) )。这个想法是使用 DSL(领域特定语言)创建一个几乎项目中每个人都能理解的脚本。很长一段时间，制作它的主要工具是黄瓜(图书馆，而不是蔬菜)。它将允许您像这样形成一个测试脚本:

```
Feature: Put items in the cart Scenario: Breaker joins a game
    Given the user has visited the awesome shopping page
    When the user adds an item to the cart
    Then the user should see the item in the cart
```

这个想法很简单，实现使用带有“给定”、“当”和“然后”格式的 Gherkin 语法。像这样的脚本是为了让涉众阅读它们并理解特性和场景，但是我很少看到他们在实践中阅读它们。

无论如何，如果你不是这类工具的粉丝，你可以跳过使用它(咄)，但是记住你应该测试行为。

# 2.一次测试一件事

几年前我给自己的一个很好的建议是在一次测试中专注于测试一件事情。我过去常常在一次测试中测试许多不同的东西。Cypress framework 做的一件好事是，他们建议只测试登录功能**一次**，并在所有其他测试中以编程方式登录。

假设您正在测试向购物车添加商品。理想情况下，如果您在测试中关注 UI 功能，那将是最好的。所有其他的事情，比如:

*   登录中，
*   播种要添加到卡中的项目，
*   发布用户将购买商品的商店

都应该是计划的一部分。您不应该在测试中直接做所有这些事情，相反，只需要关注用户向购物车中添加商品所采取的操作。

# 3.适当地构造测试

另一件让你在测试中成功的事情是遵循 AAA 模式。AAA 代表以下内容:

*   第一个 A — **安排**:为即将被测试的功能设置测试所需的一切。播种数据、登录用户、存根调用等。
*   第二个 A — **动作**:执行向购物车中添加商品这样的动作。
*   第三个 A — **断言**:确保收到的值满足期望值。确保测试验证了预期的行为。

继续，并在您的下一次测试中尝试它。

# 4.使用助手来生成测试数据

通常，您会面临同样的问题——在测试中创建特定的数据对象。无论是产品、用户还是随机物品，您都必须在测试设置中以某种方式创建对象。这里有一个软件设计模式可以帮助你，那就是工厂模式。

一个可以帮助我们生成对象的库是[渔业](https://github.com/thoughtbot/fishery)库。如果你用的是 TypeScript，这两个可以完美契合。假设我们想在测试中生成一个用户。一种方法是这样的:

```
// factories/user.ts
import { Factory } from 'fishery';
import { User } from '../my-types';
import postFactory from './post';export default Factory.define<User>(({ sequence }) => ({
  id: sequence,
  name: 'Rosa',
  address: { city: 'Austin', state: 'TX', country: 'USA' },
  posts: postFactory.buildList(2),
}));
```

然后，我们可以轻松地创建用户，如下所示:

```
const user = userFactory.build({ name: 'Sandra' });
```

您现在应该有更精确的测试，因为您可以在不指定所有属性的情况下生成对象，只指定那些与您正在编写的当前测试相关的属性。此外，用户工厂定义在一个地方，您可以很容易地从那里编辑它，当一些属性改变时，不需要进行所有的测试。

# 5.避免睡觉(在考试中)

我们都遇到过这种情况，设置一些超时来处理一个异步测试用例或强制下一个节拍。有了新工具，你就不必这么做了。如果您正在测试一些异步代码，您可以使用 Jest 来测试它:

```
test('the data is peanut butter', async () => {
 const data = await fetchData();
 expect(data).toBe('peanut butter');
});
```

有了简单的 *async / await* 语法，就不再需要 *setTimeout* 了。或者，更好的是，如果您使用的是 [Cypress](https://www.cypress.io/) ，它们有一个集成的等待机制，可以为每个命令的执行提供一定的时间。同样，在*测试库*中，你可以像 [its 文档](https://testing-library.com/docs/dom-testing-library/api-async/#waitfor)中描述的那样*等待*。

无论如何，无论你做什么，在你调用 setTimeout 或任何其他与时间相关的方法之前要三思，因为这将使你的测试可读性更差，并且可能不可靠。

# 总结

感谢你阅读这五条建议。我希望你在他们之后获得了一些洞察力。另外，我希望这些能帮助你为你的 JavaScript 应用程序编写更好的 UI 测试。

如果你对更多类似的博客文章感兴趣，可以考虑订阅[时事通讯](https://pragmaticpineapple.com/newsletter)。此外，如果你觉得这篇博文有用，你可以在下面的 Twitter 上与你的朋友和同事分享:

下次再见，干杯。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)