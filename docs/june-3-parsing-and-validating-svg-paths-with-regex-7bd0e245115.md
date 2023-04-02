# 6 月 3 日:用 regex 解析和验证 SVG 路径

> 原文：<https://javascript.plainenglish.io/june-3-parsing-and-validating-svg-paths-with-regex-7bd0e245115?source=collection_archive---------10----------------------->

![](img/82db87211ce7f4cc9319175e22aa56a2.png)

Photo credit: Milton Bradley Company

> 感谢 Yann Armelin 在这个课题上的惊人工作。

没有什么比矢量图形更令人愉快的了。使用光栅图形时，对角线和曲线看起来都很脆，很难定义，但是使用矢量时，它们在任何比例下都无比光滑和清晰。矢量文件轻如鸿毛，尤其是与 JPEGs 相比，所以加载时间可以忽略不计，性能很快。

在今天的博文中，我们将深入探讨我在矢量图形个人工作中遇到的一个任务:**解析和验证路径描述符。**我认为它将为 SVG 的活动部分提供一些深刻的见解，因为它触及了如此多的 SVG。

# 背景:用一个标签来管理它们

大多数图像文件都是光栅图形文件，本质上就是巨大的像素阵列。**矢量图形，**另一方面，用标准化语法定义笛卡尔(二维)平面上的点。这个概念是在 50 年代为空军和后来的民用空中交通管制使用的计算机而创造的，现在在消费计算机上普遍使用。

web 上矢量图形的主导标准，**可缩放矢量图形(SVG)，**大约有 20 年的历史了。您可以在任何文本编辑器中打开一个`.svg`文件，如果您这样做了，您会看到表面上类似于 HTML 的语法:

```
<?xml version="1.0" encoding="utf-8"?>
   <!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
   <svg version="1.1"  xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" width="522px" height="522px" viewBox="0 0 522 522" enable-background="new 0 0 522 522" xml:space="preserve">
...
```

它实际上只是 XML，是 HTML 的表亲。没错:**只是文本标记。这使得用 JavaScript 操作它变得轻而易举，因为形状被表示为熟悉的标签。**

# 正义之人的道路

SVG 库中有一些[基本形状](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Basic_Shapes)——基本的`<line>`段，由像`<polyline>`、`<rect>`角和`<polygon>` s 这样的线段组成的形状，以及像`<circle>` s 和`<ellipse>` s 这样的曲线形状。但是今天我们将把重点放在最重要的 SVG 元素上:`<path>`。它是如此强大**它可以取代所有其他元素；**使用 Adobe Illustrator 等典型矢量图形编辑器创建的大多数 SVG 文件都是 90% `<path>`标签。

所有的 SVG 标签都有各种各样的样式属性。有些是不言自明的样式属性，如`stroke=`和`fill=`，但重要的是特定于每个标签的属性，定义了形状的基本外观。一个`<path>`标签*需要*的唯一属性是一个**描述符**属性，用`d=`定义:

```
<path d="M 0 397.833 c 9.688 1.337 17.864 1.417 27.229 -0.735 c 7.506 -1.725 15.587 0.872 23.494 -0.734 c 13.812 -2.807 16.568 -19.019 29.683 -23.269..." />
```

路径的描述符是一系列连锁的**命令**(字母)，可以是**绝对**(大写)或**相对**(小写)，后跟一个或多个标准格式的**参数**(数字)。absolute 命令的参数表示相对于视图框的坐标；相对命令的参数表示相对于形状中上一点的坐标。这意味着下面的两个标签将绘制相同的形状:

```
<path d="M 25 25 L 75 25 L 75 75 L 25 75 Z" /> // absolute commands<path d="m 25,25 l 50,0 l 0,50 l -50,0 z" /> // relative commands
```

允许混合使用绝对命令和相对命令，但不鼓励这样做。

六种类型的路径命令是:

*   **招:** `M`，`m`
*   **行:**`L``l``H``h``V``v`
*   **立方曲线:**`C``c``S``s`
*   **四次曲线:**`Q``q``T``t`
*   **圆弧曲线:** `A`，`a`
*   **关闭:** `Z`，`z`

