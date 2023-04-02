# 使用 Socket 在 Node.js 中进行实时、双向和基于事件的通信。超正析象管(Image Orthicon)

> 原文：<https://javascript.plainenglish.io/real-time-bidirectional-event-based-communication-in-node-js-using-socket-io-edbc79b0ad25?source=collection_archive---------6----------------------->

![](img/f6e2ef21b9c5c8fbd57d4adcd6400979.png)

Photo by [Mohammad Rahmani](https://unsplash.com/@afgprogrammer?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

插座。IO 是一个库，支持服务器和客户端之间的实时、双向和基于事件的通信。这个库提供了一个 Node.js 服务器和一个客户机实现，我们可以用它来构建我们的系统。除了节点服务器，还有其他服务器实现，包括 Java 和 Python。还有许多客户机实现可以与套接字服务器通信。这使您能够用不同的技术构建客户端和服务器端。您可以在这里找到从[到](https://socket.io/docs/v4)的实现列表。

# 插座是如何？IO 工作？

要正确理解，您可能需要了解两个基本主题——web socket、单向和双向通信等。让我们逐一介绍。

# WebSocket

WebSocket 只不过是一个计算机通信协议。它通过单个 TCP 提供全双工通信信道。WebSocket 不同于 HTTP，尽管这两种协议都位于 OSI 模型的第 7 层，并且依赖于 TCP。WebSocket 以较低的开销实现了 web 服务器和 web 客户端之间的交互。它从第一次建立连接时就保持连接打开，并允许 web 服务器向客户机发送内容，而无需客户机首先请求。所以使用 WebSocket 的全双工通信特性来了。web 服务器和 web 客户端都使用该连接以全双工方式进行实时数据传输。有一些半双工替代方案可以实现这一功能，但 WebSocket 以更标准的方式提供这一功能，并且开销最小。

# 单向和双向通信

单向意味着数据只在一个方向上流动，而双向意味着数据在两个方向上流动。HTTP 是单向的，客户端发送请求，服务器做出相应的响应。我们可以将 RESTful 服务视为依赖于 HTTP 协议的单向通信。当客户机向服务器发送请求时，服务器以 HTTP 格式接收请求，并向客户机发送响应。发送响应后，连接关闭。每次客户端发送 HTTP 请求时，都会建立一个新的连接，在得到响应后，连接就会终止。因此，这个过程是单向的，并且这个连接通道不能被服务器或客户机用于以后的通信。另一方面，WebSocket 协议是双向的。它是一种全双工协议，用于相同的客户端-服务器通信场景。它是一个有状态的协议，客户端和服务器之间的连接被维护以备将来使用。例如，假设客户机-服务器进行了握手并创建了一个连接。该连接将由协议保持活动状态，直到被任何一方(服务器和客户端)终止。这个信道可以用于双方的通信。客户端可以向服务器发送一些内容，服务器也可以向客户端发送内容。消息交换将以双向模式进行。

# 使用 Socket.io 和 Express 的基本应用程序

Socket.io 能够单独处理设置了可能情况的服务器，但是通常使用带有 socket.io 的 Express framework 来呈现一些 HTTP 请求。几乎在每一个应用中，我们都可能需要这两个方面。例如，我们的套接字可能需要一个管理仪表板。IO 应用。任何 HTTP 框架都需要 Express。虽然可以用 Socket 来开发这种东西。IO，在这些情况下使用 HTTP 框架也更常见。你可以从[这里](https://socket.io/get-started/basic-crud-application/)看到一个用 Socket.io 开发的纯 CRUD 应用，但是在这篇文章里，我会用 Socket 解释一个项目。木卫一和快递一起。它可能会给你一个实际应用的想法。

# 创建项目和安装依赖项

我们需要创建一个普通节点项目，并安装 **express** 和 **socket.io** 库。

```
npm init --yes
npm i express socket.io
```

# 创建 express 服务器并集成 Socket。超正析象管(Image Orthicon)

```
const http = require('http');
const express = require('express');
const app = express();
const server = http.createServer(app);
const { Server } = require('socket.io');
const io = new Server(server);server.listen(3000, () => {
    console.log('listening on *:3000');
});
```

# 提供 HTML

插座。IO 由两部分组成，一部分是服务器，另一部分是加载到浏览器上的客户端库。要在浏览器上加载客户端库，我们需要执行以下操作，

```
<script src="/socket.io/socket.io.js"></script>
<script>
    var socket = io();
</script>
```

这就是加载[套接字所需的全部内容。io-client](https://github.com/socketio/socket.io-client) ，公开一个 **io** 全局，然后连接。让我们创建一个包含表单和列表的完整 HTML 文件。这个 HTML 文件将被提供给浏览器或客户端，它们将使用它与服务器进行通信。

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <ul id="notices"></ul>
    <form id="form" action="">
        <input id="input" autocomplete="off" /><button>Send</button>
    </form> <script src="/socket.io/socket.io.js"></script>
    <script>
      var socket = io(); var messages = document.getElementById('notices');
      var form = document.getElementById('form');
      var input = document.getElementById('input'); form.addEventListener('submit', function(e) {
        e.preventDefault();
        if (input.value) {
          socket.emit('new-notice', input.value);
          input.value = '';
        }
      }); socket.on('add-to-board', function(msg) {
        var item = document.createElement('li');
        item.textContent = msg;
        messages.appendChild(item);
        window.scrollTo(0, document.body.scrollHeight);
      });
    </script>
</body>
</html>
```

请注意，我们没有指定要连接的后端服务器主机，因为默认情况下，它会尝试连接到为页面提供服务的主机。我们还可以在 io()函数中指定服务器地址。

```
var socket = io();
```

注意 index.html 文件的两个部分， **socket.emit()** 和 **socket.on()** 。这两个方法用于发送带有数据的命名事件和从服务器监听命名事件。

现在，让我们更新 index.js 文件，以便为 index.html 页面提供服务，并在以后从浏览器接受事件。

```
const http = require('http');
const express = require('express');
const app = express();
const server = http.createServer(app);
const { Server } = require('socket.io');
const io = new Server(server);// serving the html page to browser
app.get('/', (req, res) => {
    res.sendFile(__dirname + '/index.html');
})// listen for event's form client
io.on('connection', (socket) => {
    // listen specific named event
    socket.on('new-notice', (data) => {
        io.emit('add-to-board', data);
    });
});server.listen(3000, () => {
    console.log('listening on *:3000');
});
```

# 运行服务器

```
node index.js
```

这将运行服务器。这个服务器可以拥有 Restful 方法以及 Web 套接字连接。您可以根据需要添加任何命名的事件或 API 端点。您还可以使用集群来提高性能。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)