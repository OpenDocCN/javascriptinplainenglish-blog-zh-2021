# 如何用 Jest 来表达单元测试

> 原文：<https://javascript.plainenglish.io/how-to-add-unit-testing-to-express-using-jest-6f7746f66c65?source=collection_archive---------10----------------------->

向您的 Express 应用程序添加单元测试比您想象的要容易

![](img/09875ee8454ea37a1dec946ae50fd436.png)

Photo Illustration by David Fekke

*原发布于*[*https://fek . io*](https://fek.io/blog/how-to-add-unit-testing-to-express-using-jest/)*。*

无论你是在做测试驱动开发(TDD ),还是只是在寻找一种方法将自动化测试添加到你的 [express](https://expressjs.com) 应用程序中，使用许多不同的单元测试框架都可以很容易地完成。对于 Node.js，我使用了许多不同的测试框架。Node 的一个好处是在测试时不缺少选项。

我更喜欢使用的测试框架是 [Jest](https://jestjs.io/) ，但它不是对 express 应用程序进行单元测试的要求。Jest 非常受 React 开发人员的欢迎，但是它可以用于任何 JavaScript 应用程序。

我喜欢使用 Jest，因为除了拥有运行单元测试所需的所有工具之外，它还可以检查代码覆盖率。

# 编写可测试的代码

TDD 的好处之一是帮助开发人员编写更松散耦合的代码，这不仅使代码更容易测试，而且使代码更可重用。

Express 遵循基于路由签名响应请求的基本结构，即:

```
app.get('/users/report', function(req, res) {
    res.render('userreport', { title: 'Users Report' });
});
```

将处理程序代码分解成它自己的函数，然后在路由中使用该处理程序，这是一个很好的做法。

```
function userReportHandler(req, res) {
    res.render('userreport', { title: 'Users Report' });
}

app.get('/users/report', userReportHandler);
```

这不仅使 express 代码更加有组织，现在我们只测试处理程序，而不必运行 express。

# 添加笑话

要将 Jest 添加到您的应用程序中，我们可以在应用程序目录的根目录下运行以下命令；

```
> npm i jest --save-dev
```

这将把 Jest 工具安装到我们的 node_modules 文件夹中。现在 jest 已经安装好了，让我们修改我们的`package.json`文件的`scripts`部分，在`test`属性中运行 Jest。在我们的`scripts`部分，它应该看起来像下面这样；

```
"scripts": {
    "test": "node --experimental-vm-modules node_modules/.bin/jest --coverage",
    "start": "node <name_of_mainjs_file>"
},
```

让我们快速看一下这个命令在做什么。我们告诉`Node`在`node_modules/.bin/jest`位置运行 jest 命令。这进而运行 jest-cli。我们还运行了一个标志`--experimental-vm-modules`,允许我们运行 ESModule 导入/导出语法。我们还使用 jest 的`--coverage`标志来获取代码覆盖率报告，让我们知道单元测试覆盖了我们代码的多少百分比。

# 快速应用示例

出于这个例子的目的，我将创建一个简单的 Express 应用程序，它有两条路线。一个作为主页运行，有一个路由`/`，另一个有一个路由`/hello`，有一个输入参数`:name`。

现在我们可以将一个名为`__tests__`的文件夹添加到我们的项目中。Jest 会自动查找这个目录中的任何 JavaScript 或 TypeScript 文件。

在我们创建第一个测试之前，让我们使用下面的命令将`supertest`添加到我们的项目中；

```
npm i supertest --save-dev
```

Supertest 用于模拟我们的 Express 服务器，因此我们不必运行 HTTP 服务器来测试我们的路由。

# 单元测试

让我们创建一个单元测试来测试我们的路由处理器。

我们的两个路由处理程序都在`res`对象上使用 send 函数，所以我创建了一个简单的模拟响应对象，它复制了 Express response 对象在实际应用程序中使用它时会做的事情。在这种情况下，`send`只是回显我们传入到`text`属性中的任何内容。

在我的两个单元测试中，我使用 Jest 的`expect`函数来比较我们在`toEqual`函数中的预期结果。如果匹配，两个测试都将通过。

现在让我们用`supertest`添加另一个测试套件来测试路由。我们将创建一个名为`routes.t.js`的新文件来测试实际路线。

使用`supertest`，我们可以看到这些测试比我们的 Express 应用程序所做的更彻底、更准确。在上面的测试套件中，我们使用`supertest`来运行特定的路线。我们还可以查看特定的 express 属性，以确保应用程序返回预期的结果。

在所有三个单元测试中，我们使用`expect`来检查我们是否有正确的标题结果、statusCode 和 text。

# 运行我们的测试

为了测试我们的单元测试，我们所要做的就是在我们的命令行中运行`npm test`。

```
> npm test

> expresstest@1.0.0 test
> node --experimental-vm-modules node_modules/.bin/jest --coverage

(node:56591) ExperimentalWarning: VM Modules is an experimental feature. This feature could change at any time
(Use `node --trace-warnings ...` to show where the warning was created)
 PASS  __tests__/routes.t.js
 PASS  __tests__/handlers.t.js
------------|---------|----------|---------|---------|-------------------
File        | % Stmts | % Branch | % Funcs | % Lines | Uncovered Line #s
------------|---------|----------|---------|---------|-------------------
All files   |     100 |       50 |     100 |     100 |
 default.js |     100 |       50 |     100 |     100 | 7
 main.js    |     100 |      100 |     100 |     100 |
------------|---------|----------|---------|---------|-------------------

Test Suites: 2 passed, 2 total
Tests:       5 passed, 5 total
Snapshots:   0 total
Time:        0.782 s, estimated 1 s
```

# 结论

从上面的例子中你可以看到，向你的 express 应用程序添加单元测试实际上是非常容易的。

我的一个前同事在他的隔间里有下面的标语；测试，测试，测试，一旦你认为你完成了，再测试一次。单元测试只是代码质量保证的一个小方面，但是如果与 CI/CD 一起正确使用，它将帮助您在 bug 进入测试环境之前就发现它们。

[](https://github.com/davidfekke/expresstest) [## GitHub - davidfekke/expresstest

### 在 GitHub 上创建一个帐户，为 davidfekke/expresstest 开发做贡献。

github.com](https://github.com/davidfekke/expresstest) 

*更多内容看*[***plain English . io***](http://plainenglish.io/)