# 如何使用普通 JavaScript 构建图像大小验证

> 原文：<https://javascript.plainenglish.io/how-to-build-image-size-validation-using-vanilla-js-da1fc6b258b?source=collection_archive---------10----------------------->

![](img/3ab218b2decffeea69358189c2e763b4.png)

Photo by [KOBU Agency](https://unsplash.com/@kobuagency?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Web 开发人员可以使用**普通 JavaScript** 来构建各种功能。使用普通 JavaScript 可以加快 web 编程的开发过程。这是因为不需要外部库和插件。例如，vanilla JS 提供了可用于在网站上进行图像大小验证的方法。这些方法嵌入在 JavaScript 引擎中。在本文中，我将一步步向您展示如何使用普通的 JavaScript 来验证图像。

**第一步:**创建一个文件夹，在里面创建三个文件。这些是****styles . CSS*******script . js****。***

****步骤 2:** 添加 HTML 样板代码，然后在<标题>标签之间添加图片上传标题。**

```
**<!DOCTYPE *html*>
<html *lang*="en">
<head>
 <meta *charset*="UTF-8">
 <meta *http-equiv*="X-UA-Compatible" *content*="IE=edge">
 <meta *name*="viewport" *content*="width=device-width, initial-scale=1.0"><title>Image Upload</title></head><body></body></html>**
```

****第三步:**将 *styles.css* 文件和 *script.js* 文件链接到*index.html 的头部。***

```
**<link *rel*="stylesheet" *href*="styles.css">
<script *src*="script.js"></script>**
```

****第四步:**在*index.html 的主体部分内创建一个带有名为 container 的类的 ***div*** 标签。***

```
*<body>
  <div *class*="container">
  </div>
</body>*
```

***第五步:**添加 ***标签*** ， ***输入*** ， ***span*** 标签在容器内。*

```
*<body>
 <div *class*="container">
  <label *for*="imageuploadbutton" class="label">Upload Image Here</label>
  <input  *type*="file" id="imageuploadbutton" >
  <span class="validation-message" ></span>
 </div>
</body>*
```

*最终的***index.html***文件应该是这样的*

```
*<!DOCTYPE *html*>
<html *lang*="en">
<head>
 <meta *charset*="UTF-8">
 <meta *http-equiv*="X-UA-Compatible" *content*="IE=edge">
 <meta *name*="viewport" *content*="width=device-width, initial-scale=1.0"><title>Image Upload</title>
<link *rel*="stylesheet" *href*="styles.css">
<script *src*="script.js"></script></head><body>
 <div *class*="container">
  <label *for*="imageuploadbutton" class="label">Upload Image Here</label>
  <input  *type*="file" id="imageuploadbutton" >
  <span class="validation-message" ></span>
 </div>
</body></html>*
```

***第六步:**在 ***style.css*** 中，添加*容器*、*标签*和*验证-消息*类样式。*

```
**.container*{
   padding-left: 30px;
   padding-right: 30px;
   padding-top: 15px;
   padding-bottom: 15px;
   display: flex;
   flex-direction: column;
   align-items: center;}*.label* {
   color: navy;
   font-size: larger;
   font-weight: bold;
}*.validation-message*{
   color: crimson;
   font-size: smaller;
   font-weight: normal;
}*
```

***第七步:**现在在 ***script.js*** 中创建两个名为 input 和 span 的变量。这些将保存 HTML 输入和 span 标签。*

```
**let* input = document.querySelector('input');
*let* span = document.querySelector('span');*
```

***步骤 8:** 在输入变量中创建一个事件监听器，它将响应文件上传。*

```
**let* input = document.querySelector('input');*let* span = document.querySelector('span');input.addEventListener('', () => {})*
```

***第九步:**在***addevent listener***return 语句里面，创建一个名为 *files* 的变量和一个 if 语句来检查 *files* 变量的长度。该变量将保存任何上传的文件。*

```
*input.addEventListener('change', () => {*let* files = input.files;if (files.length > 0) {}span.innerText = '';})*
```

***步骤 10:** 在 if 语句中，添加另一个将验证文件类型的 if 语句*

```
*input.addEventListener('change', () => {*let* files = input.files;if (files.length > 0) { if (files[0].type != 'jpeg' || files[0].type != 'png' ) {
   span.innerText = 'File Type must be jpeg or png';
   return;
  }}span.innerText = '';})*
```

***步骤 11:** 接下来添加另一个 if 语句，该语句现在将验证图像大小*

```
*input.addEventListener('change', () => {*let* files = input.files;if (files.length > 0) { if (files[0].type != 'jpeg' || files[0].type != 'png' ) {
   span.innerText = 'File Type must be jpeg or png';
   return;
  } if (files[0].size > 500 * 1024) {
   span.innerText = 'File Size Exceeds 500kb';
   return;
  }
}span.innerText = '';})*
```

*最终的 ***script.js*** 文件应该是这样的。*

```
**let* input = document.querySelector('input');
*let* span = document.querySelector('span');input.addEventListener('change', () => {
 *let* files = input.files;
  if (files.length > 0) {
   if (files[0].type != 'jpeg' || files[0].type != 'png' )            {span.innerText = 'File Type must be jpeg or png';return;} if (files[0].size > 500 * 1024) { span.innerText = 'File Size Exceeds 500kb'; return;}}span.innerText = '';})*
```

*在浏览器中打开索引文件来运行一切。*

## ***结论***

*现在我们有了。我希望你已经发现这是有用的。我会带着更多有趣的文章回来。感谢您的阅读。*

*去 [**Mozilla 开发者**](https://developer.mozilla.org/en-US/docs/Web/API/File/Using_files_from_web_applications) 了解更多关于这个的信息。*

**更多内容请看*[***plain English . io***](http://plainenglish.io/)*