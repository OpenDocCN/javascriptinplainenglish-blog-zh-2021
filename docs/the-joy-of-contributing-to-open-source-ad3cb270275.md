# 为开源做贡献的快乐

> 原文：<https://javascript.plainenglish.io/the-joy-of-contributing-to-open-source-ad3cb270275?source=collection_archive---------18----------------------->

![](img/2f6c5409ad111c67e185cdf6a99b57e4.png)

回到今年 7 月，我做了一个大胆的决定，完全转向 Pop OS(一个基于 ubuntu 的 Linux 发行版),我面临着许多障碍。其中之一是微软手机应用程序的替代品。

经过一些研究，我偶然发现了一个名为 [KDE 连接](https://kdeconnect.kde.org/)的应用程序，它被证明是一个很好的替代品，因为它不仅做了微软手机应用程序所做的一切，还拥有一些更漂亮的功能。

由于 Pop OS 使用 Cosmic(流行的 GNOME 桌面环境的一个分支)，我最好使用 [GSConnect](https://extensions.gnome.org/extension/1319/gsconnect/) 而不是本地的 KDE 连接应用程序。GSConnect 是 KDE 连接的一个分支，它与 GNOME 集成得很好。一切都很好，直到我发现了一个功能，允许我将当前标签的 URL 共享到我的手机上。这需要我下载 [GSConnect chrome 扩展](https://chrome.google.com/webstore/detail/gsconnect/jfnifeihccihocjbfcfhicmmgpjicaec)，但我使用微软 Edge 作为我的主要网络浏览器。现在，chrome 扩展可以在微软 Edge 上工作，因为它是基于 chrome 的，但 GSConnect chrome 扩展使用了一种称为[原生消息](https://developer.chrome.com/docs/apps/nativeMessaging/)的功能，这种功能有助于浏览器扩展和安装在计算机上的程序相互交互。可悲的是，这需要为每个浏览器进行专门的配置(这只是一行代码)。GSConnect 当时不支持微软 Edge，因此我决定[公开一个问题](https://github.com/GSConnect/gnome-shell-extension-gsconnect/issues/1139)。

一位合作者找到我，向我解释了这个问题。我有点卡住了，于是在 GitHub 上寻求更多的帮助，那个人给了我回复，给了我一个开始解决这个问题的地方。我很快发现了问题，并在我这边解决了问题。下一步是打开一个拉请求，所以我克隆了存储库，进行了更改，推送了代码，并打开了我的第一个拉请求。我确实弄乱了代码风格，因为我忘记了阅读投稿指南，因此没有运行 linter 检查。不管怎样，一个成员回复了我，我解决了问题，然后我的拉取请求被合并了🎉。

# 当我的拉取请求被合并时的喜悦

一看到我的拉请求被合并的通知，我就感受到了为一个被很多人使用的应用程序做贡献的喜悦。这一刻，你意识到你不是在白干，你从帮助别人中获得快乐，你自己也学到了很多。为开源做贡献也增加了你的投资组合，这表明你关心这个项目。

# 学习

当我打开这个问题时，我对 chrome extensions 中的原生消息传递一无所知，但从发现这个错误到修复它，我学到了很多关于原生消息传递如何工作以及开源贡献如何工作的知识。

我在我的上一篇文章中谈到了为开源做贡献的好处。

不难体验到为开源做贡献的快乐。寻找您可能想要解决的问题，如果您找到了您想要解决的问题，就像进行更改和打开一个拉请求一样简单(确保遵循存储库的贡献指南，如果它有)。另外，看看 [Hacktoberfest](https://hacktoberfest.digitalocean.com/) ，在那里你打开 4 个**有效的** pull 请求，如果你是第一个这样做的 50k 人，你会得到一些奖品。如果你感到困惑，一定要看看阿尤什·拉瓦特写的[黑客啤酒节](https://ayushirawat.com/beginners-guide-to-hacktoberfest-2021)入门指南。

如果你觉得我错过了什么或者你有问题，请随意评论。你也可以在推特上联系我。

快乐贡献:D

*原发布于*[*https://blog . anishde . dev*](https://blog.anishde.dev/the-joy-of-contributing-to-open-source)*。*

*更多内容请看*[***plain English . io***](http://plainenglish.io/)