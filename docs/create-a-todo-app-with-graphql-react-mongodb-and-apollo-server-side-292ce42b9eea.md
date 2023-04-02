# 用 GraphQL，React，MongoDB 和 Apollo 创建一个 Todo App(服务器端)

> 原文：<https://javascript.plainenglish.io/create-a-todo-app-with-graphql-react-mongodb-and-apollo-server-side-292ce42b9eea?source=collection_archive---------2----------------------->

## 了解如何使用 GraphQL 进行 CRUD 操作

在本文中，我们将学习如何使用 GraphQL、React、MongoDB 和 Apollo 创建一个 todo 应用程序。本文将关注服务器端。我们将像获取单个待办事项一样进行查询，并获取所有待办事项。并进行类似更新特定 todo 和删除 todo 的变异。

[第一部分:用 GraphQL、React、MongoDB 和 Apollo(服务器端)创建一个 Todo 应用](/create-a-todo-app-with-graphql-react-mongodb-and-apollo-server-side-292ce42b9eea)

[第二部分:用 GraphQL、React、MongoDB 和 Apollo(客户端)创建一个 Todo 应用](https://ckmobile.medium.com/create-a-todo-app-with-graphql-react-mongodb-and-apollo-client-side-8a946d869014)

![](img/babc66f056e4bb08851aaf5aa52fa9f9.png)

源代码:

[](https://ckmobile.gumroad.com/l/graphql-apollo-mongodb-todo-app) [## 用 React GraphQL MongoDB 和 Apollo 创建一个 Todo 应用程序

### 为什么选择 GraphQL？GraphQL 使我们能够通过一个查询得到我们想要东西。例如，我们通常获取一个对象数组…

ckmobile.gumroad.com](https://ckmobile.gumroad.com/l/graphql-apollo-mongodb-todo-app) 

首先，我们需要创建一个服务器文件夹

![](img/f74c5b74451fe3c542438e7526992fef.png)

进入该文件夹并键入 npm init -y。它将创建 package.json

![](img/aa17297d754774896c979a4c8f7588e9.png)

进入终端，安装 express、apollo-server-express、graphql 和 mongoose。

如果您还没有安装 nodemon，最好安装 nodemon，它允许在文件发生变化时自动重启服务器。

```
npm i express apollo-server-express graphql mongoosenpm i nodemon -g
```

然后我们转到 package.json，添加一行

```
"type":"module",
```

这意味着我们可以使用导入和导出语法。

现在我们可以导入 express，即阿波罗服务器。

创建一个名为 welcome 的简单查询，它将向 ckmobile 返回 welcome。所以在 typeDefs 下，我们输入

```
type Query{welcome:String}
```

我们希望它会返回一个字符串。

然后在解析器下，我们键入

```
Query: {welcome: () => {return "Welcome to ckmobile"}}
```

如果用户发出查询“Welcome ”,它将生成返回“Welcome to ckmobile”的响应。

之后，我们创建一个 init 服务器函数。在这个函数下，我们将 typeDefs 和解析器传递给 apollo 服务器。

在应用中间件之前启动 apollo 服务器。创建一个简单的响应，以便我们稍后可以检查服务器是否成功启动。

```
app.use((req, res) => {res.send("Server started")})
```

这样做是为了将来的部署做好准备。

```
create PORT = process.env.PORT || 5000;
```

最后，执行“initServer”函数。

```
import express from 'express';import {ApolloServer} from 'apollo-server-express';const typeDefs = gql`type Query{welcome:String}`const resolvers = {Query: {welcome: () => {return "Welcome to ckmobile"}}}async function initServer() {const app = express();const apolloServer = new ApolloServer({typeDefs, resolvers})await apolloServer.start();apolloServer.applyMiddleware({ app });app.use((req, res) => {res.send("Server started")})const PORT = process.env.PORT || 5000;app.listen(PORT, () => console.log(`Express server is running on port ${PORT}`))}initServer()
```

如果我们去

```
[http://localhost:5000](http://localhost:5000/graphql)
```

它将返回“服务器已启动”

![](img/d5fdb57c32815b183768552da8724f92.png)

如果我们说

[http://localhost:5000/graph QL](http://localhost:5000/graphql)

它将转到 GraphQL UI 页面

![](img/0688141c2135717e0262d1e03384d805.png)

按下“查询您的服务器”按钮。

![](img/544703dcde8be83294dd3a1ef49bbac3.png)

如果我们打字

```
query{welcome}
```

它会回来的

```
{"data": {"welcome": "Welcome to ckmobile"}}
```

## 将 resolvers.js 和 typeDefs.js 分开

对于 resolvers.js，我们删除了以下代码

```
const resolvers = {Query: {welcome: () => {return "Welcome to ckmobile"}}}export default resolvers
```

对于 typeDefs.js

```
const {  gql } = require('apollo-server-express');const typeDefs = gql`type Query{welcome:String}`export default typeDefs
```

我们将这两个文件导入 index.js

```
import express from 'express';import typeDefs from './typeDefs.js';import resolvers from './resolvers.js';import {ApolloServer} from 'apollo-server-express';async function initServer() {const app = express();const apolloServer = new ApolloServer({typeDefs, resolvers})await apolloServer.start();apolloServer.applyMiddleware({ app });app.use((req, res) => {res.send("Server started")})const PORT = process.env.PORT || 5000;app.listen(PORT, () => console.log(`Express server is running on port ${PORT}`))}initServer()
```

然后我们再次运行 [http://localhost/grahql](http://localhost/grahql) ，它将返回到 GraphQL UI，并且仍然工作。

![](img/8f2f5fb3727a007d591f14221f7bdae4.png)

## 创建 Todo 模型

创建一个名为“模型”的新文件夹。在此文件夹下，创建 Todo.js。

我们用 Mongoose 创建一个模式，根据需要设置标题，标题和细节的数据类型是 string，日期的数据类型是 date。

我们还启用了时间戳,“createdAt”和“updatedAt”属性将被添加到模式中。

```
import mongoose from 'mongoose';const Schema = mongoose.Schema;const todoSchema = new Schema({title: {type: String,required: true},detail: String,date:Date}, { timestamps: true });const Todo = mongoose.model('todo', todoSchema)export default Todo;
```

## 连接到 MongoDB

在连接到 MongoDB 之前，您应该已经注册了 MongoDB atlas。如果您还没有这样做的经验，请参考下面的视频，了解如何设置 MongoDB。

创建一个. env 文件

![](img/3a13c93b6382dbac724fed99fff000fa.png)

在里面。环境文件

```
mongodb=mongodb+srv://ckmobile:ckmobilepassword@nodetuts.qwlpv.mongodb.net/post-database?retryWrites=true&w=majority
```

然后安装两个包，一个是 cors，它允许我们用不同的选项启用 CORS。另一个是可以读取。env 文件并解析内容。

```
npm i cors dotenv
```

去 index.js，我们导入 mongoose，cors，和 dotenv 包。

```
import express from 'express';import typeDefs from './typeDefs.js';import resolvers from './resolvers.js';import {ApolloServer} from 'apollo-server-express';**import mongoose from 'mongoose';****import cors from 'cors';****import dotenv from 'dotenv';**async function initServer() {const app = express();**app.use(cors());****dotenv.config();**const apolloServer = new ApolloServer({typeDefs, resolvers})await apolloServer.start();apolloServer.applyMiddleware({ app });app.use((req, res) => {res.send("Server started")})const PORT = process.env.PORT || 5000;**try {****await mongoose.connect(process.env.mongodb, { useNewUrlParser: true, useUnifiedTopology: true })****console.log(`Mongoose connected on port ${PORT}`)****} catch (error) {****console.log(error)****}**app.listen(PORT, () => console.log(`Express server is running on port ${PORT}`))}initServer();
```

![](img/6395d3398ee2ff0133dd6ebaf81a2928.png)

保存后，命令行将显示上面的日志，这意味着它可以连接到 MongoDB。

## 获取所有待办事项

要获取所有的 Todo，请进入 typeDefs.js。在查询中，创建 getTodos 并期望返回 Todo 数组。

但是我们还没有创建 Todo。因此，我们需要添加带有 id、标题、细节和日期的类型 Todo。

对于 typeDefs

```
import {  gql } from 'apollo-server-express';const typeDefs = gql`scalar Datetype Todo{id:IDtitle:Stringdetail:Stringdate:Date}type Query{welcome:StringgetTodos:[Todo]}`export default typeDefs
```

在 resolvers.js 中，我们从 MongoDB 返回 todos。

对于 resolvers.js

```
import Todo from "./models/Todo.js";const resolvers = {Query: {welcome: () => {return "Welcome to ckmobile"},getTodos:async()=>{const todos = await Todo.find()return todos}}}export default resolvers; 
```

最后，我们尝试在 graphqlUI 上进行查询。我们可以看到这是一个空数组，这很正常，因为还没有 todos。

![](img/261cc3630ab841d5b07cde1f3459fd6c.png)

## 创建待办事项

转到 typeDefs.js，我们添加一个名为“addTodo”的变异。然后我们将标题、细节和日期传递给 addTodo。它应该返回类型 Todo。

```
import {  gql } from 'apollo-server-express';import { GraphQLScalarType, Kind } from 'graphql';const typeDefs = gql`scalar Datetype Todo{id:IDtitle:Stringdetail:Stringdate:Date}type Query{welcome:StringgetTodos:[Todo]}**type Mutation{****addTodo(title:String, detail:String,date:Date):Todo****}**`export default typeDefs
```

转到 resolvers.js

在变异部分，我们基于用户传递的参数创建了一个新的 todo。将使用 Todo.save()保存新创建的 todo。

```
import Todo from "./models/Todo.js";const resolvers = {Query: {welcome: () => {return "Welcome to ckmobile"},getTodos:async()=>{const todos = await Todo.find()return todos}},Mutation:{addTodo:async(root,args)=>{const newTodo = new Todo({title:args.title,detail:args.detail,date:args.date})await newTodo.save();return newTodo;},}}export default resolvers;
```

![](img/b12941c6548c040cd668300940fa01ac.png)

如果我们在 GraphQL 用户界面中键入以下内容

```
mutation{addTodo (title:"first todo"detail:"first detail first detail first detail"date:"2021-9-10"){idtitledetaildate}}
```

我们会得到

```
{"data": {"addTodo": {"id": "6131ce9079d2b4a8d9598bd0","title": "first todo","detail": "first detail first detail first detail","date": "2021-09-09T16:00:00.000Z"}}}
```

![](img/f28a4de94ba7fcf49bd12569ea025260.png)

在 MongoDB 内部我们也可以看到这一点。

如果我们在 GraphQL UI 中键入以下内容，并尝试再次获取 todos。

```
query{getTodos{titledetaildate}}
```

这次我们将得到一个 todos 数组，而不是一个空数组。

```
{"data": {"getTodos": [{"title": "first todo","detail": "first detail first detail first detail","date": "2021-09-09T16:00:00.000Z"}]}}
```

## 获得一个待办事项

来获取单个 todo，就像前面的过程一样。我们进入 typeDefs.js，添加查询 getTodo

```
import {  gql } from 'apollo-server-express';const typeDefs = gql`scalar Datetype Todo{id:IDtitle:Stringdetail:Stringdate:Date}type Query{welcome:StringgetTodos:[Todo]**getTodo(id:ID):Todo**}
```

resolvers.js 内部

```
import Todo from "./models/Todo.js";const resolvers = {Query: {welcome: () => {return "Welcome to ckmobile"},getTodos:async()=>{const todos = await Todo.find()return todos},**getTodo:async(root,args)=>{****return await Todo.findById(args.id)****}****},**Mutation:{addTodo:async(root,args)=>{const newTodo = new Todo({title:args.title,detail:args.detail,date:args.date})await newTodo.save();return newTodo;},}}export default resolvers;
```

如果我们在 GraphQL UI 中运行以下查询。复制待办事项之一的 id

```
query{getTodo(id:"6131ce9079d2b4a8d9598bd0"){titledetail}}
```

然后我们将获得该 todo 的所有属性。

```
{"data": {"getTodo": {"title": "first todo","detail": "first detail first detail first detail"}}}
```

## 删除待办事项

Delete todo 非常类似于 get single todo，这也需要一个 ID。

typeDefs.js 内部

```
type Mutation{addTodo(title:String, detail:String,date:Date):TododeleteTodo(id:ID):String}
```

在 resolvers.js 中，我们将找到 id 并删除该特定的 todo。

```
Mutation:{addTodo:async(root,args)=>{const newTodo = new Todo({title:args.title,detail:args.detail,date:args.date})await newTodo.save();return newTodo;},deleteTodo:async(root,args)=>{await Post.findByIdAndDelete(args.id)return "The todo is deleted"},}
```

现在我们可以检查它是否在 GraphQL UI 中工作

我们键入以下内容

```
{"data": {"getTodos": [{"id": "6131ce9079d2b4a8d9598bd0","title": "first todo","detail": "first detail first detail first detail","date": "2021-09-09T16:00:00.000Z"},{"id": "6131d5351ef74bdaf301cdba","title": "second todo","detail": "second detail second detail second detail","date": "2021-09-12T16:00:00.000Z"}]}}
```

我们可以看到它返回两个 todos

```
{"data": {"getTodos": [{"id": "6131ce9079d2b4a8d9598bd0","title": "first todo","detail": "first detail first detail first detail","date": "2021-09-09T16:00:00.000Z"},{"id": "6131d5351ef74bdaf301cdba","title": "second todo","detail": "second detail second detail second detail","date": "2021-09-12T16:00:00.000Z"}]}}
```

如果我们执行以下命令

```
mutation{deleteTodo(id:"6131ce9079d2b4a8d9598bd0")}
```

它会回来的

```
{"data": {"deleteTodo": "The todo is deleted"}}
```

如果我们再次执行 getTodos，它现在只有一个 todo。

```
{"data": {"getTodos": [{"id": "6131d5351ef74bdaf301cdba","title": "second todo","detail": "second detail second detail second detail","date": "2021-09-12T16:00:00.000Z"}]}}
```

## 更新待办事项

为了更新 todo，我们不仅需要 id，还需要其他属性，如标题、细节和日期。

typeDefs.js 内部

```
type Mutation{addTodo(title:String, detail:String,date:Date):TododeleteTodo(id:ID):StringupdateTodo(id:String,title:String,detail:String,date:Date):Todo}
```

回到 resolvers.js，我们从参数中获得 id、标题、细节和日期。然后，我们创建一个更新的 todo 对象，该对象已准备好将值传递给它。

接下来，我们检查是否有未定义的值，这意味着用户没有输入新值。那我们就用原来的值。

获得所有值后，我们将使用提供的 id 找到 todo，并用最新的值进行更新。

resolvers.js 内部

```
Mutation: {addTodo: async (root, args) => {const newTodo = new Todo({ title: args.title, detail: args.detail, date: args.date })await newTodo.save();return newTodo;},deleteTodo: async (root, args) => {await Todo.findByIdAndDelete(args.id)return "The todo is deleted"},**updateTodo: async (root, args) => {****const { id, title, detail, date } = args;****const updatedTodo = {};****if (title !== undefined) {****updatedTodo.title = title****}****if (detail !== undefined) {****updatedTodo.detail = detail****}****if (date !== undefined) {****updatedTodo.date = date****}****const todo = await Todo.findByIdAndUpdate(****id,****{ title, detail, date },****{ new: true }****)****return todo;****},****}**}
```

如果我们在 GraphQL UI 中键入以下内容

```
mutation{updateTodo(id:"6131d5351ef74bdaf301cdba",title:"This2 is a new titl22e2"){idtitle}}
```

它会回来的

```
{"data": {"updateTodo": {"id": "6131d5351ef74bdaf301cdba","title": "This2 is a new titl22e2"}}}
```

如果我们再次运行 getTodos 查询

```
query{getTodos{idtitledetaildate}}
```

您可以看到标题已更新

```
{"data": {"getTodos": [{"id": "6131d5351ef74bdaf301cdba","title": "This2 is a new titl22e2","detail": "second detail second detail second detail","date": "2021-09-12T16:00:00.000Z"}]}}
```

如果你喜欢这个故事，你可能也喜欢中等会员。一个月才 5 美元(一杯咖啡的价格！)但是它会在支持你最喜欢的作家的同时，给你无限的接触故事的机会。如果你用[这个链接](https://ckmobile.medium.com/membership)注册，我会赚一小笔佣金。谢谢！

# 关注我们: [YouTube](https://www.youtube.com/channel/UCu4-4FnutvSHVo9WHvq80Ww?sub_confirmation=1) ， [Medium](https://ckmobile.medium.com/) ， [Udemy](https://www.udemy.com/user/cyruschan2/) ， [Linkedin](https://www.linkedin.com/company/ckmobi/) ， [Twitter](https://twitter.com/ckmobilejavasc1) ， [Instagram](https://www.instagram.com/ckmobile8050) ， [Gumroad](https://app.gumroad.com/ckmobile) ， [Quora](https://ckmobile.quora.com/) ， [Telegram](https://t.me/ckmobi)

加入分支机构赚钱

[https://ckmobile.gumroad.com/affiliates](https://ckmobile.gumroad.com/affiliates)

*更多内容请看*[***plain English . io***](http://plainenglish.io/)