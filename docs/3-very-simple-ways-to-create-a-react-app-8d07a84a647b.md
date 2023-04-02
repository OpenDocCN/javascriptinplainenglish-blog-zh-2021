# 创建 React 应用程序的 3 种简单方法

> 原文：<https://javascript.plainenglish.io/3-very-simple-ways-to-create-a-react-app-8d07a84a647b?source=collection_archive---------20----------------------->

## 由于各种非常智能的构建工具，现在开始构建 React 应用程序比以往任何时候都简单，我们今天将讨论这些工具。

![](img/5b8687dd3a0bad337a1f3587fac3d9fd.png)

降低使用 React 的门槛非常重要，尤其是当您第一次尝试学习它的时候。我相信 React 的这三个构建工具将会做到这一点。

# 1:创建-反应-应用程序

也许搭建 React 应用程序最常用的方法就是这个工具。Create-React-App 是一个简单易用的命令行工具，用于构建 React 应用程序。唯一需要开始的是一个命令行，并安装 NodeJS/NPM。

运行以下命令将创建一个名为“demo”的全新 React 应用程序

```
npx create-react-app demo
```

这将开始创建一个 React 应用程序，完成后，您可以直接进入项目并开始编码。要运行它，只需在命令行中导航到项目目录并键入以下内容。

```
npm start
```

有关如何使用 Create-React-App 的更多信息，您可以查看下面的链接。他们有很好的文档，我强烈推荐你去看看。

[](https://create-react-app.dev/) [## 创建 React 应用

### 您不需要学习和配置许多构建工具。即时重新加载有助于您专注于开发。到时候了…

创建-反应-应用程序.开发](https://create-react-app.dev/) 

# 2: Vite

Vite 可以像 Create-React-App 一样使用，我发现这个工具对于搭建一个基本的 React 应用程序也非常有用。Vite 与 Create-React-App 的不同之处在于，你不仅可以将它用于 React 应用程序，还可以用于 Vue、Svelte 和各种其他类型的应用程序。它也非常容易开始使用。同样，您只需要一个命令行，并安装 NodeJS/NPM。

在命令行中运行以下命令将创建一个名为“demo”的新 React 应用程序

```
npm init vite@latest demo -- --template react
```

要运行我们刚刚创建的 Vite 应用程序，我们需要导航到项目目录并在命令行中运行这个命令。

```
npm run dev
```

再说一次，这就是我们需要做的所有事情，以获得一个功能完整的 React starter 应用程序。

有关如何使用 Vite 的更多详细信息，您可以查看下面的链接。

[](https://vitejs.dev/) [## 轻快地

### 通过本机 ESM 按需提供文件服务，无需捆绑！热模块更换(HMR ),无论如何都能保持快速…

vitejs.dev](https://vitejs.dev/) 

# 3:创建下一个应用程序(NextJS 框架)

这个工具与上面两个有一点不同，因为它将搭建一个名为 NextJS 的 React 框架。因此，你得到的不仅仅是一个普通的 React 应用程序，还有一些智能预设。使用这个命令，您将获得一个完整的服务器端渲染 React 框架，但是就像上面的命令一样，创建起来也很简单。

要创建一个名为“demo”的新的 NextJS 应用程序，您将在命令行中运行以下命令。

```
npx create-next-app demo
```

这将创建一个全新的 NextJS 应用程序，您可以通过导航到终端中的目录并运行该命令来启动它。

```
npm run dev
```

正如我所说的，这一个不像前两个那么轻量级，将有自己的风格来编写 React 代码以及其他特定于框架的编码模式。有关如何使用 NextJS 的更多信息，请查看下面的链接。

[](https://nextjs.org/) [## Vercel 的 next . js-React 框架

### 生产级反应可扩展的应用。世界领先的公司使用 Vercel 的 Next.js 来构建静态和…

nextjs.org](https://nextjs.org/) 

# 荣誉奖:CodeSandbox

这实际上不符合这个列表的范围，因为它是浏览器中的一个完整的代码编辑器，但 CodeSandbox 可能是启动和运行 React 应用程序的最简单的方法。你需要做的就是去他们的网站创建一个免费账户。这将允许您创建一个新的沙箱并选择 React 模板。你有一个全功能的 React 应用程序，你可以在浏览器中实时编辑，不需要任何设置。

要开始，请导航到下面的链接。

[](https://codesandbox.io/) [## CodeSandbox:用于快速 Web 开发的在线代码编辑器和 IDE

### 使用协作沙盒创建、共享和获取反馈，以实现快速 web 开发。没有设置超高速多人游戏…

codesandbox.io](https://codesandbox.io/) 

# 包扎

我发现这些工具可以帮助 React 开发人员最大化开发体验，并允许将重点放在代码而不是设置工作上。这并不是说设置步骤不重要，根据项目，拥有一个定制的构建环境有时是最好的选择，但是我发现自己经常使用这些工具，因为它们使使用 React 变得有趣、令人兴奋和容易。

一如既往，如果您有任何问题或建议，请随时留下评论。我肯定我留下了许多构建工具，并希望听到您最喜欢的！

*更多内容看*[***plain English . io***](http://plainenglish.io/)