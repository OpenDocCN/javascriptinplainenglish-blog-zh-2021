# Node.js 基础——MongoDB 排序和查询

> 原文：<https://javascript.plainenglish.io/node-js-basics-mongodb-collation-and-queries-7b75bda2d57e?source=collection_archive---------11----------------------->

![](img/5d5167f5710ce2edb443b80df5d9d7d9.png)

Photo by [National Cancer Institute](https://unsplash.com/@nci?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Node.js 是一个流行的运行时平台，用于创建在其上运行的程序。

它让我们可以在浏览器之外运行 JavaScript。

在本文中，我们将了解如何开始使用 Node.js 创建程序。

# 排序规则优先级

如果在索引和查询上应用了排序规则，那么我们可以设置排序规则的优先级。

例如，我们可以写:

```
const { MongoClient } = require('mongodb');
const connection = "mongodb://localhost:27017";
const client = new MongoClient(connection);async function run() {
  try {
    await client.connect();
    const db = client.db("test");
    await db.dropCollection('test');
    await db.createCollection("test");
    const testCollection = await db.collection('test');
    await testCollection.createIndex(
      { 'name': 1 },
      { 'collation': { 'locale': 'en' } });
    await testCollection.dropIndexes();
    await testCollection.deleteMany({})
    const result = await testCollection.insertMany([
      { "_id": 1, "name": "apples", "qty": 5, "rating": 3 },
      { "_id": 2, "name": "bananas", "qty": 7, "rating": 1 },
      { "_id": 3, "name": "oranges", "qty": 6, "rating": 2 },
      { "_id": 4, "name": "avocados", "qty": 3, "rating": 5 },
    ]);
    console.log(result)
    const options = { "collation": { "locale": "en_US", "strength": 2 } };
    const cursor = testCollection
      .find({}, options)
      .sort({ "name": -1 });
    cursor.forEach(console.dir);
  } finally {
    await client.close();
  }
}
run().catch(console.dir);
```

我们有一个`options`对象用`strength`属性来设置`collation`规则。

`strength`属性决定了我们应用的排序规则的顺序。

# 归类查询

查找和排序查询支持排序规则。

例如，我们可以写:

```
const { MongoClient } = require('mongodb');
const connection = "mongodb://localhost:27017";
const client = new MongoClient(connection);async function run() {
  try {
    await client.connect();
    const db = client.db("test");
    await db.dropCollection('test');
    await db.createCollection("test");
    const testCollection = await db.collection('test');
    await testCollection.createIndex(
      { 'name': 1 },
      { 'collation': { 'locale': 'en' } });
    await testCollection.dropIndexes();
    await testCollection.deleteMany({})
    const result = await testCollection.insertMany([
      { "_id": 1, "name": "apples", "qty": 5, "rating": 3 },
      { "_id": 2, "name": "bananas", "qty": 7, "rating": 1 },
      { "_id": 3, "name": "oranges", "qty": 6, "rating": 2 },
      { "_id": 4, "name": "avocados", "qty": 3, "rating": 5 },
    ]);
    console.log(result)
    const cursor = testCollection
      .find({ name: "name" }, { collation: { locale: "en" } })
      .sort({ name: 1 });
    cursor.forEach(console.dir);
  } finally {
    await client.close();
  }
}
run().catch(console.dir);
```

`find`的第二个参数有一个带有`collation`属性的对象来设置排序规则。

我们也可以用`findOneAndUpdate`方法设置校对规则:

```
const { MongoClient } = require('mongodb');
const connection = "mongodb://localhost:27017";
const client = new MongoClient(connection);async function run() {
  try {
    await client.connect();
    const db = client.db("test");
    await db.dropCollection('test');
    await db.createCollection("test");
    const testCollection = await db.collection('test');
    await testCollection.createIndex(
      { 'name': 1 },
      { 'collation': { 'locale': 'en' } });
    await testCollection.dropIndexes();
    await testCollection.deleteMany({})
    const result = await testCollection.insertMany([
      { "_id": 1, "name": "apples", "qty": 5, "rating": 3 },
      { "_id": 2, "name": "bananas", "qty": 7, "rating": 1 },
      { "_id": 3, "name": "oranges", "qty": 6, "rating": 2 },
      { "_id": 4, "name": "avocados", "qty": 3, "rating": 5 },
    ]);
    console.log(result)
    testCollection
      .findOneAndUpdate(
        { qty: { $lt: 5 } },
        { $set: { rating: 5 } },
        { collation: { locale: "en" } },
      )
  } finally {
    await client.close();
  }
}
run().catch(console.dir);
```

第三个参数设置了`collation`属性来设置排序规则。

# 结论

当我们进行查询时，可以设置排序规则优先级。此外，我们可以在查找、排序或更新项目时设置排序规则。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**