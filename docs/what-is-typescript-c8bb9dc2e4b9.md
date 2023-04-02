# 什么是 TypeScript？对初学者的全面介绍

> 原文：<https://javascript.plainenglish.io/what-is-typescript-c8bb9dc2e4b9?source=collection_archive---------16----------------------->

![](img/184f9065028e9b68d19f3bcf1d1f773a.png)

Photo by [Joshua Woroniecki](https://unsplash.com/@joshua_j_woroniecki?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

对于那些听说过 Typescript 并想了解更多的人来说，它是 JavaScript 的一个超集(可以认为是扩展或增强),提供了可选的静态类型。成为 JavaScript 的超集意味着默认情况下所有有效的 JavaScript 都是有效的 TypeScript。

这意味着，如果您是一名经验丰富的 JavaScript 开发人员，并且想尝试一下 TypeScript，您可以简单地将您的所有。js 文件到。ts 和大部分文件应该能够在很少错误的情况下运行。

我说很少，而不是没有，因为可能有一个函数调用或变量定义在你的代码中被错误地使用了，你必须修复它。但是通常. js 文件可以转换成。ts 并运行良好。当然，这回避了一个问题，“那么转换的意义是什么？”很高兴你问了。

TypeScript 中的类型在称为 transpiling 的编译过程中被剥离。这将类型脚本代码转换成有效的 JavaScript。默认情况下，编译后的 JavaScript 与 ES3(ECMAScript 3)兼容，但是可以使用配置文件进行修改，以编译成较新的版本。通常，在使用 TypeScript 时，为了确保您的代码面向所有正在使用的浏览器，您会希望尽可能面向最低版本的 JavaScript。

换句话说，留在 ES3 并不一定是件坏事。因为您可以编写最新最棒的 JavaScript，并让 TypeScript 将其编译成旧版本，所以可以说您获得了两个世界的最佳效果。需要注意的是，TypeScript 并不支持 JavaScript 的所有新特性，但绝大多数特性都支持。了解某个特性是否受支持的一个很好的参考可以在[这里](https://github.com/microsoft/TypeScript)找到。

## ECMAScript 什么？！

ECMAScript 是 JavaScript 遵循的语言规范。从 ES2015 开始，每年都会发布新版本的 JavaScript，使用包含规范完成年份的命名约定。例如，ES2015 完成于 2015 年，因此名称为 ES 并附加了年份，从而使其成为 ES2015。

## TypeScript 和 JavaScript 的例子

我想快速复习一下这种语言的例子。下面的代码是用符合 ES5 的 JavaScript 编写的，试图记录一条问候消息。greetingLogger 函数接受一个字符串消息，并记录使用输入字符串构造的问候语

```
function greetingLogger(message) {
  console.log('Hello there, ', message, '!');
}
var person = { name: "Jonathan" };
greetingLogger(person);
```

输出是:

```
> greetingLogger(person); 
Hello there  { name: 'Jonathan' } !
```

这不是预期的输出。我们想要一个字符串输出，但是 JavaScript 让函数返回一个对象。我们希望输出

```
> greetingLogger(person); 
Hello there, Jonathan!
```

我们当然可以用一些条件检查来修改它，确保类型是一个字符串，如果是，就记录消息。然后，我们遇到了一个问题，如果我们有更复杂的类型，比如包含一组特定值的数组，那么向外扩展这个解决方案就会成为一个问题。相反，让我们看看如何使用 TypeScript 解决这个问题。

```
function greetingLogger(message: string) {
  console.log('Hello there, ', message, '!');
}var person = { name: "Jonathan" };
greetingLogger(person);// Should return 
Argument of type '{name: string; }' is not assignable to parameter of type 'string'.
```

好吧，现在我们至少被告知我们试图完成的是错误的。然而，它仍然是不正确的输出。这次让我们通过调用 person 对象的 name 属性来解决这个问题。修改代码行，使其看起来像这样:

```
greetingLogger(person.name);// Should now output
Hello there, Jonathan !
```

好多了。现在我们正在生成我们想要的字符串值，我不必对字符串类型进行条件检查。我特别声明，我希望消息的类型是 string，并确保如果我使用一个对象，我会调用该对象的 name 属性，以便它被传入，而不是整个对象本身。

## 为什么使用 TypeScript？

好吧，好吧，我仍然可以在这里你说；但是我为什么要用 TypeScript 呢？我能想到一些你想要的理由。例如:

1.  更容易的重构——我们能够在应用程序中更改模块和函数，并确信来自它们的错误将在编译时暴露，而不是等到运行时。
2.  代码完成—我们的代码编辑器能够为应用程序中使用的对象提供自动完成功能。VS 代码在使用 TypeScript 时尤其擅长这一点，因为它是用 TypeScript 编写的。
3.  Bug 检测——让我们面对即将发生的 bug。错别字、缺少参数以及不匹配的类型都是在编码或编译时可能被发现的错误的例子。
4.  文档——类型注释系统允许优秀的文档。它们描述了应用程序中函数的输入/输出和数据结构。

我知道你也在说，“好吧，那很好，但是有什么缺点呢？从长远来看，冒险走上打字稿这条路会让我付出什么代价？”嗯，我对此也有一些看法。

1.  学习曲线——打字需要一个学习曲线。重要的是，团队中的每个开发人员都能够准确地维护和更新类型，这意味着要投入时间学习语言。
2.  额外的构建步骤—您必须配置当前构建系统的 TypeScript。根据项目的大小，它可能会增加几秒钟的构建时间。
3.  第三方库—大多数第三方库需要在安装库时添加类型。流行的库通常都是最新的，这并不是什么大问题，但是小的库如果不及时更新就会变得很痛苦。
4.  集成期—将 TypeScript 与现有项目集成将有一个调整期。这意味着您将同时管理 JavaScript 和 TypeScript 文件，这可能是一件痛苦的事情。

从我学习这门语言的经验来看，好处远远大于坏处。随着 TypeScript 越来越接近顶级编程语言，第三方支持也在增长。

# 设置您的开发环境

我们将花几分钟时间来设置开发环境。如果你已经有了一个最喜欢的编辑器，那么我不会因为你喜欢那个编辑器而试图改变你的决定。我只是希望改变你对使用打字稿的看法。根据我的经验，我使用的编辑器是 VSCode。它对几乎所有的东西都有扩展。

正如我在帖子前面提到的，它是用打字稿写的。所以当你在寻找一个对 TypeScript 有最好支持的编辑器时，我觉得忽略 VSCode 是一个错误。然而，如果你使用另一个编辑器，如 Sublime 或 Atom，并且习惯了它们的工作方式，那么你应该也没问题，尽管我会提到，我不确定自动完成或 bug 检测功能在这些编辑器中是否普遍。原谅我的无知，如果他们已经被添加。如果您使用的是 Visual Studio 20xx 或 WebStorm 这样的 IDE，

那里也支持 TypeScript，您应该会从自动完成和 bug 检测特性中受益。现在我已经提到了编辑器和 IDE，让我们实际安装一个。

## 虚拟代码

我将带您完成 VSCode 的安装，因为它是我使用的编辑器。如果你想用上面提到的其中一个，你只能自己安装了。如果您对 VSCode 满意，那么请继续操作。

1.  参观 code.visualstudio.com
2.  单击大的彩色按钮将其安装到您的机器上(如果您使用的是 Arch 等 Linux 版本，我将在下面提供安装步骤)。
3.  按照安装向导中的步骤操作。(对于 Windows 用户来说，选中“添加到路径”复选框非常重要，这样你就可以在本文后面使用命令行。)(对于 macOS 和 Linux 用户，您需要打开 VS Code 至少一次，以便将命令添加到 path 中，您可以通过按 ctrl + shift + p 并搜索 Shell 命令来完成:在 PATH 中安装“Code”命令，单击它，您就可以开始了)

## 对于 Arch Linux 或者那些使用 OS 软件包管理器的人，请遵循以下步骤。

1.  打开你的终端，输入`sudo pacman -Sy`来更新你的机器
2.  运行`sudo pacman -S code`安装 VS 代码
3.  试着运行`code .`,看看你能否用 VS 代码打开当前目录。

如果是这样，你可以继续下一部分。

## 安装节点和 NPM

我喜欢使用一个类似包管理器的工具，叫做 [Volta](https://volta.sh/) 。如果你点击链接，你可以了解更多。

## 对于 Windows

请访问该链接，然后单击“开始”按钮。它会将您带到下载页面，在 Windows 部分下，您可以单击下载并运行 Windows installer 链接。遵循这些步骤，你应该可以开始了。

## 对于 Linux 和 macOS

该网站建议使用 cURL 命令安装它

```
$curl [https://get.volta.sh](https://get.volta.sh) | bash
```

即使你使用的是 Fish 或 zsh，你也应该使用上面的命令。我在哥鲁达上使用它，它使用鱼作为默认外壳。一切都很好。现在使用 volta 来安装我们运行的节点

```
$volta install node
// this will install the latest LTS version which should install
// 14.17.3$volta install node@12.20.0
// this will install version 12 of Node$volta install node@12
// this will install the most suitable version to match the request
```

只选择其中一个命令。如果您想要最新的稳定版本，请使用第一个命令。否则，你可以选择旧版本，我在 MacBook 上用的就是这个版本。要验证节点和 npm 是否安装正确，我们可以运行

```
$node --version
// => 14.17.5
$npm --version
// => 6.14.13
```

这就是我的 Linux 机器上的输出。只要你有类似或低于你应该是好的。我一周前安装了 Node 的当前版本，发现它对我来说破坏了很多东西，所以我换了版本。如果你想走那条路，我不会阻止你，但如果有任何事情发生，你可能很难找到解决办法。

## TypeScript 演示

现在我们已经安装了允许我们编写代码的工具，我们需要一个存储代码的地方。让我们打开我们的终端，cmd/powershell，运行以下命令:

```
$cd Desktop
$mkdir typescript-demo && cd typescript-demo
```

对于不熟悉终端命令的人来说，这些命令会将您所在的目录(cd)更改为您机器的桌面。然后，他们创建一个名为 typescript-demo 的新目录(mkdir ),然后将该目录(又是 cd)更改到其中，这样现在您的当前工作目录就是 typescript-demo。如果你想确定是这种情况，你可以输入

```
$pwd
```

您应该得到以下内容:

```
>/home/redhood/Desktop/typescript-demo
```

很明显，我的上面写着 redhood，你的上面写着你的用户名，但这应该是打印出来的唯一区别。

接下来，我们将使用 package.json 文件初始化我们的项目。我们可以很容易地通过运行:

```
$npm init -y
```

这将在我们的项目文件夹中创建一个 package.json 文件，并填写一些基本信息。如果你想知道这些信息是从哪里来的，请去掉-y 标志，然后自己检查这些问题。大多数情况下，我发现自己使用了-y 标志，并在以后删除或添加项目信息。

## 安装 TypeScript

我们现在可以安装 TypeScript 了。这是一个非常简单的命令

```
$npm install --save-dev typescript
```

`--save-dev`标志确保安装的包在我们当前的目录中(而不是在我们的机器上全局安装包)。它还将在 package.json 文件中创建一个名为 devDependencies 的新部分。

TypeScript 的最新版本是 4.3。

```
$npx tsc -v // => Version 4.3.5
```

## 初始化 tsconfig.json

tsconfig.json 文件包含 IDE 使用的所有编译器信息。我们将手动创建我们的，虽然有一个替代的方法，我稍后会告诉你。

```
$touch tsconfig.json
```

如果你在 Windows 上，使用`code .`打开你的目录，手动在目录中创建文件。在文件内部，我们将键入:

```
{
  "compilerOptions": {
    "target": "es3",
    "module": "commonjs",
    "typeRoots": ["./node_modules/@types"],
    "esModuleInterop": true,
    "forceConsistentCasingInFileNames": true
  }
}
```

保存文件。以下是每个设置含义的简要说明:

1.  目标—此选项指定编译器在生成 JavaScript 文件时将输出的 ECMAScript 版本。我们以后会改变这一点，但现在，我们使用 es3。
2.  模块—此选项指定我们在生成的代码中使用的模块系统。通过将其设置为 commonjs，我们确保了代码可以在 Node 中运行。
3.  typeRoots —此选项指定 TypeScript 应在其中搜索全局类型的目录。我们把它放在这里，这样我们就可以否定从父目录中意外继承的类型。
4.  esModuleInterop——这个选项确保了 CommonJS 和 es 模块之间的兼容性。
5.  forceconsistencasingfilenames——这个选项确保我们不会因为使用不正确的大小写意外导入模块而引入错误。

## 创建我们的应用

我们将创建一个非常简单的应用程序，它接受一些变量并返回一条消息。让我们开始吧。我们将创建一个名为 app.ts 的新文件

```
$touch app.ts
```

在 app.ts 内部，我们将编写以下代码:

```
const userName: *string* = "Jonathan";
const age: number = 32;
const message: *string* = `Hello my name is ${userName} and I am ${age} years old.`;
console.log(message);
```

现在重要的事情不一定是代码看起来如何，或者其中一些是硬编码的，而是简单地查看语法。接下来我们需要运行几个命令:

```
npx tsc app.ts
// after a few seconds this will produce an app.js file in your 
// project directory.
node app.ts // this will run the app showing you your message.
```

现在是关键时刻。我们使用了一些新的 JavaScript 语法，我们能够让代码编译成旧的 JavaScript。打开 app.js 文件，看看我们的代码现在是什么样子。它应该看起来像这样:

```
>Hello my name is Jonathan and I am 32 years old
```

这就是 ES3 的样子。现在打开 tsconfig.json 文件，将其从 es3 更改为 es6。保存文件并重新运行`npx tsc app.ts`命令。打开新的 app.js 文件并查看其内容。将您的编辑器中的内容与上面的代码片段进行比较，以查看不同之处。很漂亮，对吧？现在，您应该对 TypeScript 能做什么以及作为开发人员，它如何成为您的武器库中的一种强大的语言/工具有了基本的了解。

# 结论

感谢阅读。我希望您喜欢学习一点关于 TypeScript 的知识，虽然这篇文章和项目不是世界上最大的东西，但它至少让您对 TypeScript 的工作方式有了一些了解，以及您可以如何利用它的能力来创建通常为 Java 和 C#等语言保留的企业级应用程序。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)