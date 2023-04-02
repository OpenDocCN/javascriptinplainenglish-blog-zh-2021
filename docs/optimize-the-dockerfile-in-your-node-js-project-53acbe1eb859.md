# 优化 Node.js TypeScript 项目中的 docker 文件

> 原文：<https://javascript.plainenglish.io/optimize-the-dockerfile-in-your-node-js-project-53acbe1eb859?source=collection_archive---------8----------------------->

![](img/1f793acbf9a7a0231139ce8f46415d77.png)

好吧，从积极的方面开始，如果你尝试复制一些基本的 Dockerfile 示例来构建基于 Node.js 的微服务容器，那就没问题了。如果你需要一些小而便携的东西，你可以使用 node:lts-alpine docker 基本映像，并通过构建这种简单的 docker 文件来使用它:

```
FROM node:lts-alpine
ADD . /app
WORKDIR /appRUN yarn && yarn buildENV NODE_ENV=productionCMD ['node', './dist']
```

如果你有一个 Node.js TypeScript 项目，就像我这里的[https://github.com/tigranbs/node-typescript-starter-kit](https://github.com/tigranbs/node-typescript-starter-kit)这将工作得非常好，特别是如果`alpine`本身是一个非常小的基本映像，你必须获得的唯一存储是你的 node_modules，当然，如果你的依赖项中有 20 多个包，它可能会增长到几 GB。

在微服务领域，使用小型 Docker 映像来加快服务器端的部署和正常运行时间被认为是一种很好的做法。这也意味着，如果你有一个运行自动化测试的登台环境或 Github 动作，如果你有一个较小的映像和较少的构建时间，它将花费更少的时间。因此，优化 Docker 图像的想法可以归结为以下两点

*   保持图像尺寸尽可能小
*   确保保留唯一的 Docker 图像层，以便在稍有变化时不要总是重建整个图像层

对于第一点，我们已经很好地匹配了最少的 Docker 映像，这意味着我们可能可以从 Dockerfile 中删除一些不必要的文件，如`README.md, .git, etc...`，但总体来说，这不会使匹配有所不同。

这里的主要思想是保持你的 Docker 图像与相同的独特的图像层，以便只有改变层将被上传到注册表，只有改变层将从那里下载。这归结于我们的 Node.js TypeScript 项目有这样的东西

```
FROM node:lts-alpine

ADD package.json /app/package.json
ADD yarn.lock /app/yarn.lock

WORKDIR /app

# Installing packages
RUN yarn

ADD . /app

ENV NODE_ENV=production

# Building TypeScript files
RUN yarn build

CMD ['node', './dist']
```

与原始 Docker 文件的主要变化是必须将`yarn install`和`yarn build`分开，这确保了如果您更改了`yarn.lock`或`package.json`，我们将重建 Docker 图像层，负责拥有`node_modules`，否则它将保持不变，如果我们已经有了，我们不必上传或从注册表下载。

你可以承认，在 80%的情况下，当你进行常规开发过程时，你不会接触到`yarn.lock`或`package.json`文件，只是当你需要新的包或将某些包升级到新版本时，你的`node_modules`层才会在这种情况下构建，否则 Docker 图像层将保持不变，使其在注册表和你的服务器或本地环境之间移动的构建时间非常快，网络流量/存储更少。

这种技术通常被称为多阶段构建，在这种情况下，您可以根据图像名称分配特定的图像层，并通过构建多个图像来引用它。例如，如果您必须构建`staging, test and production` docker 映像，并且您有一些特定的基于代码的差异。对于像 Go、Java 或 Rust 这样的编译语言来说，这是很常见的，在这些语言中，您可能会使用不同的优化标志编译稍有不同的库或处于调试或生产模式，但对于 Node.js TypeScript 项目来说，这是相同的代码库，只是改变了环境变量。

```
FROM node:lts-alpine AS packages

ADD package.json /app/package.json
ADD yarn.lock /app/yarn.lock

WORKDIR /app

# Installing packages
RUN yarn

# Staging Image
FROM packages 

ADD . /app

ENV NODE_ENV=staging

# Building TypeScript files
RUN yarn build

CMD ['node', './dist']
```

这主要是关于同时构建多个映像，但不确定它对基于 Node.js 的项目是否有用。我以前在 Go 项目中看到过这种情况，根据环境使用不同的编译标志构建 Go 项目是有意义的，但这也是一个特定的用例。事情是，你只需要记住，关键是保持你的独特的图像层不变，当你不断建立你的 Docker 图像，这将节省你很多时间。

# 结论

这是一个非常简单的概念，即无论你何时构建你的映像，都要保持 Docker 映像不变，但是这会为你节省大量的时间和资源。

如果这是有帮助的，请考虑订阅我的时事通讯并关注/订阅！

来源—[https://tigran . tech/optimized-docker file-for-node-typescript-project/](https://tigran.tech/optimized-dockerfile-for-node-typescript-project/)