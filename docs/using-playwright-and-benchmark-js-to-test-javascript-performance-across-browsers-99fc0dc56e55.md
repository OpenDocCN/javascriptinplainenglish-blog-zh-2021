# 如何使用剧作家和 Benchmark.js 跨浏览器测试 JavaScript 性能

> 原文：<https://javascript.plainenglish.io/using-playwright-and-benchmark-js-to-test-javascript-performance-across-browsers-99fc0dc56e55?source=collection_archive---------3----------------------->

正如我们在[上一篇文章](https://medium.com/@alowdon/testing-javascript-performance-with-benchmark-js-3d3f4e4b9fc2)中讨论的，Benchmark.js 是测试 JavaScript 代码性能的一个有用的库。然而，由于 JavaScript 是一种[解释语言](https://www.easytechjunkie.com/what-is-interpreted-language.htm)，执行代码时的性能取决于使用的 JavaScript 引擎。不同的浏览器使用不同的 JavaScript 引擎:

*   谷歌的 [V8](https://v8.dev/) 是最常用的 JavaScript 引擎，用于基于 [Chromium](https://www.chromium.org/) 的浏览器，如谷歌 Chrome 和微软 Edge，以及 [Node.js](https://nodejs.org/) 和 [Deno](https://deno.land/) 运行时
*   蜘蛛猴由 Mozilla 开发，用于 Firefox 和其他项目
*   JavaScriptCore 是苹果的产品，用于基于 WebKit 的浏览器，比如 Safari

进行更改时，我们必须验证对这些引擎性能的影响，这一点很重要；我们很容易对一些浏览器产生积极的影响，而对其他浏览器产生消极的影响，并且可能经常需要根据用户最常用的浏览器做出关于使用什么代码的务实决定。

![](img/037d8680815e5397f6cd20260948bfe1.png)

Performance varies across different browser engines

剧作家作为浏览器自动化工具正在迅速获得关注，它提供了针对 Chromium、Firefox 和 WebKit 的测试能力。因此，我们可以使用剧作家对我们上面提到的所有 JavaScript 引擎执行 Benchmark.js 测试。

我们将从我们之前在工作的示例测试套件开始。首先，我们需要安装剧作家测试运行器和支持的浏览器(使用这种方法将允许剧作家为您维护所需的浏览器引擎，但是如果您愿意，您可以[使用现有的安装](https://playwright.dev/docs/browsers#installing-browsers))。

```
npm i -D @playwright/test
npx playwright install
```

> 注意:在撰写本文时，如果您使用的是 MacOS Monterey，您应该调用`npm i -D @playwright/test@next`，因为在最新的稳定版本中，WebKit 测试存在[问题](https://github.com/microsoft/playwright/issues/9811)

接下来，我们需要创建一个 spec 文件供剧作家执行。默认情况下，测试被假定在一个`tests`文件夹中，所以让我们在`tests/bench.spec.js`创建一个新文件，内容如下:

```
const { test } = require('@playwright/test');test('Run benchmarks', async ({ page }) => {
  await page.goto(`file://${process.cwd()}/bench.html`);
});
```

我们现在可以通过运行以下命令来运行测试:

```
npx playwright test
```

我们将得到以下输出:

```
Running 1 test using 1 worker✓  tests/bench.spec.js:3:1 › Run benchmarks (728ms)1 passed (1s)
```

所以页面成功加载了，但是我们看不到基准测试的结果，这没有多大用处！幸运的是，我们可以捕获并显示控制台输出，我们之前通过监听来自剧作家的`console`事件来查看基准测试结果。

我们还可以从 Benchmark.js `complete`事件发布测试套件完成时的已知消息:

```
suite.on('complete', () => console.log('Benchmark suite complete.'))
```

并在允许剧作家测试完成之前等待已知消息以确保基准完成:

```
let benchmarkPromise = new Promise(resolve => {
  page.on('console', async message => {
    if (message.text() === 'Benchmark suite complete.') {
      // if the suite has finished, we're done
      resolve();
    } else {
      // pipe through any other console output
      console[message.type()](message);
    }
  });
});
```

> 注意:作为优秀的开发人员，我们显然应该将任何神奇的字符串放入共享常量中，但我们在这里这样做只是为了保持示例简单！

我们现在可以`await`在剧作家测试中实现这一承诺，当我们再次运行测试运行程序时，我们将在控制台上看到基准测试结果:

```
Running 1 test using 1 worker✓  tests/bench.spec.js:3:1 › Run benchmarks (13s)
Array.prototype.some x 133 ops/sec ±0.89% (56 runs sampled)
for loop x 1,724 ops/sec ±0.62% (60 runs sampled)1 passed (13s)
```

成功！🎉默认情况下，剧作家使用 Chromium 引擎运行测试，因此要在所有浏览器上运行它们，我们需要使用以下代码:

```
npx playwright test --browser=all --workers=1
```

`browser`选项配置在哪些浏览器中运行测试，而`all`将使用剧作家可以使用的所有浏览器。我们还包括了`--workers=1`,因为剧作家默认并行运行测试，但这显然会影响我们的性能测试，所以这个选项只允许一个工人强制测试串行运行。我们的输出现在看起来像这样:

```
Running 3 tests using 1 worker✓  [chromium] › tests/bench.spec.js:3:1 › Run benchmarks (13s)
Array.prototype.some x 140 ops/sec ±1.14% (56 runs sampled)
for loop x 1,793 ops/sec ±0.99% (61 runs sampled)
  ✓  [firefox] › tests/bench.spec.js:3:1 › Run benchmarks (14s)
Array.prototype.some x 224 ops/sec ±0.53% (60 runs sampled)
for loop x 242 ops/sec ±1.10% (59 runs sampled)
  ✓  [webkit] › tests/bench.spec.js:3:1 › Run benchmarks (12s)
Array.prototype.some x 757 ops/sec ±22.39% (54 runs sampled)
for loop x 1,756 ops/sec ±1.27% (60 runs sampled)3 passed (40s)
```

现在，我们可以看到所有三个浏览器引擎的基准测试结果。正如这个例子所强调的，差异可能是实质性的，这证明了运行这些测试是多么有用！

这里我们还可以做更多的事情，但是这篇介绍为使用剧作家协调跨浏览器的测试奠定了基础。以下是不同文件的最终版本，供参考:

*更多内容请看*[***plain English . io***](http://plainenglish.io/)