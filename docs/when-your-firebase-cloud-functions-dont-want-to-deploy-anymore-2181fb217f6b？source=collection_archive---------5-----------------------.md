# 当您的 Firebase 云功能不想再部署时

> 原文：<https://javascript.plainenglish.io/when-your-firebase-cloud-functions-dont-want-to-deploy-anymore-2181fb217f6b?source=collection_archive---------5----------------------->

## 不要再看了

*TL；DR —我通过将本地和云功能节点. js 版本设置为 12 来解决这个问题。*

![](img/762084da82ce648dc7b1b8b8440a70a4.png)

# 故事

我一直使用 [firebase-tools](https://www.npmjs.com/package/firebase-tools) 来手动部署我的云功能，如下所示:

```
firebase deploy --only functions
```

在我的[项目/公司](https://lazytexts.com)开展的过去八个月里，我从未遇到过部署云功能的问题，直到今天。

这一次，我得到了一个错误:

```
Deployment error. Build failed: Build error details not available.
```

![](img/c476760ecc4f60ee59c052b051400e7e.png)

为什么没有生成错误的详细信息？我永远不会知道。这个错误几乎和它们发生时一样无用。我知道我必须做什么。将这条消息粘贴到谷歌后，我偶然发现了以下 GitHub 问题:

[https://github.com/firebase/firebase-tools/issues/853](https://github.com/firebase/firebase-tools/issues/853)

在阅读了论坛上的每一条信息后，我满怀期待地等待着找到解决方案，但什么也没找到。

![](img/830e098ea3c45bdcf2c8e9970969803d.png)

我必须走得更远。我在幕后说话，扯下 Firebase 的窗帘，进入谷歌云平台日志。我发现了这个:

```
ERROR: error fetching storage source: generic::unknown: retry budget exhausted (3 attempts): fetching gcs source: unpacking source from gcs: source fetch container exited with non-zero status: 1
```

显然，这对我来说毫无意义，但我有工作要做。我把这条信息贴到谷歌上，找到了答案:

[](https://stackoverflow.com/questions/64437656/gcp-cloud-function-error-fetching-storage-source-during-build-deploy/65780066#65780066) [## GCP 云函数-在构建/部署期间获取存储源时出错

### 构建和部署功能时遇到问题。当试图以编程方式部署函数时，我得到了…

stackoverflow.com](https://stackoverflow.com/questions/64437656/gcp-cloud-function-error-fetching-storage-source-during-build-deploy/65780066#65780066) 

在这个 StackOverflow 问题的指导下，我通过将本地和云函数 Node.js 版本设置为 12 来解决这个问题。为什么这样可以解决问题？好吧，所有优秀的软件工程师都知道，不要想太多。感谢您花时间阅读这篇文章。也许它帮助了你。也许你会给我一些掌声。也许这是我自己写的，所以我再也不用处理这个了。

## 在 Mac 上将节点从版本 15 降级到版本 12(自制)

```
brew install node@12
brew unlink node
brew link --overwrite node@12
```

## 在 Firebase 云功能上将节点从版本 10 升级到版本 12

[](https://firebase.google.com/docs/functions/manage-functions#set_nodejs_version) [## 管理功能部署和运行时选项| Firebase

### 您可以使用 Firebase CLI 命令或通过在…中设置运行时选项来部署、删除和修改函数

firebase.google.com](https://firebase.google.com/docs/functions/manage-functions#set_nodejs_version) 

在您的函数文件夹的 package.json 文件中设置以下内容:

```
“engines”: { “node”: “12”}
```

## 结论

谢谢你的阅读。我希望你已经发现这很有用，不要遇到和我一样的问题。