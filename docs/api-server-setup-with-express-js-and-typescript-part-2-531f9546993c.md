# 使用 Express.js 和 TypeScript 设置 API 服务器

> 原文：<https://javascript.plainenglish.io/api-server-setup-with-express-js-and-typescript-part-2-531f9546993c?source=collection_archive---------1----------------------->

## 第 2 部分:创建模型、路由器和控制器

![](img/4727d56770d6c554640bc7915f101833.png)

在上一个教程中，我们创建了一个非常基本的 Express.js 的“Hello World”实现。在本系列的这一部分中，我们将创建一个模型、路由器和控制器。目标是创建一个电影查找 API。

打开我们在[上一个教程](https://wardprice.medium.com/api-server-setup-with-express-js-mongodb-and-typescript-part-1-bea7e4f5b526)里做的 app me。如果你现在刚刚加入，你可以从我的 github 上克隆下来，这里。

好了，现在我们准备好了，首先让我们安装`body-parser`。尽管到目前为止我们只有一个非常简单的服务器，但是当我们开始添加来自和去往`body-parser`的请求时，我们的生活会变得更加容易。它获取原始请求，提取我们需要在服务器中处理的数据，并将其放在`req.body`上。

# 安装 bodyParser

在您的终端中运行以下命令。

```
$ npm i body-parser
```

为了将它合并到我们的服务器中，让我们通过将这一行添加到我们的`index.ts`文件的顶部来导入它。

```
import bodyParser from 'body-parser'
```

现在，在当前的`app.get()`语句之上，我们添加了以下两个命令。

```
app.use(bodyParser.json())
app.use(bodyParser.urlencoded({ extended: true }))
```

这是做什么的？`app.use`安装以下函数，如果路径与请求中指定的路径匹配，将运行该函数。函数`bodyParser.json()`将解析 json 请求中的文本，并将该对象装载到`req.body`中。下一行，`bodyParser.urlencoded({ extended: true })`将文本解析为 URL 编码的数据，并将结果对象装载到`req.body`上，这对于 post 请求非常重要，因为 URL 编码的数据是浏览器从表单发送 post 请求的方式。更多信息请查看[这个堆栈溢出帖子](https://stackoverflow.com/questions/38306569/what-does-body-parser-do-with-express/48364778)。

现在我们，因为我们要添加一个路由器，继续删除这条线。

```
app.use('/', (req, res) => {
  res.send('Hello World!')
})
```

# 最初设置路由器

在`src`文件夹中创建 3 个文件夹，`routes`，`controllers`，`models`。我们将利用 [MVC 模式](https://en.wikipedia.org/wiki/Model–view–controller)创建这个 api，但是当然没有视图。

在 routes 文件夹中创建文件`index.ts`。我们将导入`express`，然后创建路由器并将其导出，以便我们可以在`src/index.ts`中使用它。

```
import express from 'express'const router = express.Router()export default router
```

在`src/index.ts`文件中导入我们新创建的路由器。

```
import routes from './routes'
```

就在`bodyParser`语句的下面加上这一行。

```
app.use(routes)
```

这个路由器索引还没有做任何事情，但那是因为我们没有路由！接下来让我们创建控制器。

*我知道这有点令人困惑，我们现在有两个* `*index.ts*` *文件，但是在 Node.js 中，当你将一个文件夹导入到一个组件时，如果没有指定文件，Node.js 将查找一个* `*index.ts*` *文件。此外，正如您将看到的，我们刚刚创建的* `routes/index.ts` *文件将充当相应控制器的切换面板。稍后会有更多的介绍…*

# 设置控制器

在控制器文件夹中添加一个文件名`moviesController.ts`。这个文件将处理访问某个端点时发生的逻辑。现在，在这个文件中，我们必须导入 express 要使用的类型。

在文件的顶部添加…

```
import { Request, Response, NextFunction } from 'express'
```

现在，为了给路由器做好准备，让我们再次创建“Hello World”响应。

创建一个名为`getHello`的函数。我们将创建一个普通的同步函数，因为这将是简单而直接的。在本系列的下一部分，我们将添加 MongoDB 作为我们的数据库。然后我们将使这些函数异步。

```
function getHello(req: Request, res: Response, next: NextFunction) {
  res.send('Hello World!')
}
```

我们必须导出该函数，以便在路由器中使用。在文件的底部添加以下内容…

```
export default { getHello }
```

# 将路线连接到控制器

在 routes 文件夹中创建一个名为`movieRoutes.ts`的新文件，导入 express 并导入我们刚刚创建的控制器，以及像我们之前在`routes/index.ts`文件中所做的那样创建一个路由器。

```
import express form 'express'
import moviesController from '../controllers/movieController'const router = express.Router()export default router
```

当我们到达`'/'`端点时，我希望它从我们的`getHello`函数返回`Hello World`。在`export default router`行之前添加以下行。

```
router.get('/', movieController.getHello)
```

好吧，就差一点了！现在我们需要做的就是将它合并到`routes/index.ts`中。导入`movieRoutes.ts`文件，然后利用路由器允许它被使用。

```
import movieRoutes from './movieRoutes'router.use('/api/v1/movies', movieRoutes)
```

太好了。现在如果我们在终端运行`npm start`。然后导航到`localhost:3000/api/v1/movies`它应该返回`Hello World!`。我们现在有了一个更模块化、更容易维护的基础。

你可能会问自己，为什么我们为`moviesController`创建了一个`routes/index.ts`文件，然后又创建了另一个路由器文件？嗯，这是为未来而建。如果 api 真的要升级到新版本，我们需要做的就是在新电影控制器的 routes 文件中设置该路由。这将一切分开，所以更容易找到快速有效地做出改变的地方。

下次，我们添加 MongoDB！

[克隆完整代码](https://github.com/woink/expressBlog/tree/8400e6a999491bc5aeb384d326dafe718f0be617)

快乐编码！！

# 系列教程

[**第 1 部分:“你好，世界！”**](https://wardprice.medium.com/api-server-setup-with-express-js-mongodb-and-typescript-part-1-bea7e4f5b526)

**第 2 部分:设置路由器**

[**第 3 部分:连接 MongoDB**](https://wardprice.medium.com/api-server-setup-with-express-js-typescript-and-mongodb-part-3-b02409f072e4)