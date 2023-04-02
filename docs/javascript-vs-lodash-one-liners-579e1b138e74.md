# JavaScript vs Lodash 一行程序

> 原文：<https://javascript.plainenglish.io/javascript-vs-lodash-one-liners-579e1b138e74?source=collection_archive---------5----------------------->

![](img/c70b5c951ec51ef7a0b2f2c6335109e0.png)

## 现代 JavaScript 中的 5 种 Lodash 替代方法

![](img/a82c93afea8a83268c4fd88e159f0df3.png)

[Lodash](https://lodash.com/) 长期以来一直是 NPM 最受欢迎的图书馆之一，每周下载量超过 3000 万次，因为它为每个项目的需求带来了巨大的实用功能。尽管随着 ES6 &数组方法的引入，这种情况不再存在，但它被认为是每个项目的必备依赖项。

![](img/624b580e5936a97f9e53ff62866a3b62.png)

向已经流过的 node_modules 添加另一个库会影响加载速度并降低性能，这就是为什么我选择在新项目中不再包含 lodash。

在添加新包之前，我经常使用 [bundlephobia](https://bundlephobia.com/) ，因为它既显示了包的大小，也显示了更小的包。

![](img/573fc54a95b391c40b55d668a769da90.png)

我们可以看到 lodash 并没有对 3G 的下载时间产生巨大的影响，只有大约 61 毫秒，但是一个更好的网络仍然是由更少的 JS 有效载荷组成的🤓。

以下所有示例都将在此阵列上:

![](img/7e6fac1b32321c5cf4d39f392a17fe8d.png)

# 1.删除重复项

在 Lodash 中，使用`uniqWith`和`isEqual`作为比较器非常简单，对于 ES6，我们需要在每次过滤器迭代中检查重复的对象。

![](img/cdebe729ad616463e2cb4bb6b5e5e332.png)

# 2.计算平均值

我们需要计算所有宠物的平均价格。

![](img/3ba05de50d263b1971c482755823eea5.png)

# 3.随机 Id

为数组中的每只宠物添加一个随机 id。

> 我不推荐使用`Math.random`来生成密钥或密码，因为它不是完全随机的。

![](img/1d8054d10eb13816b815727d59a6f9f1.png)

# 4.大写字符串

对于每只宠物，我们需要将第一个字母大写。

![](img/6f0b663f9eafa8eb200c80373e865d9b.png)

# 5.移除字段

众所周知，我们将删除价格属性🐶是无价的。

![](img/fe314d902840db750be2f5223c55e996.png)

# 额外小费

如果您使用 Lodash 或 date-fns 导入实用程序函数，如下所示:

![](img/d927dc03172e7f6d92d5301ae2e32be0.png)

这样，与导入整个模块不同，导入的大小会大大减少:

![](img/b218392bf897dd99633720496313091a.png)

如果你想检查这里的代码是 [CodeSandbox](https://codesandbox.io/s/lodash-vs-es6-6g8h4?file=/src/index.js) 。

![](img/b923d5abf31b1ebf316052a15e04e1fa.png)

buymeacoffee.com/snappy.guy

*更多内容请看*[***plain English . io***](http://plainenglish.io)