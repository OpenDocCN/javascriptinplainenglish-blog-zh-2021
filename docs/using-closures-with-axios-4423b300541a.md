# 使用 Axios 测试代码

> 原文：<https://javascript.plainenglish.io/using-closures-with-axios-4423b300541a?source=collection_archive---------18----------------------->

![](img/48d53615e2d548b250d2ec131b30c3fd.png)

最近，我一直致力于与订阅/支付网关的集成(这并不简单，但这是另一篇文章)。

我希望能够测试我的 web hook 代码，而不需要从网关重复触发事件。我以 JSON 格式存储传入的事件，这很好——但是我当然需要获取存储的事件并对它们做一些事情。

我想记下我从哪里开始以及如何到达终点可能会很有趣。我已经包括了我在这个过程中所犯的错误，所以如果你读了一点并认为“那不行！”—我可能在下一段中发现了这一点。

## 开始

从简单开始——将文件读入一个对象数组，然后循环打印每个事件的一些详细信息，这样我们就知道它加载得很好。

由于这是测试代码，我将使用 readFile 的同步版本[来保持代码简单——没有回调，我们可以将`readFileSync`的结果直接输入到](https://nodejs.org/api/fs.html#fs_fs_readfilesync_path_options)`[JSON.parse](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse)`中，就像这样:

```
const fs = require('fs');

function run()  {
    const json = JSON.parse(fs.readFileSync(__dirname + "/events.json"))

	for (const event of json) {
        console.log("event: ", event.id, event.event_type);
    }
}

run()
```

果然，我们得到了我们所期望的。

```
$ node post-events.js
event: 1 Hello
event: 2 World
```

这是可行的，但是循环会很快地发布事件。我更倾向于将它们分隔开来——这样更容易观察接收代码，并且我不打算在这一点上对其进行压力测试。

## 逐渐发送它们

`[setTimeout](https://nodejs.org/dist/latest-v14.x/docs/api/timers.html#timers_settimeout_callback_delay_args)`很好地为将来要执行的函数排队。等待时间最简单的方法是使用数组中的位置。`[for...of](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)`构造没有给出索引，所以我们必须使用不同的方法。

`[forEach](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)` 既能给我们条目又能给我们索引，所以让我们利用这一点。只是循环发生了变化——文件读取和 JSON 解析保持不变，所以我不会重复。

```
json.forEach((event, index) => {
    console.log(`Event ${event.id}: ${event.event_type}`);
    console.log(`Will delay ${(index + 1) * 1000} ms`);
})
```

是的，我们很好:

```
$ node post-events.js
Event 1: Hello
Would delay 1000 ms
Event 2: World
Would delay 2000 ms
```

## 行程安排

现在我们只需要安排一些事情。让我们先试试[最简单的东西](https://ronjeffries.com/xprog/articles/practices/pracsimplest/)——对于每个事件，将一个以`event`为参数的函数排队，以打印出事件 id。

```
json.forEach((event, index) => {
	const timeout = (index + 1) * 1000;
    console.log(`Event ${event.id}: ${event.event_type}`);
    console.log(`Will delay ${timeout} ms`);
	setTimeout(event => console.log("Posting", event.id), timeout);
})
```

并且:

```
$ node post-events.js
Event 1: Hello
Will delay 1000 ms
Event 2: World
Will delay 2000 ms
post-events.js:10
		setTimeout(event => console.log("Posting", event.id), timeout);
		                                                 ^
TypeError: Cannot read property 'id' of undefined
    at Timeout._onTimeout (post-events.js:10:52)
    at listOnTimeout (node:internal/timers:557:17)
    at processTimers (node:internal/timers:500:7)
```

仔细想想，这是有道理的，我真的应该知道更好。

当功能运行时，读取`event`参数**。由于超时，函数在循环结束后运行——此时`event`不再被定义，这就是我们所看到的。**

## 关闭

我们能做的是创建一个所谓的[闭包](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)。一个闭包本质上是一个函数以及它被创建时的环境。幸运的是，JavaScript 让这变得简单了。

```
function makeFunc(event) {
	console.log("Making func for", event);
    return async function() {
        console.log("Posting", event.event_type);
    }
}
```

我们循环的另一个版本:

```
json.forEach((event, index) => {
	const timeout = (index + 1) * 1000;
    console.log(`Setting timeout for Event ${event.id}; delay ${timeout} ms.`);
	setTimeout(event => makeFunc(event), timeout);
})$ node post-events.js
Setting timeout for Event 1; delay 1000 ms.
Setting timeout for Event 2; delay 2000 ms.
Making func for undefined
Making func for undefined
```

嗯……那里出了点问题。所发生的是因为我们写了`event => makeFunc(event)`，对`makeFunc`的调用没有立即发生，而是被延迟了——这给了我们和以前一样的问题。让我们马上打电话:

```
json.forEach((event, index) => {
	const timeout = (index + 1) * 1000;
    console.log(`Setting timeout for Event ${event.id}; delay ${timeout} ms.`);
	setTimeout(makeFunc(event), timeout);
})
```

看看这是怎么做到的:

```
$ node post-events.js
Setting timeout for Event 1; delay 1000 ms.
Making func for { id: 1, event_type: 'Hello' }
Setting timeout for Event 2; delay 2000 ms.
Making func for { id: 2, event_type: 'World' }
Posting Hello
Posting World
```

## 帖子请求

这还差不多。我们将使用 axios 对 HTTP 端点进行 POST。

```
const fs = require('fs');
const axios = require("axios");

const client = axios.create()

function makeFunc(event) {
    return async function() {
        console.log("Posting", event.event_type);
        const res = await client.post("http://localhost:8000",event);
        if (res.isAxiosError) {
            console.error("Error posting");
        }
    }
}

function run()  {
    const json = JSON.parse(fs.readFileSync(__dirname + "/events.json"))

	json.forEach((event, index) => {
		const timeout = (index + 1) * 1000;
	    console.log(`Setting timeout for Event ${event.id}; delay ${timeout} ms.`);
		setTimeout(makeFunc(event), timeout);
	})
}

run()
```

## 查看输出

你可以使用类似于 [requestbin.io](https://requestbin.io/) 的服务，作为一种简单的方法来查看帖子的样子。为此，我决定使用 [fiatjaf 的 request bin](https://github.com/fiatjaf/requestbin)——它小而简单。

我们在这里——正确的数据，间隔一秒钟，如我们所料。

```
$ ./requestbin -port 8000
Listening for requests at 0.0.0.0:8000

=== 18:00:00 ===
POST / HTTP/1.1
Host: localhost:8000
User-Agent: axios/0.21.1
Content-Length: 29
Accept: application/json, text/plain, */*
Connection: close
Content-Type: application/json;charset=utf-8

{"id":1,"event_type":"Hello"}

=== 18:00:01 ===
POST / HTTP/1.1
Host: localhost:8000
User-Agent: axios/0.21.1
Content-Length: 29
Accept: application/json, text/plain, */*
Connection: close
Content-Type: application/json;charset=utf-8

{"id":2,"event_type":"World"}
```

我希望那能帮助某人。即使我们只是遇到了同样的“糟糕”时刻，我们也一起犯过错误。感谢您的阅读。

*更多内容看* [***说白了. io***](http://plainenglish.io/)