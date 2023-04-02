# 模块化 JavaScript 模式的单元测试挑战

> 原文：<https://javascript.plainenglish.io/unit-testing-challenges-with-modular-javascript-patterns-22cc22397362?source=collection_archive---------5----------------------->

![](img/8892e69744dd38fcf6d95a307194385d.png)

A modular synthesizer Photo by [Steve Harvey](https://unsplash.com/@trommelkopf?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/modular?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

模块化 JavaScript 正处于 CommonJS 和 ES 模块之间一个有趣的十字路口。虽然 ES 模块语法很常见，但它通常符合 [CommonJS](https://en.wikipedia.org/wiki/CommonJS) ，这可能会给单元测试带来一些挑战。此外，当使用[本地的 ES 模块](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules)时，我们在编写测试时需要注意一些特性。本文探讨了这两种模式中存根和间谍的具体问题，并提供了一系列解决方案。

第一个问题是，使用 ES6 的 *export* 语法来共享单个函数，但是编译到 CommonJS 时，不可能对同一*模块中另一个调用的函数进行存根或监视。第二个是，当使用本机 ES 模块时，您不能从任何*模块中截取或监视命名导入。**

# *对同一模块出口进行窃听或监视*

*请考虑以下代码:*

```
*export function bar(str) {
  return str;
}

export function foo() {
  bar('test');
}*
```

*当我的应用程序运行时，一切似乎都很好。但是，当我对 *foo* 进行测试并为*条*创建间谍时，它没有为*条*记录任何数据:*

```
*expected spy to have been called at least once, but it was never called*
```

*在探索这个问题的解决方案时，我遇到了很多令人困惑的信息，所以让我先澄清一些事情。*

## *这个问题适用于任何 JavaScript 嘲笑框架，而不仅仅是 Jest 或 Sinon*

*让我们从消除最大的误区开始:测试框架不应该受到任何指责。测试框架根本无法读取正确的对象。*

## *这不是巴别塔的问题*

*我也看到有人认为这个问题是由于[巴别塔](https://babeljs.io/)如何编译 JavaScript 造成的。默认情况下，它会将您导出的函数分配给*导出的*对象。下一节将解释为什么这会影响相同的模块存根和间谍。*

*值得注意的是，巴贝尔确实支持 es 模块，您可以在您的目标[中指定，如本文](https://babeljs.io/docs/en/babel-preset-env#targetsesmodules)所述。如果这样做，您将需要确保您的所有目标环境都支持 es 模块，并克服我在下面“使用 ES 模块的存根和间谍”一节中解释的问题。*

## *当以一种模式书写，然后转换成另一种模式时，这是一个问题*

*当通过 [Jest](https://jestjs.io/) 或 [Mocha](https://mochajs.org/) 运行你的单元测试套件时，他们将使用[节点](https://nodejs.org/en/)环境。默认情况下，Node 使用 CommonJS 语法，不会理解您的*导入/导出*语法，所以当您运行程序时，您可能会得到类似于`Unexpected token ‘export’`的错误。这就是 Babel 等工具介入的地方——它们将您的 ES6 模块编译成 CommonJS，以便您的目标可以理解它们。*

*以我们的开放代码为例，将它[粘贴到 Repl](https://babeljs.io/repl) 中，并注意结果。编译后的代码如下所示*

```
*Object.defineProperty(exports, "__esModule", {
  value: true
});
exports.bar = bar;
exports.foo = foo;function bar(str) {
  return str;
}function foo() {
  bar('test');
}*
```

*当您尝试存根/窥探 bar 时，它将使用引用 *exports.bar* ，这与 foo 中使用的引用不同。引用一位提出这个问题的 Sinon 贡献者的话:“通过存根化 bar 导出，你覆盖了导出的符号，但不是被 foo 中的闭包绑定的内部函数引用”。*

*Node 现在支持 es 模块，这对每个人来说都是一个好消息，但这带来了一些新的挑战，所以让我们深入了解第二个难点。*

# *带有 es 模块的存根和间谍*

*既然我们已经讨论了 ES6 > CommonJS 的一个常见挑战，那么让我们来看看本机 ES 模块。这里我们不需要工具来将我们的模块从一种模式转换到另一种模式，我们只需要告诉我们的[环境我们正在使用什么类型的模块](https://nodejs.org/api/esm.html#esm_enabling)。当您运行您的测试套件时，您可能会遇到的问题是，不可能对来自任何模块的*命名导入*使用存根或间谍。如果您尝试这样做，您会得到如下错误:*

```
*ES Modules cannot be stubbed*
```

*使用本机 ES 模块，您不能存根或窥探通过简单命名的*导出/导入*方法可用的导出函数，因为 ES6 模块的导入是导出实体上的[只读视图。这实际上是使它们如此伟大的原因，因为“到模块体内声明的变量的连接仍然是活动的。”](https://exploringjs.com/es6/ch_modules.html#_imports-are-read-only-views-on-exports)*

## *存根和间谍在引擎盖下做什么？*

*在我们探索任何解决方案之前，让我们先探索一下间谍在幕后做了什么，这样我们才能更好地理解根本原因。间谍使用对象和方法。spy 临时存储对原始函数的引用，但会像这样覆盖该值:*

```
*obj[method] = function() {
//spy logic here
}*
```

*这意味着当 spy 或 stub 函数试图在运行时覆盖原始函数时，它将会失败。如果我们在上面的语句周围放一个 *try/catch* ，我们会得到这个错误:*

```
*Cannot assign to read only property 'foo' of object '[object Module]*
```

*要亲眼看到这一点，请在这里下载[我的演示报告](https://github.com/rjbultitude/mocks-stubs-and-spies-commonJS-or-ESM)，在这里你可以运行一套单元测试，演示问题和一些解决方案。此外，看看这个关于[间谍如何在这里工作的更深入的解释](https://abdulapopoola.com/2016/04/11/how-function-spies-work-in-javascript/)。*

## *有多种解决方案，每一种都有其优缺点*

*下面是对我在本文中提到的两个问题都有效的所有解决方案的列表。你选择哪一个将取决于给定你的代码库和它的上下文，你觉得什么样的妥协是可接受的。*

## ***1)作为对象存储和导出函数***

*这本质上是一个命名空间解决方案。其思想是导出一个引用所有模块公共函数的对象，然后在模块中引用该对象。*

```
*export function bar(str) {
  return str;
}

export function foo() {
  **utils.bar**('some text');
}

export const utils = {
    foo,
    bar,
};*
```

*这类似于流行的[揭示模块模式](https://addyosmani.com/resources/essentialjsdesignpatterns/book/#revealingmodulepatternjavascript)，它通过一个对象促进公共方法的导出，并使用一个[生命](https://developer.mozilla.org/en-US/docs/Glossary/IIFE)将该对象返回给外部模块。*

***请注意**，您不*而*需要将此对象导出为默认导出[，因为有时会假定](https://medium.com/@qjli/how-to-mock-specific-module-function-in-jest-715e39a391f4)。对象是否是默认导出并不重要；重要的是一个*对象*被导出。*

***优点***

*   *如果您已经在使用 import all *别名，只需对测试进行最小的更改*
*   *不需要额外的依赖*

***缺点***

*   *需要更改应用程序代码*
*   *涉及潜在的不必要的命名空间*

## *把你的函数放在一个类里*

*与上面的方法类似，这将允许您将函数作为方法来引用。*

```
*export class MyModule {
  bar() {
    return 'bar';
  }

  foo() {
    **this.**bar();
  }
}*
```

***优点***

*   *如果你已经在使用类了，那就没什么可做的了*
*   *不需要额外的依赖*

***缺点***

*   *将类引入现有代码将是一个重大的重构*

## ***3)依赖注入***

*这里我们给函数添加了一个新的参数，默认为依赖关系。在我们的测试中，我们可以用回调覆盖缺省值并监视它。*

```
*export function bar () {
    return 'bar';
}

export function foo (_bar = bar) {
    _bar();
}*
```

***优点***

*   *不涉及导出命名空间*
*   *没有新的依赖项需要配置或维护*

***缺点***

*   *职能范围可能不必要的变化*

## ***4)使用第三方工具***

*有一些工具可以拦截模块引用导出数据的方式。我所知道的两个是 [Rewire](https://www.npmjs.com/package/rewire) 和 [ProxyRequire](https://github.com/thlorenz/proxyquire) (只是常见的)。顾名思义，Rewire 允许我们完全覆盖数据引用。*

*Rewire 的一种方法是在他们的文档中描述的，尽管这里有一个更简洁的片段可以帮助你:*

```
*import __RewireAPI__, * as module from '../module';

describe('foo', () => {
  it('calls bar', () => {
    const barMock = jest.fn();
    __RewireAPI__.__Rewire__('bar', barMock);

    module.foo();

    expect(bar).toHaveBeenCalledTimes(1);
  });
});*
```

*当使用 Babel 时，你必须添加 Rewire 作为插件。请注意，当使用 Rewire 导入模块时，它将改变所有依赖项的导入方式，并可能破坏现有的测试代码。*

***优点***

*   *不需要更改应用程序代码*

***缺点***

*   *需要对现有测试代码进行更改*
*   *要维护的新依赖项*
*   *要学习的新 API*
*   *可能会破坏现有的测试*

## *其他解决方案*

*还有另外两种解决方案值得一提。首先，你可以将一个模块导入到它自身中(如 MostafaR 所描述的[，然后引用你导出的函数，就像它们是外部依赖一样。](https://stackoverflow.com/questions/45111198/how-to-mock-functions-in-the-same-module-using-jest)*

```
*import * as thisModule from './module';export function bar () {
    return 'bar';
}export function foo () {
    **thisModule.**bar();
}*
```

*尽管这是一个很好的解决方案，但是它不能用于 ES 模块，并且它引入了循环依赖，这使得代码更难推理。*

*最后，还有旧的“将依赖项转移到外部模块”解决方案，在我看来这不是一个解决方案，因为它没有解决最初的问题陈述。我不希望每个可能有相同模块依赖的函数都有一个单独的模块。*

# *结论*

*记住，无论你使用什么解决方案，你的测试库都可能希望 stubs 和 spies 引用一个方法，所以一定要使用 *all* 别名导入你的模块:*

```
*import * as myModule from './myModule';const mySpy = sinon.spy(myModule, 'myFn');*
```

*另外，要注意您使用的是哪个版本的 Node。我在旧版本上遇到过问题。*

*到目前为止，您应该已经掌握了更好地理解问题所需的所有信息，并且有了适合您的情况的解决方案。*

*如果您不想安装任何新的依赖项，并且没有重大的重构任务，那么使用类、命名空间或依赖项注入都是很好的解决方案。相反，使用第三方工具来改变导入在测试中的工作方式将意味着没有应用程序重构，但会使测试代码更难推理，并将增加(又一个)需要维护的依赖项集，这些依赖项可能会被放弃或否决。*

*如果你想亲自看看问题和解决方案，[在这里下载我的演示报告](https://github.com/rjbultitude/mocks-stubs-and-spies-commonJS-or-ESM)。*

*欢迎评论、问题和建议。*

**更多内容尽在*[***plain English . io***](http://plainenglish.io/)*