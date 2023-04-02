# 创建一个抽象的 BaseService，将 Supabase 与 Angular 一起使用

> 原文：<https://javascript.plainenglish.io/create-an-abstract-baseservice-to-use-supabase-with-angular-ba895175602e?source=collection_archive---------4----------------------->

![](img/f9d8f7b1b9d75ea2bff3f29e5144ffad.png)

Photo by [Yogi Purnama](https://unsplash.com/@yogipurnama?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Supabase 是镇上的新英雄！它正忙着把像你我这样的可怜的开发人员从讨厌的供应商束缚中解救出来。让我们看看如何在 Angular 中使用 Supabase，而不牺牲你我所热爱的 RxJS-y 风味。

我们将创建一个使用@supabase/supabase-js 客户端库的`BaseService<T>`。您将能够扩展该抽象服务，并将其用于应用程序的实体。

## 连接器服务

让我们首先创建连接器服务。请注意，我们需要来自 supabase 项目的`apiKey`和`anon`(或`public`)键。在这里，我正在导入存储在`environment.ts`文件中的密钥。

supabase.service.ts

所有的方法都很简单。只需要注意一个方法——`table(resource: string)`，这只是一个返回我们经常需要的`SupabaseQueryBuilder`类的小抽象。

## 助手类型

现在我们可以创建`BaseService.`来以一种类型化的方式编写查询构建器，我们可以创建一些帮助器类型，如下所示:

*如果你想知道——我是从哪里得到 FilterOperators 的，你可以看看* [*PostgREST 文档*](https://postgrest.org/en/stable/api.html#operators) *。*

## 基础服务

最后，我们能够编写我们的服务。

我们编写了基本的 CRUD 方法。超级电话是基于承诺的。这意味着理想情况下你必须使用`async/await`或回调函数来处理它们。但是我们希望保留反应性，因为大多数 Angular 开发人员习惯于使用反应性编程。RxJS 运营商`from`撬动我们的欲望！官方文件说—

> [**from**](https://rxjs.dev/api/index/function/from)**:***从数组中创建一个可观察对象，一个类数组对象，一个承诺，一个可迭代对象，或者一个类可观察对象。*

## 履行

现在让我们看看如何使用 BaseService 来对我们选择的实体执行 CRUD 操作:

现在，您可以像使用 Angular 中的常规休息服务一样使用该服务。

感谢阅读！

*更多内容请看*[***plain English . io***](http://plainenglish.io/)