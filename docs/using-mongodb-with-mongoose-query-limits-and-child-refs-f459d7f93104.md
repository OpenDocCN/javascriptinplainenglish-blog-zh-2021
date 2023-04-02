# 使用 MongoDB 和 mongose—查询限制和子引用

> 原文：<https://javascript.plainenglish.io/using-mongodb-with-mongoose-query-limits-and-child-refs-f459d7f93104?source=collection_archive---------12----------------------->

![](img/1522744f67af24b925223db6fa9e1b9d.png)

Photo by [Dušan Smetana](https://unsplash.com/@veverkolog?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

为了简化 MongoDB 数据库操作，我们可以使用 mongose NPM 包来简化 MongoDB 数据库的操作。

在本文中，我们将了解如何使用 Mongoose 来操作我们的 MongoDB 数据库。

# limit 与 perDocumentLimit

Populate 有一个`limit`选项，但是它不支持基于每个文档的限制。

例如，我们可以写:

```
async function run() {
  const { createConnection, Types, Schema } = require('mongoose');
  const connection = createConnection('mongodb://localhost:27017/test');
  const personSchema = Schema({
    _id: Schema.Types.ObjectId,
    name: String,
    age: Number,
    stories: [{ type: Schema.Types.ObjectId, ref: 'Story' }]
  });
  const storySchema = Schema({
    author: { type: Schema.Types.ObjectId, ref: 'Person' },
    title: String,
    fans: [{ type: Schema.Types.ObjectId, ref: 'Person' }]
  });
  const Story = connection.model('Story', storySchema);
  const Person = connection.model('Person', personSchema);
  const author = new Person({
    _id: new Types.ObjectId(),
    name: 'James Smith',
    age: 50
  });
  await author.save();
  const fan = new Person({
    _id: new Types.ObjectId(),
    name: 'Fan Smith',
    age: 50
  });
  await fan.save();
  const story1 = new Story({
    title: 'Mongoose Story',
    author: author._id,
    fans: [fan._id]
  });
  await story1.save();
  const story = await Story.findOne({ title: 'Mongoose Story' })
    .populate({
      path: 'fans',
      options: { limit: 2 }
    })
    .exec();
  console.log(story.fans)
}
run();
```

最多可查询`numDocuments * limit`。

mongose 5 . 9 . 0 或更高版本支持`perDocumentLimit`属性来添加每个文档的限制。

例如，我们可以写:

```
async function run() {
  const { createConnection, Types, Schema } = require('mongoose');
  const connection = createConnection('mongodb://localhost:27017/test');
  const personSchema = Schema({
    _id: Schema.Types.ObjectId,
    name: String,
    age: Number,
    stories: [{ type: Schema.Types.ObjectId, ref: 'Story' }]
  });
  const storySchema = Schema({
    author: { type: Schema.Types.ObjectId, ref: 'Person' },
    title: String,
    fans: [{ type: Schema.Types.ObjectId, ref: 'Person' }]
  });
  const Story = connection.model('Story', storySchema);
  const Person = connection.model('Person', personSchema);
  const author = new Person({
    _id: new Types.ObjectId(),
    name: 'James Smith',
    age: 50
  });
  await author.save();
  const fan = new Person({
    _id: new Types.ObjectId(),
    name: 'Fan Smith',
    age: 50
  });
  await fan.save();
  const story1 = new Story({
    title: 'Mongoose Story',
    author: author._id,
    fans: [fan._id]
  });
  await story1.save();
  const story = await Story.findOne({ title: 'Mongoose Story' })
    .populate({
      path: 'fans',
      perDocumentLimit: 2
    })
    .exec();
  console.log(story.fans)
}
run();
```

# 儿童参考

如果我们调用`push`到子项的条目，那么我们可以得到子项的引用。

例如，我们可以写:

```
async function run() {
  const { createConnection, Types, Schema } = require('mongoose');
  const connection = createConnection('mongodb://localhost:27017/test');
  const personSchema = Schema({
    _id: Schema.Types.ObjectId,
    name: String,
    age: Number,
    stories: [{ type: Schema.Types.ObjectId, ref: 'Story' }]
  });
  const storySchema = Schema({
    author: { type: Schema.Types.ObjectId, ref: 'Person' },
    title: String,
    fans: [{ type: Schema.Types.ObjectId, ref: 'Person' }]
  });
  const Story = connection.model('Story', storySchema);
  const Person = connection.model('Person', personSchema);
  const author = new Person({
    _id: new Types.ObjectId(),
    name: 'James Smith',
    age: 50
  });
  await author.save();
  const fan = new Person({
    _id: new Types.ObjectId(),
    name: 'Fan Smith',
    age: 50
  });
  await fan.save();
  const story1 = new Story({
    title: 'Mongoose Story',
    author: author._id,
  });
  story1.fans.push(fan);
  await story1.save();
  const story = await Story.findOne({ title: 'Mongoose Story' })
    .populate('fans')
    .exec();
  console.log(story.fans)
}
run();
```

我们在`story.fans`上调用`push`来向`fans`数组字段添加一个条目。

现在，当我们查询这个故事时，我们得到了包含`fan`的`fans`数组。

# 结论

我们可以限制返回的文档数量，并向数组字段添加条目，这样我们就可以访问子条目的引用。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**