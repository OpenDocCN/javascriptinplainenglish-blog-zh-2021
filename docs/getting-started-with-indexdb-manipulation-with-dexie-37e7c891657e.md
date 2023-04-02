# Dexie indexed db 操作入门

> 原文：<https://javascript.plainenglish.io/getting-started-with-indexdb-manipulation-with-dexie-37e7c891657e?source=collection_archive---------15----------------------->

![](img/fbfdb0b43efaf1e2a43bfdd376bc251f.png)

Photo by [Dusty Barnes](https://unsplash.com/@dustbarnes?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

IndexedDB 是在浏览器中存储数据的一种方式。

它允许我们以异步方式存储比本地存储更多的数据。

Dexie 使得使用 IndexedDB 更加容易。

在本文中，我们将了解如何使用 Dexie 开始使用 IndexedDB。

# 入门指南

我们可以从添加带有脚本标记的 Dexie 开始:

```
<script src="https://unpkg.com/dexie@latest/dist/dexie.js"></script>
```

然后我们可以用它来创建我们的数据。

然后我们可以用它创建一个数据库，并从中读写数据。

为此，我们写道:

```
const db = new Dexie("friend_database");
(async () => {
  try {
    await db.version(1).stores({
      friends: 'name,age'
    });
    await db.friends.put({
      name: "mary",
      age: 28
    })
    const friend = await db.friends.get('mary');
    console.log(friend.age);
  } catch (error) {
    console.log(error);
  }
})()
```

我们用`Dexie`构造函数创建数据库。

然后，我们在数据库中创建一个商店，其中包含:

```
await db.version(1).stores({
  friends: 'name,age'
});
```

我们用索引的`name`和`age`字段将`friends`商店添加到数据库中。

索引列可用于搜索条目。

然后我们用`put`方法添加数据:

```
await db.friends.put({
  name: "mary",
  age: 28
})
```

然后我们得到一个带有给定索引列的条目:

```
const friend = await db.friends.get('mary');
```

然后用以下公式获得`age`字段的值:

```
console.log(friend.age);
```

# 使用 Dexie 作为模块

我们可以在`dexie`模块中使用 Dexie。

要安装它，我们运行:

```
npm i dexie
```

然后可以用以下代码编写相同的代码:

```
import Dexie from "dexie";
const db = new Dexie("friend_database");(async () => {
  try {
    await db.version(1).stores({
      friends: "name,age"
    });
    await db.friends.put({
      name: "mary",
      age: 28
    });
    const friend = await db.friends.get("mary");
    console.log(friend.age);
  } catch (error) {
    console.log(error);
  }
})();
```

# 德协级

`Dexie`类既是类又是名称空间。

`Dexie`实例代表一个数据库连接。

它还可以用作函数、实用程序和类的导出区域。

如果它在浏览器中用作脚本标签，那么只添加`window.Dexie`属性。

如果它被用作一个模块，那么它可以作为一个默认的导出。

# 表格类

该表表示一个对象存储。

对于我们在模式中拒绝的每个对象存储，我们可以直接访问`Table`的实例。

例如，如果我们有:

```
(async () => {
  const db = new Dexie("FriendsAndPetsDB");
  await db.version(1).stores({
    friends: "++id,name,isCloseFriend",
    pets: "++id,name,kind"
  });
  await db.open();
  await db.friends.add({
    name: "james",
    isCloseFriend: true
  });
  await db.pets.add({
    name: "mary",
    kind: "dog",
    fur: "long"
  });
})()
```

然后我们创建了`friends`和`pets`商店。

`db.friends`和`db.pets`是表格实例。

我们可以用它们来处理数据。

`db.open`打开数据库连接。

我们调用了`db.friends.add`来向`db.friends`存储添加数据。

我们调用了`db.pets.add`来向`db.pets`存储添加数据。

# 结论

我们可以使用 Dexie 库轻松操作 IndexDB 数据。

喜欢这篇文章吗？如果有，在[**plain English . io**](https://plainenglish.io)获取更多类似内容