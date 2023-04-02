# 如何将您的 Web 开发项目快速迁移到新的 Mac 上

> 原文：<https://javascript.plainenglish.io/how-to-migrate-your-web-development-projects-to-a-new-mac-quickly-d4806210e38c?source=collection_archive---------10----------------------->

![](img/2c7852c53d2a54b5cc678abe831983b2.png)

Photo by [Ilya Pavlov](https://unsplash.com/@ilyapavlov?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/apple-mac?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

最近，我的 Macbook Pro 的蓝牙决定停止工作，所以 IT 部门在我送去维修时给了我另一台机器。你可以想象，我想花尽可能少的时间来转移项目，因为这将是非常临时的。

当我试图简单地将文件从一台计算机复制到另一台计算机时，我发现估计复制文件需要一天多的时间，而复制速度只有几 KB/s。原因是它必须为每个单独的文件初始化副本，这有一个开销。

解决这种开销的方法是首先将文件压缩成一个文件，然后在新系统上解压缩。

为此，我首先在终端中使用`tar`捆绑文件，如下所示:

```
tar -czf Projects.tgz Projects
```

在我的例子中，这导致了一个大约 3GB 大小的所有项目的捆绑包。

下一步是将`Projects.tgz`包复制到新系统，这将比单个文件的复制速度快得多，在我的 WiFi 网络上，我达到了大约 60MB/s。

完成复制后，您可以按如下方式解包文件:

```
tar -xvf Projects.tgz
```

这不会花费太长时间，现在您已经准备好了新系统上的所有项目，可以继续工作了。

# 概括起来

尝试将项目的文件分开会花费大量的时间，但是将它们捆绑到一个单独的文件中可以减少开销，使您可以更快地将文件从一个系统移动到另一个系统。

如果你觉得这篇文章有帮助，请告诉我，如果你喜欢这篇文章，我鼓励你关注我，这样你就可以阅读更多我的文章。

如果你想支持我的帖子，并且你还不是 Medium 的成员，那么请随意加入 https://jonthanfielding.medium.com/membership 的。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)