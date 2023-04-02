# 如何删除 JavaScript 字符串中某个字符之后的所有内容

> 原文：<https://javascript.plainenglish.io/how-to-remove-everything-after-a-certain-character-df59c805ba40?source=collection_archive---------3----------------------->

![](img/b76bd9b6e065cd4fbcb37898e1bf3074.png)

Photo by [Christopher Robin Ebbinghaus](https://unsplash.com/@cebbbinghaus?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望删除 JavaScript 字符串中给定字符之后的所有内容。

在本文中，我们将看看如何删除某个字符后的所有内容。

# 字符串.原型. split

我们可以用`split`方法分割一个字符串。

例如，我们可以写:

```
const url = '/Controller/Action?id=1111&value=2222'
const [path] = url.split('?')
console.log(path)
```

获取带`split`的问号前的路径字符串。

`split`返回由给定字符分隔的子字符串数组。

所以我们可以析构返回的数组并得到第一项。

因此，`path`就是:`'/Controller/Action’`。

# string . prototype .`indexOf and` string . prototype . substring

`indexOf`方法让我们获得字符串中给定字符的索引。

我们可以将它与`substring`方法一起使用，从开头到`indexOf`返回的给定索引提取子串。

例如，我们可以写:

```
const url = '/Controller/Action?id=1111&value=2222'
const path = url.substring(0, url.indexOf('?'));
console.log(path)
```

我们调用`url.indexOf('?')`来获取问号字符的索引。

然后我们把它作为第二个参数传递给`substring`。

0 作为第一个参数意味着我们得到从第一个字符到第二个参数中传递的索引的子串。

所以`path`和之前的值一样。

# 正则表达式替换

我们也可以用正则表达式调用 string `replace`方法来删除字符串中给定字符之后的部分。

例如，我们可以写:

```
const url = '/Controller/Action?id=1111&value=2222'
const path = url.replace(/\?.*/, '');
console.log(path)
```

`/\?.*/`正则表达式匹配从问题到字符串结尾的所有内容。

因为我们传入了一个空字符串作为第二个参数，所有这些都将被一个空字符串替换。

`replace`返回应用了替换的新字符串。

所以`path`是和之前一样的值。

# 结论

有几种方法可以用来提取给定字符后的字符串部分。

## 进一步阅读

[](/best-tool-for-web-scraping-beautifulsoup-vs-regex-vs-advanced-web-scrapers-50b8fb92950d) [## 最佳网络抓取工具:beautiful soup vs . Regex vs . Advanced Web Scrapers

### BeautifulSoup、正则表达式或高级 web scraper——哪一个是 web 抓取的最佳工具？深潜…

javascript.plainenglish.io](/best-tool-for-web-scraping-beautifulsoup-vs-regex-vs-advanced-web-scrapers-50b8fb92950d) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。*****

*****对缩放您的软件启动感兴趣*** *？检查* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。***