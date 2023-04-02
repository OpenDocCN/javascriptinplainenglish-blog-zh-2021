# 如何使用 Node Express 构建 API 数据分页

> 原文：<https://javascript.plainenglish.io/how-to-build-api-data-pagination-using-node-express-58d31d6b9e2a?source=collection_archive---------8----------------------->

![](img/bc81e370c812e9a5200b38abe9f1d0e7.png)

Image by [AIOSEO](https://aioseo.com/pagination-seo/)

**Node Express** 是一个 JavaScript 框架，可以用来开发各种 web 应用。它可以用于开发各种客户端应用程序(web 应用程序或移动应用程序)可以使用的 web API。**数据分页**必须在包含长数据列表的 API 响应上实现。本文将逐步向您展示如何在 Node Express APIs 中实现数据分页。

这个例子将是一个新闻应用程序。

**第一步:**创建一个名为 ***newsapp*** 的空文件夹。

```
$ mkdir newsapp
cd newsapp
$ npm init
```

**第二步:**在文件夹中设置快递。[阅读此处获取信息](https://expressjs.com/en/starter/installing.html)

```
$ npm install express --save
```

**第三步:**将 mongoose 安装到项目中。

```
$ npm install mongoose --save
```

**第四步:**在根文件夹中创建一个名为 *article.js* 的文件。使用 requite 函数导入 *article.js* 文件中的猫鼬。

```
*const* mongoose = require('mongoose')
```

**第 5 步:**创建一个模式，用*标题*和*内容*属性表示新闻文章。

```
*const* mongoose = require('mongoose')*const* ArticleSchema = new mongoose.Schema({
   title: { 
    type: String,
    required: true
   },
   content: {
    type: String,
    required: true
 }})
```

下一步是将我们的模式编译成一个模型，然后导出它。[阅读此处了解更多信息](https://mongoosejs.com/docs/index.html)

```
*module*.*exports* = mongoose.model('Article', ArticleSchema)
```

最终的 ***article.js*** 文件会是这样的

```
*const* mongoose = require('mongoose')*const* ArticleSchema = new mongoose.Schema({
   title: { 
    type: String,
    required: true
   },
   content: {
    type: String,
    required: true
 }})*module*.*exports* = mongoose.model('Article', ArticleSchema)
```

**第七步:**在 index.js 文件中，导入**mongose**，使用 *require()* 函数 **express** 。

```
*const* express = require('express')
*const* newsapp = express()
*const* mongoosedb = require('mongoose')
```

**步骤 8:** 将 *articles.js* 文件导入到 *index.js* 文件中。

```
*const* article = require('./articles')
```

**第九步:**连接 MongoDB 数据库。

```
mongoose.connect('mongodb://localhost:27017/test', {useNewUrlParser: true, useUnifiedTopology: true});
```

步骤 10: 使用一个承诺，显示一个来自数据库的新闻文章列表。

```
*const* db = mongoose.connection
db.once('open', *async* () => {
  if (await article.countDocuments().exec() > 0) returnPromise.all([article.create({ title: 'article 1', 
                content: "News content for article 1" }),article.create({ title: 'article 2', 
                content: "News content for article 2" }),article.create({ title: 'article 3', 
                content: "News content for article 3" }),article.create({ title: 'article 4', 
                content: "News content for article 4" }),article.create({ title: 'article 5', 
                content: "News content for article 5" }),article.create({ title: 'article 6', 
                content: "News content for article 6" }),article.create({ title: 'article 7', 
                content: "News content for article 7" }),article.create({ title: 'article 8', 
                content: "News content for article 8" }),article.create({ title: 'article 9', 
                content: "News content for article 9" }),article.create({ title: 'article 10', 
                 content: "News content for article 10" }),article.create({ title: 'article 11', 
                content: "News content for article 11" }),article.create({ title: 'article 12', 
                content: "News content for article 12" }),article.create({ title: 'article 13', 
                content: "News content for article 13" })]).then(() => console.log('Added Articles'))})
```

**步骤 11:** 创建一个名为***paginated news articles()***的函数，该函数将接受文章模型作为参数。在 return 语句中，创建三个名为 *querypage* 、 *querylimit* 和 *paginatedArticlesList* 的变量。 *querypage* 和 *querylimit* 将存储从每个 URL 查询传递的页面和限制。*分页文章列表*将存储所有分页的文章。

```
*function* paginatedNewsArticles(*model*) { return *async* (*request*, *response*, *next*) => {
     *const* querypage = parseInt(request.query.page)
     *const* querylimit = parseInt(request.query.limit)
}}
```

**步骤 12:** 接下来添加两个 if 语句，将检查页码以确定上一页和下一页。该信息将在 JSON 响应中与*paginated article list*一起发送。

```
*const* firstIndex = (page - 1) * limit
*const* lastIndex = page * limitif (firstIndex > 0) {
      paginatedArticlesList.previous = {
      previouspage: page - 1,
      limit: limit
    }
  }if (lastIndex < await model.countDocuments().exec()) {
      paginatedArticlesList.next = {
       nextpage: page + 1,
       limit: limit
     }}
```

最终的 ***index.js*** 文件会是这样的。

```
*const* express = require('express')
*const* newsapp = express()
*const* mongoosedb = require('mongoose')
*const* article = require('./articles')mongoose.connect('mongodb://localhost/pagination', { useNewUrlParser: true, useUnifiedTopology: true })*const* db = mongoose.connectiondb.on('error', console.error.bind(console, 'connection error:'));
db.once('open', *async* () => {
  if (await article.countDocuments().exec() > 0) returnPromise.all([ article.create({ title: 'article 1', 
                content: "News content for article 1" }), article.create({ title: 'article 2', 
                content: "News content for article 2" }), article.create({ title: 'article 3', 
                content: "News content for article 3" }), article.create({ title: 'article 4', 
                content: "News content for article 4" }), article.create({ title: 'article 5', 
                content: "News content for article 5" }), article.create({ title: 'article 6', 
                content: "News content for article 6" }), article.create({ title: 'article 7', 
                content: "News content for article 7" }), article.create({ title: 'article 8', 
                content: "News content for article 8" }), article.create({ title: 'article 9', 
                content: "News content for article 9" }), article.create({ title: 'article 10', 
                 content: "News content for article 10" }), article.create({ title: 'article 11', 
                content: "News content for article 11" }), article.create({ title: 'article 12', 
                content: "News content for article 12" }), article.create({ title: 'article 13', 
                content: "News content for article 13" })]).then(() => console.log('Added Articles'))})newsapp.get('/article', paginatedNewsArticles(article), (*request*, *response*) => {response.json(response.paginatedResults)})*function* paginatedNewsArticles(*model*) { return *async* (*request*, *response*, *next*) => {
    *const* querypage = parseInt(request.query.page)
    *const* querylimit = parseInt(request.query.limit)
    *const* firstIndex = (page - 1) * limit
    *const* lastIndex = page * limit *const* paginatedArticlesList = {} if (firstIndex > 0) {
       paginatedArticlesList.previous = {
       previouspage: page - 1,
       limit: limit
     }
   } if (lastIndex < await model.countDocuments().exec()) {
       paginatedArticlesList.next = {
       nextpage: page + 1,
       limit: limit
     }
}try {
   paginatedArticlesList.results = await
   model.find().limit(limit).skip(firstIndex).exec()
   response.paginatedArticles = paginatedArticlesList
   next()
} catch (e) {
   response.status(500).json({ message: e.message })
}
}}newsapp.listen(3000)
```

测试应用程序

现在我们有了。我希望你已经发现这是有用的。我会带着更多有趣的文章回来。感谢您的阅读。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)