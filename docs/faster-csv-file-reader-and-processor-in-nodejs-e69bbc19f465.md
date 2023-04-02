# Node.js 中更快的 CSV 文件阅读器和处理器

> 原文：<https://javascript.plainenglish.io/faster-csv-file-reader-and-processor-in-nodejs-e69bbc19f465?source=collection_archive---------3----------------------->

![](img/d0505d72e51b733a1c9394881edf1514.png)

# 有什么问题？

首先，我想解释一下我的问题是什么，以及我是如何解决的。有一天，我的一个同事发给我一个 **1GB CSV** (关于 **60M** 线的一些东西)文件，并说有许多客户的电话号码，其中一些是重复的，我们不需要它们。请将它们**插入数据库**，并给我表格名称。

# 一开始我做了什么？

起初，我认为这很容易，并开始逐行读取文件。
对于每个数据，我通过 **SQL 查询**检查数据库，如果我之前添加了这个数字，跳过插入过程，如果没有，将数字插入表中。

这样，我遇到了三个问题:

1.  由于**内存限制**，我无法用 fs 库这样的普通文件阅读器读取大文件
2.  为每个号码运行一个查询需要花费太多的时间。
3.  **我无法通过这种方式运行子进程**，所以需要 10 多天。

# 我是如何解决这个问题的？

总结一下:

*   [**行阅读器**](https://www.npmjs.com/package/line-reader) 用于读取文件。
*   **MySQL** 作为**数据库**
*   [**rabbit MQ**](https://www.rabbitmq.com/)**为**消息控制****
*   **[**PM2**](https://www.npmjs.com/package/pm2) 用于在后台运行服务**

**起初，我决定将我的数据库表**结构**改为**以避免**使用 **SQL 查询**来查找这个数字是否与**重复**。所以我把 number 列结构改成了 unique。**

```
ALTER TABLE numbers
ADD CONSTRAINT constraint_name UNIQUE (number);
```

**更改后，我不会检查号码是否重复，我只是插入号码，**数据库将决定**是否是新号码。为了提高效率，我通过以下命令将索引添加到我的列中:**

```
CREATE UNIQUE INDEX number_idx ON numbers (number);
```

**为了读取文件，我开始通过 [**行阅读器**](https://www.npmjs.com/package/line-reader) 包**读取文件**，因为它帮助我逐行读取文件**缓冲**和**。但问题是，它不能是同步的，所以如果我想在读取文件时插入数据，我会得到一个错误，因为我向数据库并行发送了太多的数据。****

**起初，我写了这段代码:**

```
*const* lineReader = require('line-reader');
*async function* start() {
    *const* csvFile = __dirname + "/assets/data.csv";
    lineReader.eachLine(csvFile, *async function*(line, last, cb) {
        *// My insertion Process*
        cb();
    });
}
```

**在这之后，我决定用 **RabbitMQ** 来解决这个问题。**

**我创建了两个服务，一个**阅读器服务**，一个**插入服务**，我通过 RabbitMQ 连接它们。**

**我从阅读器服务发布数据，从插入服务读取数据并将其插入数据库。为了提高速度，我克隆了三个插入服务。**

**在这里，我分享我的服务准则:**

**让我解释一些重要的事情:**

*   **在第 **23** 行，我使用了**持久**因为当服务关闭时，所有的数据都会丢失。可以**降低速度**但是值得。**
*   **在第 **19** 行，因为我使用的是持久数据，所以我需要有一个选项，在我需要的时候，我可以**清除队列**。**

**我来解释一些**重要的**事情:**

*   **在 **39** 行中， **ack** 表示我们的服务收到了消息，流程结束，消息代理**可以将**从**队列**中移除。**
*   **在第 **37** 行中，prefetch 表示消息代理在我们调用 ack 之前不会发送文本消息。这意味着我们的服务将逐个插入数据。**

**由于**预取**，我们的第二个服务是一个接一个的读取数据**，所以我们可以从第二个服务中打开**多个**，我们的数据库可以支持**提高速度。******

****部署之后，我想从我们的服务器上关闭我的 **SSH** ，所以我想使用 [PM2](https://www.npmjs.com/package/pm2) 。为了管理它，我创建了一个文件，并将其命名为 **run.json******

```
**{
  "apps": [
    {
      "name": "reader-service",
      "script": "./reader.service.js",
      "autorestart": true
    },
    {
      "name": "insertion-service-1",
      "script": "./insertion-service.js",
      "autorestart": true
    },
    {
      "name": "insertion-service-2",
      "script": "./insertion-service.js",
      "autorestart": true
    }
  ]
}**
```

*****更多内容请看*[*plain English . io*](http://plainenglish.io/)****