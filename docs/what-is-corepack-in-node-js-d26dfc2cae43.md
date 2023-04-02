# Node.js 中的 Corepack 是什么？

> 原文：<https://javascript.plainenglish.io/what-is-corepack-in-node-js-d26dfc2cae43?source=collection_archive---------2----------------------->

## Corepack 允许节点开发人员使用新的打包选项！

![](img/5b89f0ace4cb3b0576aa884b86264372.png)

Image courtesy of Pawel Czerwinski on Unsplash

随着 Node.js 16.9.0 的发布，出现了一个名为 [Corepack](https://github.com/nodejs/corepack) 的新工具。`Corepack`被描述为一个零运行时依赖性的节点脚本，在节点项目和包管理器(如 [Yarn](https://yarnpkg.com/) 和 [Pnpm](https://pnpm.io/) )之间充当桥梁。Node.js 附带了一个名为`NPM`的包管理器，每次在计算机或服务器上安装 Node.js 时，它都会随 Node.js 一起安装。

所以本质上 Corepack 允许我们使用第三方包管理器，而不必在我们的开发计算机或构建服务器上全局安装它们。

虽然 NPM 很可能是最大的软件包管理器，但许多组织在根据自己的需求选择软件包管理器时，必须考虑一些因素。许多组织不能使用 NPM，因为当 Node.js 开发人员对他们的应用程序有依赖时，他们被复制到一个名为`node_modules`的子目录中。大多数 CI/CD 服务器和流程不允许构建服务器从其网络外部访问或下载模块。这是发明纱线的原因之一。Yarn 和 PNPM 既可以在开发者的计算机上存档和缓存模块，也可以在应用程序的源代码中存储模块包。

# Corepack 简介

Corepack 是 Node.js 附带的一个脚本，可以通过命令行访问。它有专门用于启用、禁用、准备和合并软件包管理器的命令。因为它仍然被认为是一个实验性的特性，所以默认情况下是禁用的。要启用 Corepack，只需在终端中键入以下命令；

```
> corepack enable
```

您还可以通过在`enable`后包含其名称来启用特定的包管理器 shim。在下面的例子中，我们将只启用`yarn`的垫片。

```
> corepack enable yarn
```

如果您想禁用 corepack，您可以简单地使用以下命令将其关闭；

```
> corepack disable
```

# 激活软件包管理器

在本例中，我将激活`yarn`包管理器。使用 Corepack，您可以激活一个软件包管理器、所有软件包管理器或特定版本的软件包管理器。我们将安装一个特定版本的`yarn`包管理器；

```
> corepack prepare yarn@1.22.11 --activate
```

这将安装 yarn 版本 1.22.11 并为我们的项目激活。一旦我们激活了我们的软件包管理器，我们就可以使用 Corepack 运行现有的软件包管理器命令。如果我们想使用特定的包管理器添加一个模块，我们只需将这些命令添加到`corepack`命令中；

```
> corepack yarn add axios
```

如果我们在全球范围内安装了 yarn，那么运行`yarn add axios`也是一样的。如果我们看一下`package.json`文件，它将对`axios`有一个依赖关系。我们在 package.json 文件中还有一个`packageManager`设置，它列出了我们希望在项目中使用的包管理器。

```
{
  "name": "sampleproject",
  "version": "1.0.0",
  "main": "index.js",
  "type": "module",
  "license": "MIT",
  "scripts": {
    "start": "node index.js"
  },
  "packageManager": "yarn@1.22.11",
  "dependencies": {
    "axios": "^0.21.4"
  }
}
```

# 归档和分发我们的包管理器

Corepack 还允许我们将我们的包管理器归档到我们的项目中。当我们的项目被部署到我们的构建环境中时，这些档案可以被水化。

为了归档我们的包管理器，我们可以在使用`prepare`命令时添加一个`-o`输出标志。

```
> corepack prepare yarn@1.22.11 --activate -o
```

这将添加一个`corepack.tgz`文件到包含我们的包管理器的项目中。如果我们将项目的源代码复制到另一台机器上，我们可以使用 hydrate 命令对包管理器进行解归档，如下所示；

```
> corepack hydrate --activate corepack.tgz
```

# 结论

Corepack 是 Node.js 社区如何让 Node 逐渐成为更好的工具的另一个例子。通过为不同的包管理器提供支持，这是工具使我们的生活变得更容易的另一种方式。

现在 Corepack 只是预览版，但是通过安装和使用 Node.js 的最新版本，您可以在它成为默认版本的一部分之前开始感受这个新工具。

*原发布于*[*https://fek . io*](https://fek.io/blog/what-is-corepack-in-node-js/)*。*