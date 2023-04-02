# Node.js 基础— MongoDB 索引类型

> 原文：<https://javascript.plainenglish.io/node-js-basics-mongodb-index-types-b4db49122190?source=collection_archive---------15----------------------->

![](img/d380757795c4c38cd7fbb097d5fcd460.png)

Photo by [Dusty Barnes](https://unsplash.com/@dustbarnes?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Node.js 是一个流行的运行时平台，用于创建在其上运行的程序。

它让我们可以在浏览器之外运行 JavaScript。

在本文中，我们将了解如何开始使用 Node.js 创建程序。

# 索引类型

MongoDB 有不同的文本类型。

我们可以添加单个字段索引，以提高在文档的单个字段上指定升序或降序排序的查询的性能。

例如，我们可以写:

```
const { MongoClient } = require('mongodb');
const connection = "mongodb://localhost:27017";
const client = new MongoClient(connection);async function run() {
  try {
    await client.connect();
    const db = client.db("test");
    const testCollection = await db.collection('test');
    await testCollection.dropIndexes();
    const indexResult = await testCollection.createIndex({ name: 1 });
    console.log(indexResult)
    await testCollection.deleteMany({})
    const result = await testCollection.insertMany([
      { "_id": 1, "name": "apples", "qty": 5, "rating": 3 },
      { "_id": 2, "name": "bananas", "qty": 7, "rating": 1 },
      { "_id": 3, "name": "oranges", "qty": 6, "rating": 2 },
      { "_id": 4, "name": "avocados", "qty": 3, "rating": 5 },
    ]);
    console.log(result)
    const query = {};
    const sort = { name: 1 };
    const cursor = testCollection
      .find(query)
      .sort(sort);
    cursor.forEach(console.dir);
  } finally {
    await client.close();
  }
}
run().catch(console.dir);
```

我们调用带有排序顺序的对象的`sort`方法。

复合索引是提高查询性能的索引，这些查询为文档中的多个字段指定升序或降序排序。

例如，我们可以为`name`和`rating`字段添加一个复合，并通过编写以下内容来使用它:

```
const { MongoClient } = require('mongodb');
const connection = "mongodb://localhost:27017";
const client = new MongoClient(connection);async function run() {
  try {
    await client.connect();
    const db = client.db("test");
    const testCollection = await db.collection('test');
    await testCollection.dropIndexes();
    const indexResult = await testCollection.createIndex({ name: 1, rating: 1 });
    console.log(indexResult)
    await testCollection.deleteMany({})
    const result = await testCollection.insertMany([
      { "_id": 1, "name": "apples", "qty": 5, "rating": 3 },
      { "_id": 2, "name": "bananas", "qty": 7, "rating": 1 },
      { "_id": 3, "name": "oranges", "qty": 6, "rating": 2 },
      { "_id": 4, "name": "avocados", "qty": 3, "rating": 5 },
    ]);
    console.log(result)
    const query = {};
    const sort = { name: 1, rating: 1 };
    const cursor = testCollection
      .find(query)
      .sort(sort);
    cursor.forEach(console.dir);
  } finally {
    await client.close();
  }
}
run().catch(console.dir);
```

我们有:

```
const indexResult = await testCollection.createIndex({ name: 1, rating: 1 });
```

添加复合指数。

然后我们用一个既有`name`又有`rating`字段的对象调用`sort`。

多键索引是提高查询性能的索引，该查询对具有数组值的字段指定升序或降序索引。

例如，我们可以创建一个多键索引，并通过编写以下内容来使用它:

```
const { MongoClient } = require('mongodb');
const connection = "mongodb://localhost:27017";
const client = new MongoClient(connection);async function run() {
  try {
    await client.connect();
    const db = client.db("test");
    const testCollection = await db.collection('test');
    await testCollection.dropIndexes();
    const indexResult = await testCollection.createIndex({ types: 1 });
    console.log(indexResult)
    await testCollection.deleteMany({})
    const result = await testCollection.insertMany([
      { "_id": 1, "name": "apples", "qty": 5, "rating": 3, "types": ["granny smith", "mcintosh"] },
      { "_id": 2, "name": "bananas", "qty": 7, "rating": 1, "types": ["chiquita", "del monte"] },
      { "_id": 3, "name": "oranges", "qty": 6, "rating": 2, "types": [] },
      { "_id": 4, "name": "avocados", "qty": 3, "rating": 5, "types": [] },
    ]);
    console.log(result)
    const query = { types: "granny smith" };
    const sort = { types: 1 };
    const projection = { types: 1 };
    const cursor = testCollection
      .find(query)
      .sort(sort)
      .project(projection);
    cursor.forEach(console.dir);
  } finally {
    await client.close();
  }
}
run().catch(console.dir);
```

我们有:

```
const indexResult = await testCollection.createIndex({ types: 1 });
```

在`types`字段上创建索引。

然后我们可以对`types`字段进行查询。

# 结论

MongoDB 有各种类型的索引来优化各种查询的性能。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**