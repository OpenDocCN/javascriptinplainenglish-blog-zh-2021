# 用 esbuild 为 Web 构建 JavaScript 库

> 原文：<https://javascript.plainenglish.io/esbuild-library-6ec5fdb26e2c?source=collection_archive---------6----------------------->

## 最快的捆扎机之一

![](img/2ea7716015ff48f861d19f5ab542e3fd.png)

Image Credits: [GitHub](https://github.com/evanw/esbuild)

我们都喜欢 JavaScript 库。而且有时候，我们想自己写一个库。为什么？要捆绑通用代码，我们需要解决一个问题。下面是如何使用 esbuild，一个速度极快的 JavaScript bundler 来做这件事。

首先，有三种方式为浏览器捆绑库:

1.  “老派”方式，用典型的脚本标签捆绑加载我们的 JavaScript，并从脚本中访问所需的变量。
2.  使用 bundler 来构建应用程序，这消耗了我们的库捆绑包:像 create-react-app、webpack 或 parcel，我们可以在其中编写导入语句，然后代码被捆绑并生成 HTML 模板。这个 HTML 模板主要使用方式 1。所以它使用典型的脚本标记。
3.  更现代也更危险的方法:在浏览器中使用 JavaScript 模块。由于脚本标签的`type="module"`属性，我们可以在浏览器中直接使用导入语法。然而，这种方式并不被所有的浏览器所支持。

您可能已经注意到了一些事情:实际上，在捆绑我们的库代码时，方式 2 和方式 3 是相同的。由于使用`export` `import`语法没问题，我们在捆绑代码中进行单次或多次导出——多亏了 JS web 模块，我们甚至可以在浏览器中使用它。

我们开始吧！

这是我们的小“库”的代码，导出一个函数和一个类:

要使用 esbuild 进行捆绑，我们首先需要将它安装在我们的项目中:

`npm install esbuild`

是的，直接在我们的项目中，而不是在全球范围内。然后，我们可以运行 esbuild 来捆绑我们的文件。为此，我建议在 package.json 中创建一个脚本:

```
"build": "./node_modules/.bin/esbuild index.js --outfile=bundle.js"
```

现在你可以运行`npm run build`或`yarn run build`——两者都应该产生一个 bundle.js。现在，bundle.js 包含我们刚刚编写的相同代码——原因是，我们没有传递任何 bundle 选项。

让我们提供所需的选项，这样我们就可以导入一个最小化的库，它应该可以在每个浏览器中运行。

使用目标选项，我们可以指定目标——在我们的例子中，是现代浏览器。我们选择的格式是 ESM 格式，代表 ES 模块。我们得到的包现在很小，导出了我们想要公开的函数和类。由于我们捆绑了 ES 模块语法，我们现在可以像这样导入和使用我们的库代码:

```
*import* { doubleNumber, Calculator } *from '*./bundle.js'console.log(doubleNumber(2)) // 4const calc = new Calculator(0)
calc.add(10)console.log(calc.getNumber()) // 10
```

在现代 web 开发中，这是最常见的方式。我们可以在发布前捆绑的项目中轻松使用 import-statement——我使用的 create-react-app、Vue CLI、webpack 或 package。

## 在浏览器中使用导入语法

我们刚刚创建的库包也可以直接在浏览器中使用——这要归功于`type="module"`属性。这里有一个小设置:

和以前一样，代码运行。然而，目前并不是所有的浏览器都可以使用`type="module"`。如果我们想要 100%安全，最好只使用 script 标签来加载 JavaScript 文件。问题是:我们刚刚创建的包不能这样工作。当您使用普通的脚本标签在浏览器中加载`bundle.js`时，您会看到一个错误:

![](img/01516cd7cd7858013e1f1e161e966774.png)

让我们为老派的案例做一个包裹。我们需要改变的是 esbuild 的格式选项。除了值`esm`，还有`iife`可用，代表“立即调用的函数表达式”。

将我们的库代码捆绑到这样一个函数会产生这样一个代码:

```
(() => {
  // our code
})(); 
```

问题:我们在库中定义的类和函数将只在这个函数的范围内可用。没有办法从外面接近它。为了避免这个问题，我们可以将整个函数保存为一个全局可用的变量。我们用`--global-name`选项来做这件事。

下面是运行它的整个脚本:

作为全局变量，我选择了`lib`。如您所见，我们通过这个变量访问函数和类:

但是这个自调用函数的好处是什么呢？因为我们确定了函数和类(以及其他所有东西)的范围，所以在全局范围内不可能有任何与其他变量的冲突。

感谢您的阅读！

*更多内容请看*[***plain English . io***](http://plainenglish.io/)