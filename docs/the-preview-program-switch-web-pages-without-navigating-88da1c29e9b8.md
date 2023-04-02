# 预览程序:不导航切换网页

> 原文：<https://javascript.plainenglish.io/the-preview-program-switch-web-pages-without-navigating-88da1c29e9b8?source=collection_archive---------20----------------------->

![](img/8f4fba1fd1cfabda8f0cd12194cb0373.png)

Photo by [Bram Naus](https://unsplash.com/@bramnaus?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

你知道你可以在你当前的网页上预览不同网页的内容吗？你既不需要创建多个页面，也不需要创建导航栏。

所以，你所要做的就是用更少的努力来检查你的页面的外观。有趣的是，预览程序是一个基于单页的 PHP 程序，它允许从页面列表中选择一个特定的页面，并在同一个页面上预览它。

信不信由你！它不需要任何先进的技术，只需要一些基本的东西。

稍微揭开这个秘密，你只需要 HTML 和 PHP 代码来切换不同的内容。继续阅读，看看如何开发它并获得其源代码。

作为一名开发人员，您可能已经知道 PHP 中的 if-else 语句，它根据特定条件的实现来执行特定的操作。如果是这样的话，那么你就准备开发预览程序了。给你。

## 如何开发一个预览程序？

首先创建一个包含选择列表和提交按钮的表单。接下来，检查表单是否已提交，并根据列表中选择的网页编写不同网页的代码。这意味着每个 if 或 else-if 块将包含各自网页的内容。此外，您可以添加任意多的页面。就这么简单！

## 源代码:

下面是用 PHP 创建“预览程序”的源代码:

```
<!DOCTYPE html>
<html lang=”en”>
<head>
<meta charset=”UTF-8">
<meta http-equiv=”X-UA-Compatible” content=”IE=edge”>
<meta name=”viewport” content=”width=device-width, initial-scale=1.0">
<title>Preview Program</title>
</head>
<body>
<form action=”” method=”post”>
<select name=”change”>
<option value=””>Select Page</option>
<option value=”home”>Landing Page</option>
<option value=”about”>About Us</option>
<option value=”contact”>Contact</option>
<option value=”faqs”>FAQs</option>
</select>
<input type=”submit” name=”SubmitBtn” value=”Preview”>
</form>
<center><h1>Preview Web Pages</h1></center>
<?php
if(isset($_POST[“SubmitBtn”])){
$page = $_POST[“change”];
?>
<?php if($page == “home”): ?>
<center><h1>Landing PAGE</h1></center>
<! — Add your desired home page content here. →
<?php elseif($page == “about”): ?>
<center><h1>ABOUT US</h1></center>
<! — Add something about your business here. →
<?php elseif($page == “contact”): ?>
<center><h1>CONTACT</h1></center>
<! — Add your contact details here. →
<?php elseif($page == “faqs”): ?>
<center><h1>FAQs</h1></center>
<! — Answer the frequently asked questions here. →
<?php else: ?>
<center><h1>Select a Page to Preview</h1></center>
<?php endif; } ?>
</body>
</html>
```

## 怎么用？

上面给出的代码展示了创建预览程序的步骤和思想。将其复制并粘贴到您的代码编辑器中，并为不同的网页添加内容。你可以随意定制它，添加 CSS 或引导类，使它更具吸引力和响应性。您甚至可以在列表中添加更多的选项，并为相应的页面创建更多的 else-if 块。

试试看，让我知道它对你有什么效果。我迫不及待地想看你的回复。

感谢您的阅读。

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)