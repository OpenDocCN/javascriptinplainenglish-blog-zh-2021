# 如何在低规格服务器上运行“npm 运行构建”?

> 原文：<https://javascript.plainenglish.io/how-to-execute-nuxt-npm-run-build-on-low-spec-server-ef7442b5c03d?source=collection_archive---------2----------------------->

![](img/b2138a0b474833dbdb885d4c30f90566.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/javascript-node?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

我相信在 NPM 的世界里，你会遇到难以解决的问题。尝试在您的服务器或本地环境中执行`npm run build`时，您是否感到头晕？例如，得到下面的错误信息。

```
Killed
npm ERR! code ELIFECYCLE
npm ERR! errno 137
npm ERR! project-nuxt@1.0.0 build: `nuxt build`
npm ERR! **Exit status 137**
npm ERR! 
npm ERR! Failed at the project-nuxt@1.0.0 build script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.npm ERR! A complete log of this run can be found in:
npm ERR!     /home/administrator/.npm/_logs/2021-04-11T08_48_48_675Z-debug.log
```

如果是，你并不孤单。错误消息“**退出状态 137** ”指的是 NPM 没有足够的内存在你的土豆服务器上编译你的代码的情况。`npm run build`所做的是运行 package.json 中的脚本“build ”,它通常是编译或构建或运行应用程序的脚本。所以基本上，这是一个吃公羊的家庭😅。

在这篇文章中，我将根据我的经验分享解决方案。

# 解决方法是什么？

有一种方法可以解决这个问题，那就是限制构建 package.json 所需的最大内存。

去`package.json`看剧本

```
....
"scripts": {
    "dev": "nuxt",
    **"build": "nuxt build",**
    "start": "nuxt start",
    "generate": "nuxt generate"
},
....
```

您所需要的只是在构建阶段指定限制内存。为了避免错误 137，使用参数`—-max-old-space-size`增加内存限制量。这将有助于避免内存限制问题。举个例子，

```
node --max-old-space-size=800 node_modules/nuxt/bin/nuxt.js build
node --max-old-space-size=1000 node_modules/nuxt/bin/nuxt.js build
node --max-old-space-size=**VALUE** node_modules/nuxt/bin/nuxt.js build
....
....
```

您可以选择任何想要的值(以 MB 为单位)并替换它。复制并将其放入 package . JSON“build”脚本中。

```
....
"scripts": {
    "dev": "nuxt",
    **"build": "PASTE HERE",**
    "start": "nuxt start",
    "generate": "nuxt generate"
},
....
```

在那之后，就又拯救了`npm run build`🍻。

一切都会顺利的。但是您会注意到脚本运行缓慢，因为您为 NPM 编译代码分配了较低的内存限制。

# 如果不起作用呢？

如果上述解决方案对您不起作用，请检查是否有可用的交换内存。如果没有，您需要按照以下步骤创建一个交换文件:

1.  通过运行以下命令检查系统交换信息

```
# sudo swapon --show
**NAME      TYPE  SIZE USED PRIO**

# free -h
              total    used    free   shared  buff/cache   available
Mem:          1987     555     991      36         440        1279
**Swap:          0        0        0**
```

如果您没有得到任何输出，这意味着您的系统当前没有可用的交换空间。如果你已经有了，可能会有一些其他的问题，很可能是你的代码的问题。

2.在创建交换内存之前，您应该检查当前的磁盘使用情况

```
# dh -f
...
/dev/vda1        49G  6.0G   43G  13% /
...
```

3.所以，根据上面的例子，有足够的空间可用。继续创建交换文件

```
# sudo fallocate -l 1G /swapfile
# sudo chmod 600 /swapfile# sudo mkswap /swapfile
# sudo swapon /swapfile
# sudo swapon --show
# free -h
```

至此，您的交换文件就创建好了。尝试重新运行“npm 运行构建”。现在应该可以正常工作了。😁

太好了！现在你可以面带微笑愉快地跑你的 NPM 了。希望这个解决方案能够帮助您减轻与 JavaScript 相关的压力。感谢阅读。编码快乐，工作快乐！

# 参考

[](https://medium.com/@vuongtran/how-to-solve-process-out-of-memory-in-node-js-5f0de8f8464c) [## 如何解决 Node.js 中进程内存不足的问题

### 我将在 Node.js 中展示如何解决内存不足的问题。

medium.com](https://medium.com/@vuongtran/how-to-solve-process-out-of-memory-in-node-js-5f0de8f8464c) 

*更多内容请看*[*plain English . io*](http://plainenglish.io/)