# 使用 Cheerio 进行网页抓取

> 原文：<https://javascript.plainenglish.io/web-scraping-with-cheerio-d4061e703411?source=collection_archive---------13----------------------->

## Cheero 介绍——一种流行的节点 web 解析器。

![](img/9a88051bf33d6bb8a85921f2a8686014.png)

Bowl of Cheerios Photo By [John Matychuk](https://unsplash.com/@john_matychuk) on [Unsplash](https://unsplash.com/)

# 介绍

最近我一直在开发一个 API 来提供棒球统计数据，因为我还没有找到一个免费的有深度统计数据的 API。在这个过程中，我一直在学习许多新技能，我想谈谈 [cheerio](https://www.npmjs.com/package/cheerio) ，这是一个流行的抓取和解析 web 内容的节点包。首先，将 [node-fetch](https://www.npmjs.com/package/node-fetch) 和 cheerio 添加到 package.json 中，并将它们导入 JavaScript 文件。

```
import cheerio from cheerio
import fetch from node-fetch
```

顺便提一下，您会注意到我导入了这些文件，而不是需要它们。可以通过将`"type": "module"`添加到 package.json 文件中来实现这一点。我这样做的原因有两个:一方面，我认为 ES6 语法看起来更干净，与你在许多前端框架中看到的一致，另一方面，它允许你在代码的顶层使用`await`关键字。

# 抓取维基百科

在本教程中，我们将创建一个 scraper 来获取所有美国总统的列表。我们将从[维基百科](https://en.wikipedia.org/wiki/List_of_presidents_of_the_United_States)中抓取。前往该页面并查看页面源代码。搜索“乔治·华盛顿”的出处。您会发现页面上出现了 13 次，并注意到在第 12 次出现时有一个总统列表，每个总统都有一个带有 href 属性的“a”标记，它遵循相同的基本格式:“/wiki/Presidency _ of _ first name _ last name”。这对于抓取来说非常理想，因为我们可以抓取所有的‘a’标签，并过滤掉那些 href 属性与格式不匹配的标签。为此，首先我们定义一个异步函数，然后使用 cheerio 加载并解析我们的网站:

```
// Keep scrape function dynamic by adding url and query parameter
const scrape = async (url, query) => {
  // First we fetch from our url 
  const website = await fetch(url)
    .then(res => res.text())

  // next we load the website with cheerio
  const $ = cheerio.load(website) // Then we can grab our a tags
  let queryRes = $(query).toArray() return queryRes
}// parse wiki page
const parsePresidents = async () => {
  const query = 'a'
  const url =   "[https://en.wikipedia.org/wiki/List_of_presidents_of_the_United_States](https://en.wikipedia.org/wiki/List_of_presidents_of_the_United_States)"    // Grab our collection of a tags returned by scrape
  let aTags = await scrape(url, query) // Finally we can filter our a tags
  aTags = aTags.filter(
    a => 
      a.attribs.href?.match(/Presidenc[a-z]*_of/)
  ) ... 
```

你可能想知道为什么我们定义一个常数为`$`。实际上，您如何命名您的常量并不重要，但是在 cheerio 的文档中，他们使用了`$`，所以这也是标准的做法。Cheerio 是 jQuery 的子集，所以这就是它的来源。您还会注意到我们在过滤‘a’标签时使用的正则表达式。当我写这篇文章的时候，这对我来说有点“迷惑”,但是如果你花一分钟回到页面源代码，你会注意到对于格罗弗·克利夫兰，href 实际上读的是“Presidencies _ of”而不是“Presidency”。他连任两届总统。因此，你看到的`[a-z]*`将匹配任何字母任意次。您也可以使用`.*`来匹配[中的任何字符](https://www.w3schools.com/jsref/jsref_regexp_dot.asp)或`\w*`来匹配[中的任何单词字符](https://www.w3schools.com/jsref/jsref_regexp_wordchar.asp)，但是在这种情况下，更具体一些也无妨。

接下来，我们需要将我们收集的“a”标签映射到总统的名字。如果您还记得，href 属性的格式是“Presidency _ of _ first name _ last name”。因此，我们可以在每个下划线处拆分 href，在“of”之后分割结果数组，并在空格上连接这些元素:

```
 ... let presidents = aTags.map(
    a =>
      // Some of the presidents have middle initials
      a.attribs.href // 'Presidency_of_James_K._Polk'
      .split('_') // ['Presidency', 'of', 'James', 'K.', 'Polk']
      .slice(2)   // ['James', 'K.', 'Polk']
      .join(' ')  // 'James K. Polk'
  ) ...
```

我们现在有一个所有总统名字的数组。唯一的问题是，如果你运行这个程序并查看总统名单，他们都是重复的。这是因为对于每一位总统来说，实际上有两个“a”标签符合我们的标准。这没有问题，我们可以通过唯一性来过滤总统数组:

```
 ...

  presidents = presidents.filter(
    (ele, i, array) => 
      array.indexOf(ele) === i
  ) return presidents
}
```

如果您对此感到陌生，让我快速解释一下这是怎么回事。对于数组中的每个元素，我们查看元素本身、它在数组中的索引以及数组本身。当我们调用`array.indexOf(ele)`时，它返回数组中匹配我们的元素的第一个索引，因此对于重复的元素，表达式`array.indexOf(ele) === i`将返回 false，它们将被过滤掉。

# 结论

Cheerio 是抓取和解析网站的优秀工具，但有一个主要缺点:它不加载外部资源或执行 JavaScript。所以对于依靠 JavaScript 来呈现数据的网站，你需要使用一个无头的 chromium 包，比如[木偶师](https://www.npmjs.com/package/puppeteer/v/1.11.0-next.1547527073587)，来模仿用户行为。我将很快写一篇关于木偶师的文章，但现在，我希望你喜欢这篇文章，并发现它很有帮助。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)