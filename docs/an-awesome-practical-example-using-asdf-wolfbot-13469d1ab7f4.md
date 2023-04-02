# 使用 ASDF 的一个令人敬畏的实际例子:Wolfbot

> 原文：<https://javascript.plainenglish.io/an-awesome-practical-example-using-asdf-wolfbot-13469d1ab7f4?source=collection_archive---------15----------------------->

![](img/907f0439bb30abd05a09891f72bc989a.png)

[https://pixabay.com/illustrations/bitcoin-btc-cryptocurrency-1813503/](https://pixabay.com/illustrations/bitcoin-btc-cryptocurrency-1813503/)

*关于安装 asdf 的前一篇文章:*

[](https://anup-vasudevan.medium.com/the-greatest-package-manager-at-the-moment-e6d3547e510b) [## 目前最伟大的包装经理

### 魔镜魔镜，谁是最漂亮的包装经理？

anup-vasudevan.medium.com](https://anup-vasudevan.medium.com/the-greatest-package-manager-at-the-moment-e6d3547e510b) 

**免责声明**:这不是财务建议。

*本文中的材料仅供参考，并不构成出售要约、购买邀约或对任何证券或策略的推荐或认可，也不构成 Servingniches 或 me 提供投资咨询服务的要约。*

既然我们已经解决了这个问题…

## 好东西

因此，我们希望安装或用作这方面示例的项目是 Wolfbot。你可以在 https://github.com/Ekliptor/WolfBot 找到它

随意安装一个回购或项目更接近你的心。你将不得不修改 asdf 插件的步骤来匹配你选择的语言或技术，但这将是相似的，不会太痛苦。如果你正在处理一个相对主要的编程语言，那么你会很好。否则，在 asdf 中编写自己的插件来支持它。这相对容易，你会因此得到加分。我会说去吧。

## *Wolfbot 是一个加密货币交易机器人。*

*功能:*

*   交易:买入+卖出，投资组合管理(与交易所同步余额)
*   保证金交易:杠杆交易，包括卖空和期货交易
*   套利:从两个交易所之间的差价中获利(在两个交易所都有余额的情况下“账面”完成，不需要从交易所提款)
*   借贷:在受支持的加密交易所的借贷市场上以尽可能高的利率借出你的硬币
*   回溯测试:根据历史数据模拟测试你的交易策略
*   Web 插件:从 Twitter、Reddit、Telegram Channels、RSS Feeds 等获取社交媒体数据，根据新闻和真实事件进行交易(还不是开源版本的一部分)

Git 克隆回购。

```
git clone [https://github.com/Ekliptor/WolfBot](https://github.com/Ekliptor/WolfBot)
```

# 使用 asdf 安装和设置依赖项

因为我们之前已经详细讨论了这些步骤，所以我不再赘述。

要启动并运行 Wolfbot 我们需要。复制粘贴自[https://github.com/Ekliptor/WolfBot](https://github.com/Ekliptor/WolfBot)

*   Node.js >= 12 && <= 14
*   MongoDB > = 4.0
*   打字稿> = 3.5
*   yarn >= 1.9.4 (npm 应该也可以工作，但是如果遇到错误，则不提供支持)
*   Webpack >= 4(仅用于 UI 修改)

```
cd Wolfbot
asdf current # to see what versions are being used in this directory

asdf plugin add nodejs https://github.com/asdf-vm/asdf-nodejs.git 
asdf install nodejs 14.17.5
asdf local nodejs 14.17.5

asdf plugin add golang https://github.com/kennyp/asdf-golang.git
asdf install golang 1.15
asdf local golang 1.15

# For local mongodb development, you can get away with this setup.
# Don't use asdf for production
asdf plugin add mongodb https://github.com/sylph01/asdf-mongodb.git
asdf plugin add mongosh https://github.com/itspngu/asdf-mongosh.git
asdf install mongodb latest
asdf install mongosh latest
asdf local mongodb 5.0.2
asdf local mongosh 1.0.5

# For more details: #https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/# If a brand new installation on an Apple M1 Mac
mkdir -p /opt/homebrew/var/log/mongodb
mkdir -p /opt/homebrew/var/mongodb
touch /opt/homebrew/etc/mongod.conf
```

为下面的命令打开一个新标签。下面的命令在前台启动 MongoDB。

```
mongod --dbpath /opt/homebrew/var/mongodb # starts up the mongo db in foreground
```

将 Wolfbot 目录中的`configLocal-sample.ts`重命名为`configLocal.ts`。编辑 configLocal.ts 文件。

在文件的 mongo URL 部分添加您的 MongoDB URL。

```
mongodb://127.0.0.1:27017/?directConnection=true&serverSelectionTimeoutMS=2000
```

安装纱线

```
asdf plugin add yarn https://github.com/twuni/asdf-yarn.git
asdf install yarn latest
asdf local yarn 1.22.11
```

运行到目前为止安装的所有程序的最后步骤。

```
yarn install# to compile all TypeScript files. Ignore the errors. Press Ctrl-C
# once you see the watch message.
yarn tsc # the default node_module download for this particular package
# doesn't seem to have a build directory so we're building one
yarn tsc --project node_modules/@ekliptor/bit-models/tsconfig.json # The above command compiles all TypeScript files. Ignore the
# errors. Press Ctrl-C once you see the watch message. # Finally to run the bot
node build/app.js --debug --config=WhaleWatcher.json --trader=RealTimeTrader --noUpdate --noBrowser
```

您将会有额外的配置，比如用于各种交换的 API 键，以使机器人完全运行，但是上面的配置是为了使机器人处于可运行状态。

*多内容于* [***浅显易懂***](http://plainenglish.io/)