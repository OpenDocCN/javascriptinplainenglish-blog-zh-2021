# 用 Node.js 构建一个日志记录器

> 原文：<https://javascript.plainenglish.io/build-a-logger-with-node-js-7b5d3842c2c1?source=collection_archive---------2----------------------->

![](img/d4f519100af78e8f92fca275c3bf0305.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

日志是记录信息的行为，通常输出到终端或文件。根据您的应用程序，您可能会因为许多不同的原因记录许多不同的事情。您可以保留 API 请求的日志，或者记录错误/警告，以供以后调试使用。日志是任何主要应用程序的关键部分。

在本教程中，我们将为 Node.js 构建一个简单的日志记录器，包括日志级别、缓存，并将这些日志写入控制台和磁盘。

# 入门指南

首先，让我们创建一个新的 Node.js 项目。我使用 NPM，但我也包括了所有的纱线命令。

1.  `mkdir my-logger`
2.  `npm init -y` ( `yarn init -y`)

在本教程中我们不会使用任何包，所以我们可以直接进入代码。

# **构造我们的记录器**

让我们首先将我们的日志记录器定义为一个类。我们会在构造函数中要求一些参数。

1.  名称—我们将用来指代记录器的名称。
2.  目录—保存日志的目录。
3.  cacheSize——它控制在将日志写入文件之前我们保留多少日志，这很重要，这样我们就不会花费大量时间将每个日志写入文件。

然后，我们将缓存定义为一个空列表。我们将很快用日志填充它。另外，如果输出目录不存在，我们将使用`fs`模块来创建它。

```
const fs = require("fs");
const path = require("path");class Logger {
  constructor(name, dir="./logs", cacheSize=100) {
    this.name = name;
    if (!fs.existsSync(dir)) fs.mkdirSync(dir);
    this.path = path.join(dir, `${
      new Date().toISOString().replaceAll(':', '-').split('.')[0]
    }-${this.name}.log`);
    this.cacheSize = cacheSize;this.cache = []
  }
}
```

# **并非所有日志都是平等创建的**

日志可以用于各种不同的事情，所以通常我们把它们分成不同的级别。不管平台如何，大多数记录器都使用以下级别(尽管有些级别有不同的名称)。

*   信息—信息性消息，如开始、停止或其他重要事件
*   调试—对调试应用程序有用的信息
*   Trace(也称为 Verbose) —调试的更详细信息，可能记录所有事件
*   警告—记录不属于错误的潜在有害事件或不正确使用
*   错误—不要求应用程序停止的错误消息
*   致命—导致整个应用程序崩溃并退出的错误消息

在我们添加这些不同的日志类型之前，我们需要添加一个通用的`log`方法来避免在每种日志类型中重复我们自己。我们将我们的日志格式化为`YYYY-MM-DD HH:MM:SS NAME LEVEL MESSAGE`，但是如果你有自己的喜好，可以随意定制。我们还需要将该消息添加到缓存中，并检查是否需要将缓存写入日志文件。

```
 log(level, message) {
    const output = `${new Date().toISOString().replace('T',' ').split('.')[0]} ${this.name} ${level} ${message}`
    console.log(output)
    this.cache.push(output)if (this.cache.length >= this.cacheSize) {
      fs.appendFileSync(this.path, this.cache.map(l => `${l}\n`).join(''))
      this.cache = []
    }
  }
```

现在，对于每个级别，我们可以添加一个用户可以调用的方法。

```
 info(message) {this.log(‘info’, message)}
  debug(message) {this.log(‘debug’, message)}
  trace(message) {this.log(‘trace’, message)}
  warn(message) {this.log(‘warn’, message)}
  error(message) {this.log(‘error’, message)}
  fatal(message) {this.log(‘fatal’, message)}
```

# **用途**

我们现在可以通过在我们的应用程序中创建一个日志实例来使用这些函数。

```
const logger = new Logger('my-app')logger.info('App started')
logger.debug('Event START triggered')
logger.warn('THING Deprecated')
logger.error('Logging is too cool')
logger.fatal('App crashed because of X, Y and Z')
```

# 安全关机

在我们结束教程之前，我们需要在所有日志记录完成并且应用程序关闭后关闭日志记录器，因为我们需要将缓存中的所有日志写入文件。添加下面的方法，如果你想把它添加到你的应用中，在你的应用的关闭函数中调用它。

```
 close() {
    fs.appendFileSync(this.path, this.cache.map(l => `${l}\n`).join(''))
  }
```

# **结论**

恭喜你！您现在有了一个完整的工作日志记录器，并且可以在您的项目中使用它。日志记录非常重要，尤其是在较大的项目中，它使调试变得非常容易。

# **挑战**

对于想超越本教程的人来说，这里有一个小小的挑战。

*   使用库添加一些颜色，如[粉笔](https://www.npmjs.com/package/chalk)。
*   添加一种方法来过滤控制台记录的日志(例如，从控制台隐藏详细日志)。
*   添加一些实用函数，比如计时器(查看 Node.js `performance.now`方法)。

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/)***[***免费每周简讯点击这里***](http://newsletter.plainenglish.io/) *。****