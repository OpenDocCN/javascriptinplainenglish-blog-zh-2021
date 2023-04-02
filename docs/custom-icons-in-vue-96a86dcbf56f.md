# Vue 中自定义图标的介绍

> 原文：<https://javascript.plainenglish.io/custom-icons-in-vue-96a86dcbf56f?source=collection_archive---------10----------------------->

## 向您的 Vue 项目添加自定义图标。

![](img/d42dbc211d05fdf81c74a19fb4035782.png)

# 丰塔斯蒂克

本文第一部分与 Vue 无关。相反，它是关于一年前我偶然发现的一个很棒的资源，叫做 [Fontastic](https://fontastic.me/) 。

主页上有一个幽默的小视频，告诉你这个工具可以做什么，页面下方还有一些摘要广告。

你必须创建一个帐户，但它是完全免费的。一旦登录，我个人觉得界面有点笨拙，但它的工作。

鸟瞰图非常明显。这个网站是一个存储库，里面有一些流行的(有些晦涩的)字体图标集合，比如字体牛逼。

## 新的自定义收藏

如果您想创建自定义字体集，请点击屏幕右上角(工具栏下方)的*新字体*菜单项。没有明显的事情发生(进入沉闷)。现在，一直走到左边，你会看到“无标题字体 1”有一个下拉箭头。这是您刚刚创建的集合。点击*修改字体，*可以编辑字体名称，设置字体的 CSS 类前缀。它默认为“图标”，但我喜欢添加一个更具体的项目前缀，你的选择。这个前缀会在你的 HTML 中用到，我们稍后会讨论。

## 添加更多图标

现在，您可以将任何库中的图标添加到您自己的自定义集中，方法是转到库中并单击您想要添加到自定义集中的图标。在工具栏中，有一个*添加更多图标*选项，提供对更多库的访问，您可以在那里激活/停用任何库。他们也有一些你可以购买的高级图标集。

在*添加更多图标*屏幕的顶部，有一个*导入图标*按钮，在那里可以找到一些主要的 mojo。如果您已经有一个 SVG 图标或字体，您可以将它上传到那里，它将作为一个库提供给您，您可以从中选择图标，以便将来导入到任何自定义的图标集中。

## 定制

一旦您在自定义收藏中选择了想要的图标，您可以在*自定义*部分进一步自定义它们。在那里，您可以更改自定义收藏中每个图标的名称。例如，如果你有字体 Awesome 的 *trash-o* 图标，你可以把它的名字改成“trash ”,因为这是你自定义设置中的唯一一个图标。*自定义*区域也是您可以从收藏中移除图标的地方。

## 出版

在*发布*部分，您将看到自定义图标的 CSS 类映射。每个图标都有一个类名[前缀(前面提到的)]-[图标名]。

我使用字体图标而不是 SVG，但是你可以在发布页面上看到 SVG sprite 选项。因为我从来没有用过，所以你必须自己想出它的细节。

对于字体图标，一旦你有了你想要的字体，点击发布界面顶部“手动安装”部分的*下载*按钮。它会将一个 zip 文件下载到您的默认下载目录中。

# 导入到 Vue 项目

现在我们到了 Vue 部分。我编写了一个 quick & dirty Node.js 脚本，将图标从下载文件夹导入到我的项目中。这可能看起来有些多余，但是如果您决定修改您的 Fontastic 图标集合并下载它的新版本，这些步骤会变得很乏味。

该脚本(import-icons.js)使用了[解压缩器](https://www.npmjs.com/package/unzipper)包，如下所示:

```
const fs = require("fs");const { join } = require("path");
const file = "/path/to/downloaded/icon-collection.zip";
const outputPath = join(__dirname, "src", "assets", "icons");const unzipper = require("unzipper");fs.createReadStream(file)
  .pipe(unzipper.Extract({ path: outputPath }))
  .on("close", () => {
    fs.rmSync(file);
  });
```

然后，在我的 *package.json* 文件中，我将它添加到脚本部分:

```
"import-icons": "node ./import-icons.js"
```

在我创建了我的*图标集合*(或者我想叫它什么)，发布并下载它之后，我进入我的项目文件夹并输入`yarn import-icons`(或者如果你喜欢的话，输入等价的`npm`)。它将内容解压缩到我的/src/assets/icons 目录中，并从我的下载目录中删除 zip 文件。

# 在 Vue 项目中使用

在您的 *main.js* 文件中(如果您不使用 Vue CLI，则为等效部分):

```
import Vue from "vue";
import "./assets/icons/styles.css";
```

此时，您可以使用`<i class="icon-class-name" />`,或者在 Vuetify 中:

```
<v-icon>
  icon-class-name
</v-icon>
```

# 工作示例

[](https://github.com/mcasto/fontastic-implementation-demo) [## GitHub-mcasto/font astic-实现-演示

### 此时您不能执行该操作。您已使用另一个标签页或窗口登录。您已在另一个选项卡中注销，或者…

github.com](https://github.com/mcasto/fontastic-implementation-demo) 

感谢您的阅读。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)*。报名参加我们的* [*免费周报在这里*](http://newsletter.plainenglish.io/) *。*