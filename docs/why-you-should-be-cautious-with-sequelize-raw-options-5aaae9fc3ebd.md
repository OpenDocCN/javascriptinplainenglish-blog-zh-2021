# 为什么您应该谨慎对待 Sequelize Raw 选项

> 原文：<https://javascript.plainenglish.io/why-you-should-be-cautious-with-sequelize-raw-options-5aaae9fc3ebd?source=collection_archive---------3----------------------->

## 在使用 Sequelize Raw 查询时，您应该更有意识

![](img/abeea06e264e49bad4053966c5ef2520.png)

Photo by [Caspar Camille Rubin](https://unsplash.com/@casparrubin?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在这个故事中，我将记录我自己在 Sequelize ORM 中使用`raw`选项的经历。

虽然我告诉你要小心使用 raw 选项，但这并不意味着我说不要使用它。其实我们用的时候只要更用心就好了。这仅仅意味着**我知道自己在做什么，也知道为什么要这样做。**当您尝试使用`raw`选项时，请回答以下问题。

> 我知道我在这个查询中使用了`{ raw: true }`,我使用它是因为…

这个故事可以分为三个部分:

*   为什么我要使用`raw`选项？(我的目的)
*   我遇到了什么问题？
*   有没有更好的方法可以毫无问题地达到我的目的？

事不宜迟，我们开始吧。

# 为什么我要使用`raw`选项？

此时，你可能会问我——为什么要使用那个`raw`选项？你想要的产出到底是什么？我很高兴你问这个问题。

将`raw`设置为`true`的主要区别是缺少虚拟设置器、获取器和一堆序列数据。有关返回的输出差异，请参考以下要点。

Sample of different outputs for raw option

所以在我的大多数情况下，我只想要数据库中的数据。这里可能没有使用 Sequelize setters 和 getters。**因此将** `**raw**` **设置为 true 为我提供了想要的输出，看起来&感觉**。

# 布尔类型的问题

大多数时候，使用`raw`属性不会给你带来太多的问题。但是，它会影响**布尔**数据类型字段。你们大多数人可能都知道:

> **MySQL 不包含内置的布尔**或 Bool 数据类型。它们提供 TINYINT 数据类型，而不是 Boolean 或 Bool 数据类型。MySQL 认为零值为假，非零值为真。——[Javatpoint.com](https://www.javatpoint.com/mysql-boolean#:~:text=MySQL%20does%20not%20contain%20built,to%200%20and%201%20value.)

因此，在 Sequelize 中使用 raw 选项将为布尔字段返回一个 0 或 1 的数字，因为 MySQL 使用`TINYINT`而不是布尔。

# 更好的方法——使用 toJSON

更好的方法是在顺序模型中使用`toJSON`函数。使用`toJSON`时，代码和输出请参考以下要点。

`toJSON`函数调用帮助我获得了想要的结果:

*   具有更清晰外观和感觉的数据(没有与对象相关的序列)
*   `sold_out`字段作为布尔值而不是数字返回。

# 结论

简而言之，这个故事分享了我使用 Sequelize `raw`选项的经验，设置`raw`为真将改变你的布尔期望字段为数字，最后，我们可以使用一个更好的方法，即`toJSON`来实现我想要的结果。

感谢阅读。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)