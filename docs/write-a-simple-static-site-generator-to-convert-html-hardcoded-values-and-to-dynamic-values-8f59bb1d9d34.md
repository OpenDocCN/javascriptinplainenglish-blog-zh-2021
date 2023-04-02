# 编写一个简单的静态站点生成器，将 HTML 硬编码值转换为动态值

> 原文：<https://javascript.plainenglish.io/write-a-simple-static-site-generator-to-convert-html-hardcoded-values-and-to-dynamic-values-8f59bb1d9d34?source=collection_archive---------12----------------------->

![](img/f20d6d25690b19f35305fbcc1357a912.png)

今天，我要写的是我们如何轻松地创建自己的静态站点生成器。

最近，我接到一个任务，我必须转换一个有大量硬编码数据的 HTML 网站。我被要求删除它，并使用一个内容丰富或棱柱形的数据源。

由于 Node.js 和文件系统(fs ),编写一个获取代码、更改内容并输出项目的生成器非常容易。

但为了让它变得非常简单，我想出了一个每个人都能理解的解决方案。这是需要的步骤。

## 步伐

1.  读取输入文件
2.  修改输入文件的内容
3.  将输入文件文件夹复制到输出目录
4.  替换步骤 2 中修改的内容，并将其与您在步骤 3 中创建的输出文件合并

可以创造奇迹但并不容易的四个步骤。阅读输入文件意味着我们将有一个装满各种垃圾的文件夹。我们将只针对 HTML 文件。我们将在源文件夹或嵌套的根目录中找到所有的 HTML。

下一步将修改输入文件的内容。为了修改输入文件的内容，我们将不得不使用 Node.js 可以解析的某种模板引擎，在我们的例子中，考虑到它的流行和支持以及 GitHub 上的明星，它将是 handlebars。

下一步相当简单。您只需将所有文件从 src 复制并粘贴到 output (src - > output)，我们将借助 Node.js.

提供的文件系统来完成这项工作。最后一步将包括合并编译后的修改代码，并将其替换到输出文件中。为了在输出文件中替换它，我们需要知道需要替换的文件的确切位置。

好了，不要再说了！让我们从结构开始吧。我们将只有一个 Node.js 文件，所需的依赖关系是:

```
const path = require("path");
const fs = require("fs");
const fse = require("fs-extra");
const walkSync = require("walk-sync");
const Handlebars = require("handlebars");
```

让我们创建一个函数给我们所有人 **。文件夹中的 html* 文件。我们将使用一个已经为此创建的库。它的名字叫 walkSync。函数会是这样的。

```
const getAllTheHTMLFiles = (directory) => {
 const paths = walkSync(directory, { globs: ["**/*.html"] });
 return paths;
};
```

让我们写一个函数，这个函数将使用车把编译后的 HTML 返回给我们。但在此之前，让我给你一个车把的小例子。

假设我们有一个数据对象:

```
const data = {
  title: “The Boring Company”,
   description : “Just a boring company”
 }
```

我们有这样一个 HTML 结构:

```
<h1>{{ title }}</h1>
 <p> {{ description }} </p>
```

在编译时，它返回:

```
<h1>The Boring Company</h1>
 <p> Just a boring company</p>
```

现在，函数。我们考虑数据对象看起来像这样:

```
const data = {
 ["index.html"]: {
    title: “The Boring Company - Home”,
   description: “Just a boring company”
 },
 ["blog-detail.html"]: {
    title: “The Boring Company - Blog”,
   description : “Just a boring company”
 },
};
```

然后:

```
const compileFilesOneByOne = (path) => {fs.readFile(outDir + "/" + path, (e, file) => {
  const source = file.toString();
 // Handlebars compile the html and saved in template
  var template = Handlebars.compile(source);const magic = data[path];
  if (!magic) return;
// and now the out can be written in the files of output directory
  const output = template(magic);fs.writeFile(outDir + "/" + path, output, (e, a) => {
   console.log({ e, a });
  });
 });
};
```

现在，让我们编写一个函数，将一个文件夹的内容复制到另一个文件夹，为了进行复制，我们将使用 FS-extra 库。

```
const copySrcContent = async () => {
 await fse.copySync(srcDir, outDir, { overwrite: true }, function (err) {
  if (err) {
   console.error(err); // add if you want to replace existing folder or file with same name
  } else {
   console.log("success!");
  }
 });
};
```

最后，总结一下，让我们创建一个名为 init()的函数，并按顺序调用上述所有函数。

```
const srcDir = path.join(__dirname, "src");
const outDir = path.join(__dirname, "output");const init = async () => {
// Copy the content form src -> output
 await copySrcContent();
// We now fetch all the .html files
 const htmlFiles = getAllTheHTMLFiles(srcDir);
 // Now we rewrite the output files with the compiled data
 htmlFiles.forEach((e) => {
  compileFilesOneByOne(e);
 });
};init()
```

砰的一声。运行时，所有 HTML 模板化的代码将被转移到另一个名为 output 的文件夹中，在那里您将拥有 HTML 编译后的代码。

今天就到这里，希望你喜欢这篇文章。请随意竖起大拇指，如果您有任何疑问，请告诉我。

![](img/38b8591e729e1cf3a97754591886fd0f.png)

如果你愿意，你可以雇佣我通过 https://www.fiverr.com/share/b5ydeW 建立一个静态站点生成器

## 谢谢你。

*更内容于*[T5](http://plainenglish.io/)