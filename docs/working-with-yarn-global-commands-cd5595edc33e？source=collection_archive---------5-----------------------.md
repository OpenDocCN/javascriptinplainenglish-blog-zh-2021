# 使用纱线全局命令

> 原文：<https://javascript.plainenglish.io/working-with-yarn-global-commands-cd5595edc33e?source=collection_archive---------5----------------------->

## 使用 yarn 来安装和管理一个全局的包，该包可用于您机器上的所有项目

## NPM 全球期权的替代方案

![](img/019ea366f297cf71686fe209d12e3222.png)

随着 NPM(节点包管理器)的出现，每个项目都在自己的 node_modules 中维护依赖关系。然而，我们在全球范围内安装了一些软件包、工具和实用程序。这些包可以跨项目和目录使用。在一个示例中，在全局级别安装以下工具和实用程序是合适的——Angular CLI、create-react-app、http-server、json-server 等。

带有-*-全局*选项的 *npm install* 命令将软件包复制到一个全局目录。然而，就速度和安全性而言，Yarn“可以说”比 NPM 更好。本文详细介绍了如何使用 Yarn 在全局级别安装工具或包。

对于 Yarn，所有全局命令都需要以 yarn global 开始。考虑下面的片段。

```
# The following command lists information about all global packages
**yarn global list**# The following command uninstalls Json Server package 
# at global level
**yarn global remove json-server**
```

要在全局级别添加包，请使用以下命令。它安装 Http 服务器，可以跨项目和目录使用。

```
yarn global add http-server
```

> Http Server 是一个基于 Node.js 的零配置 Http 服务器，对于呈现静态内容、应用程序包等非常有用。

# 抓住你了

成功安装后，在任何目录或项目中运行 http-server。它应该会启动节点服务器。在少数情况下，它可能不起作用。让我们进一步探讨这一点！

它在哪里安装了 Http Server 的可执行文件和包？考虑以下命令。当您运行 http-server 命令时，bin 中的可执行文件会运行以启动 http 服务器。

```
# 1\. Print yarn directory with symlinks to executable.
**yarn global bin**# 2\. Print yarn directory for global node_modules
**yarn global dir**
```

有可能，终端(或命令提示符)不知道*纱仓*目录的位置。设置此目录的路径，以便终端在此处查找可执行文件。

```
# On Windows
set PATH=%PATH%;C:\Users\my_user_name\AppData\Local\Yarn\bin# On macOS
export PATH="$(yarn global bin):$PATH"
```

运行 http-server 从任何目录或项目启动 Node.js http 服务器。

# 添加到自定义目录

您可以使用 *-前缀*选项将软件包添加到自定义目录。考虑下面的片段

```
yarn global add http-server --prefix C:\yarn-temp
```

现在，指向 Http 服务器可执行文件的符号链接被复制到 **C:\yarn-temp\bin** 中，而不是默认位置(或配置的位置)。

```
c:\yarn-temp\bin>dir
 Volume in drive C is Windows
 Volume Serial Number is 24C0-1F85Directory of c:\yarn-temp\bin26-05-2021  14:19    <DIR>          .
26-05-2021  14:19    <DIR>          ..
26-05-2021  14:19               414 hs
26-05-2021  14:19                90 hs.cmd
26-05-2021  14:19               432 http-server
26-05-2021  14:19                99 http-server.cmd
               4 File(s)          1,035 bytes
               2 Dir(s)  434,982,051,840 bytes free
```

> 编码快乐！顺便用下面的链接了解更多关于我和我的观点
> 
> [CodeVenkey](https://codevenkey.com/)|[Twitter](https://twitter.com/KeertiKotaru)

# 参考资料和有用的链接

*   链接到*纱线全球*文档[https://classic.yarnpkg.com/en/docs/cli/global/](https://classic.yarnpkg.com/en/docs/cli/global/)
*   链接到 *Http 服务器 GitHub* 自述[https://www.npmjs.com/package/http-server](https://github.com/http-party/http-server#readme)

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)