# 我的超级简单的开发人员指南写干净和可读的代码

> 原文：<https://javascript.plainenglish.io/8-simple-developers-guide-to-writing-super-clean-and-readable-code-3f4f5c3dab8f?source=collection_archive---------12----------------------->

## 可读性和可维护性代码的最佳实践

![](img/9274d778fb19c42e2df19f88c89fc0d6.png)

Photo by [Dean Pugh](https://unsplash.com/@wezlar11?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

好的代码易于阅读、理解和维护。作为一名程序员，我不能总是期望我的代码能够顺利运行，并且能够被任何试图修改它的人理解。

所以这里有一个我一直遵循的八步计划，让我的脚本对维护者来说更容易。

## 1.保持你的语法和结构的整洁和逻辑性

这意味着你缩进你的代码，保持 80 个字符的行长度限制，并且保持函数合理的小。一个经验法则是让每个任务保持在它自己的功能中，而不是让一个大的功能做所有的事情。

另一个好处是，这意味着您可以在以后扩展脚本时重用这些函数。但是，不要走“IDE 生成— Java”的路线，创建许多单行函数—这可能比使用一个庞大的函数更令人困惑。

有一场关于制表符和空格的圣战正在进行，是为了在自己的行上缩进和花括号，还是为了开始命令。只要你保持一致，并与其他代码一致，我不在乎扩展一个现有的项目。

例如，让我们用一个为弹出窗口生成“关闭”和“打印”链接的函数——这些链接只有在 JavaScript 可用时才有意义，因此应该用 JavaScript 生成。

```
function toolLinks(){
  var tools = document.createElement('ul');
  var item = document.createElement('li');
  var itemlink = document.createElement('a');
  itemlink.setAttribute('href', '#');
  itemlink.appendChild(document.createTextNode('close'));
  itemlink.onclick = function(){window.close();}
  item.appendChild(itemlink);
  tools.appendChild(item);
  var item2 = document.createElement('li');
  var itemlink2 = document.createElement('a');
  itemlink2.setAttribute('href', '#');
  itemlink2.appendChild(document.createTextNode('print'));
  itemlink2.onclick = function(){window.print();}
  item2.appendChild(itemlink2);
  tools.appendChild(item2);
  document.body.appendChild(tools);
}
```

通过将每个任务缩进并分离成各自的功能，您可以使它更具可读性:

```
function toolLinks(){
  var tools = document.createElement('ul');
  var item = document.createElement('li');
  var itemlink = createLink('#', 'close', closeWindow);
  item.appendChild(itemlink);
  tools.appendChild(item);
  var item2 = document.createElement('li');
  var itemlink2 = createLink('#', 'print', printWindow);
  item2.appendChild(itemlink2);
  tools.appendChild(item2);
  document.body.appendChild(tools);
}
function printWindow(){
  window.print();
}
function closeWindow() {
  window.close();
}
function createLink(url,text,func){
  var temp = document.createElement('a');
  temp.setAttribute('href', url);
  temp.appendChild(document.createTextNode(text));
  temp.onclick = func;
  return temp;
}
```

## 2.使用清晰的变量名和函数名

这是基本的良好编码实践，尽管你看到它做得更差。再一次，快速解决方案和迫在眉睫的最后期限是罪魁祸首。本质上，这意味着您使用的变量和函数名称可以立即告诉维护人员这部分数据是什么。

你可以使用下划线或者 came case 来连接不同的单词——我个人更喜欢 came case，这与 JavaScript 为你提供的方法一致(例如`getElementsByTagName()`)。对于那些只在函数或循环中计算的、不需要维护的变量，比如前面例子中的`createLink()`函数中的“temp”变量，使用通用名称可能是个好主意。

从书中学习好的 CSS 设计——确保你的函数和变量名是通用的，描述一个任务而不是一个视觉结果。在另一次代码迭代中,`createFatRedBoxForLeftNavigation()`可能会变成`createTopBarForSectionNavigation()`,但如果从一开始就调用了 createSecondaryMenu (),就不会变成这样。
它也是坚持英文变量和函数名的完美选择——你永远不知道你是否必须在世界范围内共享代码，或者把它送到另一个国家进行维护。

## 3.注释您的代码

评论可以节省很多时间和悲伤。但是，也可以过度。在教程和书籍中，你会发现代码的每一行都有注释，解释发生了什么。这是因为目标受众的缘故，在教程中很有意义，但在实际代码中却是多余的。

**在下列情况下需要意见:**

*   有一段代码需要维护，例如“在此更改 ID 名称”
*   一个部分可能会过时，因为它现在为 hip 用户代理解决了一个问题。
*   当可能有更好的方法时，你用一种方法编程是有原因的，你想解释一下。
*   代码段依赖于另一个脚本，或者获取最初来源可能不明显的参数。

## 4.保持你的脚本独立

这一步与不引人注目的 JavaScript 有关，所以我们不要在这上面纠缠。本质上，这意味着维护人员可以将您的脚本添加到任何页面中，而不必冒覆盖其他代码的风险。你可以通过命名空间或者通过[对象文字](http://christianheilmann.com/2006/02/16/show-love-to-the-object-literal/)将它们包装在一个对象中来保持脚本的自包含性。通过 var 关键字将变量保持在函数范围内，可以确保不会劫持变量，也不会通过使用`addEvent()`或其派生词劫持事件。

## 5.将维护的变量分开，并测试依赖性

这一步很简单:在函数开始时保留需要维护的变量，必要时用虚拟值预先设置它们。这样，维护人员总是知道在哪里改变设置，而不必浏览整个脚本，你也不会遇到“未定义”的错误。

```
function toolLinks(){
  var tools, closeWinItem, closeWinLink, printWinItem, printWinLink; // link labels, please edit
  **var printLinkLabel = ‘print’;**
  ** var closeLinkLabel = ‘close’;**# tools = document.createElement(’ul’);
   closeWinItem = document.createElement(’li’);
   closeWinLink = createLink(’#', **closeLinkLabel**, closeWindow);
   closeWinItem.appendChild(closeWinLink);
   tools.appendChild(closeWinItem);
   printWinItem = document.createElement(’li’);
   printWinLink = createLink(’#', **printLinkLabel**, printWindow);
   printWinItem.appendChild(printWinLink);
   tools.appendChild(printWinItem);
   document.body.appendChild(tools);
}
```

测试依赖关系是不引人注目的 JavaScript 的一个特点——在通过 DOM 方法访问 HTML 元素之前，先测试它们是否存在。

## 6.分离和传达视觉效果

对于不引人注目的 JavaScript，没有办法动态地应用和删除 CSS 类名来形成元素。几乎没有任何情况下你需要直接访问一个对象的样式集合，以免给维护者增加难度。

拖放接口是个例外，但即使这样，通过 JavaScript 改变的只是元素的 x 和 y 坐标。其余的外观应该留在它应该在的地方:在 CSS 文件中。这确保了 CSS 设计者不会弄乱你的代码，你也不需要知道浏览器中 CSS 错误的所有细节——而且比我们希望的要多得多。

传达这些类的名称的最基本的方法是将它们保存在变量中，并在脚本的开头对它们进行注释:

```
demo = {
  // CSS classes
  hideClass : 'hide', // hide elements
  currentClass : 'current', // current navigation element
  hoverClass : 'over', // hover state
  [... rest of the code ...]
}
```

如果您想进一步分离，那么您可以创建一个自己的包含文件，例如名为`cssClassNames.js`的文件，并在这个文件中使用一个 [JSON](https://web.archive.org/web/20101130194708/http://www.json.org/) 符号。

```
css={
  'hide' : 'hide', // hide elements
  'current' : 'current', // current navigation element
  'hover' : 'over', // hover state [... and so on for a lot of them...]
}
```

在您的脚本中，您可以分别使用`css.hide`或`css.current`到达不同的类名。你甚至可以使用更自然的标签，比如“隐藏元素”，并通过 CSS 的“隐藏元素”来访问它们，这对维护人员来说更容易，但对编码人员来说就更难了。

一个简单的技巧是用一个类名来与 CSS 设计器通信，以应用于文档的主体。这将允许 CSS 设计者区分应用于非 JavaScript 版本和脚本增强版本的样式。

```
if(!document.getElementById || !document.createElement){return;}
  cssjs('add',document.body,'jsenabled');
```

CSS:

```
/* No JavaScript */
#nav li{
  [...settings...]
}
/* JavaScript */
body.jsenabled #nav li{
  [...settings...]
}
```

这也非常方便通过 CSS 隐藏许多元素，而不是遍历所有元素。在极端的情况下，对于支持脚本的版本，您有许多样式和完全不同的设置，您甚至可以通过 JavaScript 应用一个完全不同的样式表(或者使用`document.write()`或者创建一个新的 LINK 元素)。

## 7.分离文本内容和代码

同样的技巧也适用于文本内容。你可以将标签作为变量分离出来，或者——更好的是——放入一个名为`textContent.js`的 JSON 格式的文档中。一个非常有效的例子是:

```
var locales = {
  'en': {
    'homePageAnswerLink':'Answer a question now',
    'homePageQuestionLink':'Ask a question now',
    'contactHoverMessage':'Click to send this info as a message',
    'loadingMessage' : 'Loading your data...',
    'noQAmessage' : 'You have no Questions or Answers yet',
    'questionsDefault': 'You have not asked any questions yet',
    'answersDefault': 'You have not answered any questions yet.',
    'questionHeading' : 'My Questions',
    'answersHeading' : 'My Answers',
    'seeAllAnswers' : 'See all your Answers',
    'seeAllQuestions' : 'See all your Questions',
    'refresh': 'refresh'
  },
  'fr': {
  },
  'de': {
  }
};
```

它允许编辑人员在不接触代码的情况下翻译和维护所有不同语言的标签。我甚至设法将 id 分开，以便他们与 HTML 开发人员一起整理。JavaScript 所要做的就是读出应用程序的区域设置，并遍历可用的元素:

```
function doI18N(){
   var lang = yhost.PluginLocale;
   for(i in locales[lang]){
     if(document.getElementById(i)){
       document.getElementById(i).innerHTML = **locales[lang][i]**;
     }
   }
  }
```

## 8.记录您的代码

最后，但不是最不重要的:写关于你的脚本/库/效果的文档。好的文档考虑到了受众，这意味着最好保持经典的 API 文档，包含一些库的“techspeak”中解释的方法的所有可能的属性和参数。不过，总的来说，我在“举例说明，然后列出所有可能性”的文档方面取得了更多的成功。

好的文档可以节省最多的时间和金钱，事实上，我们很少有时间去创建它。

其他编程语言从代码注释中自动生成文档(例如 PHP)。然而，这并不一定会带来更好的文档，只会减少工作量。

## 高流量网站怎么办？

如果您在一个高流量的环境中工作，或者只允许小的代码包(移动市场)，您可能会反对这里解释的想法，因为它们会使代码膨胀。解决这个问题的方法是在去掉注释、用较短的变量名替换较长的变量名以及执行其他打包和缩小任务之后，维护一个代码库和一个从原始代码生成的动态代码库。为你做到这一点的工具是道格拉斯·克洛克福特的 JSmin 和迪安·爱德华的 T2 packer。

# 结论

是的，有些步骤对于那些时髦的、游历广泛的、经验丰富的 JavaScript 开发人员来说可能是非常明显的，但是提醒我们自己它们的优点也无妨。

我希望我给出的上面的例子给你一个让你的代码更易维护的想法，或者提醒你一些潜伏在你大脑深处的想法。如果您有其他想法或强烈反对某些实践(您有充分的理由)，请让我知道，就像所有最佳实践一样，“这是一项正在进行的工作，协作只会使它变得更好。