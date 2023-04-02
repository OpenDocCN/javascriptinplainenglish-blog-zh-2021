# 如何在 JavaScript 中使用 Tokenizer

> 原文：<https://javascript.plainenglish.io/tokenizer-in-javascript-b05d29438dd7?source=collection_archive---------4----------------------->

## 如何在 JavaScript 中使用您熟悉的 Python 标记器

![](img/124eb5f0584b1f764e1f2d353991567a.png)

Photo by [Karl Pawlowicz](https://unsplash.com/@karlp?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果您已经使用 Python 为您的自然语言处理(NLP)项目创建了标记器，您可能已经知道标记器的功能。然后有一天，你想把你的项目移植到 JavaScript 中，用 Tensorflow.js 代替 Python 中的 Tensorflow，你可能会像我以前一样问自己这个问题:我怎样才能改为用 JavaScript 对来自 HTML 的输入进行标记化？

嗯，答案很简单。只要遵循这篇文章，它会节省你像我一样浏览互联网的大量时间。

首先给大家介绍一下解决方案的关键词:`**split()**`。

```
**let text = "This is an example sentence!";
let tokenizer = text.split(/\W+/);** // Remove special characters
// This will return ['This', 'is', 'an', 'example', 'sentence', '']
```

如果只使用空白 text.split(" ")，您可能会在数组中得到意外的字符(有时来自 HTML)，如下所示:

```
**let text = "This is an#%$ $%example sentence!";
let tokenizer = text.split(" ");**
// This will return ['This', 'is', 'an#%$', '$%example', 'sentence!']
```

此外，如果您想让**中的所有单词都小写和/或使用过滤器**，您可以使用带有`**filter**`关键字的`**split()**`方法，如下所示:

```
**let text =** **"This is an example sentence."****;
let filters = ['this', 'is'];

let words = text.split(****/\W+/****).filter(function(token) {
    token = token.toLowerCase();** // transform each word into lower case
   **return** **filters****.indexOf(token) == -1;** // applying filters, you could add other conditions here as well such as token.length >= 3 (at least 3 characters included in a word)
**});**

**console.log(words);**
// This will return ['an', 'example', 'sentence', '']
```

恭喜，你成功了！

# 英语以外的语言加分

如果您想对像越南语这样有复杂大小写的语言进行标记，请尝试使用`**split(" ")**` 来代替:

```
let text = "Bạn khỏe không?";    
let tokenizer = **text.split(" ");** // Example: Character 'á' is **U+00E1**
let corpus = [];
for (let i = 0; i < tokenizer.length; i++) {      
   if (tokenizer[i] == "") continue;      
   else corpus[i] = tokenizer[i].toLowerCase();    
}
console.log(corpus);
// Output: ['bạn', 'khỏe', 'không?']
```

或者

```
let text = "Bạn khỏe không?";    
let tokenizer = **text.replace(/[&\/\\#`,+()$~%.'":*!?<>{}]/g, '').split(" ");**    
let corpus = [];
for (let i = 0; i < tokenizer.length; i++) {      
   if (tokenizer[i] == "") continue;      
   else corpus[i] = tokenizer[i].toLowerCase();    
}
console.log(corpus); 
// This will return ['bạn', 'khỏe', 'không']
```

原因是当与后端通信时，这些字母可能会被翻译成 Unicode 格式，其中包含一些特殊字符，如`/`。因此，如果我们像处理英语一样省略特殊字符，输出会很奇怪！

示例:

```
let text = "Bạn tên gì?";
let tokenizer = text.split(/\W+/); // Filtering special characters
**// Output: ['B', 'n', 't', 'n', 'g', '']**
```

# 更多高级功能

如果您想创建自己的更灵活的小型标记器，可以访问我发现有用的要点:

[](https://gist.github.com/borgar/451393/7698c95178898c9466214867b46acb2ab2f56d68) [## 一个用 JavaScript 写的紧凑的记号赋予器。

### 即时共享代码、笔记和代码片段。一个用 JavaScript 写的紧凑的记号赋予器。您不能在…执行该动作

gist.github.com](https://gist.github.com/borgar/451393/7698c95178898c9466214867b46acb2ab2f56d68) 

我希望这有所帮助，请随时通过 Twitter 联系我，或者在下面留下您认为在 JavaScript 中标记文本最有用的方法的评论！

如果你觉得这个帖子有帮助，让我们击掌吧。谢谢大家！

*更多内容看* [***说白了. io***](http://plainenglish.io/) ***。*****[***免费每周简讯***](http://newsletter.plainenglish.io/) ***。*** *在我们的**[***社区不和谐***](https://discord.gg/GtDtUAvyhW) ***中获取独家写作机会和建议。******