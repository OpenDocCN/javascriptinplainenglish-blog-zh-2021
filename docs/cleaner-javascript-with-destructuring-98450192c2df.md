# 带有析构的更干净的 JavaScript

> 原文：<https://javascript.plainenglish.io/cleaner-javascript-with-destructuring-98450192c2df?source=collection_archive---------7----------------------->

![](img/1e469bb4065278774b2df10969662041.png)

Photo by [Iker Urteaga](https://unsplash.com/@iurte?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

首先，我有点不高兴我花了这么长时间才意识到析构是如此的棒！我发现自己越来越多地将它用于数组和对象的基本任务，如解包，不必要的冗长任务，如分配默认值，或通过分配新的变量名赋予数据语义。每一种方法都有显而易见的方法，但我真的爱上了在保持代码整洁的同时，析构语法允许我表达的程度。它可以将一些非常棘手的操作变成一个命令行程序。

在生产中使用析构语法之前，确保[检查兼容性](https://caniuse.com/mdn-javascript_operators_destructuring)并在必要时安装[合适的工具](https://babeljs.io/docs/en/babel-plugin-transform-destructuring)。

# 基本阵列解包

对于阵列

```
**const foo = ['zero', 'one', 'two', 'three'];**
```

我们可以使用析构来实现**变量赋值**。

```
**const [a, b, c, d] = foo;**// is equivalent to
**const a = foo[0];
const b = foo[1];
const c = foo[2];
const d = foo[3];**// in both cases
**a** // 'zero'
**b** // 'one'
**c** // 'two'
**d** // 'three
```

我们也可以通过让索引为空来忽略值

```
**const [a, , , b] = foo;**// is equivalent to
**const a = foo[0];
const b = foo[3];**// in both cases
**a** // 'zero'
**b** // 'three'
```

或者**使用扩展语法将剩余值分配给变量**。

```
**const [a, ...b] = foo;**// is equivalent to
**const a = foo[0];
const b = foo.slice(1);**// in both cases
**a** // 'zero'
**b** // ['one', 'two', 'three']
```

# 基本对象解包

对于该对象

```
**const bar = {
  id: 11,
  hidden: false,
};**
```

我们可以使用析构来实现**变量赋值**。

```
**const { id, hidden } = bar;**// is equivalent to
**const id = bar.id;
const hidden = bar.hidden;**// in both cases
**id** // 11
**hidden** // false
```

我们还可以**将对象属性重命名为新变量**。

对于该对象

```
**const user = {
  id: 8164,
  name: 'Tom',
  active: true,
};**
```

将对象属性重命名为

```
**const {
  id: userId,
  name: userName,
  active: userIsActive,
} = user;****userId** // 8164
**userName** // 'Tom'
**userIsActive** // true
```

避免与其他变量冲突或赋予数据语义。

# 分配默认值

默认值在数组和对象中是一样的。默认值适用于返回值为`undefined`的情况。

```
**const skills = [];
const [firstSkill = 'Still learning!'] = skills;** **const projects = {};
const { firstProject = 'Still working!' } = projects;** **firstSkill** // 'Still learning!'
**firstProject** // 'Still working!'
```

# 一些使用案例

## 解包、重命名和分配默认值

我们能做到这三点吗？为什么？是的，我们可以。

```
**const obj = {
  foo: 1,
  bar: 0,
  baz: undefined,
};**// unpack, rename, and assign defaults **const {
  foo: apple = 500,
  bar: banana = 501,
  baz: orange = 502,
  qux: mango = 503,
} = obj;****apple** // 1
**banana** // 0
**orange** // 502
**mango** // 503
```

一个接一个:别名`apple`按照预期从`foo`解析出值`1`。`banana`也解析`bar`的值，但值为零。`0`的 falsy 值不是应该降回默认值吗？嗯，不……请记住“默认值应用于返回值为`undefined`的情况”，不一定是 falsy。这就把我们带到了`orange`，它实际上解析了一个值`undefined`，并返回到默认值`502`。

至于`mango`，如何解包一个不存在的对象属性？如果我们回到 JavaScript 101，我们会回忆起未声明和未初始化的变量返回一个值`undefined`，所以在这种情况下，我们实际上可以查询`qux`，并依靠我们设置的默认值来捕捉任何不存在它的实例。没有`if`语句、三元、布尔或逻辑运算符；纯粹的 JS 魔法！

## 解包作为函数参数传递的对象

析构传递给函数参数的参数可以避免在函数中使用任意参数名。

```
**const book = {
  title: 'Some Great Book',
  author: {
    firstName: 'Seymour',
    lastName: 'Penman',
  },
};****function getAuthorName({ author: { firstName, lastName }) {
  return `The author is ${firstName} ${lastName}`;
};****getAuthorName(book);** // 'The author is Seymour Penman'
```

我发现这在处理运行在对象数组上的**数组方法时特别有用。对于阵列**

```
**const arrOfObjs = [
  { name: 'foo' },
  { name: 'bar' },
  { name: 'baz' },
];**
```

我们可以析构回调的参数

```
**arrOfObjs.forEach(({ name }) => console.log(name));**
```

而不是

```
**arrOfObjs.forEach((i) => console.log(i.name));**
```

显然，在这样一个简单的例子中，这没什么大不了的，我选择`i`只是为了唱反调。`i`可能表示项目，可能是索引，可能是整数；看看周围的代码就不难发现，但是我真的很喜欢这种析构让我们不必考虑选择一个全新的(但是希望是语义上的)参数名。

## 组合数组和对象析构

对于(不寻常的)阵列

```
**const favoriteColors = [
  { possibilities: ['lilac', 'aqua', 'coral', 'gold'] },
  { rank: 1, color: 'aqua' },
  { rank: 2, color: 'gold' },
  { rank: 3, color: 'coral' },
];**
```

比方说，在代码的其他地方，我们需要引用颜色 aqua，这是一个嵌套的可能性数组，但如果没有指定，则只返回黑色和白色，以及 rank 1 后面的每个对象。在一个奇怪的阵列上完成一项奇怪的任务，但我们可以轻松地完成它。

```
**const [
  { possibilities = ['black', 'white']: palette },
  { color: favoriteColor},
  ...rest
] = favoriteColors;****palette** // ['lilac', 'aqua', 'coral', 'gold']
**favoriteColor** // 'aqua'
**rest** // [{ rank: 2, color: 'gold' }, { rank: 3, color: 'coral' }]
```

分解一下，我们的析构赋值中的第一项在第一个索引位置获取对象，并寻找一个名为`possibilities`的属性。然后，我们为它分配一个包含两个项目`black`和`white`的数组的默认值，然后为了语义的原因，将其重命名为`palette`。

第二项从对象中解包`color`属性，然后将其重命名为`favoriteColor`。

最后一项将数组中剩余的对象分配给一个名为`rest`的变量。

显然，这不是组织或排列某人最喜欢的颜色的理想方式，但我想说明，无论原始数据有多古怪，组合数组和对象析构都可以保持整洁。

## 深度嵌套的值

假设我们需要深入到一个对象中寻找一个值。

对于该对象

```
**const data = {
  post: {
    fields: {
      slug: 'a-blog-post',
    },
    type: 'technology',
    metadata: {
      title: 'A Blog Post',
      date: 2021-01-01,
      credits: [
        { name: 'Generic Namesake', role: 'author' },
        { name: 'Universal Surname', role: 'editor' },
      ],
      keywords: ['javascript', 'destructuring'],
    },
  },
};**
```

如果我们需要访问这段代码，我们可以如下进行析构。

```
**const { post: { fields: slug } } = data;**// is equivalent to
**const slug = data.post.fields.slug;**// in both cases
**slug** // 'a-blog-post'
```

或者，我们可以提取多个参数，并添加一些换行符以提高可读性。让我们先析构一次，对信用执行一个数组方法，然后在回调中再次析构信用。

```
**const {
  post: {
    fileds: { slug },
    metadata: {
      title: postTitle,** // rename **date: publishDate,** // rename **credits: postCredits,** // rename **},
  },
} = data;**// check for role of `editor` and that name exists
**const hasEditor = postCredits.some(
  ({ name, role }) => role === 'editor' && name
);**
```

## 解析从函数返回的数组

对于那些使用过 React 的“使用状态”钩子的人来说，这个可能看起来很熟悉。简单地说，从函数返回的数组可以在一行中解析。

```
**function foo() {
  return [1, 2];
};****const [a, b] = foo();**
```

# 包扎

希望此时你也同意解构 JavaScript 是很棒的。它总是正确的答案吗？取决于项目和团队。难道只是句法糖。可能吧，但对我来说，任何维护代码可读性的解决方案都值得长期研究和投资。将来调试你代码的人会感谢你……可能是你。