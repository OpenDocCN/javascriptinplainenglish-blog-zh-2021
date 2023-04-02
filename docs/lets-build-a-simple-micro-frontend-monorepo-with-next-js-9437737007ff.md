# 让我们用 Next.js 构建一个简单的微前端 Monorepo

> 原文：<https://javascript.plainenglish.io/lets-build-a-simple-micro-frontend-monorepo-with-next-js-9437737007ff?source=collection_archive---------0----------------------->

![](img/177efacf3b7ac93608c17f998245292b.png)

Photo by [Kelsey Weinkauf](https://unsplash.com/@kejeki?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

除非你一直生活在岩石下，否则你会非常清楚 JavaScript 生态系统有多饱和。您的技术堆栈有许多很好的选项，权衡每个选择的利弊似乎是一项相当艰巨的任务。

本文将使用人们喜欢的所有流行词汇，如“Next.js”、“Monorepo”、“TypeScript”和“Micro-Frontend”，谦逊地为现代前端演示一个这样的选项。

# **下一件大事**

我觉得这年头选择 [Next.js](https://nextjs.org/) 作为你的前端框架是不可能出错的。这并不是说没有一些优秀的替代品，比如 Gatsby 和 create-react-app，事实上，如果你打算使用这些框架中的一个，你仍然可以和我一起编写代码，只需用 Next.js 替换你选择的框架。

重要的是微前端架构。依我拙见，将应用程序的不同部分部署到生产环境中，而其他部分并不知道，并且不会给这些部分带来任何风险，这才是王道，并且可以提供更加友好的开发人员体验。

为了实现这一点，我们将创建一个带有 Yarn 工作空间的简单 Monorepo，并利用 [Vercel cloud](https://vercel.com/) 的强大功能，它对 mono repo 提供一流的支持，包括那些包含在单个 Git repo 中的 mono repo。关于 Yarn 工作空间的一个伟大的事情是共享的依赖项将被提升到根目录，而不是在每个子应用`node_modules`中复制那些包！你可以在这里阅读更多关于[纱线工作区的信息。](https://classic.yarnpkg.com/blog/2017/08/02/introducing-workspaces/)

# 让我们开始吧

好了，废话少说，让我们开始建设我们的新项目吧！首先，我们将创建一个新目录并移入其中:

`$ mkdir MyApp && cd MyApp`

现在，我们将确保我们已经安装了 Yarn(在本指南中，我们使用的是版本 1 或 Yarn Classic)。

`$ npm install -g yarn`

接下来，我们将使用默认值初始化项目。您可以现在为`private`属性键入`true`，或者稍后手动键入。

```
$ yarn init
yarn init v1.22.10
question name (MyApp):
question version (1.0.0):
question description: My App
question entry point (index.js):
question repository url:
question author:
question license (MIT):
question private: true
success Saved package.json
✨  Done in 11.84s.
```

然后我们将行`"workspaces": ["packages/*"]`添加到我们的`package.json`文件中。这就是告诉 Yarn 我们正在使用工作区所需要的全部内容，我们 Monorepo 的所有不同部分都可以在`packages`目录中找到。你可以选择叫它别的名字，但是`packages`很好听，因为它被 [Lerna](https://lerna.js.org/) 使用，而且我喜欢一致性。

# **建立我们的第一个工作空间**

我们的下一步是创建我们项目的第一个“工作空间”或微前端。对于这个例子，让我们假设我们将制作一个仪表板，它将作为我们的 web 应用程序的主页。让我们继续创建该目录，并在其中设置一个 Next.js 应用程序！

```
$ mkdir packages && cd packages
$ yarn create next-app --typescript
```

如果您愿意，如果您想使用 JavaScript，可以省略`--typescript`。当提示输入姓名时，键入`dashboard`或任何符合您目的的内容。

# **建立我们的第二个工作空间**

接下来，让我们创建另一个工作空间来存储我们共享的[钩子](https://reactjs.org/docs/hooks-custom.html)。像我们的仪表板一样，它会有`react`，但不像我们的仪表板，它没有`next`。这个更小的钩子应用程序实际上会更复杂一些，因为我们没有使用超级`create next-app`向导！

确保在创建`hooks`工作空间之前导航回`packages`目录(或者只是从您的 IDE 创建文件和目录)。

```
$ cd .. 
$ mkdir hooks && cd hooks
$ yarn initquestion name (hooks):
question version (1.0.0):
question description: Shared React Hooks
question entry point (index.js): dist/index.js
question repository url:
question author:
question license (MIT):
question private:
```

请注意，稍后我将入口点设置为`dist/index.js`。

我喜欢做的一件事是用一个共同的前缀将我的工作空间分组；在这种情况下，我们将使用`@myapp`，因此让我们继续修改我们两个工作空间的`package.json`，并将`name`值分别更改为`@myapp/dashboard`和`@myapp/hooks`。

最后，我们希望将`react`依赖项安装到 hooks 应用程序中。我将使用 TypeScript，所以我也将把`typescript` `tsc`和`@types/react`包安装到 devDependencies 中。

```
$ yarn workspace @myapp/hooks add react
$ yarn workspace @myapp/hooks add typescript tsc @types/react -D
$ yarn workspace @myapp/hooks tsc --init
```

你会看到一个`tsconfig.json`文件已经被创建。取消注释并设置以下行的值:

```
"declaration": true,"sourceMap": true,
"outDir": "./dist",
"rootDir": "./lib",
```

还记得我们把入口点设为`dist/index.js`的时候吗？这指示 TypeScript transpiler 从`lib`目录读取并将原始 JavaScript 输出到`dist`目录。Yarn 工作空间然后将结果`dist/index.js`文件暴露给其他工作空间。

接下来，编辑 hooks apps `package.json`文件以包含以下脚本:

```
"scripts": {
    "dev": "yarn run clean && yarn run watch",
    "build": "yarn run clean && yarn run compile",
    "clean": "rm -rf ./dist",
    "compile": "tsc",
    "watch": "tsc --watch"
}
```

接下来，在 hooks 应用程序中创建一个`.gitignore`，同时创建一个`lib`目录。用以下内容填充钩子应用程序`.gitignore`:

```
/node_modules
/dist
```

好了，我们都准备好了，让我们开始写代码吧！我们将编写一个简单的 React 钩子，它最终将被 Monorepo 中的其他应用程序使用。

```
// packages/hooks/lib/useDebounce.tsimport { useState, useEffect } from 'react';const useDebounce = <T>(value: T, delay: number): T => {
  const [debouncedValue, setDebouncedValue] = useState(value);useEffect(() => {
    const handler = setTimeout(() => {
      setDebouncedValue(value);
    }, delay);return () => {
      clearTimeout(handler);
    };
  }, [value, delay]);return debouncedValue;
};export default useDebounce;
```

```
// packages/hooks/lib/index.tsexport { default as useDebounce } from "./useDebounce";
```

最后，我们将把源 TypeScript 文件及其相关的源映射和类型文件传输到`dist`目录，同时观察源`lib`目录的变化:

`$ yarn workspace @myapp/hooks run dev`

# **将所有这些放在一起**

hooks 应用程序是一个简单的例子。您可以创建更多应用来满足您的需求；一个共享组件应用程序，一个集中的翻译区，或者你的用户界面的其他区域，比如导航栏，评论区等等，都是有效的选择。

在我们的例子中，我们将使用仪表板应用程序中的`useDebounce`挂钩。让我们在下面概述实现这一目标的步骤:

*   将`"@myapp/hooks": "1.0.0"`添加到仪表板应用`package.json`的依赖对象中
*   从项目根目录中，运行`yarn install`将它们链接在一起
*   使用`import { useDebounce } from "@myapp/hooks";`从仪表板导入挂钩，就像导入任何其他依赖关系一样

就是这样！我们有一个伟大项目的基础，我们可以通过我们认为合适的额外工作空间来扩大规模！

# **独立部署微前端**

这种方法的一个奇妙的好处是能够将单个应用程序分割成可以独立构建、维护和部署的独立部分。

这篇文章不会详细介绍部署过程，但是我推荐使用 Vercel，因为它有一流的 Monorepo 支持。您可以将项目推送到 GitHub、GitLab 或 BitBucket，并让 Vercel 平台导入每个工作区。默认情况下，Vercel 支持应用程序之间的代码共享，这对我们的需求至关重要。你可以在这里阅读更多关于整个过程的信息。

你可以在这里找到我的包含这段代码的 GitHub repo。

编码快乐！

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)