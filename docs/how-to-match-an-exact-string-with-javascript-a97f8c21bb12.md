# 如何用 JavaScript 匹配一个精确的字符串？

> 原文：<https://javascript.plainenglish.io/how-to-match-an-exact-string-with-javascript-a97f8c21bb12?source=collection_archive---------3----------------------->

![](img/7bc580638a55b15a955d8bcf22013ec0.png)

Photo by [Fionn Große](https://unsplash.com/@fionngrosse?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望在 JavaScript 代码中找到一个精确的字符串。

在本文中，我们将看看如何用 JavaScript 找到一个精确的字符串。

# 使用 String.prototype.match 方法

我们可以使用 JavaScript string 实例的`match`方法来搜索匹配给定模式的字符串。

例如，我们可以写:

```
const str1 = 'abc'
const str2 = 'abcd'
console.log(str1.match(/^abc$/))
console.log(str2.match(/^abc$/))
```

用与单词完全匹配的正则表达式调用`match`。

`^`是单词开头的分隔符。

而`$`是单词结尾的分隔符。

因此，正则表达式匹配分隔符之间的精确单词。

第一个控制台日志应该将`'abc'`记录为匹配项。

第二控制台日志应该记录`null`。

我们可以将匹配的字符串转换成数组。

例如，我们可以写:

```
const str1 = 'abc'
console.log([...str1.match(/^abc$/)])
```

我们使用 spread 操作符将 match 对象转换为数组，因为 match 对象是一个 iterable 对象。

# 结论

我们可以通过使用 JavaScript 字符串的`match`方法和一个 regex 模式来用 JavaScript 匹配一个精确的字符串，这个 regex 模式有字符串的开始和结束的分隔符，中间有精确的单词。

## 进一步阅读

[](/best-tool-for-web-scraping-beautifulsoup-vs-regex-vs-advanced-web-scrapers-50b8fb92950d) [## 最佳网络抓取工具:beautiful soup vs . Regex vs . Advanced Web Scrapers

### BeautifulSoup、正则表达式或高级 web scraper——哪一个是 web 抓取的最佳工具？深潜…

javascript.plainenglish.io](/best-tool-for-web-scraping-beautifulsoup-vs-regex-vs-advanced-web-scrapers-50b8fb92950d) 

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，* [***不和***](https://discord.gg/GtDtUAvyhW) ***。*****

***有兴趣规模化你的软件创业*** *？检查* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。*