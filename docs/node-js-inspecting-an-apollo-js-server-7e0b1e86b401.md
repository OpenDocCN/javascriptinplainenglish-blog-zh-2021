# Node.js |检查 Apollo.js 服务器

> 原文：<https://javascript.plainenglish.io/node-js-inspecting-an-apollo-js-server-7e0b1e86b401?source=collection_archive---------17----------------------->

![](img/4dd7a0ba5de7c008681f95c8ecfa8d81.png)

Photo by [Raoul Droog](https://unsplash.com/@raouldroog?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

要继续操作，运行本文末尾的文件，打开浏览器，转到服务器注销的 URL。GraphQL playground 将自动提供给你的浏览器。

在下面的代码中，我们使用 ApolloServer 构造函数实例化了一个 Apollo.js 服务器。构造函数将选项对象作为参数，用于配置服务器。请参考以下链接，查看所有可能的选项和配置。

API 参考:
[https://www . apollographql . com/docs/Apollo-server/API/Apollo-server/](https://www.apollographql.com/docs/apollo-server/api/apollo-server/)

```
const { ApolloServer, gql } = require(`apollo-server`);const mockData = `qux`;new ApolloServer({
  typeDefs,
  resolvers,
  context({ req, res }) {
    return { mockData, req, res };
  },
})
```

在上面的代码中，您可以看到我们只关心三个选项:typeDefs、resolvers 和 context。TypeDefs 表示服务器的 GraphQL 模式。解析器是映射到模式的函数。响应由解析器的解析器函数生成，这些函数按照 typeDefs 定义的顺序执行。

Context 返回一个对象，该对象作为变量传递给每个解析器函数的 context 参数。

我们使用模式定义语言来创建我们的类型定义。当我们创建我们的模式时，我们创建了一个供服务器遵循的映射。该映射导致一系列解析器功能执行。

有三种特殊的类型，它们也是对应于三种可能的客户端操作的入口点:查询、变异和订阅。你可以把这些类型看作旅程的开始。和它们的子对象作为旅程的下一步。

模式定义语言有两种类型:基本类型和对象类型。基本类型表示单个值，而对象类型是具有字段的类型。嵌套的对象类型表示子对象和父对象之间的关系。父项的解析函数总是在子项的解析函数之前执行，依此类推。嵌套最多的对象类型将对应于最后一次执行的解析器函数。

在下面的示例代码中，Query 是入口点，我们可以预期查询解析器对象有两个函数 bar 和 foo。foo 的解析函数返回 baz 的父对象，foo 没有父对象。foo 查询的解析器执行将通过在查询对象上搜索与 foo 匹配的属性开始，如果查询要求 baz 属性，则下一个要执行的解析器函数将在名为 Foo 的对象上执行，并且该函数将存在于名为 baz 的属性上。根据 baz 的类型定义，baz，Baz 函数将返回一个具有名为 qux 的单个属性的对象，该属性保存一个字符串值。

```
const typeDefs = gql`
type Query {
  bar: String!
  foo(id: Int!): Foo!
}type Foo {
  id: Int!
  baz: Baz!
}type Baz {
  qux: String
}
`;// The Resolver Object:const resolvers = {
 Query: {
   foo: (parent, args, context, info) => {
     return { id: args.id };
   },
   bar: () => `bar`,
 },
 Foo: {
   baz: (parent, args, context, info) => {
     return { qux: context.mockData };
   },
 },
};
```

解析器对象是对象的集合。每个顶级对象对应于一个操作类型或一个对象类型。

下面的代码表示查询类型的客户端操作。

在 GraphQL playground 中运行这个查询。

```
query {
  bar
}
```

与客户端操作匹配的操作类型的名称将是服务器在解析器对象上查找解析器函数的第一个位置。接下来，它将查看客户端操作的最顶层字段 bar，并使用该名称 bar 来查找解析器。

一旦解析器 bar 被执行并且解析器返回了返回值‘bar ’,服务器将发送回下面的 JSON 有效负载。

```
{
  “data”: {
    “bar”: “bar”
  }
}
```

用于查询和 Foo 的模式定义语言(SDL ):

```
type Query {
  bar: String!
  foo(id: Int!): Foo!
}type Foo {
  id: Int!
  baz: Baz!
}
```

在 GraphQL Playground 中运行下面的查询。

foo 的查询类型的客户端操作:

```
query {
  foo(id: 1) {
    id
    baz {
      qux
    }
  }
}
```

看看 Query 的类型定义，foo 字段需要一个参数。我们通过向上面代码中括号内的 id 字段传递一个整数参数来查询 foo。

类型查询中 foo 字段的定义类型是什么？是福！感叹号意味着它是一个必需的返回值，因此在 resolver 对象中，我们必须再次遍历，首先是操作名查询对象，然后是名为 foo 的属性，以找到解析器。

foo 属性解析器函数通过访问 foo 解析器函数的 args 参数，将作为参数传递的 id 作为响应的值返回。服务器仍然没有找到对象类型为 baz 的类型为 Foo，Baz 的第二个数据字段。检索 baz 字段，并传递 Baz 类型的数据。服务器在解析器对象的最顶端字段中查找父对象的名称。

在这里，服务器找到与 Foo 类型匹配的 Foo 属性。服务器识别出 Foo 对象持有对应于 Foo 类型属性上的对象类型的解析器。服务器在 Foo 对象上找到 baz 解析器，并执行该函数。baz 解析器到达上下文对象，为 qux 返回任意模拟数据。

```
const resolvers = {
  Query: {
    foo: (parent, args, context, info) => {
      return { id: args.id };
    },
    bar: () => `bar`,
  },
  Foo: {
   baz: (parent, args, context, info) => {
     return { qux: context.mockData };
   },
  },
};
```

然后，Apollo Server 将聚合数据，并将这个 JSON 有效负载发送回客户机:

```
{
  “data”: {
    “foo”: {
      “id”: 1,
      “baz”: {
        “qux”: “qux”
      }
    }
  }
}
```

在服务器实例化期间，使用 context 选项将 mockData 传递给 ApolloServer。如下图所示。

上下文选项显示为传递给每个解析器函数的上下文参数的对象属性。上下文对象还可以用于与 req、res 等对象进行交互，这些对象对应于底层的 HTTP 请求响应对象。

```
const { ApolloServer, gql } = require(`apollo-server`);const mockData = `qux`;new ApolloServer({
 typeDefs,
 resolvers,
 context({ req, res }) {
   return { mockData, req, res };
 },
})
```

有关解析器参数的更多信息，请点击此[链接](https://www.apollographql.com/docs/apollo-server/data/resolvers/#resolver-arguments)。

我们没有使用的两个参数是 info 和 parent 参数。父参数是保存父解析器的返回值的地方。它不需要用在子节点的返回值中。子节点和父节点的返回值将被自动聚合到一个匹配相应字段的 JSON 有效负载响应中。父对象可用于其他目的，例如构建数据库查询。向 info 参数传递一个表示执行状态的参数，该参数描述了当前的解析器执行以及之前和即将执行的解析器执行。

服务器的完整代码如下所示。

按顺序运行以下两个命令。

```
npm init -y
npm i -S apollo-server graphql
```

👇🏻(运行该文件)

`node server.js`

server.js👇🏻

```
const { ApolloServer, gql } = require(`apollo-server`);const typeDefs = gql`
 type Query {
 bar: String!
 foo(id: Int!): Foo!
 }type Foo {
 id: Int!
 baz: Baz!
 }type Baz {
 qux: String
 }
`;const mockData = `qux`;const resolvers = {
  Query: {
    foo: (parent, args, context, info) => {
      return { id: args.id };
    },
    bar: () => `bar`,
  },
  Foo: {
    baz: (parent, args, context, info) => {
      return { qux: context.mockData };
    },
  },
};new ApolloServer({
  typeDefs,
  resolvers,
  context({ req, res }) {
    return { mockData, req, res };
  },
})
.listen()
.then(({ url }) => console.log(url));
```

谢谢！

*更多内容看*[*plain English . io*](http://plainenglish.io/)