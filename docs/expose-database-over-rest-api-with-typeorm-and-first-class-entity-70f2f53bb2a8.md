# 用 TypeORM 和一流实体公开 Rest 之上的数据库 API

> 原文：<https://javascript.plainenglish.io/expose-database-over-rest-api-with-typeorm-and-first-class-entity-70f2f53bb2a8?source=collection_archive---------4----------------------->

![](img/91c485c6b507747edb5be0b13d5e7bda.png)

Photo by [Arnold Francisca](https://unsplash.com/@clark_fransa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

通过 REST API 公开数据库似乎是一个疯狂的想法。但是有了良好的 API 设计、适当的安全处理和定制选项，它可以为立即构建 API 提供优势。

对于一个需要创建具有后端功能的应用程序的小团队或全栈程序员来说，这很有帮助，因为他们需要集中精力为用户体验创建一个好的 UI/UX。

在这个故事中，我将解释称为一级实体的 [Plumier](https://plumierjs.com) 特性，它在内部使用 TypeORM 进行数据访问。一流的实体注重安全性、定制性和清晰性。一流的实体保证公开的 API 是安全的，完全可定制的，并且对于安全审查是透明的。

对于不熟悉的人来说，Plumier 是一个 TypeScript 后端框架，它专注于工作效率，并有一个专用的反射库来帮助您愉快地创建一个健壮、安全和快速的 API。

## 挑战

出现的一些问题与通过 API 公开数据库有关，尤其是通过 Rest API 公开 SQL 数据库。大多数都是安全问题，但也有更多。

*   它是如何处理关系的？一对多、多对一和一对一？如何设置关系数据？以及如何检索与父母记录相关的记录？
*   由于数据库表可能包含敏感数据，它如何防止数据泄漏？它如何基于用户角色保护读/写访问？
*   在保存记录之前，它如何处理密码哈希等微过程？保存数据后，它是否会发送通知(电子邮件或推送通知)？或者甚至使用请求上下文值，比如获取`createdBy`列的当前登录用户？
*   由于表是在使用 REST API 时直接公开的，它如何处理查询(过滤、选择、排序)？它如何确保查询对敏感数据无害？

在深入细节之前，我们将先了解一下这个一流的实体是什么样子的，以及 Plumier 是如何在幕后处理它的。

## **术语**

第一类实体是指在框架组件中被视为第一类公民的 ORM(对象关系映射)实体。它比普通的 ORM 实体有更多的控制权，这使得它可以安全地作为 API 公开。除了作为表模式表示的原始任务之外，第一类实体还可以控制框架特性，例如。

*   对应用编程接口网址的控制。
*   对验证的控制。
*   控制值/数据类型转换的请求和响应模式。
*   对安全和授权的控制。

一流的实体不是 ORM 特有的特性，相反，它是 Plumier 提供的实体的独立扩展特性。通过一些规范化，它可以应用于其他 ORM。

## 它是如何工作的？

最简单的一级实体是一个用 Plumier 配置修饰的 TypeORM 实体，如下所示。

通过像上面一样在实体上应用`@genericController()` decorator，Plumier route generator 知道实体将由通用控制器处理。Plumier 有一些内置的通用控制器，它们将成为每个控制器的基类。例如，对于简单(非关系)实体，基本通用控制器如下所示。

上面是内置通用控制器的简化版本。它有`T`通用参数，这将是响应的模型和请求体，在本例中，请求体是实体。

它还有定义实体 ID 的数据类型的`TID`参数，此外，这用于检查 ID 为的资源标识符上 ID 的数据类型，如`GET /path/:id`、`PUT /path/:id`等。它确保提供的值与实体 ID 的数据类型相匹配。

Plumier 反射库支持泛型类型自省，这使得 Plumier 路由生成器可以生成从泛型控制器继承的控制器。在后台，Plumier route generator 动态创建一个新的控制器，如下图所示。

上面的控制器继承了它的所有基类方法，这些方法产生了下面的六条路线。

```
GET    /products       # get products list
GET    /products/:id   # get product by id
POST   /products       # add new product
PUT    /products/:id   # replace product
PATCH  /products/:id   # modify product 
DELETE /products/:id   # delete product
```

## 它是如何处理对象关系的？

一个 ORM 实体拥有一对一或多对一的关系是很常见的行为，这通常有一个 object 的数据类型，例如，我们的最后一个 Product 实体可能拥有类型为`Category`的`category`属性。

问题是，我们将如何设置`category`属性的值？因为它只是一个引用属性，所以它的值是`Category`的 ID，而不是 category 对象本身。另一个重要的问题是，由于`category`属性的数据类型是`Category`类型，我们不可能提供 number(ID)类型的值，因为框架类型转换器会拒绝它。

Plumier 通过提供一个自定义类型转换器来解决这个问题，它允许通过 ID 匹配对象 ID 数据类型来设置对象关系，并保持数据类型转换。所以在这种情况下，我们可以像下面这样在`POST`方法上发送产品请求体。

```
POST /products
{    /** ---- other properties ---- **/ // use the ID instead of the category object 
   "category": 20
}
```

`category`属性在请求产品 API `GET /products`或`GET /products/:id`时也会自动填充，解决了检索对象关系时的问题。

## 它是如何处理数组关系的？

与对象关系不同，在数组关系中设置值可能会有问题，因为它不能通过提供 id 来完成。例如，当修改记录时，不清楚是打算添加集合还是用新值替换当前集合。当属性有大量记录时，检索值也有问题，这通常通过分页来解决。

REST 在描述嵌套资源时有最佳实践。这是通过使用嵌套的资源标识符(URL)来实现的，例如。

```
GET    /parents/{parentId}/children?offset&limit&filter
GET    /parents/{parentId}/children/{id}
POST   /parents/{parentId}/children
PUT    /parents/{parentId}/children/{id}
PATCH  /parents/{parentId}/children/{id}
DELETE /parents/{parentId}/children/{id}
```

Plumier 遵循这些实践，并提供了一个特殊的通用控制器来服务嵌套资源。例如，有一个实体与关系商店-产品像下面的例子。

注意，`@genericController()`装饰器直接应用于`products`属性。它告诉 Plumier route generator 在生成路线时使用嵌套的通用控制器。因此，它会生成下面的嵌套路由。

```
GET    /shops/:pid/products       # get shop's products list
GET    /shops/:pid/products/:id   # get shop's product by id
POST   /shops/:pid/products       # add new shop's product
PUT    /shops/:pid/products/:id   # replace shop's product
PATCH  /shops/:pid/products/:id   # modify shop's product
DELETE /shops/:pid/products/:id   # delete shop's product
```

## 它如何保护数据？

最后，我们到达了故事最重要的部分。我们如何保护被 API 客户端访问(读/写)的敏感数据，比如密码或信用卡号被泄露？时间戳或删除标志被覆盖？甚至我们如何保护基于用户角色的敏感数据？

Plumier 具有基于策略的授权，可以应用于第一类实体声明，旨在保护 API 端点、请求体和响应体。我们最后一个产品实体是这样的。

上面的代码片段显示，我们添加了一些配置，根据用户的角色来限制对用户的访问。

1.  我们配置通用控制器来限制对其变异器(`PUT`、`PATCH`、`POST`、`DELETE`)端点的访问，只有`ShopOwner`和`Staff`策略可以访问。
2.  我们保护仅可通过`ShopOwner`和`Staff`策略访问的`basePrice`财产。因为我们已经保护了 mutators 端点，所以没有必要保护对`basePrice`属性的写访问，因为路由授权比其他授权评估得更早。
3.  我们保护的`price`属性只能由`ShopOwner`策略设置，任何人都可以看到。
4.  我们保护`createdOn`不被任何人覆盖。因为它将由 TypeORM 填充。

定义策略`ShopwOnwer`和`Staff`非常简单。诀窍在于我们在登录过程中在 JWT 令牌上添加的角色声明。然后，我们检查授权逻辑声明，如下所示。

## 它是如何解决请求上下文过程的？

如前所述，API 有时需要在实体保存到数据库之前或之后执行一些微处理。TypeORM 提供了[实体监听器](https://typeorm.io/#/listeners-and-subscribers)在实体事件中执行一些微进程，如`BeforeInsert`、`AfterInsert`、`BeforeUpdate`、`AfterUpdate`等。但是，我们不能依赖它们，因为这不是一个请求上下文流程。我们无法从方法内部检索请求数据。

Plumier 提供了[请求钩子](https://plumierjs.com/generic-controller#request-hook)，这是一个由专门的中间件内部调用的方法。它支持的[参数绑定](https://plumierjs.com/controller/#parameter-binding)，可以轻松地将请求上下文值绑定到方法参数中，以供将来使用。

例如，在我们之前的产品实体中，我们添加了`createdBy`实体，该实体将自动填充当前登录用户。

上面代码的重要部分是从第 9 行到第 16 行。首先，我们用`@authorize.readonly()` decorator 保护`createdBy`属性，防止任何用户覆盖该属性的值。然后我们提供了`@preSave("post")`钩子，它将方法标记为在实体保存到数据库之前执行的请求钩子。注意，它使用了`post`过滤器，这意味着钩子只调用了`POST`方法。

然后在第 14 行，我们绑定请求上下文值(JWT 声明),用于填充`createdBy`属性的值。

## 它是如何处理查询的？

由于表直接暴露在一个 API 上，默认情况下，当获取记录列表时会以默认的模式和顺序返回记录。它需要进一步的查询(过滤、选择、排序)来使返回的数据符合我们的需要。

回到 REST 最佳实践，使用如下查询字符串定义 REST 标识符的额外参数。

```
GET /users?name=john&deleted=false
```

使用查询字符串的问题是，API 客户端不可能使用复杂的过滤来查询数据，比如使用`OR`操作符，甚至不能使用分组过滤，比如`(name=john or name=jane) and deleted=false`。

Plumier 提供了[查询解析器](https://plumierjs.com/query-parser/)，它提供了一个简单的表达式语言解析器。它提供了三种类型的解析器，即:过滤解析器、选择解析器和顺序解析器。基于上述问题，可以通过以下请求轻松解决。

```
GET /users?filter=((name='john' or name='jane') and deleted=false)
```

也可以像下面一样同时提供订单和选择。

```
# get list users which is not deleted
# select only the name and email
# order by createdAt descendingGET /users?filter=(deleted=false)&select=name,email&order=-createdAt
```

上面的查询字符串没有直接解析为 SQL 查询，而是解析为 TypeORM 查询。所以保证会妥善处理 SQL 注入。

查询解析器尊重用户对查询属性的访问。它检查用户是否拥有对该属性的读取权限。比如下面给我们之前的产品实体。

基于上面的配置，我们将对`basePrice`属性的读取权限只授予特定的角色。这意味着查询`basePrice`也只适用于那些角色。

```
GET /products?filter=basePrice > 200
```

上述请求仅在当前登录用户拥有`ShopOwner`或`Staff`角色时有效。否则将返回 HTTP 错误 401 或 403。这个安全限制也适用于选择解析器和顺序解析器。

## 更极端的定制？

第一类实体是如此的灵活，`@genericController()`接受一些配置来定制你需要的通用控制器行为，你可以在这里查看全面的文档[。如果这些定制不能满足您的需要，您可以省略使用一级实体，手动创建控制器，或者直接扩展通用控制器。Plumier 提供了一个工厂来创建可重用的通用控制器，如下所示。](https://plumierjs.com/generic-controller)

`GenericController`是一个返回通用控制器类的工厂函数。你可以把上面的控制器放在你的项目目录的任何地方，Plumier 会像对待一个普通的控制器一样对待它们。

请记住，上述修改很少需要，大多数情况下所有的`@genericController()`配置都可以解决您需要的定制。

## 遗言

最后，我们来到了这个故事的结尾。如果您一直在关注上面的故事，那么您现在已经理解了一级实体如何通过直接公开数据库和提供良好的 API 端点来加速您的 API 开发，同时维护您的数据的安全性。在这里参考关于如何开始一个一流实体项目[的 Plumier 文档。](https://plumierjs.com/quick-start)

Plumier 是一个相对年轻的框架。如果你喜欢这个特性，可以在它的 [GitHub 库](https://github.com/plumier/plumier)上开始这个项目。

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)