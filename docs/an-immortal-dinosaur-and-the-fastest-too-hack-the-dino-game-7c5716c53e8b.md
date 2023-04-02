# 我黑了 Chrome 恐龙游戏。我是这样做的。

> 原文：<https://javascript.plainenglish.io/an-immortal-dinosaur-and-the-fastest-too-hack-the-dino-game-7c5716c53e8b?source=collection_archive---------9----------------------->

![](img/cc5be7ad4276093510d57c05aec46cdf.png)

我们要把这个恐龙变成这个星球上最酷的恐龙。是的，最酷的，即使没有恐龙可以比较:)我不在乎！

首先，打开恐龙游戏。你不需要断开网络来玩这个游戏，你只需要在搜索栏中输入`chrome://dino`就可以了。

游戏实际操控:
**空格键/上箭头:**跳跃或开始游戏
**下箭头:**鸭子(恭敬地低头)
**Alt:** 暂停
**黑暗模式:**游戏每满 700 分的倍数，下一个 100 分就进入黑色背景模式。

一旦游戏开始，右击并选择`Inspect`打开 Chrome DevTools，然后选择`Console`标签。您也可以通过使用`Ctrl+shift+I`快捷方式来做到这一点，它会直接将您带到 DevTools 的 Console 选项卡。

## 尤塞恩·博尔特，谁？

在控制台中键入以下命令，然后按 enter 键。你可以用你希望的任何速度。是免费房产:)

```
Runner.instance_.setSpeed(1000) 
```

## 想知道这种恐龙是如何从灭绝中幸存下来的吗？事情就是这样的！

在控制台中键入以下命令，然后按 enter 键。

```
Runner.prototype.gameOver = function(){}
```

现在我们的 8 位恐龙可以生存任何东西，我的意思是字面上的任何东西。不要试图砸碎你的电脑来测试它。恐龙肯定能挺过去，但我不确定电脑。

如果你想让恐龙在某个时候死去，让它变得不死很无聊，你可以在把函数变成空函数之前把它保存在一个单独的变量里。然后在需要时恢复它。

```
var temp = Runner.prototype.gameOver
Runner.prototype.gameOver = temp
```

## 想炫耀你的分数吗？

我们可以手动设置分数。但是它有 99999 的限制，因为即使是恐龙也有限制，否则它们就会灭绝😱让我们给我们的恐龙打 98765 分。现在开始玩的时候，98765 分起步。

```
Runner.instance_.distanceRan =
 98765/ Runner.instance_.distanceMeter.config.COEFFICIENT
```

## 你喜欢袋鼠吗？

您可以使用以下命令来控制恐龙跳跃的高度。这也是有限度的。对孤独的恐龙来说限制太多了，对吧？

```
Runner.instance_.tRex.setJumpVelocity(10)
```

我们还可以玩许多其他的属性。你可以在网上搜索一下，就有了。你想要吗？你明白了！

这个帖子到此为止。下一集见。阿德乌斯。

你可以看看我其他的一些帖子:

[我编写了一个脚本来下载 Google Drive](https://mohithgupta.medium.com/how-i-coded-a-script-to-download-the-download-restricted-files-of-google-drive-718e74c55a68?source=your_stories_page-------------------------------------)
[的“下载受限”文件，只需点击一下](https://python.plainenglish.io/play-youtube-videos-in-vlc-with-just-1-click-2baca84c03f3)
[转换你的就可以在 VLC 播放 YouTube 视频。py '到 a '。exe '文件，只需 2 个命令](https://python.plainenglish.io/convert-your-py-to-exe-with-just-2-commands-4c6cefe9af4c)
[的 C++代码就可以绘制一张印度地图](https://medium.com/geekculture/c-code-to-draw-an-india-map-and-maybe-other-countries-too-9b0236f76d40)

在评论区分享你的想法。如有任何疑问或其他问题，你可以在 mohithguptak@gmail.com 上联系我，或者在推特上找到我。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)