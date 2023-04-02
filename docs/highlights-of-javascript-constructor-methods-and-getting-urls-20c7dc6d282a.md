# JavaScript 的亮点——构造函数方法和获取 URL

> 原文：<https://javascript.plainenglish.io/highlights-of-javascript-constructor-methods-and-getting-urls-20c7dc6d282a?source=collection_archive---------11----------------------->

![](img/7529dd5dd601836baf4dbccb0e256757.png)

Photo by [Ivan Bandura](https://unsplash.com/@unstable_affliction?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

要学习 JavaScript，我们必须学习基础知识。

在本文中，我们将了解 JavaScript 语言的最基本部分。

# 构造函数方法

我们可以向构造函数或类添加方法。

例如，我们可以写:

```
class Plan {
  constructor(name, price, space, pages) {
    this.name = name;
    this.price = price;
    this.space = space;
    this.pages = pages;
  } calcAnnualPrice() {
    return this.price * 12;
  }
}
```

我们加入`calcAnnualPrice`方法返回`this.price * 12`的值。

`this`是类实例，它是当我们调用`Plan`类时创建并返回的对象。

因此，我们从类创建的对象中获得`price`属性，并将其乘以 12。

要在创建的对象上调用构造函数和方法，我们可以编写:

```
const plan = new Plan('basic', 3, 100, 10)
console.log(plan.calcAnnualPrice())
```

我们用`new`关键字调用`Plan`构造函数。

然后我们在`plan`对象上调用`calcAnnualPrice`来获得年度价格。

类语法只是原型继承之上的语法糖。

`calcAnnualPrice`方法只是`Plan`的`prototype`属性的一个属性。

`prototype`是`Plan`类的原型，是它继承的对象。

如果我们记录`Plan.prototype.calcAnnualPrice`的值:

```
console.log(Plan.prototype.calcAnnualPrice)
```

我们看到记录了`calcAnnualPrice`方法的代码。

# 检查属性和方法

要检查一个属性或方法是否实际存在于对象本身而不是它的原型中，我们可以使用`hasOwnProperty`方法。

例如，如果我们从`Plan`类创建了一个对象:

```
const plan = new Plan('basic', 3, 100, 10)
```

那么我们可以这样称呼`hasOwnProperty`:

```
console.log(plan.hasOwnProperty('name'))
```

然后我们应该看到`true`被记录，因为`name`是`plan`对象本身的属性。

`hasOwnProperty`方法来自于`Object.prototype`，这是几乎所有 JavaScript 对象的属性。

如果我们想列出一个对象的属性，我们可以写:

```
for (const prop in plan) {
  if (plan.hasOwnProperty(prop)) {
    console.log(prop);
  }
}
```

我们用 for-in 循环遍历`plan`的属性键。

for-in 循环遍历所有属性及其原型，所以我们必须使用`hasOwnProperty`方法来检查属性是否实际上存在于`plan`对象本身中。

`prop`是属性名称本身。

因此，我们应该看到:

```
name
price
space
pages
```

已记录。

# 获取 URL

我们可以用 JavaScript 获取并设置页面的 URL。

要获取 URL，我们可以使用`window.location.href`属性。

如果我们输入到浏览器开发控制台，我们应该得到完整的网页网址。

`window.location.hostname`的主机名是 URL 的第一部分。

例如，如果我们有 URL `“https://jsfiddle.net/09t6La27/10/"`，那么`window.location.hostname`返回`“jsfiddle.net”`。

`window.location.hash`返回 URL 中位于`#`符号之后的部分。

例如，如果我们有`http://example.com/#foo`，`window.location.hash`返回`“#foo”`。

# 结论

我们可以给构造函数或类添加方法。

同样，我们可以用`window.location`对象获取 URL 的一部分。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**