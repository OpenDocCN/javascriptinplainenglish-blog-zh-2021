# 如何用 Node.js 在 TypeScript 中创建全局变量

> 原文：<https://javascript.plainenglish.io/how-to-create-global-variables-in-typescript-with-node-js-9ca24f648991?source=collection_archive---------2----------------------->

![](img/893246106f44ac09ff4f4cece6c44876.png)

此时，你可能知道 Node.js 版本 16 已经移除了`NodeJS.Global`而支持`globalThis`，正因为如此，现在创建全局变量可能有点棘手(查看这个[链接](https://github.com/DefinitelyTyped/DefinitelyTyped/pull/53669)了解更多信息)。

## 我们是如何在 Node.js 14 ≤中创建全局变量的？

嗯，这很简单，我们只需要从`NodeJS.Global`出发`extend`。

然后我们必须声明一个全局变量，就像魔术一样，我们的全局变量在任何地方都是可用的。

## 我们如何在 Node.js 16 ≥中创建全局变量？

现在，我们只需要在全局命名空间中声明类型、接口或变量，为了实现这一点，我们必须创建一个`.d.ts`文件，请看这个例子:

这里我们声明了一个全局变量、接口和类型，这样，它们在我们的项目中随处可见。而且是的，很遗憾，我们必须使用`var`，否则，它将无法工作。到目前为止，一切都很好，现在如果我们想让 TypeScript 识别我们的全局变量、接口和类型，我们必须创建一个`@types`文件夹，并将我们的`.d.ts`文件放在那里。

但是，这种方法主要用于声明全局变量，如果只需要声明全局接口或类型，甚至还有更简单的方法。让我们假设你想定义一个自定义 DTO 作为一个接口，因为 DTO 可以用在很多地方，你可能会发现将其声明为一个全局接口或类型很有用。你怎么能这样？嗯，你只需要在你的`@types`文件夹中创建一个`d.ts`文件，让我们想象你的 d to 代表一个用户如下:

所以你只需要在你的`@types`文件夹中创建一个文件，比如说`user.d.ts`，就可以了。现在，您的 DTO 是全球可用的，但是您甚至可以通过创建一个`dto`文件夹并将您所有的 dto 放在那里来改进这种方法，然后，如果您需要它，您可以为您的类型或接口创建一个新文件夹。

## 注意

如果不需要从外部包导入类型，这种更简单的方法非常有用。如果您想从外部包中导入一个类型，您可能会遇到一些问题。例如:

因为我正在导入一个特定类型的`mqtt`包，我的全局类型`Route`将不会被检测到。这个问题有两个解决方案。第一个是把`Route`接口放在`global`里面，如下所示:

不使用全局变量也可以使用另一种方法:

## 初始化变量呢？

正如我上面几行所说，你可以声明全局变量，不幸的是你不能初始化它们，为什么？因为那些是类型定义文件，`.d.ts`文件。这意味着，你只能在那里定义事物。

然而，我发现了一个你可能会觉得有用的方法，假设你想在某个文件中使用`globalString`。首先，你必须初始化你的全局变量，我建议你在你的应用程序的入口点做(只是为了有条理)，它看起来会像这样:

```
// entryPoint.ts
global.globalString = 'Hi mom, I am global'
```

然后，您可以使用`globalString`(不带全局)来访问您的全局变量，例如:

```
// some/other/ts/file.ts
console.log({ globalString })
```

## 自定义类型文件夹

如果我们想要一个自定义位置，我们必须将它添加到我们的`tsconfig.json`中的`typeRoots`数组中。类似于:

```
{
  ...
  "compilerOptions": {
    ...
    "typeRoots": ["path/to/our/global/variables.d.ts"],
    ...
  }
}
```

如果您使用`ts-node`来运行您的项目，您必须在您的`tsconfig.json`文件中添加文件选项，或者遵循本[指南](https://github.com/TypeStrong/ts-node#missing-types)。就个人而言，我更喜欢第一种选择，因为它更简单:

```
{
  ...
  "ts-node": {
    "files": true
  },
  ...
}
```

就是这样，你的全局变量、接口、类型随处可用！

## 警告！

在这一点上，你被赋予了巨大的权力。还有…

> 权力越大，责任越大。
> ——本大叔。

**你必须尽可能避免使用全局变量**，因为它会把你逼到[意大利面条代码](https://en.wikipedia.org/wiki/Spaghetti_code)。记住，它们是**变量**，它们可以**改变**，所以要非常小心。如果不需要用，就不要用。你可能会发现这个问题很有用。

最后，有空的话，看看我的 npm CLI 工具， [simba.js](https://www.npmjs.com/package/@anthonylzq/simba.js) 。它有点像 [cra](https://create-react-app.dev/) ，但用于后端开发。它使用 MongoDB、Express 和 TypeScript。只需一个简单的命令，您就可以让服务器运行一些您可能会觉得有用的端点。

编码快乐！

*更多内容看* [***说白了就是***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费每周简讯点击这里***](http://newsletter.plainenglish.io/) ***。***