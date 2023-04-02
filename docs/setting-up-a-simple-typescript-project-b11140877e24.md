# 设置简单的 TypeScript 项目

> 原文：<https://javascript.plainenglish.io/setting-up-a-simple-typescript-project-b11140877e24?source=collection_archive---------2----------------------->

![](img/eaf67ea04aa5f3d0a84ac7971503206a.png)

Photo by [Arnold Francisca](https://unsplash.com/@clark_fransa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

*这篇文章记录了我创建一个完整网站的旅程的一小部分，这个网站可以在三个并行框架和三个并行设计系统中呈现(*[*React*](https://reactjs.org/)*+*[*Material UI*](https://material-ui.com/)*)；*[](https://angular.io/)**+*[*清晰度*](https://clarity.design/)*；* [【香草】JS](https://www.javascript.com/) *+* [碳](https://www.carbondesignsystem.com/) *)。**

*[←上一篇:你好，世界！](https://simon-lutterbie.medium.com/hello-world-starting-a-web-app-from-a-blank-canvas-9b73fa2cb7e6)*

*[→下一篇文章:将静态 HTML 站点重构为类型脚本，第 1 部分，共 2 部分](https://simon-lutterbie.medium.com/refactoring-a-static-html-site-into-typescript-part-1-of-2-the-content-b4c975ecab00)*

*在我的[上一篇(也是第一篇！)文章](https://simon-lutterbie.medium.com/hello-world-starting-a-web-app-from-a-blank-canvas-9b73fa2cb7e6)，我创建了一个*非常*基本的 HTML+JS 页面:一个单独的`index.html`文件作为模板，一个单独的`index.js`呈现“Hello，World！”在所述模板中。我还创建了一个`git repository`，进行了第一次提交，并将其推送到 [Github](https://github.com/sjlutterbie/parallel-frameworks-website) 。*

***但是比起普通的 JavaScript，我更喜欢**[**TypeScript**](https://www.typescriptlang.org/)**。起初，从 JavaScript 过渡到 TypeScript 可能看起来是不必要的开销。但相信我，这是值得的。***

*采用打字稿*

*   ***帮助减少代码中的错误和难以发现的 bug。**每个函数或类方法都可以提供一个关于它所期望的参数和它所返回的值类型的清晰契约。*
*   *促进代码的整洁和可读性。现在我们用 TypeScript 编写了，我的团队以最小化我们添加到代码中的注释数量为荣，因为清晰的类型允许代码自己说话。*
*   ***实现新水平的测试。**大多数开发人员都熟悉*单元*、*集成*、*、*和*端到端*测试。类型化代码自动包含静态测试——运行类型检查可以在代码运行之前检测出某些代码错误。有了好的 IDE，这些错误将在开发中期被检测出来。是实时 TDD。*

*深信不疑？很好。让我们开始吧。*

*在实现 TypeScript 之前，我需要将我的项目设置为一个 [npm 包](https://www.npmjs.com/)，这样我就可以加载必要的 TypeScript 模块。只需要一个简单的命令:`npm init`，和几个回答的问题。结果是项目目录中的一个`package.json`文件，它包含了关于项目的各种细节。这个文件将随着项目的复杂程度而增长，但是现在它足够简单，可以作为一个片段包含进来:*

```
*{
  "name": "sjlutterbie-website-ui",
  "version": "1.0.0",
  "description": "Starting from a blank canvas, building a site that 
                  can be rendered in multiple frameworks.",
  "main": "src/index.js",
  "scripts": {},
  "repository": {
    "type": "git",
    "url": "git+https://github.com/sjlutterbie/parallel-frameworks-website.git"
  },
  "author": "Dr. Simon Lutterbie",
  "license": "ISC"
}*
```

*目前，它只不过是该项目的一个元描述。`main: src/index.js`是我的源代码的入口点。`scripts: {}`列举了我能跑的各种`npm commands`；它开始是空的(好吧，有一个占位符`test`命令，我已经删除了)，但不会持续很久。*

*将我的项目设置为一个`npm package`的主要好处是我现在可以安装依赖项…比如 TypeScript！*

```
*npm i -D typescript tsc*
```

*上面的命令安装主`typescript`包以及`tsc`，TypeScript 的“命令行解释器”。`-D`命令告诉 npm 将它们安装为`devDependencies`——开发所必需的包，但不会包含在最终版本中。TypeScript 已加载！*

*在我进入编码之前，还有一个重要的步骤。安装依赖项会在我的项目中创建一个`node_modules`文件夹，其中存储了所有的依赖项代码。这个目录会变得非常大和复杂，在您的`git history`中跟踪它实际上是有害的。因此，是时候设置一个`.gitignore`文件了。*

*默认情况下，像`git add .`这样的命令会跟踪项目中的每个文件，包括`node_modules`。但是创建一个`.gitignore`文件，您可以指示`git`忽略特定的文件、文件类型，甚至整个目录。*

*我现在唯一真正需要忽略的是。然而，忽略其他文件几乎总是有意义的，并且在早期忽略它们会让它们随着项目的增长而溜走。我最初的`.gitignore`是基于[为节点项目](https://github.com/github/gitignore/blob/master/Node.gitignore)推荐的模板。我对它进行了删减，排除了我不想实现的文件，并添加了一些我自己的定制:*

```
*.gitignore
==========*# Cache files* .eslintcache
.npm
*.tsbuildinfo*# Directories* dist/           # This is the build process will output code.
node_modules/   # The original reason we're here!*# Env files      # A good safeguard against accidentally publishing* .env.           #  private information, including security keys
.env.test*# Logs* *.log
logs
npm-debug.log**# Misc files* .DS_Store       # Macs often create this file
notes.md        # Personal project notes, not my reference.*
```

*最后，让我们实现一些类型脚本！*

*一旦安装并配置了 TypeScript，我就采取三个步骤将我的 JavaScript 项目转换成 TypeScript 项目。*

***首先我配置了 TypeScript** 。这是通过在您的项目中创建一个`tsconfig.json`文件来实现的，您可以在其中添加您想要的配置选项。像`package.json`一样，这个文件可能会随着我的项目的复杂性而增长。但是现在，它相对简单:*

```
*tsconfig.json
============={
  "compilerOptions": {
    "allowJs": true,            
    "checkJs": true,
    "outDir": "dist",
    "sourceMap": true,
    "target": "ES6",
    "noImplicitAny": true,
    "noImplicitReturns": true,
    "strict": true
  }
}*
```

*关于 TypeScript 的一个简短说明:浏览器(目前)不支持 TypeScript，它们只支持 JavaScript。TypeScript 所做的是检查您的`.ts`代码的类型错误，然后将其转换成 JavaScript。例如，`index.ts`将被转换为`index.js`——代码将包括 TypeScript 提供的所有保护，但以浏览器可以理解的方式编写。*

*上述选项可分为三个部分:*

*   *`allowJS`和`checkJs`告诉 TypeScript 如何处理它遇到的本地 JavaScript 代码。*
*   *`outDir`告诉 TypeScript 将转换后的文件放在哪里，`sourceMap`指示它将转换后的代码链接回原始代码(对调试有用)，而`target`告诉它转换成浏览器友好但仍然现代的 JavaScript 版本。*
*   *`noImplicitAny`、`noImplicitReturns`和`strict`对代码施加了一系列额外的测试，IMHO(和 TypeScript)提倡最佳实践。*

*第二，我将我的包配置为使用 TypeScript 构建。为此，我对我的`package.json`文件做了两处修改。我将`main: src/index.js`改成了`main: src/index.ts`,以代表我们即将实现的新文件类型。我还加了三个`npm scripts`:*

```
*package.json:
=============scripts: {
  "build": "tsc && npm run build:cp-public",
  "build:cp-public": "cp ./public/** ./dist",
  "type": "tsc --noEmit"
}*
```

*让我们从下往上开始:*

*   *`**type**` : `tsc`是 TypeScript“命令行解释器”。如前所述，`tsc`通常会检查类型错误，然后将`.ts`文件转换为`.js`文件，并将其写入您选择的目录。如果我只想检查错误而不构建，我添加`--noEmit`来防止转换&输出。由`npm run type`触发的`type`脚本是一个帮助调试的助手命令，而不是每次都要修改代码。*
*   *`**build:cp-public**`:如`tsconfig.json`所述，TypeScript 将把转换后的文件放在`dist`文件夹中。所以，我希望所有的文件，将使建成的网站进入该文件夹。现在，唯一的其他文件是`public/index.html`——但是后来添加到`public`的其他文件也应该包括在内。该命令将所有文件从`public`复制到`dist`。你会注意到我在命令前加了前缀`build:`——这告诉我这个命令并不打算独立运行(尽管它可以独立运行)；这是一个帮助命令，使核心命令`build`更具可读性。*
*   *两个命令的组合，以及魔法发生的地方。`tsc`对代码进行类型检查，这次它会将转换后的代码输出到`dist`目录。然后将`public`文件复制过来，构建就完成了！*

**注意:* `build` *命令当前* ***会覆盖* `dist` *文件夹中的*** *文件。如果您更改文件名，这可能会导致旧文件留在* `dist` *中。最佳实践是在每次构建开始时清空* `dist` *文件夹；然而，我计划在不久的将来以不同的方式实现它，所以我现在跳过它。**

***终于到了写 TypeScript 代码的时候了！**我把`index.js`改成`index.ts`，看看我需要做哪些编辑。这是我的原始函数:*

```
**function* helloWorld() {
  document.getElementById("hello-world").textContent =
    "Hello, World!";
}helloWorld();*
```

*我在我的 IDE 中使用了 [VSCode](https://code.visualstudio.com/) ，它可以即时识别打字错误。马上，警告我说`document.getElementById("hello-world")`有问题，因为`Object is possibly 'null'.`的静态测试在起作用！如果我在一个不包含带有`id="hello-world"`的元素的 HTML 文档中运行这个函数，或者如果 id 拼错了(`hell-world`，有人知道吗？)那么程序就会崩溃，因为没有元素可以修改它的`textContent`。在 JavaScript 中，您将不得不艰难地解决这个问题。*

*所以我修改了我的函数。首先，我将尝试找到该元素，只有当它存在时，我才会更新它的内容:*

```
*function helloWorld() {
  const element= document.getElementById("hello-world");

  if (element) {
    element.textContent = "Hello, World!";
  }
}helloWorld();*
```

*警告信息消失。我运行`npm run type`，确认没有错误。打字稿是快乐的，我是快乐的，并且*错误被阻止*意味着未来*到我的网站*的访问者会更快乐。*

*还需要做最后一个改变。*

*之前`public/index.html`拉进了`src/index.js`，所以它通过路径`../src/index.js`找到了它。然而，有了新的构建，它们都将在`dist`文件夹中。所以，我做了如下编辑:*

```
*<html>
  <body>
    <p *id*="hello-world"></p>
      <script *src*="./index.js"></script>  # Simpler import!
  </body>
</html>*
```

*注意`index.html`指的是转换后的 JavaScript 文件，而不是原始的 TypeScript 文件。相信我，这是个容易犯的错误！🤦‍♂*

*该收拾东西了。首先，我运行`npm run build`来确保所有新的部分都在工作；我在浏览器中打开`dist/index.html`，一切正常！我检查我更改的文件，运行`git add .`来跟踪它们(但不是`.gitignore`中的那些)，运行`git commit`来保存我的工作，运行`git push`来将它存储在 GitHub 上。*

*任务完成。该睡觉了。*

*[本次提交的变化](https://github.com/sjlutterbie/parallel-frameworks-website/commit/1a590cefb26b7491f8db3bee41ae45e9a7bced16) | [浏览截至本次提交的回购](https://github.com/sjlutterbie/parallel-frameworks-website/tree/1a590cefb26b7491f8db3bee41ae45e9a7bced16) | [我今天的回购](https://github.com/sjlutterbie/parallel-frameworks-website)*

*[←上一篇:你好，世界！](https://simon-lutterbie.medium.com/hello-world-starting-a-web-app-from-a-blank-canvas-9b73fa2cb7e6)*

*[→下一篇文章:将静态 HTML 站点重构为 TypeScript，第 1 部分，共 2 部分](https://simon-lutterbie.medium.com/refactoring-a-static-html-site-into-typescript-part-1-of-2-the-content-b4c975ecab00)*