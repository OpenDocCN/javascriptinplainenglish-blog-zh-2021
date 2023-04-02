# 用于版本控制的引导客户端 Git 挂钩

> 原文：<https://javascript.plainenglish.io/bootstrap-client-side-git-hooks-for-version-control-5e34708f61e?source=collection_archive---------20----------------------->

## 零依赖性 package.json 脚本

![](img/8793c5c588486e33eab276aaba2e2050.png)

Photo by [Pankaj Patel](https://unsplash.com/@pankajpatel?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

外面有很多关于 [Git hooks](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks) 的很好的入门书籍，所以如果你是这个概念的新手，先花点时间熟悉一下——我们将在这里开门见山。

默认情况下，Git 将客户端钩子存储在*中。git/hooks* 在版本控制之外。虽然像 [Husky](https://github.com/typicode/husky) 这样的包可以使创建和版本控制挂钩变得容易，但我发现最新版本的设置过程太接近于“滚动你自己的”方法，以至于不值得学习另一组命令。

Git 在*的`core`表中提供了一个名为`hooksPath`的可配置设置。git/config* 文件以及设置和取消设置它的命令。在 *package.json* 中添加:

就是这样！运行`hooks:install`脚本后，Git 识别出*脚本/git/hooks* 中有效的客户端钩子，更重要的是，它们是受版本控制的。

请注意，您可以选择最适合项目架构的路径。您还可以将`npm run hooks:install`包含在一个单独的`bootstrap`脚本中，以组合和运行引导项目所需的任何其他流程。

当然还有其他方法可以实现这种行为，但是这个解决方案对我来说特别优雅。希望它有用，并一如既往，随时指出任何边缘情况或您自己的首选解决方案。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)