假设你正在写一个矢量编辑器或者一个矢量游戏。如果是的话，您可能需要一种快速、简单的方法来获取整数，这些整数表示定义 SVG 形状的坐标，以便它们能够正确显示和碰撞。事实上，这正是像 [Snap](http://snapsvg.io/) 和 [SVG.js](https://github.com/svgdotjs) 这样的软件包所做的——但是，与其使用软件包，不如让我们亲自动手编写一些逻辑代码。

# 一种方法:用正则表达式验证 SVG 路径

我的方法将使用 **regex，** [，我在之前的](https://joshgoestoflatiron.medium.com/january-23-a-word-matching-game-using-regular-expressions-in-ruby-19268bb92c02)博客中已经讨论过了，强调每次我这样做的时候，写它就像切一个疖子一样有趣。我尽我所能召唤这些**被诅咒的式神**来验证命令并从字符串中提取它们:

```
const validCommand = /([ml](\s?-?((\d+(\.\d+)?)|(\.\d+)))[,\s]?(-?((\d+(\.\d+)?)|(\.\d+))))|([hv](\s?-?((\d+(\.\d+)?)|(\.\d+))))|(c(\s?-?((\d+(\.\d+)?)|(\.\d+)))([,\s]?(-?((\d+(\.\d+)?)|(\.\d+)))){5})|(q(\s?-?((\d+(\.\d+)?)|(\.\d+)))([,\s]?(-?((\d+(\.\d+)?)|(\.\d+)))){3}(\s?t?(\s?-?((\d+(\.\d+)?)|(\.\d+)))[,\s]?(-?((\d+(\.\d+)?)|(\.\d+))))*)|(a(\s?-?((\d+(\.\d+)?)|(\.\d+)))([,\s]?(-?((\d+(\.\d+)?)|(\.\d+)))){2}[,\s]?[01][,\s]+[01][,\s]+([,\s]?(-?((\d+(\.\d+)?)|(\.\d+)))){2})|(s(\s?-?((\d+(\.\d+)?)|(\.\d+)))([,\s]?(-?((\d+(\.\d+)?)|(\.\d+)))){3})|z/ig;const isValidDescriptor = /^m(\s?-?((\d+(\.\d+)?)|(\.\d+)))[,\s]?(-?((\d+(\.\d+)?)|(\.\d+)))([,\s]?(([ml](\s?-?((\d+(\.\d+)?)|(\.\d+)))[,\s]?(-?((\d+(\.\d+)?)|(\.\d+))))|([hv](\s?-?((\d+(\.\d+)?)|(\.\d+))))|(c(\s?-?((\d+(\.\d+)?)|(\.\d+)))([,\s]?(-?((\d+(\.\d+)?)|(\.\d+)))){5})|(q(\s?-?((\d+(\.\d+)?)|(\.\d+)))([,\s]?(-?((\d+(\.\d+)?)|(\.\d+)))){3}(\s?t?(\s?-?((\d+(\.\d+)?)|(\.\d+)))[,\s]?(-?((\d+(\.\d+)?)|(\.\d+))))*)|(a(\s?-?((\d+(\.\d+)?)|(\.\d+)))([,\s]?(-?((\d+(\.\d+)?)|(\.\d+)))){2}[,\s]?[01][,\s]+[01][,\s]+([,\s]?(-?((\d+(\.\d+)?)|(\.\d+)))){2}))[,\s]?)+z/ig;
```

> 完全公开:这两种方法都让一些极端的边缘情况溜走了，但是它们捕捉到了大量有效的路径，对于一些凌晨 2 点的本地主机来说已经足够好了。

这两个表达式看起来都像一家失火的儿童医院，因为有效的 SVG 路径有多种形式:路径命令参数通常必须用空格分隔，但在某些情况下可以用逗号、负/十进制符号分隔，或者根本不用分隔。显然，Regex 中的分支并不好看；这里是通过一个`()`捕获组列表来完成的，由于正则表达式或`|`元字符，任何一个捕获组都将触发一个匹配，就像这样:`()|()|()|...`路径命令根据它们必须接受的参数数量来分别处理。

## 这种方法的局限性和副作用

`.match()` `validCommand`的能力出头就好了...

```
const shape1 = "m 150,150 a 25,25 0 1,1 50,0 a 25,25 0 1,1 -50,0 z";
const shape2 = "m 40 254 s 35 -27 30 -69 s 33 -49 75 -25 z";
const wrongShape = "m l 250 a -400, -350 .";isValidDescriptor.test( shape2 )
   -> true
isValidDescriptor.test( wrongShape )
   -> falseshape1.match( validCommand )
   -> [ 'm 150,150', 'a 25,25 0 1,1 50,0', 'a 25,25 0 1,1 -50,0', 'z' ]shape2.match( validCommand ).map( command => command.split( /[\s,]/ ).map( parameter => parseInt( parameter ) || parameter ) );
   -> [ [ 'm', 40, 254 ], [ 's', 35, -27, 30, -69 ], [ 's', 33, -49, 75, -25 ], [ 'z' ] ]
```

但是 JavaScript 中这种语法的简单和清晰是以 regex 中的绝对垃圾火为代价的。正则表达式通常以指数时间运行，因此它们容易受到一种独特的攻击，即所谓的邪恶正则表达式。

我不认为这能很好地扩展或者证明是健壮的。结合我上面提到的偶尔出现的错误匹配，我认为仅仅为了使用`.match()`和`.test()`这两种已经很慢的方法是不值得的。所以我没有直接使用 regex，而是选择了一种混合的方法…

# 另一种方法:用正则表达式分割/切片，用 JavaScript 验证

与其将邪恶引入我们的生活，不如定义一些更小的正则表达式来匹配命令的核心组成部分——它的**命令**字母、数字(**参数**、**标志**或**坐标**)和**分隔符**(逗号、空格和负/十进制符号——都是可选的，但有些在某些情况下是必需的)。

```
const validFlagEx = /^[01]/;const commaEx = /^(([\t\n\f\r\s]+,?[\t\n\f\r\s]*)|(,[\t\n\f\r\s]*))/;const validCommandEx = /^[\t\n\f\r\s]*([achlmqstvz])[\t\n\f\r\s]*/i;const validCoordinateEx = /^[+-]?((\d*\.\d+)|(\d+\.)|(\d+))(e[+-]?\d+)?/i;
```

让我们简单地分解一下:

*   注意**这些表达式不再携带** `**/g**` **叶形标志**和**都以一个开始** `**^**` **元字符开始代替！这个稍后会很重要。**
*   有效标志是一个零或一个`[01]`。
*   有效的分隔符要么是可选逗号`,?`和可选空格前的一个空格，要么是任意数量的可选空格前的一个逗号。
*   一个有效的命令字母`[achlmqstvz]`前后可以有任意数量的可选空格。
*   一个有效的数字有一个可选的负号`[+-]?`，并且必须是零个或多个数字，零个或多个数字带一个小数点，或者零个或多个数字后跟一个小数点和一个或多个数字。(在电子记数法的最后还有一个恼人的边缘情况。)

然后让我们创建一个**语法—** 对象来存储每个命令的语法是如何正确形成的，就像小学一样:

```
const pathGrammar = {
   z: [],
   h: [ validCoordinateEx ],
   v: [ validCoordinateEx ],
   m: [ validCoordinateEx, validCoordinateEx ],
   l: [ validCoordinateEx, validCoordinateEx ],
   t: [ validCoordinateEx, validCoordinateEx ],
   s: [ validCoordinateEx, validCoordinateEx, validCoordinateEx, validCoordinateEx ],
   q: [ validCoordinateEx, validCoordinateEx, validCoordinateEx, validCoordinateEx ],
   c: [ validCoordinateEx, validCoordinateEx, validCoordinateEx, validCoordinateEx, validCoordinateEx, validCoordinateEx ],
   a: [ validCoordinateEx, validCoordinateEx, validCoordinateEx, validFlagEx, validFlagEx, validCoordinateEx, validCoordinateEx ],
};
```

现在我们有了语法和一些规则，让我们制作这些变量`static`并定义一个**类**来存储它们并构造如何使用它们。

```
class PathParser {static validCommand = /^[\t\n\f\r\s]*([achlmqstvz])[\t\n\f\r\s]*/i;
   static validFlag = /^[01]/;
   static validCoordinate = /^[+-]?((\d*\.\d+)|(\d+\.)|(\d+))(e[+-]?\d+)?/i;
   static validComma = /^(([\t\n\f\r\s]+,?[\t\n\f\r\s]*)|(,[\t\n\f\r\s]*))/;static pathGrammar = {
      z: [],
      h: [ validCoordinateEx ],
      v: [ validCoordinateEx ],
      m: [ validCoordinateEx, validCoordinateEx ],
      l: [ validCoordinateEx, validCoordinateEx ],
      t: [ validCoordinateEx, validCoordinateEx ],
      s: [ validCoordinateEx, validCoordinateEx, validCoordinateEx, validCoordinateEx ],
      q: [ validCoordinateEx, validCoordinateEx, validCoordinateEx, validCoordinateEx ],
      c: [ validCoordinateEx, validCoordinateEx, validCoordinateEx, validCoordinateEx, validCoordinateEx, validCoordinateEx ],
      a: [ validCoordinateEx, validCoordinateEx, validCoordinateEx, validFlagEx, validFlagEx, validCoordinateEx, validCoordinateEx ],
   };static parseRaw( path ) {}static parseComponents( type, path, cursor ) {}}
```

我们的类将有一个 main 方法来`parseRaw()`将整个路径分解为 raw 原语，它使用一个 helper 方法来`parseComponents()`。`parse()`稳步地啃掉`path`，一次啃掉字符串开头的`cursor`大小的块——因此有了开始`^`元字符！

```
static parseRaw( path ) {
   let cursor = 0, parsedComponents = [];
   while ( cursor < path.length ) {
const match = path.slice( cursor ).match( this.validCommand );
      if ( match !== null ) {
         const command = match[ 1 ];
         cursor += match[ 0 ].length;
         const componentList = PathParser.parseComponents( command, path, cursor );
         cursor = componentList[ 0 ];
         parsedComponents = [ ...parsedComponents, ...componentList[1] ];
      } else {throw new Error(  `Invalid path: first error at char ${ cursor }`  );
      }
   }
   return parsedComponents;
}static parseComponents( type, path, cursor ) {
   const expectedCommands = this.pathGrammar[ type.toLowerCase() ];
   const components = [];
   while ( cursor <= path.length ) {
      const component = [ type ];
      for ( const regex of expectedCommands ) {
         const match = path.slice( cursor ).match( regex );
         if ( match !== null ) {
            component.push( parseInt( match[ 0 ] ) );
            cursor += match[ 0 ].length;
            const nextSlice = path.slice( cursor ).match( this.validComma );
            if ( nextSlice !== null ) cursor += nextSlice[ 0 ].length;
         } else if ( component.length === 1 ) {
            return [ cursor, components ];
         } else {
            throw new Error( `Invalid path: first error at char ${ cursor }` );
         }
      }
      components.push( component );
      if ( expectedCommands.length === 0 ) return [ cursor, components ];
      if ( type === 'm' ) type = 'l';
      if ( type === 'M' ) type = 'L';
   }
   throw new Error( `Invalid path: first error at char ${ cursor }` );
}
```

`parseRaw()`将路径分割成组件，然后将它们传递给`parseComponents()`方法，根据`expectedCommand`的构造规则从我们的`pathGrammar`以及任何`validComma`中搜索一个`match()`。注意`parseComponents()` `return`是一个数组，包含命令的`cursor`位置(起始索引)和新解析的`command`。

当`parseComponents()`快速通过我们正在解析的`path`时，它检查匹配，将其作为一个整数解析到结果`components`数组，如果当前正在解析的命令在`path`字符串的末尾，则返回，如果有任何错误，则在`Error()`中执行`throw`。

# 1000 个光点

我们的`PathParser`解决了两个重要问题。当然，它很好地解析和格式化了 SVG 路径字符串，但是当解析一个无效路径时，它也是一个`throw`,使得用`try {} catch {} finally {}`块处理验证变得容易。

```
const shape = "m 150,150 a 25,25 0 1,1 50,0 a 25,25 0 1,1 -50,0 z";const parsedShape = PathParser.parseRaw( shape )
   -> [ [ 'm', 50, 50 ], [ 'l', 100, 0 ], [ 'l', 0, 100 ], [ 'l', -100, 0 ], [ 'z' ] ]
```

这也将有助于我们映射经过解析的点，为 DOM 创建`<path>`标签。但是要记住，*路径可以用绝对或者相对的术语来定义，* 并且不同的命令有不同的规则。所以计算视图框坐标将是另一个带语法的方法的工作——这次是`pointGrammar`:

```
static pointGrammar = {
   z: () => [],
   Z: () => [],
   m: ( point, command ) => [ point[ 0 ] + command[ 1 ], point[ 1 ] + command[ 2 ] ],
   M: ( point, command ) => command.slice( 1 ),
   h: ( point, command ) => [ point[ 0 ] + command[ 1 ], point[ 1 ] ],
   H: ( point, command ) => [ command[ 1 ], point[ 1 ] ],
   v: ( point, command ) => [ point[ 0 ], point[ 1 ] + command[ 1 ] ],
   V: ( point, command ) => [ point[ 0 ], command[ 1 ] ],
   l: ( point, command ) => [ point[ 0 ] + command[ 1 ], point[ 1 ] + command[ 2 ] ],
   L: ( point, command ) => command.slice( 1 ),
   a: ( point, command ) => [ point[ 0 ] + command[ 6 ], point[ 1 ] + command[ 7 ] ],
   A: ( point, command ) => command.slice( 6 ),
   c: ( point, command ) => [ point[ 0 ] + command[ 5 ], point[ 1 ] + command[ 6 ] ],
   C: ( point, command ) => command.slice( 5 ),
   t: ( point, command ) => [ point[ 0 ] + command[ 1 ], point[ 1 ] + command[ 2 ] ],
   T: ( point, command ) => command.slice( 1 ),
   q: ( point, command ) => [ point[ 0 ] + command[ 3 ], point[ 1 ] + command[ 4 ] ],
   Q: ( point, command ) => command.slice( 3 ),
   s: ( point, command ) => [ point[ 0 ] + command[ 3 ], point[ 1 ] + command[ 4 ] ],
   S: ( point, command ) => command.slice( 3 ),
};
```

`pointGrammar`的键这次指向的不是 regex，而是取当前点和命令，吐出下一个点的纯函数。当然，绝对(大写)命令要简单得多，因为在这种情况下，我不需要知道当前点的任何信息就可以找到下一个点的位置。

准备就绪后，我的`PathParser`就可以解析来自 SVG 路径的坐标了:

```
static points( path ) {
   let currentPoint = [ 0, 0 ];
   return PathParser.parseRaw( path ).reduce( ( result, command ) => {
      currentPoint = this.pointGrammar[ command[ 0 ] ]( currentPoint, command );
      return [ ...result, currentPoint ];
   }, [] );
}
```

该方法使用`pointGrammar`和`currentPoint`缓冲区将那些`parse` d 命令`reduce()`到一个视图框坐标数组中:

```
const sameShape = [
   "m 25,25 l 50,0 l 0,50 l -50,0 z",
   "M 25 25 L 75 25 L 75 75 L 25 75 Z"
];PathParser.parseRaw( sameShape[ 0 ] )
   -> [ [ 25, 25 ], [ 75, 25 ], [ 75, 75 ], [ 25, 75 ], [] ]
PathParser.parseRaw( sameShape[ 1 ] )
   -> [ [ 25, 25 ], [ 75, 25 ], [ 75, 75 ], [ 25, 75 ], [] ]
```

# 结论:阻力最小的路径

我们结合了 regex 的文本匹配能力和 JavaScript 的灵活性，可以将原始文本路径解析为点坐标数组。仅此一点就足以让用户在 DOM 中对一个`<svg>` `<path>`拥有很大的控制权。添加`PathParser`方法来计算曲线手柄等并不困难，这使得从 Adobe Illustrator 等品牌图形编辑器中复制选项/功能变得容易。

这个故事的寓意是什么？ **Regex 本身不好，不好，对解析技术语法不好；**通常只是嵌套太多。[这个帖子](https://stackoverflow.com/questions/6751105/why-its-not-possible-to-use-regex-to-parse-html-xml-a-formal-explanation-in-la)有最好的电梯解释为什么。

*更多内容尽在*[***plain English . io***](http://plainenglish.io)