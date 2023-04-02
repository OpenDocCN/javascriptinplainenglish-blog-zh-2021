# 8 个对 Web 开发有用的 JavaScript 代码片段

> 原文：<https://javascript.plainenglish.io/eight-useful-javascript-snippets-for-web-development-d8bd15a9bc22?source=collection_archive---------6----------------------->

![](img/be593633dcee1ca7ac1a011ddf047d7a.png)

JavaScript 一直被列为顶级编程语言是有充分理由的。它的灵活性适合初学者和高级开发人员。它不需要环境设置——只需打开浏览器，导航到它的开发工具，然后开始编码。

它还可以在任何地方运行，从移动设备和平板电脑到具有全栈开发能力的笔记本电脑和台式机。JavaScript 的全平台特性使其成为一种通用语言，再加上 React、Angular 和 Vue.js 等现代框架，很容易看出它是如何成为 web 标准语言的。简而言之，JavaScript 已经存在，下面是一些有助于您开发工作的片段。

# 1.将数组转换为 CSV 格式

```
const arrayToCSV = (arr, delimiter = ',') =>
 arr.map(v => v.map(x => `"${x}"`).join(delimiter)).join('\n');

arrayToCSV([['a', 'b'], ['c', 'd']]); *// '"a","b"\n"c","d"'*
arrayToCSV([['a', 'b'], ['c', 'd']], ';'); *// '"a";"b"\n"c";"d"'```
```

# 2.平滑滚动到当前页面的顶部

```
const scrollToTop = () => {
 const c = document.documentElement.scrollTop || document.body.scrollTop;
 if (c > 0) {
 window.requestAnimationFrame(scrollToTop);
 window.scrollTo(0, c - c / 8);
 }
};

scrollToTop();
```

# 3.从字符串中移除 HTML/XML 标签

从 HTML/XML 元素中提取原始文本的简单方法。

```
const stripHTMLTags = str => str.replace(/<[^>]*>/g, '');

stripHTMLTags('<p><em>lorem</em> <strong>ipsum</strong></p>'); 
*// 'lorem ipsum'*
```

# 4.打印页面链接

这个特殊的片段允许开发人员利用浏览器内置的快速打印功能。

```
<a href="javascript:window.print();">Print Page</a>
```

# 5.格式化日期

在网页的任何地方显示当前日期，而不需要经常更新。设置好了就算了。

```
 function showDate() {
   let = new Date();
   let current_date = d.getDate();
   let current_month = d.getMonth() + 1; //months are zero based
   let current_year = d.getFullYear();
   document.write(current_date + "-" + current_month + "-" + current_year);
  }
```

# 6.具有可选延迟的页面重定向

一个相当有价值的小片段放在你的后口袋里。

```
setTimeout( "window.location.href = 'http://website.com/'", 5*1000 );
```

# 7.将消息打印到状态栏

以吸引用户眼球的方式向用户显示最近的或重要的信息。

```
window.status = "Your message here";
```

# 8.允许用户通过链接轻松地为您的网站添加书签

像这样的小功能可以增加用户的整体体验。

```
<a href="javascript:window.external.AddFavorite('http://www.yoursite.com', 'your site name')">Add to Favorites</a>
```

## 结论

感谢你阅读这 8 个片段。我希望你已经发现它们有用。这些片段对你来说是新的吗？如果有，请在评论中告诉我！