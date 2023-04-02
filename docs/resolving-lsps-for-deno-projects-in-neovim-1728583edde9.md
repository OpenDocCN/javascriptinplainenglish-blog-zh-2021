# 如何解决 Neovim 中 Deno 项目的 LSP

> 原文：<https://javascript.plainenglish.io/resolving-lsps-for-deno-projects-in-neovim-1728583edde9?source=collection_archive---------7----------------------->

![](img/3d988e159fee9ea33799467e4ea0da4a.png)

Photo by [Pankaj Patel](https://unsplash.com/@pankajpatel?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我选择 Neovim 作为我的编辑器。为了给它类似 IDE 的特性，我安装了 [nvim-lspconfig](https://github.com/neovim/nvim-lspconfig) 和 [nvim-cmp](https://github.com/hrsh7th/nvim-cmp) 。nvim-lspconfig 允许我配置、启动和初始化我机器上的各种语言服务器。对于我的 JavaScript 和 TypeScript 工作，这通常意味着初始化`tsserver`。不过最近在 TypeScript 中研究 LeetCode 问题，发现用 TypeScript 设置节点项目有点过分。所以我决定尝试一下 Deno 对 TypeScript 的现成支持。

将 Deno 的 LSP 添加到我的配置中并不困难。其实过程很简单。我们可以检查 [nvim-lspconfig](https://github.com/neovim/nvim-lspconfig) repo 中的`CONFIG.md`文件，看看他们是否为此提供了 LSP。然后，我们通过一个简单的命令安装它。

```
-- in my nvim/init.lua file
local nvim_lsp = require("lspconfig")
nvim_lsp.denols.setup{}
```

在这种情况下，`denols`是我们可以安装使用 Deno 的 LSP 服务器的名称。就这样，我们结束了。至少我是这么认为的。

我的大部分 LSP 配置都是空的，就像你在上面看到的一样，这是我在创建 Deno 项目时犯的一个错误。

当我开始写一些代码时，一切似乎都很正常。看起来 LSP 正在做它的工作，但是当我开始编写单元测试时，我遇到了一个问题,`Deno.test`没有被识别。所以我检查了`:LSPInfo`，发现有两个客户端连接到缓冲区:`tsserver`和`denols`

这是有意义的，因为它会识别`TypeScript`文件类型，因为我没有任何其他方法来解决冲突。为了解决这个问题，我在 LSP 配置中添加了以下内容:

```
nvim_lsp.tsserver.setup{
  -- Omitting some options
  root_dir = nvim_lsp.util.root_pattern("package.json")
}nvim_lsp.denols.setup {
  -- Omitting some options
  root_dir = nvim_lsp.util.root_pattern("deno.json"),

}
```

通过在我的 Deno 项目的根目录下创建一个空的`deno.json`文件，Neovim 缓冲区将确保连接了正确的 LSP 客户端。类似地，如果我想使用`tsserver`作为我的 LSP 客户端，我必须确保在项目的根目录下存在一个`package.json`文件。

***TLDR:*** *确保设置* `*root_dir*` *选项指向一个文件，该文件可以唯一地表示您想要连接到您的缓冲区的 LSP 客户端。*

*更多内容请看*[***plain English . io***](http://plainenglish.io/)