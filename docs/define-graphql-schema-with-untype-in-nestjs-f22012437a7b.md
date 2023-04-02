# 在 NestJS 中用 Untype 定义 GraphQL 模式

> 原文：<https://javascript.plainenglish.io/define-graphql-schema-with-untype-in-nestjs-f22012437a7b?source=collection_archive---------16----------------------->

![](img/f00f77ed56b5ae8e90727f2a16e0b5d0.png)

Photo by [Blake Connally](https://unsplash.com/@blakeconnally?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

大家好！这是一篇关于我的文档的短文，因为我一直在使用带有 NestJS 的 GraphQL 进行开发。

这个场景是当我想在突变中创建一个有效负载，而这个有效负载并不总是相同的，例如:

```
...
{
  component: [
    {
      key: 'A',
      value: [1,2,3,4]
    }
  ]
}
...
```

但目前，你有一个几乎相似的有效载荷，如下图所示。

```
...
{
  component: [
    {
      key: 'A',
      value: 'This is string'
    }
  ]
}
...
```

你如何提供这一点？

就我而言，我找到了一种解决这个问题的方法。希望，如果你读了这篇文章，它也能帮助你。

看这个:

1.  我安装了 **graphql-type-json**
2.  将包导入 args 类
3.  然后将 args 类导入解析器。
4.  试试这个。结案了。希望如此。

# 警惕！

如果你们来自**印尼**，想要支持我写更多的东西，希望你们能从钱包里拿出一点来。你可以通过一些方式分享你的天赋，

## 萨韦里亚

【https://saweria.co/pandhuwibowo 

![](img/0089e6c52b43886c90f7f853a7b8a73b.png)

## 特拉克特尔

[https://trakteer.id/goodpeopletogivemoney](https://trakteer.id/goodpeopletogivemoney)

![](img/d26e4901a3c5106b7c99a3c8a99d74a0.png)[](https://www.npmjs.com/package/graphql-type-json?activeTab=dependents) [## graphql-type-json

### 这个包导出一个 JSON 值标量 GraphQL.js 类型:它也导出一个 JSON…

www.npmjs.com](https://www.npmjs.com/package/graphql-type-json?activeTab=dependents) [](https://github.com/taion/graphql-type-json) [## GitHub-taion/graph QL-type-json:graph QL . js 的 JSON 标量类型

### 这个包导出一个 JSON 值标量 GraphQL.js 类型:它也导出一个 JSON…

github.com](https://github.com/taion/graphql-type-json) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)