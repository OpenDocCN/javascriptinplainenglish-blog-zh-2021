# 如何为你的 Next.js 应用编写一个简单的测试

> 原文：<https://javascript.plainenglish.io/how-to-write-a-simple-test-for-your-next-js-app-7e7e83420d7a?source=collection_archive---------1----------------------->

## 为 Next.js 应用程序编写简单测试的指南。

# **首先最重要的事情**

对软件开发人员来说，为他们的软件编写测试是很重要的，尤其是在生产中，以正确地确定它是否有效地工作，是否如预期的那样。我们不想假设它的工作只是为了以后失败。

![](img/581b47bd641268c9627ab594a366cb8b.png)

嗯，它可能“工作”,但您仍然需要编写测试:)

在本教程中，我将带您使用 [Jest](https://jestjs.io/) 和 [React 测试库](https://testing-library.com/docs/react-testing-library/intro)为您的 [Next.js](https://nextjs.org/) 应用程序中的表单编写一组简单的测试。让我们简要地看一下上面提到的这些工具，并设置我们的项目。

# Next.js

Next.js 是由 [Vercel](https://vercel.com/breezeio) 构建的开源 JavaScript 框架，它提供了基于 React 的 web 应用功能。它支持诸如服务器端渲染、无服务器功能、静态应用等功能。

我们将通过创建一个新的 Next.js 应用程序来设置我们的项目。

打开您的终端，导航到您保存回复的位置，然后键入下面的命令。

```
$ npx create next-app@latest
```

这将带您完成一些安装提示，然后在我们的文件夹中创建一个基本的 Next.js 应用程序。如果您更喜欢 TypeScript 设置，请添加如下所示的 TypeScript 标志:

```
npx create-next-app@latest --typescript
```

现在我们已经设置了 Next.js 应用程序，让我们将测试工具添加到我们的应用程序中。

# 玩笑

Jest 是一个 Javascript 测试框架，由克里斯托夫·中泽友秀创建，目前由脸书维护。Jest 的主要优点之一是简单。这相对容易设置，尤其是对于第一次使用的用户。

让我们使用 npm 安装 Jest 依赖项:

```
$ npm install -D jest babel-jest
```

这将安装 Jest 和`Babel Jest`，确保 Jest 与 Next.js 一起正常工作。

接下来，我们将创建一个`.babelrc`文件，并添加如下所示的配置。这将有助于配置我们已经安装的`Babel Jest`。

```
{  
 "presets": ["next/babel"] 
}
```

这确保 Jest 在我们的应用程序中正常工作。

虽然 Jest 使我们能够轻松地测试 javascript 应用程序和代码，但它不能直接测试我们的 Next.js 应用程序，因为它没有呈现基于 React 的组件的功能。因此，我们需要一个可以与 Jest 一起工作的工具来呈现我们的 Next.js 应用程序，然后在其上运行测试。

![](img/d8bec1ca439fc2d1bb00c420b12ef87a.png)

这就是 **React 测试库**的用武之地。

# 反应测试库

React Testing Library 是一个开源工具，通过呈现 React.js 应用程序并公开要查询的 DOM 来帮助测试它。这有助于测试 React.js 应用程序的使用意图，而不仅仅是实现细节。

让我们将依赖项安装到我们的应用程序中。

```
$ npm install -D @testing-library/jest-dom @testing-library/react
```

这将安装 React 测试库和一个`@testing-library/jest-dom`包，它将与 Jest 一起测试我们的应用程序。

在我们开始编写测试之前，让我们对项目目录中的`package.json`文件进行一些修改。

第一个变化是在`scripts`字段，它告诉 npm 如何在我们的应用上运行测试。

```
“test”: “jest — watch”
```

这告诉 npm 在我们运行`npm test a` 命令时，以监视模式运行 jest(监视我们的更改并相应地运行测试)。我们的`scripts`字段现在应该如下所示。

```
“scripts”: {
 “dev”: “next dev”,
 “build”: “next build”,
 “start”: “next start”,
 “test”: “jest — watch”
},
```

其次，我们将向我们的`package.json`添加一个名为`jest`的新字段。

```
"jest": {
 "testEnvironment": "jsdom"
}
```

这告诉 Node 使用`jsdom` 作为我们的测试环境。默认的节点测试环境不允许我们使用浏览器环境进行测试。

设置好这些工具后，我们现在可以开始编码和编写测试了。

![](img/9797fe755237396ad615c06e5f36f1c9.png)

我们将从创建一个基本的注册表单开始，然后我们将为它编写测试。

# 注册表单

我们将导航到我们的`index.js`文件，删除它的所有内容，并导入`useState`。

```
import { useState } from 'react';
```

接下来，我们创建一个`RegisterPage`组件，并在其中创建一个我们将要测试的基本表单。

在这个`RegisterPage`组件中，我们声明了一个`isLoading`状态值，并将其设置为 false。该值将指示我们是否正在提交(正在加载)。

然后我们继续创建一个`registerUser`函数，我们将使用它来模拟表单提交，它将阻止默认表单提交，将`isLoading`设置为`true`，并在 5 秒或 5000 毫秒后将其设置回`false`。

接下来我们创建`formInputs`，一个对象数组，包含表单输入，我们将在`return`块中呈现它。

接下来，在我们的组件中，我们将创建一个表单，映射我们的`formInputs`数组，并添加一个按钮，当它被点击时调用`registerUser`。我们现在可以导出我们的组件了。

# 风格

让我们给我们的`styles/globals.css`添加一些基本的样式。如果您没有该文件，创建一个并导入到您的`_app.js`文件中。

我们现在将保存这些文件，并使用`npm run dev`运行下一个应用程序。当我们打开浏览器到`[http://localhost:3000](http://localhost:3000)` 时，我们应该看到我们的应用程序已经启动并运行了。

现在是时候为我们的应用程序中的表单编写测试了。

# 测试应用程序

让我们首先创建一个`tests`文件夹，在其中，我们将创建一个名为`pages`的子文件夹。这是我们保存页面测试文件的地方(创建你的第一个测试文件并命名为`index.test.js`)。

首先，我们将对测试文件进行一些导入。

```
import '@testing-library/jest-dom';import { render, screen, fireEvent } from '@testing-library/react';
```

我们导入了之前安装的`@testing-library/jest-dom`，我们还从`@testing-library/react`中导入了`render`、`screen`和`fireEvent`更多关于它们在本教程中的用法。

接下来，我们导入将要测试的`Index`文件。

```
import Index from '../../pages/index';
```

在我们编写测试之前，让我们创建一个数组`formInputValues`，它将包含我们将在测试表单时使用的模拟数据。

现在，测试。

我们将从描述我们测试的目的开始。我们将从创建一个`describe`代码块开始。`Describe`是一种 Jest 方法，用于将相关测试块分组在一起。它有两个参数:一个描述测试套件的字符串和一个包装将要编写的测试的回调函数。

```
describe(‘Simple working form’, () => {});
```

接下来，我们将在`it`块中编写测试用例。`it`是一个 Jest 方法，其中编写了实际的测试功能。就像一个`describe`块一样，它有两个参数:一个描述测试套件的字符串和一个包装测试功能的回调函数。`it`的替代方法是`test`。让我们从编写一个测试所有表单输入是否正确呈现的程序开始。我们将在我们的`describe`街区这样做。

在我们的`it`块中，我们将把我们的`Index`组件传递给一个`render`方法。`render`是一个`@testing-library/react`方法，模拟作为参数传递的 React 组件的渲染。

然后我们使用`forEach`继续循环我们的`formInputValues`。对于每个`value`，我们在`value.label`上调用`screen.getByLabelText`。`screen`是一个`@testing-library/react`对象，它公开了用于查询我们之前呈现的组件的方法，其中一个是`getByLabelText`。`getByLabelText`用于检索标签作为参数传递的一个元素。

我们将从`screen.getByLabelText`返回的值作为参数传递给`expect` 。`expect`是一个 Jest 方法，它允许我们访问匹配器，帮助我们测试某些条件。我们使用的匹配器的一个例子是`toBeInTheDocument`，在我们的 expect 函数上调用它，检查我们传递给 expect 的参数是否存在于我们呈现的组件中，即在文档中。

本质上，我们期望在我们的`formInputValues`数组中带有标签的元素存在于我们的组件中。

让我们再添加两个测试来完成我们的测试用例。一个将检查我们的按钮是否出现在文档中，另一个将检查我们的按钮被点击后是否加载。

在我们的第二个`it`块中，我们渲染`Index`，通过调用屏幕对象中的`getByRole`方法检索我们的按钮，并用值初始化`submitButton`。`getByRole`有几个参数，但是对于本教程，我们只传递我们正在查询的角色的`name`和一个包含按钮的`name`的对象(按钮的文本)。我们使用两个匹配器来测试我们的按钮。`toBeInTheDocument`和`not.toBeDisabled`检查我们的按钮是否存在且未被禁用。

**注意**:在任何匹配器测试之前使用`not`进行匹配器的反转。

在我们的第三个`it`块中，我们渲染`Index`并取回我们的`submitButton`。我们循环遍历我们的`inputFormValues array`，获得各自的输入，并使用`fireEvent.change`来模拟用数组中的值填充每个输入。

fireEvent 是来自`@testing-library/react`的一个对象，具有用于模拟真实 dom 事件的方法。我们使用`change`来改变表单值，然后我们使用`click`来模拟点击按钮。

最后，我们检查我们的按钮的值在点击后是否已经变成了`Loading…`。我们可以用另一种查询方法`findByRole`来实现。它类似于`getByRole`,但是它返回一个承诺，过一会儿就解决了。

**注意**:如果您预计您的`fireEvent`更改不会立即反映出来，请使用`findBy`，而不是`getBy`。

我们的`index.test.js`现在应该是这样的:

运行`npm test a`来查看您的测试结果，您应该会看到类似这样的内容

```
PASS  tests/pages/index.test.js (14.833 s)
  Simple working form
    √ Should render all form inputs (208 ms)
    √ Should render submit button (458 ms)
    √ Should submit when inputs are filled and submit button clicked (303 ms)Test Suites: 1 passed, 1 total
Tests:       3 passed, 3 total
Snapshots:   0 total
Time:        30.426 s
Ran all test suites matching /a/i.
```

# 结论

恭喜，我们已经成功测试了 Next.js 应用程序。随意加入更多的测试案例/增加测试的范围。完整的项目可以在我的 GitHub 上的[这里](https://github.com/chani24/Testing-React-Form)找到。

关于本教程中使用的工具的更多细节，请查看 [Next.js](https://nextjs.org/docs/getting-started) 、 [Jest](https://jestjs.io/docs/getting-started) 和 [React 测试库](https://testing-library.com/docs/react-testing-library/intro)文档。

我将感谢对本教程的反馈:)，好运编码！

*更多内容请看*[*plain English . io*](http://plainenglish.io/)*。在这里注册我们的* [*免费周报*](http://newsletter.plainenglish.io/) *。*