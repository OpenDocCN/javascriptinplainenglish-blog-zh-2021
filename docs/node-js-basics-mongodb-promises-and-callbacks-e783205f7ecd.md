# Node.js 基础——MongoDB 承诺和回调

> 原文：<https://javascript.plainenglish.io/node-js-basics-mongodb-promises-and-callbacks-e783205f7ecd?source=collection_archive---------9----------------------->

![](img/239158814bb47dc2f6494c93f3c11982.png)

Photo by [Ester Marie Doysabas](https://unsplash.com/@estersthetic?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Node.js 是一个流行的运行时平台，用于创建在其上运行的程序。

它让我们可以在浏览器之外运行 JavaScript。

在本文中，我们将了解如何开始使用 Node.js 创建程序。

# 承诺和回访

MongoDB 客户端有返回承诺的方法。

它们是异步代码，在有结果之前可以有挂起状态。

一旦有了结果，如果操作成功，就可以实现它。

否则，它的状态为已拒绝。

例如，`updateOne`方法返回一个承诺。

我们可以通过书写来使用它:

```
const { MongoClient } = require('mongodb');
const connection = "mongodb://localhost:27017";
const client = new MongoClient(connection);async function run() {
  try {
    await client.connect();
    const testCollection = await client.db("test").collection('test');
    await testCollection.deleteMany({})
    const result = await testCollection.insertMany([
      { "_id": 1, "name": "apples", "qty": 5, "rating": 3 },
      { "_id": 2, "name": "bananas", "qty": 7, "rating": 1 },
      { "_id": 3, "name": "oranges", "qty": 6, "rating": 2 },
      { "_id": 4, "name": "avocados", "qty": 3, "rating": 5 },
    ]);
    console.log(result)
    const updateResult = await testCollection
      .updateOne({ name: "apple" }, { $set: { qty: 100 } })
    console.log(updateResult);
  } finally {
    await client.close();
  }
}
run().catch(console.dir);
```

我们用`await`关键字调用`updateOne`，这样一旦得到解析后的值，我们就可以得到它。

`updateOne`返回一个承诺，所以我们可以使用`await`关键字。

如果我们想捕捉错误，那么我们可以写:

```
const { MongoClient } = require('mongodb');
const connection = "mongodb://localhost:27017";
const client = new MongoClient(connection);async function run() {
  try {
    await client.connect();
    const testCollection = await client.db("test").collection('test');
    await testCollection.deleteMany({})
    const result = await testCollection.insertMany([
      { "_id": 1, "name": "apples", "qty": 5, "rating": 3 },
      { "_id": 2, "name": "bananas", "qty": 7, "rating": 1 },
      { "_id": 3, "name": "oranges", "qty": 6, "rating": 2 },
      { "_id": 4, "name": "avocados", "qty": 3, "rating": 5 },
    ]);
    console.log(result)
    try {
      const updateResult = await testCollection
        .updateOne({ name: "apple" }, { $set: { qty: 100 } })
      console.log(updateResult);
    } catch (error) {
      console.log(`Updated ${res.result.n} documents`)
    }} finally {
    await client.close();
  }
}
run().catch(console.dir);
```

添加一个`catch`块来记录被拒绝的承诺引起的任何错误。

# 复试

我们也可以使用回调来获得操作的结果。

例如，我们可以写:

```
const { MongoClient } = require('mongodb');
const connection = "mongodb://localhost:27017";
const client = new MongoClient(connection);async function run() {
  try {
    await client.connect();
    const testCollection = await client.db("test").collection('test');
    await testCollection.deleteMany({})
    const result = await testCollection.insertMany([
      { "_id": 1, "name": "apples", "qty": 5, "rating": 3 },
      { "_id": 2, "name": "bananas", "qty": 7, "rating": 1 },
      { "_id": 3, "name": "oranges", "qty": 6, "rating": 2 },
      { "_id": 4, "name": "avocados", "qty": 3, "rating": 5 },
    ]);
    console.log(result)
    testCollection
      .updateOne({ name: "apple" }, { $set: { qty: 100 } }, (error, result) => {
        if (!error) {
          console.log(`Operation completed successfully`);
        } else {
          console.log(`An error occurred: ${error}`);
        }
      })
  } finally {
    await client.close();
  }
}
run().catch(console.dir);
```

我们用第三个参数中的回调来调用`updateOne`。

这让我们可以通过回调获得异步结果，而不是返回一个承诺。

# 结论

MongoDB 客户端返回承诺，或者我们可以使用回调从异步操作中获得结果。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**