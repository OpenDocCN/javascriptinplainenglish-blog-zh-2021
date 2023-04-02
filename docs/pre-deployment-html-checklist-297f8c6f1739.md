# 部署前 HTML 清单

> 原文：<https://javascript.plainenglish.io/pre-deployment-html-checklist-297f8c6f1739?source=collection_archive---------15----------------------->

## 适用于任何网站的 HTML 元素和良好实践列表

![](img/c410bbd99e48245ba54c9b1a6c29e455.png)

Image by [Valery Sysoev](https://unsplash.com/@valerysysoev) on [Unsplash](https://unsplash.com/photos/p9OkL4yW3C8)

HTML 标记用于创建任何网站的框架。这个博客是你的网站中 HTML 元素的汇编，用来检查你是否指定了所有必需的标签。由于 HTML 不显示任何错误，因此需要遵循良好的编码实践。

*基于您的使用案例的使用变更需求。*

这些是你可以在你的网站中使用的一些标签/做法，以提高可读性，搜索引擎优化，可访问性和网站的整体性能。

*   确保良好的文档结构——标签的缩进和正确嵌套；不要忘记结束标签。

```
<html>
   <head> 
      <!-- other HTML elements-->
   </head>
   <body>
      <!-- other HTML elements-->
  </body>
</html>
```

*   使用`<!DOCTYPE html>`标签——给浏览器一个关于用于编码网站的 HTML 版本的提示。

```
**<!DOCTYPE html>**
<html>
  <!-- other HTML elements-->
</html>
```

*   使用`head`标签指定网站特定信息

```
<!DOCTYPE html>
<html lang="en">
  <head>
     <title>HTML Head Example</title>
  </head>
  <body>
     <!-- other HTML elements-->
  </body>
</html>
```

*   使用`title`标签在浏览器的标题栏中指定网站的名称。建议使用 50-60 个字符的标题。建议在你的网站上为不同的网页使用不同的标题。

```
<!DOCTYPE html>
<html>
  <head>
    <title>HTML Title Example</title>
  </head>
</html>
```

*   使用`meta`标签指定字符编码`UTF-8`——将键入的字符转换成机器可读的代码，并提供向后兼容性

```
<meta **charset="UTF-8"**>
```

*   总是使用`meta`标签来指定`viewport`。它定义了网站将显示的窗口大小，可以用来改善网站的外观。设置视口的宽度和初始比例。

```
<meta name="**viewport**" content="**width=device-width, initial-scale=1, viewport-fit=cover**">
```

*   使用`meta`标签添加一个`description` —描述您的网站，并在任何搜索引擎中显示时显示在 URL 下方。建议使用 50-160 个字符的描述。

```
<meta name="**description**" content="**Description of the page between 60 and 150 characters**">
```

*   使用`meta`标签提及网站的`author`

```
<meta name='**author**' content='**Jane Doe**'>
```

*   使用`meta`标签添加任何特定于网站的`keywords`

```
<meta name='**keywords**' content='**all, your, tags**'>
```

*   当您想要强调网站上多个相似页面的主页时，请在`link`标签中使用`[canonical](https://moz.com/learn/seo/canonicalization)`属性

```
<link rel="**canonical**" href="https://sample-webpage.com" />
```

*   使用`nofollow`属性指定搜索引擎不应该使用`link`进行页面排名计算

```
<a rel="**nofollow**" href="https://www.sample-webpage.com" />Sample</a>
```

*   使用`language`属性指定网站的语言

```
<html **lang="language-code"**>
```

*   使用`hreflang`标签和属性来指定语言；对于搜索引擎向用户提供特定语言网站的 SEO 非常有用

```
<link rel="alternate" href="https://fr.example.com/" **hreflang="fr"** /><link rel="alternate" href="https://en-us.example.com/" **hreflang="en-us"** />
```

*   当网站以多种语言提供内容并且不特定于语言时，在`hreflang`标签中使用`x-default`

```
<link rel="alternate" href="http://example.com/" **hreflang="x-default"** />
```

*   在`bdo`标签中使用一个`direction`属性来指定文本从`left to right — ltr`(默认)或`right-to-left — rtl`的方向

```
<bdo **dir="ltr"**>
<!-- some text -->
</bdo>
```

*   使用`link`标签将`html`链接到`css`文件。建议使用`external` CSS，不要使用`inline`或`internal`。

```
<link rel="stylesheet" href="style.css">
```

*   如果需要，在`head`标签内和`style`标签之间指定`internal` CSS

```
<!DOCTYPE html>
<html>
  <head>
    <style>
       body {
         background-color: lightblue;
       }
       h1 {
         color: navy;
         margin-left: 20px;
       }
    </style>
    <title>Internal Style Sheet Example</title>
  </head>
  <body>
     <h1>Heading:</h1>
     <p>Some text.</p>
  </body>
</html>
```

*   减少`links`的数量，使用`minified` CSS/ JS 删除代码中不必要的字符，从而减小文件大小，加快网站加载速度
*   尽可能使用`semantic`元素

`non-semantic`元素的示例— `<div class="header">`、`<div class="footer">`、`span`等

```
<div class="header">
  Some Heading!
</div><div class="nav">
  <ul>
    <li>Home</li>
    <li>About</li>
  </ul>
</div>
```

`semantic`元素的示例— `header`、`footer`、`nav`、`section`等

```
<header>
  Some Heading!
</header><nav>
  <ul>
    <li>Home</li>
    <li>About</li>
  </ul>
</nav>
```

*   给所有图像添加`alt`标签

```
<img src="images/logo.png" **alt="organization logo"** />
```

*   尽可能使用`picture`标签；它提供了基于目标浏览器指定不同大小的图像资源的灵活性

```
<picture>
  <source media="(min-width:650px)" srcset="sample-img.jpg">
  <source media="(min-width:465px)" srcset="sample-img.jpg">
  <img src="sample-img.jpg" alt="sample image">
</picture>
```

*   在媒体中指定多个来源— `audio`和`video`标签，如果它们在浏览器中不起作用，则指定一条默认消息

```
<video controls width="50%">
  <source src="example.webm" type="video/webm">
  <source src="example.mp4" type="video/mp4">
  <p>Browser doesn't support HTML5 video.</p>
</video><audio controls>
  <source src="example.mp3" type="audio/mpeg">
  <source src="example.ogg" type="audio/ogg">
  <p>Browser doesn't support HTML5 audio.</p>
</audio>
```

*   对图像和视频使用延迟加载，以减少页面加载时间和每个用户的网络带宽

```
<!-- lazy loading an image -->
<img src="test-img.jpg" alt="test image" **loading="lazy"**><!-- lazy loading a video -->
<video controls **preload="none"** poster="example.jpg">
  <source src="example.webm" type="video/webm">
  <source src="example.mp4" type="video/mp4">
</video>
```

*   使用`role`属性向屏幕阅读器描述元素的角色

```
<a href="#" **role="button"**>Button Link</a>
<!-- considered as a button and not link -->
```

*   建议在部署网站之前删除过多的评论

```
<!DOCTYPE html>
<html lang="en">
<!-- HTML head elements-->
  <head>
     <!-- head title elements-->
     <title>HTML Head Example</title>
  </head><!-- HTML body elements-->
  <body>
     <!-- body ul elements-->
    <ul>
      <!-- ul li elements-->
      <li>Home</li>
      <li>About</li>
    </ul>
  </body>
</html>
```

*   建议不要将布尔值与布尔属性一起使用

```
<label>
  <input type="checkbox" **checked** name="test-checkbox" **disabled**>Test Checkbox
</label>
<button type="button" **disabled**/>
```

*   使用`address`标签定义作者的社交媒体链接

```
<address>
  <p>Contact the author via: </p>
  <a href="mailto:example@example.com">Email</a>
  <a href="https://linkedin.com/jane-doe">LinkedIn</a>
</address>
```

*   使用`button`标签中的`type="button"`属性覆盖默认的`type=”submit”`属性

```
<button **type="button"**>Click on Button</button>
```

*   建议使用`blockquote`而不是`q`,因为后者是一个行内元素，向包含的文本添加额外的引号；前者是一个 block 元素，它引用了从其他来源引用的部分

```
<!-- blockquote -->
<blockquote cite="[http://www.worldwildlife.org/who/index.html](http://www.worldwildlife.org/who/index.html)">
  For 50 years, WWF has been protecting the future of nature. The world's leading conservation organization, WWF works in 100 countries and is supported by 1.2 million members in the United States and close to 5 million globally.
</blockquote><!-- q -->
<p>WWF's goal is to: 
<q>Build a future where people live in harmony with nature.</q>
We hope they succeed.</p>
```

*   在`block`标签中使用`inline`标签，而不是相反

```
<div class="welcome-message"> <!-- block tag -->
  <span> <!-- inline tag -->
     Hello World
  </span>
</div>
```

*   任何`script`标签都必须添加到`body`标签的末尾，或者使用`async`或`defer`属性来允许浏览器继续执行

```
<script src="script1.js"></script>
<script src="script2.js" **async**></script>
<script src="script3.js" **defer**></script>
```

*   如果浏览器不支持 JavaScript，请使用`noscript`标签显示替代选项

```
<!-- 1st example -->
<noscript>
  <link rel="stylesheet" href="noscript.css" />
</noscript><!-- 2nd example -->
<script>
  alert("JavaScript is supported by the browser");
</script>
<noscript> 
  JavaScript is not supported by the browser!
</noscript>
```

*   使用`time`标签显示特定的时间点。使用`datetime`属性将日期转换成机器可读的格式。

```
<p>The bakery is open from <time>10:00</time> to <time>21:00</time> every day.</p><p>The meeting is scheduled on <time **datetime**="2021-07-15 10:00">Friday</time>.</p>
```

*   使用`var`标签显示数学元素

```
<p>Find the value of <var>x</var> and <var>y</var>
<var>12x</var> + <var>4y</var> = 84
<var>2x</var> - <var>8y</var> = 61
```

*   使用`<article>`标签来指定独立的、自包含的内容。它独立于网站的其他部分。

```
<article class="test">
    <h1>Test Heading</h1>
    <p>This is a test paragraph.</p>
  </article>
```

*   使用`<details>`标签在交互式打开/关闭小部件中指定附加细节

```
<details>
  <summary>Open this sample widget!</summary>
  <p>This is a test widget for the <details> & <summary> tags!</p>
</details>
```

*   使用 code 标记将文本格式化为类似代码块的形式。默认情况下，标签内的信息被格式化为单空格字体。

```
<p>Try to run this in your personal system!</p>
<code>
  int <var>a</var> = 10;
  System.out.println("Value of a: " + a);
</code>
```

*   使用`map`标签创建图像地图，通过网站上的图像将其链接到不同的外部或内部页面

```
<p>Click on the individual components of the image to read more:</p><img src="sample.jpg" alt="sample image" **usemap="#workmap"** /><map **name="workmap"**>
  <area shape="rect" coords="34,44,270,350" alt="component-1" href="component1.html">
  <area shape="rect" coords="290,172,333,250" alt="component-2" href="component2.html">
  <area shape="circle" coords="337,300,44" alt="component-3" href="component3.html">
</map>
```

*   在`select`标签和`datalist`标签之间选择:`datalist`允许用户输入所提供选项之外的选项；`select`要求用户在现有选项中进行选择。

```
<select name="books">
  <option value="Harry Potter">Harry Potter</option>
  <option value="Hunger Games">Hunger Games</option>
  <option value="Tintin Comics">Tintin Comics</option>
  <option value="Mein Kampf">Mein Kampf</option>
  <option value="Imperial Blandings">Imperial Blandings</option>
</select><input type="text" list="books">
  <datalist id="books">
    <option value="Harry Potter">
    <option value="Hunger Games">
    <option value=""Tintin Comics">
    <option value="Mein Kampf">
    <option value="Imperial Blandings">
<!-- the user can enter any other book name -->
</datalist>
```

*   通过根据后端代码给出不同的`names`或`formactions`，在一个表单中使用多个`submit`按钮

```
<!-- different names -->
<button type="submit" name="update_button" value="Update"> Update</button>
<button type="submit" name="delete_button" value="Delete"> Delete</button><!-- different formactions -->
<button type="submit" formaction="/accept">Accept</button>   
<button type="submit" formaction="/reject">Reject</button>
```

*   使用`template`标签隐藏数据，并使用`JavaScript function`显示数据

```
<button onclick="showContent()">Display hidden content</button><template>
  <h2>Sample Heading</h2>
  <p>Sample Text</p>
</template><script>
  function showContent() {
    var temp = document.getElementsByTagName("template")[0];
    var clon = temp.content.cloneNode(true);
    document.body.appendChild(clon);
  }
</script>
```

*   使用`meter`标签显示进度条

```
<label for="java-course-completion">Java Course Completion</label>
<meter id="java-course-completion" value="4" min="0" max="10"></meter><br><label for="javascript-course-completion">JavaScript Course Completion</label>
<meter id="javascript-course-completion" value="0.7"></meter>
```

*   使用带有任何`input`标签的`multiple`属性来接受多个输入

```
<form action="upload-multiple-files">
  <label for="files">Select Files:</label>
  <input type="file" id="files" name="files" **multiple**>
  <input type="submit">
</form>
```

*   使用`abbr`标签指定缩写

```
<abbr title="Cascading Style Sheets">CSS</abbr>
```

*   使用`contenteditable`属性指定元素的内容是否可编辑

```
<p contenteditable="true">
  This paragraph is editable!
</p>
```

*   避免使用文本格式标签— `b`、`i`、`em`、`sup`、`sub`等
*   根据需要使用特殊字符— `&copy;`(版权)、`&reg;`(注册商标)、`&nbsp;`(不中断空格)等。
*   检查`anchor`标签中的所有链接是否正常工作，是否将用户重定向到预期的目标网站。使用链接检查器——死链接检查器——确保你网站上的所有链接都工作正常。
*   在使用 [W3C 验证服务](https://validator.w3.org)部署网站之前，通过验证 HTML 标记来识别网站中过时的元素和属性。

## 结论

遵循这些实践可以提高可访问性、SEO 和网站性能。请记住，每个用例都是不同的。找出最适合你的方法。

如果我遗漏了任何其他重要的标签/元素/属性，请告诉我。

*更多内容请看*[***plain English . io***](http://plainenglish.io)