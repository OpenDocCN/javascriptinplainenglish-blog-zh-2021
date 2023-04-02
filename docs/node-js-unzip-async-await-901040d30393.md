# Node.js: Unzip 异步等待

> 原文：<https://javascript.plainenglish.io/node-js-unzip-async-await-901040d30393?source=collection_archive---------5----------------------->

## 在异步 Node.js 上下文中解压缩一个. zip 文件。

![](img/b51e1be77707d1331575abf92df48a87.png)

Photo by [Florian Steciuk](https://unsplash.com/@flo_stk?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](/s/photos/highway?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

我正在开发 [DeckDeckGo](https://deckdeckgo.com) 的新功能，为此我必须在 [Firebase 函数](https://firebase.google.com/docs/functions)中解压缩数据。

编写这样一个 [Node.js](https://nodejs.org/) 函数花费了比预期更多的时间，这就是为什么我分享这个解决方案，希望有一天它也能帮助你😇。

# 解压缩程序

Node.js 提供了一个压缩模块 [Zlib](https://nodejs.org/api/zlib.html) ，但是它不支持 ZIP 文件。幸运的是，我们可以使用库[解压缩器](https://github.com/ZJONSSON/node-unzipper)来处理这些。

```
npm i unzipper --save
```

# 用异步 Await 解压缩

我的新特性通过流读写上传到 [Firebase 存储器](https://firebase.google.com/docs/storage)的数据。我也用 promises (async / await)方法开发我的代码。因此，两者必须共存。

为了缩小以下示例的范围，我用文件系统流(`fs`)处理的本地文件替换了云存储。

函数`unzip`在通过`unzipper`传输的`zip`数据上实例化一个流。每个条目都被迭代并通过管道传输到可写输出。摘要:打开 zip 文件，并提取其中包含的每个文件。

`unzip`在一个复古兼容的 top await 函数中被调用，基本上就是它的🥳.

```
const {Parse} = require('unzipper');
const {createWriteStream, createReadStream} = require('fs');

const unzip = () => {
  const stream = 
    createReadStream('/Users/david/data.zip').pipe(Parse());

  return new Promise((resolve, reject) => {
    stream.on('entry', (entry) => {
      const writeStream = 
        createWriteStream(`/Users/david/${entry.path}`);
      return entry.pipe(writeStream);
    });
    stream.on('finish', () => resolve());
    stream.on('error', (error) => reject(error));
  });
};

(async () => {
  try {
    await unzip();
  } catch (err) {
    console.error(err);
  }
})();
```

# 用异步 Await 读取字符串

我也必须用流来读取文件。因此，樱桃在顶部，这里是我如何在我的代码集成这些。

```
const {createReadStream} = require('fs');

const read = () => {
  const stream = 
    createReadStream('/Users/david/meta.json');

  return new Promise((resolve, reject) => {
    let data = '';

    stream.on('data', (chunk) => (data += chunk));
    stream.on('end', () => resolve(data));
    stream.on('error', (error) => reject(error));
  });
};

(async () => {
  try {
    const meta = await read();

    console.log({meta});
  } catch (err) {
    console.error(err);
  }
})();
```

它遵循与前面相同的方法，将文件内容读入内存`string`。

# 摘要

![](img/49f06bcb32d187d378e9131e1d5d5e18.png)

> 编码就像一盒巧克力。你永远不知道你会得到什么。有时候要快，需要时间。有时候这需要很长时间，但是它很快就过去了——对阿甘来说

到无限和更远的地方！

大卫

你可以在推特上或者我的网站上联系到我。

尝试 [DeckDeckGo](https://deckdeckgo.com/) 制作您的下一张幻灯片🤟。

[![](img/60715bd16846fb2485281256d8cf3a98.png)](https://deckdeckgo.com)