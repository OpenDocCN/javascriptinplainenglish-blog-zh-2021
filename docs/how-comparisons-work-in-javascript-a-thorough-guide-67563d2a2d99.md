# JavaScript 中的比较是如何工作的:全面指南

> 原文：<https://javascript.plainenglish.io/how-comparisons-work-in-javascript-a-thorough-guide-67563d2a2d99?source=collection_archive---------14----------------------->

![](img/285e4fd3fc0866ed031d8182b09c7957.png)

几年前看过凯尔·辛普森的 JS 系列丛书[《你不知道的 JS》](https://github.com/getify/You-Dont-Know-JS)的部分内容。现在有第二版正在进行中，我开始重读它。正如作者本人所推荐的，这些书要多看几遍。它们需要适当消化，因为内容很重。所以我又读了一遍关于比较的章节，这是我写下我所学到的东西的尝试。

# `==`和`===`有什么区别？

当你申请前端开发人员的职位时，你可能会被问到这个问题。你可能会回答,“三等”`===`更严格。这意味着`===`不允许强制，即从一个值类型到另一个值类型的转换。这里有一个例子:

```
‘2’ == 2 => true 
‘2’ === 2 => false
```

很好。我认为这是一个相当充分的答案。但是，哦，亲爱的，还有这么多。让我们回顾更多的 Javascript 基础知识。有原始值类型和对象。常见的原语有:

*   线
*   数字
*   布尔代数学体系的
*   空
*   不明确的

作为对象，我们可以对数组甚至函数进行分类。

# 比较原始值

我们可以使用`**typeof**` **运算符**来检查一个类型。在某些情况下，你不会得到你所期望的。

```
typeof(null) => 'object'
```

这个运算符在我们进行比较时很有用。考虑下面的例子:

```
const num1 = 9007199254740992;
const num2 = 9007199254740992n;num1 == num2    => true
num1 === num2   => false
```

这几乎不明显，但是如果我们检查类型，我们可以看到 num2 实际上是类型`bigint`，而 num 是`number`；

```
typeof(num2) => bigint
```

所以现在很清楚`==`和`===`都比较值和类型，但是`==`检查类型，如果必要的话**在比较之前转换它**。

> *JS 中所有的值比较都考虑被比较值的类型，而不仅仅是===运算符。具体来说，===在其比较中不允许任何类型转换(也称为“强制”)，而其他 JS 比较允许强制。*

Triple-equals 也有一些不符合预期的边缘情况。

```
NaN === NaN;    => false
0 === -0;       => true
```

为了检查这些值，我们可以使用`Number.isNaN()`方法。有趣的是，还有另一种比较值的方法，它不会给我们那些误导性的答案。它是`Object.is()`，它返回正确的值。

```
Object.is(null, null);  => true
Object.is(NaN, NaN) => true
Object.is(-0, -0) => true
```

# 比较对象

涉及对象的更复杂的场景呢？我们如何比较它们？正如你注意到的基本类型，我们比较了 2 个值，比如 4 === "4 "。对象通常有嵌套的属性，我们不能通过它们的结构或内容(结构相等)来比较它们。以这个物体为例:

```
let books = {
  title: 'Climate Library',
  list: [
    {
      id: 1,
      name: "[Speed & Scale](https://speedandscale.com/speed-and-scale/)",
      author: "John Doerr",
      published: "October 28th 2021"
    },
    {
      id: 2,
      name: "[A New Earth - The Apocalypse Locus](https://www.amazon.com/New-Earth-Apocalypse-Locus/dp/B09KNGHVSW/ref=sr_1_8?crid=3DJCXYOP836VI&keywords=apocalypse+earth&qid=1637416028&s=books&sprefix=apoca%2Cstripbooks-intl-ship%2C366&sr=1-8#customerReviews)",
      author: "George Tsakraklides",
      published: "November 8th 2021"
    }
  ]
}
```

除了上面的例子之外，比较`{ a: 2 } === { a: 2 }`会产生 false(如果我们试图将它与另一个对象进行比较)。这是为什么呢？

> *在 JS 中，所有的对象值都是通过引用持有的，都是通过 reference-copy 赋值和传递的，对于我们目前的讨论，都是通过引用(identity)相等来比较的。*

我们可以有另一个变量 favouriteBooks，并给它赋值 Books。那么我们可以这样比较它们:

```
let books = {...};
let favouriteBooks = {};
favouriteBooks = books;books === favouriteBooks   => true
```

`favouriteBooks`指的是同一个对象`books`，所以比较它们返回 true。

# 其他比较

请记住，还有其他关系比较运算符，如`<`、`>`、`<=`和`>=`。我们在 if 条件、循环和其他地方使用它们，值类型的转换也适用，所以要小心。

# 结论

我们了解到，即使简单的 Javascript 比较也隐藏了表面下的许多本质细节。应该用`==`还是`===`？看情况。双相等确实转换了类型！我们可以看到`Object.is()`是一种更严格的比较两个值的方法。我觉得我遗漏了很多信息，我必须一遍又一遍地阅读才能完全吸收。看看这本书，正如附录 B 所说:[练习，练习，再练习！](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/get-started/apB.md#practicing-comparisons)

这是书中的一个例子，你可以在上面练习:

`scheduleMeeting(..)`应该取一个开始时间(以 24 小时格式为字符串“hh:mm”)和一个会议持续时间(分钟数)。如果会议完全在工作日内(根据`dayStart`和`dayEnd`中指定的时间)，则返回`true`；如果会议违反了工作日界限，则返回`false`。

```
const dayStart = "07:30";
const dayEnd = "17:45";function scheduleMeeting(startTime,durationMinutes) {
    // ..TODO..
}scheduleMeeting("7:00",15);     // false
scheduleMeeting("07:15",30);    // false
scheduleMeeting("7:30",30);     // true
scheduleMeeting("11:30",60);    // true
scheduleMeeting("17:00",45);    // true
scheduleMeeting("17:30",30);    // false
scheduleMeeting("18:00",15);    // false
```

*原载于*[*https://blog . mairo . eu*](https://blog.mairo.eu/comparisons-in-javascript)*。*

*更多内容看* [*说白了。在这里注册我们的*](http://plainenglish.io/) [*免费周报*](http://newsletter.plainenglish.io/) *。*