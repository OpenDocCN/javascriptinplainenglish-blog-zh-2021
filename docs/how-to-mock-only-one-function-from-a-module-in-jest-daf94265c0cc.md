# 如何在 Jest 中只模仿模块中的一个函数

> 原文：<https://javascript.plainenglish.io/how-to-mock-only-one-function-from-a-module-in-jest-daf94265c0cc?source=collection_archive---------22----------------------->

![](img/22ac58a3e9cf36219a41b6c93e574d9b.png)

Photo by [Oskar Yildiz](https://unsplash.com/@oskaryil?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

模拟代码的依赖性是软件测试的基本方面之一，它允许开发人员获得对数据流和代码行为的控制。

作为一个 JavaScript 测试框架，Jest 有一个广泛的 API 集合，这将使我们的生活更容易，并有助于模仿依赖。然而，有时选项太多，很难知道所有选项，更不用说确定最佳选项。

我有一个类似的案例，我从一个模块`@module/api`导入了几个不同的导出，并在我的代码中使用它。然而，在我的测试中，我想模拟一个特定的导入函数`functionToMock`,并让所有其他的导入保持不变。

这个特定的函数在后台执行一些在测试环境中无法模拟的逻辑，并且对我的测试的完整性没有意义。所以，我想嘲笑它，但重要的是，所有其他的进口仍然会像最终用户将如何体验它。

在做了一些研究并尝试了不同的方法之后，我对不同的可用模仿方法、它们之间的差异有了更多的了解，并且总体上对 Jest 中的模仿依赖有了更好的理解。在这篇文章中，我将分享我在 Jest 中如何模拟一个导入模块的特定函数的经验。

# 人工模拟

在整个过程之后，我发现的主要问题是，试图模仿一个导入模块中的某个特定函数与模仿任何其他模块中的任何函数在本质上是一样的。因此，从最基本的方法开始是有意义的，即手动模拟函数。

```
import * as moduleApi from '@module/api';// Somewhere in your test case or test suite
moduleApi.functionToMock = jest.fn().mockReturnValue({ someObjectProperty: 42 });
```

我们在这里所做的是首先从`@module/api`导入所有的导入，将其捆绑成一个对象，并存储到名为`moduleApi`的变量中。然后，我们用一个 Jest 模仿函数覆盖了我们想要模仿的函数`functionToMock`。这意味着在我们的测试环境中，从我们的代码对`functionToMock`的任何调用都不会触发实际的函数，而是这个 jest mock 函数。

在这之后，我们可以使用 Jest 实用函数来根据测试或测试套件的需求改变这个函数的行为。在上面的例子中，我们使用了`mockReturnValue`让 mock 函数总是返回某个值，在本例中，这个值是一个具有某个键和值的对象。

这是最低级的方法，应该适用于大多数用例。其他方法基本上使用 Jest 实用函数，这些函数基本上是这种基本方法的某种形式的抽象。然而，手动模拟相当乏味，在处理更复杂的情况时，需要手动记账。因此，在尝试了 Jest 的内置实用函数后，这种方法可能是最好的退路。

在某些情况下，这种方法也不起作用。尝试这种方法时，我遇到最多的错误是`TypeError: Cannot set property functionToMock of #<Object> which has only a getter`。在这种情况下，您可以尝试本文中的其他方法之一。

# 使用`jest.spyOn`刺探功能

从导入的模块中模拟特定函数的另一种方法是使用`jest.spyOn`函数。这个函数的 API 似乎正是我们的用例所需要的，因为它接受一个完整的模块和应该被监视的特定输出。

```
import * as moduleApi from '@module/api';// Somewhere in your test case or test suite
jest.spyOn(moduleApi, 'functionToMock').mockReturnValue({ someObjectProperty: 42 });
```

就用法而言，这基本上与上一节所述的手动模拟相同。但是这是稍微干净的语法，允许更容易地清理模拟，并且使得对函数执行断言更容易，因为`jest.spyOn`将返回模拟的函数。但是就功能而言，在这个用例中，使用这段代码监视函数和手动嘲笑它没有区别。

然而，从技术角度来看，这有很大的不同，因为`jest.spyOn(moduleApi, 'functionToMock')`仍然会自己运行实际的`functionToMock`代码，而不是嘲笑它。从模块中窥探一个函数只会跟踪它的调用。如果你还想模拟底层代码，你必须用普通的模拟实用函数如`mockReturnValue`或`mockImplementation`来链接它。

使用这种方法，您有可能会遇到`TypeError: Cannot redefine property: functionToMock at Function.defineProperty (<anonymous>)`。这类似于我们尝试手动模拟时遇到的错误。尽管如此，我还是建议您首先尝试进行手动模拟来解决这个问题，如果您还没有这样做的话，因为开销没有那么大。但是，如果手动嘲笑和监视功能都不起作用，你可以参考下一个也是最后一个方法。

# 使用`jest.requireActual`模拟整个模块并恢复不必要的模拟

在大多数情况下，其他方法之一应该可以满足您的用例。但是在极少数情况下，您会遇到错误，无法重新定义单个导出的函数。这正是我所面临的，我使用的解决方案如下。

```
import { functionToMock } from "@module/api"; // Step 3.// Step 1.
jest.mock("@module/api", () => {
    const original = jest.requireActual("@module/api"); // Step 2.
    return {
        ...original,
        functionToMock: jest.fn()
    };
});// Step 4\. Inside of your test suite:
functionToMock.mockImplementation(() => ({ mockedValue: 2 }));
```

这里发生了很多事情，让我们来分析一下。

在步骤 1 中，我们使用`jest.mock("@module/api", ...)`来模拟整个模块。这意味着*模块的每个*导入在测试环境中都将是一个模拟函数。这显然不是我们想要的，因为我们只想模拟`functionToMock`导出。我们可以在`jest.mock`调用的第二个参数中解决这个问题，它接受一个应该返回一个对象的回调。当模块在我们的测试环境中以任何方式导入时，这个对象被返回，而不是实际的模块。

然后在步骤 2 中，在第二个参数回调中，我们使用`jest.requireActual("@module/api")`来捕获原始代码并从模块中导入，并将它存储在一个变量中。然后，我们通过做两件事来创建应该替换模块导入的对象:将所有原始导入放入其中，并用 jest 模仿函数覆盖我们想要模仿的`functionToMock`。

然后，要使用模拟函数，我们必须从模块导入函数，步骤 3。最后，在测试套件中的某个地方，步骤 4，您可以使用该导入来做各种事情，比如定制模拟实现，如上面的示例代码所示，或者对其执行断言。

我们所做的基本上是模拟整个模块，创建模块实际导入的快照，使用该快照作为模拟版本，然后通过在模拟模块中覆盖它来调整我们测试环境中喜欢的任何导入。在这种情况下，我们只想模仿`functionToMock`函数，所以我们只需用 jest 模仿函数覆盖它。

由于这种方法“抛弃一切，从头开始”的性质，当试图模仿 Jest 模块中的某个特定函数时，这是最好的解决方案。

虽然这种方法在所有情况下都适用，但对于我们试图实现的目标来说，这是一种矫枉过正的解决方案，可能会给其他开发人员带来一些困惑。如果可能，尝试使用更复杂的方法来监视出口，甚至手动模仿出口。但是如果其他方法都失败了，或者其他两种方法都行不通，这个方法可以解决你的问题。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)