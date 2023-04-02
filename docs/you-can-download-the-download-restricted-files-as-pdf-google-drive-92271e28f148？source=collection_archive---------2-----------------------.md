# 您可以下载 PDF 格式的“下载受限”文件(Google Drive)

> 原文：<https://javascript.plainenglish.io/you-can-download-the-download-restricted-files-as-pdf-google-drive-92271e28f148?source=collection_archive---------2----------------------->

## 如何使用 *jspdf* 从 Google Drive 下载 PDF 格式的“受限”文件？

![](img/eabf31f67e816d53d23414b93a349219.png)

你好，

在今天的短文中，我们将会看到一些有趣的东西。当它成功的时候我很兴奋，我希望你也一样。

当你被限制了从 Google Drive 下载文件的权限时，你不会感到沮丧吗？？对我来说，这是一个很大的**是的**。

今天，我将分享一个代码，你可以毫不费力地下载这样的文件(受限的)。

> **回顾我写代码的原因:**
> 我不得不下载一些(实际上是许多)文件，这些文件的内容与我的研究有关，但下载受到限制。我们有一个期限，过了这个期限，共享文件夹中的文件将不再可用。因为我想要这些文件，至少是作为将来的参考，我开始寻找下载这些受限文件的方法，但是没有找到。后来我偶然发现了这个叫做“jspdf”的 JavaScript 库，它允许我们根据自己的要求下载 pdf 格式的网页。因此，我用它来满足我的需求，这对我来说已经足够了。

在这篇文章中，我将分享相同的代码。我正试图为它编写一个更好的版本，那将会给 T10 更好的 pdf 质量。

## 如何使用代码:

> 复制代码→转到您想要下载的文件并打开它(当然是在浏览器中)→打开开发人员工具(为此使用`ctrl + shift + I` )→转到控制台选项卡→粘贴代码并按回车键。

在使用代码之前，请确保向下滚动到文件的末尾，以确保没有页面保持卸载状态，否则您可能会错过一些内容。

代码如下:

希望它能达到目的。

> 优点:
> 你可以下载受限文件以备将来使用。
> 
> 缺点:
> 你得到的 PDF 是一堆放在一起的图像，所以你既不能复制文本，也不能对其执行单词搜索操作。

但是总有替代方法，例如，您可以对下载的 PDF 文件执行 OCR，这将涵盖上述两个问题。

此外，图像质量也不是一流的。但是正如我前面提到的，我正在开发这个代码的更好版本，通过它你可以得到质量更好的图像。因此，请关注并关注更新后的代码。

今天到此为止。下一个我会在[中见到你，在那里我会浏览这段代码并解释每一个步骤，这样你就可以轻松地按照你的需求来构建代码。](https://mohithgupta.medium.com/how-i-coded-a-script-to-download-the-download-restricted-files-of-google-drive-718e74c55a68?source=your_stories_page-------------------------------------)

如果你觉得代码或帖子有意义，考虑在评论区分享你的想法和建议。

如果你太高兴，你可以请我喝杯咖啡😉

![](img/5b1677007395fdea8f210fa1369b05a4.png)

你可以看看我其他的一些帖子:

[只需点击](https://python.plainenglish.io/play-youtube-videos-in-vlc-with-just-1-click-2baca84c03f3)
[“转换您的”,即可在 VLC 播放 YouTube 视频。py '到 a '。exe '文件，只需两个命令](https://python.plainenglish.io/convert-your-py-to-exe-with-just-2-commands-4c6cefe9af4c)
[你需要知道的关于 JavaScript](/all-you-need-to-know-about-the-fetch-api-6929930572a8) 中的“获取 API”

如果还有其他疑问，你可以在 mohithguptak@gmail.com 上联系我，或者在推特上找到我。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)