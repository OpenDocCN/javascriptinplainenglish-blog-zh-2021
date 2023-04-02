# Jest:轻松清除模块模仿

> 原文：<https://javascript.plainenglish.io/jest-clearing-module-mocks-effortlessly-6656d104cab?source=collection_archive---------3----------------------->

![](img/7e98635eec232b735788c9c9b68a3f70.png)

Photo by [Oskar Yildiz](https://unsplash.com/@oskaryil?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我有一个在整个应用程序中使用的查询模块。因此，这个模块在我的测试中经常被嘲笑。为了节省时间，我通过每次 Jest 运行时加载的设置文件对它进行了全局模拟。它的工作几乎完美无缺，我的规格更清晰，我可以准确地测试我想要的。

然而，我意识到不管我对模块做了什么，查询模块的测试都通过了。我无意中通过全局嘲笑破坏了模块的测试。

我尝试以各种形式和组合使用:`jest.restoreAllMocks`、`jest.clearAllMocks`和`jest.resetAllMocks`来移除模拟，但没有任何效果。然后我发现了`jest.unmock`。这个函数让你传递模块名或路径，它将确保模块永远不会被模仿。这很简单，它可以让你在其他测试套件中模拟这个文件。太完美了。这是你如何使用它。

# 嘲笑

这里我使用`jest.mock`模拟查询模块，特别是`active_bank_request`对象。模拟监听`active_bank_request`上的`query`方法，并返回模拟响应。

```
jest.mock('@/queries/accounts_query', () => { return { active_bank_request: { query: () => new Promise(resolve => resolve(mock_accounts)) } }})
```

注意我在`jest.mock`调用中使用的模块的路径。这需要与您传递给`jest.unmock`的路径相同。

`@`是`src`文件夹的快捷方式，所以我不必为每个路径都写`../../`。

# 清除模拟

在`accounts_query`的规范中，我卸载了调用`jest.unmock`的模块，并将路径传递给它。

```
describe('Accounts Query', () => { beforeAll(() => { jest.unmock('@/queries/accounts_query') }) describe('Active Accounts', () => { // tests })})
```

就是这样，测试愉快！

# 来源

[](https://jestjs.io/docs/jest-object#jestunmockmodulename) [## 笑话对象笑话

### jest 对象自动在每个测试文件的范围内。jest 对象中的方法有助于创建模拟和…

jet js . io](https://jestjs.io/docs/jest-object#jestunmockmodulename) [](https://jestjs.io/docs/jest-object#jestmockmodulename-factory-options) [## 笑话对象笑话

### jest 对象自动在每个测试文件的范围内。jest 对象中的方法有助于创建模拟和…

jet js . io](https://jestjs.io/docs/jest-object#jestmockmodulename-factory-options) 

[*更多内容尽在 plainenglish.io*](http://plainenglish.io/)