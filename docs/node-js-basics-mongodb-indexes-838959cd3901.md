# Node.js 基础— MongoDB 索引

> 原文：<https://javascript.plainenglish.io/node-js-basics-mongodb-indexes-838959cd3901?source=collection_archive---------15----------------------->

![](img/79d2ff87e4fc3dd2d433fe068a1a40db.png)

Photo by [Alexander Schimmeck](https://unsplash.com/@alschim?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Node.js 是一个流行的运行时平台，用于创建在其上运行的程序。

它让我们可以在浏览器之外运行 JavaScript。

在本文中，我们将了解如何开始使用 Node.js 创建程序。

# 创建索引

我们可以在集合中创建索引，以便能够在集合中进行搜索。

例如，我们可以写:

```
const { MongoClient } = require('mongodb');
const connection = "mongodb://localhost:27017";
const client = new MongoClient(connection);async function run() {
  try {
    await client.connect();
    const db = client.db("test");
    const testCollection = await db.collection('test');
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
  } finally {
    await client.close();
  }
}
run().catch(console.dir);
```

我们调用`testCollection`上的`createIndex`方法来为它添加一个索引。

然后，我们可以通过编写以下内容来查询集合:

```
const { MongoClient } = require('mongodb');
const connection = "mongodb://localhost:27017";
const client = new MongoClient(connection);async function run() {
  try {
    await client.connect();
    const db = client.db("test");
    const testCollection = await db.collection('test');
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
    const query = { name: "apples" };
    const sort = { name: 1 };
    const projection = { name: 1 };
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

当我们调用`createIndex`时，我们可以通过将 index 键的值设置为`'text'`来创建一个文本索引。

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
    const indexResult = await testCollection.createIndex({ name: 'text' });
    console.log(indexResult)
    await testCollection.deleteMany({})
    const result = await testCollection.insertMany([
      { "_id": 1, "name": "apples", "qty": 5, "rating": 3 },
      { "_id": 2, "name": "bananas", "qty": 7, "rating": 1 },
      { "_id": 3, "name": "oranges", "qty": 6, "rating": 2 },
      { "_id": 4, "name": "avocados", "qty": 3, "rating": 5 },
    ]);
    console.log(result)
    const query = { $text: { $search: "apples" } };
    const projection = { name: 1 };
    const cursor = testCollection
      .find(query)
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
const indexResult = await testCollection.createIndex({ name: 'text' });
```

向`name`字段添加文本索引。

然后我们可以写:

```
const query = { $text: { $search: "apples" } };
```

进行文本搜索查询并返回结果。

# 结论

我们可以用`createIndex`方法向 MongoDB 集合添加索引。

要启用文本搜索，我们可以添加文本索引。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**