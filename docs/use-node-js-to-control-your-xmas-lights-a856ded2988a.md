# 使用 Node.js 来控制你的圣诞灯

> 原文：<https://javascript.plainenglish.io/use-node-js-to-control-your-xmas-lights-a856ded2988a?source=collection_archive---------5----------------------->

或者如何过度设计你的圣诞灯

![](img/0b2513fdbcb047ee69b4ad2201044afd.png)

Photo by [Madison Kaminski](https://unsplash.com/@mkaminski) on Unsplash

*最初发布于*[*https://fek . io*](https://fek.io/blog/use-node-js-to-control-your-xmas-lights/)*。*

多年来，我一直想得到可以通过网络或智能手机控制的灯泡。我终于挥霍，得到了飞利浦色相桥和灯泡。你现在可以在大多数五金店找到这些。这座桥花了我大约 59 美元。你也可以花大约 69 美元购买带有一些灯泡的初学者工具包。

你可以购买一些智能灯泡，通过 WiFi 连接直接连接到互联网，但并不是所有的智能灯泡都具有相同的物联网功能。Hue bridge 可以通过智能手机应用程序、Amazon Dots、Google Home 以及一些开源 API 进行控制。

我有一个彩色灯泡，我想做一个在圣诞节期间在绿色和红色之间循环的灯。为了编写一个可以与 Hue 网桥通信的应用程序，您需要两条信息，即网络上网桥的 IP 地址和用户 id。

您可以通过使用用于配置和设置桥的 smartphone 应用程序来找到您的 Hue 桥的 IP 地址。在应用程序中，您可以选择设置选项卡，然后选择桥>和您设置的桥。它将在网桥的信息中列出 IP 地址。

获得白名单用户的下一步是向 Hue 桥发送一个 HTTP post。查看下面的说明；

[](https://developers.meethue.com/develop/get-started-2/) [## 开始行动-飞利浦色相开发者计划

### 遵循 3 个简单的步骤第 1 步首先确保您的网桥连接到您的网络并且运行正常。测试…

developers.meethue.com](https://developers.meethue.com/develop/get-started-2/) 

一旦有了 IP 地址和用户令牌，就有了控制桥上灯泡所需的所有信息。

# 拿到你桥上灯泡的清单

在我们可以向灯泡发送命令之前，我们需要找到灯泡及其 id，这样我们就可以使用 Hue REST API 进行调用。下面是一个脚本，用于返回网桥上所有设备的列表；

现在我只有一个灯泡亮着，所以我将只得到一个灯泡的结果；

```
{
  '1': {
    state: {
      on: true,
      bri: 254,
      hue: 41371,
      sat: 82,
      effect: 'none',
      xy: [Array],
      ct: 153,
      alert: 'select',
      colormode: 'xy',
      mode: 'homeautomation',
      reachable: true
    },
    ...
  }
}
```

如果我想获得特定灯泡的灯泡状态，我可以将灯泡的编号添加到端点。我们可以重写脚本，只返回第一个灯泡；

```
{
  state: {
    on: true,
    bri: 254,
    hue: 41371,
    sat: 82,
    effect: 'none',
    xy: [ 0.3085, 0.3266 ],
    ct: 153,
    alert: 'select',
    colormode: 'xy',
    mode: 'homeautomation',
    reachable: true
  },
  ...
}
```

如果我想将灯泡的颜色改为绿色，我可以使用 PUT 动词并在 URL 端点的末尾添加`state`来向灯泡传递一个新的状态。下面是一个将灯泡设置为绿色的例子；

# 在绿色和红色之间切换灯泡

为了给灯泡一种圣诞节的感觉，我将每两秒钟在绿色和红色之间切换灯泡。对于主脚本，我将使用一个`setInterval`函数，并设置它每 2000 毫秒运行一次。

完整的脚本应该如下所示:

# 作为服务运行

如果我们想将我们的脚本作为服务运行，我们可以通过使用`pm2`来实现。PM2 是一个用 Node 编写的进程管理器，可以在任何操作系统上运行。使用以下命令在我们的计算机上安装 pm2。

```
npm i pm2 -g
```

这将在我们的系统上全局安装 pm2。现在我们可以把我们的主脚本作为一个服务安装在我们的计算机上。

```
> pm2 start cyclexmaslights.js --name xmaslights
```

现在，如果我们想保存这个配置，让我们的计算机记住这个服务，我们可以使用下面的命令。

```
pm2 save
```

如果我们想在重启后继续使用我们的 pm2 配置，我们可以使用下面的命令来生成我们将需要用来使 pm2 成为系统服务的命令。

```
> pm2 startup 
# To setup the Startup Script, copy/paste the following command: sudo env = $PATH:/usr/bin /usr/lib/node_modules/pm2/bin/pm2 startup systemd -u pi --hp /home/user
```

在 Linux 上，它很可能会使用`systemd`。在 Mac 上，它可能会使用`launchd`。

# 如果我的计算机进入睡眠状态或者我关闭了它，该怎么办？

如果你和我一样，你想让你的灯整夜亮着，使用一台进入睡眠状态或者关机的电脑将会杀死脚本。这里一个很好的选择是使用像 Raspberry Pi 这样的计算机。它们不会消耗很多电能，你可以把它们放在家里的任何地方。

# 结论

像这样的物联网项目可以是与家人在家一起做的有趣项目。学习更多关于硬件和嵌入式系统的知识也很有趣。像这样的项目也帮助我们了解更多关于 API 和 Rest 的知识。

Hue 还有一个远程 API，可以通过互联网控制 Hue 桥。有许多不同语言的开源框架可用于控制照明。

*更多内容看* [***说白了. io***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) ***。***