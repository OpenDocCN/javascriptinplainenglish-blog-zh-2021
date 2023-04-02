# 阿波罗客户端数据标准化和存储

> 原文：<https://javascript.plainenglish.io/apollo-client-data-normalization-and-storage-e03c75dd52b9?source=collection_archive---------11----------------------->

![](img/2c88d57d3ddab449ae0db9f48d5a10e1.png)

Apollo client 是一个强大的前端 GraphQL 库，允许使用 GraphQL 的应用程序查询自身，以及连接的 GraphQL 数据服务。它是一个客户端状态管理库，与 GraphQL 后端深度集成。

在幕后，Apollo client 接受您的 GraphQL 查询响应，并将其展平成一个键值存储系统。举以下例子:

```
// GraphQL Query and Type
type Account { 
  id: ID!
  userName: String!}query getAccount() {
  account {
    id
    userName
    __typename // not required, but for illustration
  }  
}
```

上面对类型 Account 上的值的查询将返回如下响应:

```
{
  data: {
    account: {
      id: 1,
      userName: 'user',
      __typename: 'Account'
    }
  }
}
```

默认情况下，Apollo 客户端会以下面的键-值方式将它存储在客户端:

```
{
  'Account:1': { // this key is stored by Apollo client
      id: 1,
      userName: 'user',
      __typename: 'Account'
    }
}
```

Apollo 从响应中获取 **__typename** 和 **id** 字段，然后[将它们组合成键，](https://www.apollographql.com/docs/react/caching/cache-configuration/#generating-unique-identifiers)然后用它存储相关的值。

**问题**

Apollo 客户端不知道你的数据，也不知道你的类型之间的关系。对于更复杂的场景，Apollo 可能会错误地存储您正在查询的数据，并导致您的应用程序显示重复的值。您的 GraphQL 服务器将按照您的预期返回数据，但是 Apollo 客户机将数据正常化——导致冲突。要解决这个问题，您需要在受影响的类型的 TypePolicy 上使用[键字段](https://www.apollographql.com/docs/react/caching/cache-configuration/#disabling-normalization)。

**示例**

假设我们运行一个应用程序，跟踪不同公司的所有者权益。

```
type User {
  id: ID!
  name: String!  
  email: String!
}
type Company {
  id: ID!
  name: String!
  country: String!
  owners: [Owner]!
}type Owner implements User {
  equity: Float!
  company: Company!
}--- Example Query ---
query getCompanies() {
  companies {
    id
    name
    owners {
     id
     name
     equity 
    }
  }
}
```

股权是基于每家公司的，没有什么可以阻止用户拥有多家公司的股份。因此，当我们从后端获取数据时，有可能会发生冲突，因为*所有者*类型与*用户*类型使用相同的 id，Apollo 客户端最终会在其扁平化的数据存储中生成重复的键。

![](img/d791a8b781e9c7cd6c312bba61b75e58.png)

就拿埃隆·马斯克来说吧，他在 SpaceX 和特斯拉都有股权。我们对上述示例查询的数据响应如下所示:

```
{
  "data": {
    "companies": [
      {
        "id": 1,
        "name": "SpaceX",
        "owners": [
          {
            "id": 1,
            "name": "Elon Musk",
            "equity": 0.95
          }
        ]
      },
      {
        "id": 2,
        "name": "Tesla",
        "owners": [
          {
            "id": 1,
            "name": "Elon Musk",
            "equity": 0.93
          }
        ]
      }
    ]
  }
}
```

当 Apollo client 收到这些数据时，它会试图保存 Owner:1 下 Musk 的所有权，并产生冲突。

```
{
  "Owner:1": {
    "id": 1,
    "name": "Elon Musk",
    "equity": 0.95
  }
}---- Clashes With ----
{
  "Owner:1": {
    "id": 1,
    "name": "Elon Musk",
    "equity": 0.93
  }
}
```

在我们的客户端类型策略中为**所有者**类型实现一个关键字段定义可以解决这个问题

```
const Owner = {
  keyFields: ['id', 'equity', 'name'] // Apollo Client will generate a new identifier, based on the fields you pass in.
}const typePolicies = {
  Owner
}
export default typePolicies
```

[键字段可以是许多不同的东西](https://www.apollographql.com/docs/react/caching/cache-configuration/#disabling-normalization)，你可以把它设置为`false`，Apollo 将获取整个值，将其字符串化，并把它作为键使用。您也可以使用一个字段数组，如上所示，或者使用一个`KeyFieldsFunction`来生成您自己的数组。现在，我们的扁平数据结构将包含两个所有者数据集。

```
{
  "Owner:1|equity:0.95|name:'Elon Musk'": {
    "id": 1,
    "name": "Elon Musk",
    "equity": 0.95
  },
  "Owner:1|equity:0.93|name:'Elon Musk'": {
    "id": 1,
    "name": "Elon Musk",
    "equity": 0.93
  }
}
```

## 结论

感谢阅读！我希望这有助于解决一些人在为他们的前端应用程序实现 Apollo 客户端时遇到的问题。如果这篇文章有问题，请联系我，我可以解决它！

—Pat
[@ Pat zawa](https://twitter.com/PatZawa)
[patz . dev](http://www.patz.dev)