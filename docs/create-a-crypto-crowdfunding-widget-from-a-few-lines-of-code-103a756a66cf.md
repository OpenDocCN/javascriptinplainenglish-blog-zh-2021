# 用几行代码创建一个加密众筹窗口小部件

> 原文：<https://javascript.plainenglish.io/create-a-crypto-crowdfunding-widget-from-a-few-lines-of-code-103a756a66cf?source=collection_archive---------14----------------------->

![](img/281759c0c1a429486a21a16939a7d6ca.png)

Source: [https://www.pexels.com/](https://www.pexels.com/)

你想开始自己的众筹活动吗？或者为修复 Github 问题筹集资金？或者你会为你的文章接受一些捐赠吗？有了密码就非常简单了。在本文中，我们将构建一个加密众筹小部件，用于在任何以太坊兼容网络上接受 ERC-20 令牌或加密。

## 该理论

我们的小部件将是一个动态生成的 PNG，它是从我们的以太坊地址和余额生成的。您可以在任何可以通过 URL 嵌入图像的地方嵌入此图像。你可以把它添加到你的 GitHub readme 或者一个问题的描述中，或者你可以把它嵌入到你的文章中，等等。该图像将包含一个二维码到您的以太坊地址和一个指示器，显示您的平衡，以及它离目标有多远。当你开始一个新的活动，你必须创建一个新的以太坊帐户或智能合同(例如。ICO 合同)来接受资金。

用户可以简单地扫描二维码，然后发送一些密码。大约需要 10 秒钟。向众筹活动发送 crypto 从未如此简单。

## 代码

我们将使用 JavaScript 来实现，使用 node-canvas 来生成结果 PNG 图像。

首先，我们将创建一个灰色画布。

```
const canvas = createCanvas(200, 270) 
const ctx = canvas.getContext(‘2d’) 
ctx.fillStyle = “#aaaaaa” 
ctx.fillRect(0, 0, canvas.width, canvas.height)
```

然后把二维码涂在上面。为此，我们将使用 [qrcode](https://www.npmjs.com/package/qrcode) 库。

```
let qrcode = new Image()
qrcode.src = await QRCode.toDataURL(config.ETH_ADDRESS)
ctx.drawImage(qrcode, 10, 10, 180, 180)
```

下一步是查询余额。我们可以通过使用 [web3](https://www.npmjs.com/package/web3) 库轻松做到这一点。

```
const web3 = new Web3(config.PROVIDER_URL)
const balance = parseInt(
  await web3.eth.getBalance(config.ETH_ADDRESS))
```

Web3 类的构造函数有一个 provider 参数。这是[以太坊 JSON-RPC](https://ethereum.org/en/developers/docs/apis/json-rpc/) 端点的 URL。如果你想使用以太坊主网，或者一个测试网络，那么最好的方法是使用 ConsenSys 的 [Infura](https://infura.io/) 。MetaMask 也用这个。如果你想在另一个以太坊兼容的网络上接受支付，比如 Polygon 或 xDAI 等。然后你可以[在这里](https://github.com/ethereum-lists/chains/tree/master/_data/chains)找到 RPC 端点。

如果您想接受代币支付，也可以查询您的 ERC20 余额。

```
const contract = new web3.eth.Contract(erc20_abi as AbiItem[],
  CONTRACT_ADDRESS)
const balance = 
  await contract.methods.balanceOf(config.ETH_ADDRESS).call()
```

契约类的构造函数有两个参数:接口定义(ABI)和 ERC20 令牌契约的地址。

如果余额已知，计算百分比就很容易了。

```
let percent = balance / (config.TARGET_VALUE * 10 ** 18);
if (percent > 1)
  percent = 1;
```

重要的是余额是，所以你必须用 10 除以

完整的代码如下所示:

23 行代码。正如我写的，这没什么大不了的。完整代码可在 [GitHub](https://github.com/TheBojda/Ethereum-crowdfunding-widget-javascript) 上获得。(我还有一个 [PHP 实现](https://github.com/TheBojda/Ethereum-crowdfunding-widget)。)

代码可以在一个最小的 Lightsail 实例(3，5 美元/mo)上运行，但是如果您不想为它分配一个完整的 EC2 实例，您可以将其部署到 AWS lambda。所有的东西都包含在 GitHub 回购协议中。

这是一个收集 xDAI 的示例小部件(顺便说一下，如果您喜欢这篇文章，或者只是想试试它是如何工作的，您可以给我发一些 xDAI):

[https://qiaby8b8pf.execute-api.eu-central-1.amazonaws.com](https://qiaby8b8pf.execute-api.eu-central-1.amazonaws.com)

本文最初发表于[黑客线上](https://hackernoon.com/create-a-crypto-crowdfunding-widget-from-a-few-lines-of-code)。

*更多内容参见* [*浅显英语。io*](http://plainenglish.io/) *。注册我们的* [*免费周报*](http://newsletter.plainenglish.io/) *。在我们的* [*社区不和*](https://discord.gg/GtDtUAvyhW) *中获得独家写作机会和建议。*