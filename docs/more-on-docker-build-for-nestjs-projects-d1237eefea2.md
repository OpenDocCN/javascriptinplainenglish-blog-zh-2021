# 用于 NestJS 应用程序的 Docker 构建

> 原文：<https://javascript.plainenglish.io/more-on-docker-build-for-nestjs-projects-d1237eefea2?source=collection_archive---------10----------------------->

## 用 Docker 构建自己的 NestJS 项目的另一种方法

![](img/53b8a639927a5ba6401fcb33bb76f887.png)

Thanks to [Andrey](https://unsplash.com/photos/_PcWGCSoqRg)

## 什么是 NestJS？

NestJS 是一个为 NodeJS 开发者构建后端应用程序的不可思议的框架，它主要使用了普通的 ExpressJS，不仅如此。该框架非常统一且对企业友好。如果您有兴趣了解更多关于 NestJS 的内容，请阅读我写的关于如何用 NestJS 编写 [REST API 的文章](https://makinhs.medium.com/creating-a-rest-api-series-with-nestjs-part-01-scaffolding-and-basic-cli-usage-30ace19c5bb8)

## Docker build 有什么问题？

当使用容器运行应用程序时，尤其是使用 NodeJS 应用程序时，您通常希望构建速度更快，并且不会消耗太多内存。使用 NestJS 进行基本构建时，不需要太多的关注就可以轻松达到 1gb，这将消耗您的 CI/CD 管道中的时间以及大量的内存浪费。如果你想快速解决这个问题，你可以看看我以前写的关于 NestJS 的 [docker 图片的文章。](/create-reduced-docker-images-in-your-nestjs-application-b25ab32a840d)

当我说一个基本的 docker 文件时，我的意思是这样的:

```
FROM node:14.15.0-alpine3.10

USER 2000
RUN mkdir -p /home/node/app/node_modules && chown -R 2000:2000 /home/node/app

WORKDIR /home/node/app
COPY --chown=2000:2000 . /home/node/appRUN yarn installRUN yarn build

EXPOSE 3000

ENTRYPOINT ["node"]
CMD ["/home/node/app/dist/main.js"]
```

这将创建大约 900mb 的图像。

对于简单的解决方案，基于我以前的文章，您可以开始使用 multi build 来构建您的项目，最新的方法如下:

```
FROM node:16-alpine3.11 AS *BUILD_IMAGE* RUN apk update && apk add yarn curl bash make && rm -rf /var/cache/apk/*

RUN curl -sfL https://install.goreleaser.com/github.com/tj/node-prune.sh | bash -s -- -b /usr/local/bin

WORKDIR /usr/src/app

# install dependencies
RUN yarn --frozen-lockfile

COPY . .

RUN yarn install
RUN yarn build

RUN npm prune --production

RUN /usr/local/bin/node-prune

FROM node:16-alpine3.11

USER 1000
RUN mkdir -p /home/node/app/
RUN mkdir -p /home/node/app/node_modules
RUN mkdir -p /home/node/app/dist

RUN chown -R 1000:1000 /home/node/app
RUN chown -R 1000:1000 /home/node/app/node_modules
RUN chown -R 1000:1000 /home/node/app/dist

WORKDIR /home/node/app

COPY --from=*BUILD_IMAGE* /usr/src/app/dist /home/node/app/dist
COPY --from=*BUILD_IMAGE* /usr/src/app/node_modules /home/node/app/node_modules

EXPOSE 3000
ENTRYPOINT ["node"]
CMD ["/home/node/app/dist/main.js"]
```

看起来很棒，最终的图像大约有 156mb。但是我们能提高建造的速度吗？

经过一些研究，我想在建筑过程中有三个图像，但以不同的方式运行:

*   一个干净的图像，带有我比较喜欢的节点图像(我个人比较喜欢[官方节点——高山](https://hub.docker.com/_/node))。从我们的首选基础映像，我们然后安装所有需要的库来运行我们的项目，包括在我们的情况下节点修剪。
*   第二个映像安装了我们所需的 node_modules，我们可以将其用作“映像依赖项”
*   最后一个映像将构建项目并准备运行它。

## 干净的形象

为了创建一个干净的映像，我将添加一个公共的 [docker 存储库](https://hub.docker.com/repository/docker/makinhs/nestjs-base)。它将包含:

```
FROM node:16-alpine3.11 AS *base_image* RUN apk update && apk add yarn curl bash make && rm -rf /var/cache/apk/*

RUN curl -sfL https://install.goreleaser.com/github.com/tj/node-prune.sh | bash -s -- -b /usr/local/bin
```

然后，为了构建，我将已经指向我的名为[***makin hs/nestjs-base***](https://hub.docker.com/repository/docker/makinhs/nestjs-base)的公共存储库

```
docker build -t makinhs/nestjs-base .
```

很好，这张图片将有助于避免在构建 NestJS 项目时出现 python 警告问题，以及在项目运行后安装 node-prune 以供执行。推送到我的存储库很简单，因为:

```
docker push makinhs/nestjs-base:latest
```

> 请记住，你不会被允许推到我的仓库，但你可以使用这个作为你的基础图像，因为它是公开的；)源文件可以在这里找到[。](https://github.com/makinhs/docker-nestjs-base/blob/main/Dockerfile)

酷，接下来呢？从属关系！

## 设置依赖关系图像

根据具体情况，可以避免这一步，但是对于我来说，作为概念验证，我希望有一个包含所有必需的 node_modules 的映像。对于依赖项，我将使用这个 [git 库](https://github.com/makinhs/docker-nestjs-dependencies)。我想要构建的项目也属于这个[仓库](https://github.com/makinhs/nestjs-api-tutorial/tree/003-docker)。暂时，我将从我的 NestJS 项目中复制 package.json，并将其用作我的依赖关系映像存储库的基础。最终，我们的 package.json 会有这样的内容

```
{
  "name": "docker-nestjs-dependencies",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "repository": {
    "type": "git",
    "url": "git+https://github.com/makinhs/docker-nestjs-dependencies.git"
  },
  "author": "",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/makinhs/docker-nestjs-dependencies/issues"
  },
  "homepage": "https://github.com/makinhs/docker-nestjs-dependencies#readme",
  "scripts": {
    "prebuild": "rimraf dist",
    "build": "nest build",
    "format": "prettier --write \"src/**/*.ts\" \"test/**/*.ts\"",
    "start": "nest start",
    "start:dev": "nest start --watch",
    "start:debug": "nest start --debug --watch",
    "start:prod": "node dist/main",
    "lint": "eslint \"{src,apps,libs,test}/**/*.ts\" --fix",
    "test": "jest",
    "test:watch": "jest --watch",
    "test:cov": "jest --coverage",
    "test:debug": "node --inspect-brk -r tsconfig-paths/register -r ts-node/register node_modules/.bin/jest --runInBand",
    "test:e2e": "jest --config ./test/jest-e2e.json"
  },
  "dependencies": {
    "@nestjs/common": "^7.5.1",
    "@nestjs/config": "^0.6.1",
    "@nestjs/core": "^7.5.1",
    "@nestjs/mapped-types": "^0.2.0",
    "@nestjs/platform-express": "^7.5.1",
    "@nestjs/typeorm": "^7.1.5",
    "bcrypt": "^5.0.0",
    "class-transformer": "^0.3.2",
    "class-validator": "^0.13.1",
    "pg": "^8.5.1",
    "reflect-metadata": "^0.1.13",
    "rimraf": "^3.0.2",
    "rxjs": "^6.6.3",
    "typeorm": "^0.2.30"
  },
  "devDependencies": {
    "@nestjs/cli": "^7.5.1",
    "@nestjs/schematics": "^7.1.3",
    "@nestjs/testing": "^7.5.1",
    "@types/express": "^4.17.8",
    "@types/jest": "^26.0.15",
    "@types/node": "^14.14.6",
    "@types/supertest": "^2.0.10",
    "@typescript-eslint/eslint-plugin": "^4.6.1",
    "@typescript-eslint/parser": "^4.6.1",
    "eslint": "^7.12.1",
    "eslint-config-prettier": "7.1.0",
    "eslint-plugin-prettier": "^3.1.4",
    "jest": "^26.6.3",
    "prettier": "^2.1.2",
    "supertest": "^6.0.0",
    "ts-jest": "^26.4.3",
    "ts-loader": "^8.0.8",
    "ts-node": "^9.0.0",
    "tsconfig-paths": "^3.9.0",
    "typescript": "^4.0.5"
  },
  "jest": {
    "moduleFileExtensions": [
      "js",
      "json",
      "ts"
    ],
    "rootDir": "src",
    "testRegex": ".*\\.spec\\.ts$",
    "transform": {
      "^.+\\.(t|j)s$": "ts-jest"
    },
    "collectCoverageFrom": [
      "**/*.(t|j)s"
    ],
    "coverageDirectory": "../coverage",
    "testEnvironment": "node"
  }
}
```

请记住，这是我从我的 NestJS 项目中获得的，可以在这里找到。

现在让我们使用以下内容创建 docker 文件:

```
FROM makinhs/nestjs-base:latest AS *dependencies* WORKDIR /usr/src/app

# install dependencies
RUN yarn --frozen-lockfile

COPY . .

RUN yarn install
```

为了发送 public，我将存储在这个 [public repository](https://hub.docker.com/repository/docker/makinhs/nestjs-dependencies) 中，名称设置为 makinhs/nestjs-dependencies。

> 别忘了加上**。使用 node_modules 来防止构建问题。**

```
docker build -t makinhs/nestjs-dependencies .
```

这是 NodeJS 应用程序的缺陷…这个带有 node_modules 的映像包含大约 1gb。如果您的项目不经常添加新的依赖项，为什么不在某个地方设置这个庞然大物呢？这就是为什么在这篇文章中，我试图达到中间依赖图像，以加快建设过程。推到码头的将是:

```
docker push makinhs/nestjs-dependencies
```

> 我现在不关心 docker 标签，但是在你的项目中，你真的需要在这个意义上更有条理。

## 统一各个部分并构建我们的项目

现在，在我们的 NestJS 项目中，我们将对 docker 文件进行更新，以尝试和测试构建:

```
FROM makinhs/nestjs-dependencies:latest AS *BUILD_IMAGE* WORKDIR /usr/src/app

COPY . .

RUN yarn build

RUN npm prune --production

RUN /usr/local/bin/node-prune

FROM makinhs/nestjs-base:latest

USER 1000
RUN mkdir -p /home/node/app/
RUN mkdir -p /home/node/app/node_modules
RUN mkdir -p /home/node/app/dist

RUN chown -R 1000:1000 /home/node/app
RUN chown -R 1000:1000 /home/node/app/node_modules
RUN chown -R 1000:1000 /home/node/app/dist

WORKDIR /home/node/app

COPY --from=*BUILD_IMAGE* /usr/src/app/dist /home/node/app/dist
COPY --from=*BUILD_IMAGE* /usr/src/app/node_modules /home/node/app/node_modules

EXPOSE 3000
ENTRYPOINT ["node"]
CMD ["/home/node/app/dist/main.js"]
```

请注意，我们使用依赖关系映像来构建映像，然后运行 node-prune，并在运行回我们的基本映像后，只获取所需的文件，以最终维持一个简短的构建(请记住，依赖关系得到了大约 1gb，我们希望避免这种情况)。

```
docker build -t nestjs-api .
```

您的最终图像大小约为 200mb o/

在本文中，我试图提供一个构建 NestJS 项目的不同方法的概念证明。如果您的项目非常小，并且您可以避免将依赖项用作外部映像，那么这可能会过于复杂。在下一篇文章中，我将提供与一些 CI 的集成，并使用这个版本的方法与我以前的统一方法进行性能构建测试。

这篇文章更多的是一个概念的证明，而不是指导你建立形象的最佳方法。我对采用这种方法很好奇，但仍然有实际的 CI/CD 性能测试，并且有一个额外的层来处理 package.json 依赖关系，这需要在管道中实现一些自动化来避免问题。

*   带有更新 Dockerfile 的 NestJS 分支可以在[这里](https://github.com/makinhs/nestjs-api-tutorial/tree/003-docker-2)找到
*   依赖项 Dockerfile 可以在[这里](https://github.com/makinhs/docker-nestjs-dependencies)找到
*   基本图像 Dockerfile 可以在[这里](https://github.com/makinhs/docker-nestjs-base)找到

[](/create-reduced-docker-images-in-your-nestjs-application-b25ab32a840d) [## 使用 NestJS 创建 REST API 第 4 部分——快速添加一个缩减了图像大小的 Dockerfile 文件

### 从+900MB 到 200MB 不到五分钟的阅读量！如果你和 NestJS 一起工作，这篇文章是必须的…

javascript.plainenglish.io](/create-reduced-docker-images-in-your-nestjs-application-b25ab32a840d) 

*更多内容请看*[***plain English . io***](http://plainenglish.io)