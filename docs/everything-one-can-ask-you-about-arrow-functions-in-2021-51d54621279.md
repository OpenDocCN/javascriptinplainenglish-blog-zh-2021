# 关于 2021 年的 JavaScript Arrow 函数，你能问的一切

> 原文：<https://javascript.plainenglish.io/everything-one-can-ask-you-about-arrow-functions-in-2021-51d54621279?source=collection_archive---------7----------------------->

![](img/4535853d720c08c1742c1faf4f684f66.png)

Photo by [Tudor Baciu](https://unsplash.com/@baciutudor?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

你最近是否被术语“箭头函数”弄得措手不及？

或者说，你知道它的存在，但当讨论到它的本质时，你发现自己被遗忘了？

如果你的答案是“去过那里，做过那个！”那你就登陆了正确的页面，我的朋友！️🚀

我们，世界的开发者，总是渴望了解更多。但与此同时，我们也缺乏耐心去无休止地翻页，去彻底了解一些东西。

![](img/682efb4a90ba7e8ee1c765390a35b885.png)

作为一名初露头角的学者，我确实发现自己被夹在成千上万的书签之间，并被不确定的重定向所困扰。有时，它甚至会削弱寻找更多的欲望。因此，我决定考虑克林特·伊斯特伍德几十年前给我们的一条建议——“有时，如果你想看到更好的变化，你必须把事情掌握在自己手中”。

我采纳了他的建议，整理了我从各种渠道和采访经历中收集的所有信息，因为我们必须纵容好奇心，而不是削弱它！

事不宜迟，这就是了！一个关于箭头函数的 A-Z！对于那些对此一无所知的人和那些好奇想知道它的一切的人(做好长时间阅读的准备，一个人不能从 A 跳到 Z 而跳过中间的字母。所以系好安全带，走完这 26 步！😉).

# 从非常明显的问题开始:什么是箭头函数？

箭头函数是 Javascript ES6 中引入的众多概念之一。ES6 中引入的一些其他概念包括:

*   ***块范围的变量(Let 和 Const)***
*   ***字符串插值***
*   ***解构***
*   ***散歇符***
*   ***默认参数***

***这样的例子还可以持续一段时间……***

您将会在下面的内容中发现一些这样的概念。不过，我保证你再也不用跳页了！我抓住你了。

现在让我们设计一个箭头函数的紧凑定义，涵盖它的所有方面(基本上只有两个方面，因为 Javascript 坚信简单🤟).

> “箭头函数是常规函数的语法糖，因为它允许我们为函数声明编写简短的语法。arrow 函数和我们以前的 pal 常规函数的区别在于，arrow 函数中的“this”上下文“总是”引用其词法父级的“this”上下文(它不能被代码世界中的任何其他力量改变)。”

箭头函数通常也被称为**胖函数或λ函数**。所以，当有人向你抛出这两个术语时，不要翻转，因为这只是测试你对箭头函数的理解有多深。

# 为什么胖，为什么是 Lambda？

它从语法中使用的粗箭头(= >)继承了名称“fat”。

它继承了名称“Lambda ”,因为 Lambda functions 是一个通用术语，在许多编程语言中用来表示提供简单语法的函数，或者可以写成匿名函数(没有名称)。箭头函数的工作原理类似，因此得名。

# 是时候玩“发现差异”了😁

```
**//Arrow function
const greenArrow = () => {
 return “Hey, I am an arrow function”;
}****//Regular function
const deathStroke = function (){
 return “Hey, I am a regular function”;
}**
```

你发现了吗？当然，你做到了！如您所见，上述两种语法之间唯一的细微差别是:

`**“function ()”** replaced by “**() =>”**`

很简单，对吧？

从上面的两个例子中，我们可以看到 arrow 函数是如何独立于“function”关键字来定义函数的，因此语法很短。但是，如果它只是从表达式中删除一个关键字，这难道不是一个被高估的概念吗？正如你已经猜到的，它还有更多！

# 越短越好！

箭头函数带来的好处是我们可以让它变得更短！但是！

***仅当一个参数传递给函数，且函数在其返回块*** 中包含一条语句时。

如果没有或者有一个以上的参数被传递，那么它们必须用圆括号()括起来。类似地，如果函数块中没有或有一个以上的 return 语句，它们必须用花括号{}括起来。

## 较短语法的不同组合

***1。最短语法—一个 return 语句和一个参数。***

让我们考虑下面的片段:

```
**const greenArrow = (shoot) => {
 return shoot * 100;
}**
```

请记住，它是“返回”一个表达式，而不是在块中执行任何其他单行操作，比如`console.log`。我们稍后也会谈到这一点。

设计简短的语法，去掉 return 关键字和任何你能找到的括号👀。

```
**const greenArrow = shoot => shoot * 100;**
```

很美，不是吗？这是常规函数永远无法实现的。无意冒犯，老朋友！😛

***特例*** *:* ***如果返回值是一个对象，我们可以直接去掉 return 关键字，但是必须将返回的块用圆括号()括起来。***

```
**const greenArrow = () => {
 return {shot: "bullseye"};
}**
```

*将被写成—*

```
**const greenArrow = () => ({shot: “bullseye”});**
```

**2*2。短语法-函数块中的一个参数和一条语句(不返回)。***

让我们考虑下面的片段:

```
**const greenArrow = (shoot) => {
 console.log(`Hey, I shot deathstroke ${shoot} times`);
}**
```

*将被写成—*

```
**const greenArrow = shoot => console.log(`Hey, I shot deathstroke ${shoot} times`);**
```

我们将再次省略表达式中的所有括号，但我们必须写出完整的`**console.log()**`语句，因为只有`**return**`在其不存在时拥有存在的能力。

```
**NOTE : In case you are confused by the** **` `** **backticks I have used to enclose the statement inside** **console.log** **instead of the** **“ ” double quotes** **that we are quite familiar with, then here is the answer you are looking for -** **` ` does string interpolation! Yes, one of the many other concepts introduced in ES6\. String interpolation is helpful for evaluating a statement containing one or more placeholders which are replaced by their corresponding values in the final output.** 
```

***3。短语法-功能块中的一个参数和多个语句。***

让我们考虑下面的片段:

```
**const greenArrow = (shoot) => {
  console.log(`Hey, I shot deathstroke ${shoot} times`);
  console.log("And guess what? He didn't even flinch!");
}**
```

*将被写成—*

```
**const greenArrow = shoot => {
  console.log(`Hey, I shot deathstroke ${shoot} times`);
  console.log("And guess what? He didn't even flinch!");
}**
```

去掉了参数周围的括号，因为我们接收的是一个参数，但是我们现在必须用花括号将返回的代码块中的多行代码括起来。

***4。短语法—功能块中有多个参数和一条语句。***

让我们考虑下面的片段:

```
**const greenArrow = (people, computers) => {
 return `${people} keep secrets, ${computers} do not.`;
}**
```

*将被写成—*

```
**const greenArrow = (people, computers) => `${people} keep secrets, ${computers} do not.`;** 
```

保留了多个参数周围的括号，并从包含单个 return 语句的功能块中省略了括号和 return 语句。

我希望你很清楚我们如何创建更短的 arrow/fat/lambda 函数语法。现在，让我们转到更面向逻辑的方面，这是箭头函数中`**this**` 的行为。

如果您不太确定什么是`this`上下文，请不要惊慌。我掩护你！如果很清楚`this`的背景，跳过下一节。

# **《本纪** `**"**` **上下文**

`this`指对象内部的上下文。并且当使用一个没有附加到任何用户定义对象的`this`时，浏览器会自动将其附加到窗口对象。(浏览器，终极救星！).

让我们通过几个例子来更好地理解它。

```
**const gryffindor = {
  founder : "Godric Gryffindor",
  houseGhost : "Nearly-Headless-Nick",
  madeUpFacts : function () {
    return `Once upon a time, ${this.founder} hung out with  ${this.houseGhost}!`      
   }
};****gryffindor.madeUpFacts();**
```

在上面的代码片段中，对象`**gryffindor**` 中定义的所有属性都属于对象的**上下文**。

`**founder**`、`**houseGhost**` 、`**madeUpFacts**` 属于`**gryffindor.**` 对象的`**this**` 上下文，函数内部的`**this**` 上下文由调用函数的对象**决定。**既然如此，我们就在`**gryffindor**` **上调用`**madeUpFacts**` ，**里面的`**this**` 上下文****就是`**gryffindor**` **的上下文。******

****为了更清楚，让我们看另一个例子:****

```
****function potterHead () {
  this.potterFanatic = true;
  this.beatsGreenArrow = "It's complicated!";
}****potterHead();
console.log(this.potterFanatic); //prints true
console.log(this.beatsGreenArrow); //prints It's complicated!****
```

****你拿到了吗？`**potterHead**` 在窗口对象上被调用。因此，变量`**potterFanatic**` 和`**beatsGreenArrow**` 被附加到窗口对象的上下文中。****

****所以，不要徘徊太多。`**this**` 上下文只是指一个对象的上下文。不多不少。****

****现在，对象的`**this**` 上下文可以很容易地传递，但只能用**常规函数**。****

# ****将“天选之物”附加到常规函数的两种方法****

*******1。一个常规函数总是拾取用于调用常规函数*** 的对象的 `***this***` ***上下文。*******

```
****const gryffindor = {
  founder : "Godric Gryffindor",
  houseGhost : "Nearly-Headless-Nick",
  madeUpFacts : function () {
    return `Once upon a time, ${this.founder} hung out with  ${this.houseGhost}!`      
   }
};****gryffindor.madeUpFacts();****
```

****考虑我们在上一节看到的同一个例子。向上滚动阅读解释。****

## ******后续问题:******

> ****但是如果，`**madeUpFacts**` 不是`**gryffindor**` 的属性，我们仍然想访问`***madeUpFacts***`中`***gryffindor***` 的`**this**` 上下文，该怎么办呢？****

******②*。我们还可以通过调用/应用/绑定将*** `***this***` ***上下文附加到常规函数上。让我们调整前面的代码片段来达到同样的效果。*******

```
****const gryffindor = {
  founder : "Godric Gryffindor",
  houseGhost : "Nearly-Headless-Nick",
};
const madeUpFacts = function () {
    return `Once upon a time, ${this.founder} hung out with  ${this.houseGhost}!`      
};****madeUpFacts.call(gryffindor);****
```

****我们使用`**call/apply/bind**`将对象的`**this**` 上下文附加到不是对象属性的函数上。传递给`**call/apply/bind**`的第一个参数是我们想要分配给常规函数的新的`**this**` 上下文。****

****`**Call/Apply/Bind**`除了对`**this**` 上下文的依附之外，在其他方面都做了不同的工作。****

****这是为了让您对常规函数的`**this**` 如何工作有一个大致的了解。现在是我们进入箭头函数如何处理`**this**` 上下文的好时机。****

# ******箭头功能和“this”上下文的关系******

****我们现在非常清楚如何将任何`**this**` 上下文附加到常规函数上。****

> *******但是，我们可以对箭头函数做同样的事情吗？*******

****不，从来没有！****

> *******那么，箭头函数里面的*** `***this***` ***上下文会是什么呢？*******

****这才是你需要掌握的诀窍！所有关于箭头函数的输出型问题都围绕着对这个概念的理解。所以，仔细看！****

> ****arrow 函数的"`**this”**` 上下文总是指其词法父级的" this "上下文。还有…****

> ****arrow 函数的词法父类要么是封装它的函数(如果有的话)，要么是窗口对象！不多不少。****

****如果你对以上两种说法有一个水晶般清晰的理解，你就可以解决任何涉及到箭头函数的情况。虽然，如果你还没有做到，看看下面的例子，你会做到的！😊****

# ******基于输出的箭头功能问题******

# ****1.****

```
****const justiceLeague = {
  superVillain: "Darkseid",
  firstEdition : function () {
      return `Who is ${this.superVillain}? Wasn't SteppenWolf the villain in Justice League?`;
  }, 
  secondEdition : () => {
         return `Sad that you haven't watched the Snyder Cut yet because ${this.superVillain} is the GOAT!`;
 }
};
justiceLeague.firstEdition();
justiceLeague.secondEdition();****
```

******输出—******

```
**Who is Darkseid? Wasn't SteppenWolf the villain in Justice League?Sad that you haven't watched the Snyder Cut yet because **undefined** is the GOAT!**
```

****不幸的是，就像正义联盟的第一次切割一样，达克赛德再次拒绝露面。😯****

******那么，为什么是未定义的呢？******

****再次提醒自己:****

*******“当一个箭头函数被定义为一个对象的属性时，它的词法作用域不是这个对象，而是它所包装的函数或者窗口对象。”*******

****在上面的代码片段中，函数的词法范围:`**secondEdition**` 是`**window**` 对象，因为它没有被另一个函数包装。并且窗口对象没有为其定义的`**superVillain**` 属性。因此，未定义的值。对其调用 arrow 函数的对象没有任何影响。****

****而函数`**firstEdition**` **，**是一个常规函数，它获取调用它的对象`**justiceLeague**` 的`**this**` 上下文，并因此在返回语句中返回`**this.superVillain**`的正确值。****

## ******跟进问题:******

****现在解决上述情况。从箭头函数返回`**this.superVillain**`的正确值，而不是`**undefined**`。****

****又陷入困境了？不要想太多。箭头函数很简单，记住，它只基于两个原则。****

****只需应用**将`**this**` 上下文附加到箭头函数的**方式。****

**用你选择的词法父类包装它！**

**不确定怎么做？让我们来了解一下！**

# **2.**

```
**const justiceLeague = {
  superVillain: "Darkseid",
  firstEdition : function () {
   return `Who is ${this.superVillain}? Wasn't SteppenWolf the   villain in Justice League?`;
  }, 
  secondEdition : function () {
    return function = () => {
       return `Sad that you haven't watched the Snyder Cut yet because ${this.superVillain} is the GOAT!`;
     }
  }
};
justiceLeague.firstEdition();
justiceLeague.secondEdition()();**
```

****输出—****

```
Who is Darkseid? Wasn't SteppenWolf the villain in Justice League?Sad that you haven't watched the Snyder Cut yet because Darkseid is the GOAT!
```

**现在我们知道谁是有史以来最大的恶棍了！🤭**

**我做了什么来弥补？正如我之前所说的，只是围绕箭头函数的一个新的词法父类。**

**现在，让我们一步一步来看:**

**将函数`**secondEdition**` 更改为一个常规函数，现在它可以接受我们希望它接受的`**this**` 上下文，并用这个常规函数包装箭头函数。包装意味着从常规函数内部返回箭头函数。**

```
**justiceLeague.secondEdition()**
```

**将`**justiceLeague**` 的`**this**` 上下文附加到`**secondEdition**` 上，因为`**secondEdition**` 现在是常规函数。**

```
**justiceLeague.secondEdition()();**
```

**从`**secondEdition**` 调用返回的函数，即箭头函数。arrow 函数消耗其词法父级的`**this**`上下文，该父级是一个函数(`**secondEdition**` )。**

*****“因此，将*** `***this***` ***上下文附加到箭头函数的唯一方法是用一个可以接受您想要的任何*** `***this***` ***上下文的常规函数来包装它。”*****

# **你认为你什么都知道，但你真的知道吗？**

**你准备好看看我们对箭头函数的理解中的一些漏洞了吗？**

# ****漏洞-1:****

```
**const hero = "Green Arrow";
const ultimate = () => {
 console.log(`Who is the ultimate hero? ${this.hero}!`);
};
ultimate();**
```

**你认为上面的输出应该是什么？**

**箭头函数`**ultimate**`的词汇父项是窗口对象，我们在窗口的上下文中定义了一个名为`**hero**`的变量。所以，它应该返回:**

```
**Who is the ultimate hero? Green Arrow!**
```

**让我们运行这段代码并检查输出。**

```
**Who is the ultimate hero? undefined!**
```

**以上是我收到的输出。太奇怪了！不要太多，如果你知道接下来会发生什么——**

*****所有块范围的变量(const 和 let 变量)从不依附于*** `***this***` ***上下文的“窗口”。*****

**因此，这段代码也将返回一个未定义的。**

```
**const hero = "Green Arrow";
console.log(this.hero); //returns undefined**
```

## **后续问题:**

****您如何解决上述问题？****

```
**var hero = "Green Arrow";
const ultimate = () => {
 console.log(`Who is the ultimate hero? ${this.hero}!`);
};
ultimate();**
```

***返回—***

```
**Who is the ultimate hero? Green Arrow!**
```

**此外——**

```
**var hero = "Green Arrow";
console.log(this.hero); //returns Green Arrow**
```

*****故事的寓意——如果您打算稍后使用***`***this***` **来访问它，请不要在窗口的作用域中使用块作用域变量。****

# *****漏洞二:*****

```
***deathStroke();
greenArrow();
var greenArrow = () => {
   return "I want peace and no war!";
};
function deathStroke() {
   return "I want peace too but that comes after war!"
};***
```

***上面代码的输出应该是什么？***

***通过提升的概念，所有的`**var**`类型变量和函数声明都被提升到作用域的顶部。所以它应该执行这两个函数。***

***但是你还记得吊装到底是怎么工作的吗？***

***当一个变量被提升到一个作用域的顶部时，只有声明被提升到顶部并被赋予一个值`**undefined.**` 当程序到达它被写入的行**时，用户定义的赋值发生。*****

***在后台进行提升后，我们的代码将如下所示:***

```
***var greenArrow = undefined;
function deathStroke() {
   return "I want peace too but that comes after war!"
};
deathStroke();
greenArrow();
greenArrow = () => {
   return "I want peace and no war!";
};***
```

******寓意——箭头功能不能悬挂。就像我们自己的块范围变量一样。******

***当被问及上述程序的输出时，只要它试图调用还没有被定义为该程序的函数的`**greenArrow()**`，它就会在第 1 行抛出一个错误。***

# *****关于箭头函数的主观题*****

## *****1。为什么不能用带箭头的函数调用/应用/绑定？*****

***`**Call/apply/bind**`用于将新的`**this**` 上下文绑定到一个函数，而箭头函数严格遵循基于其词法父元素提取`**this**` 上下文的规则。***

*****跟进问题:*****

*****如果用箭头函数写一个** `**call/apply/bind**` **会怎么样？它会抛出错误吗？*****

***不会。它执行语句时没有任何错误。只是它没有将新的`**this**` 上下文绑定到 arrow 函数，arrow 函数仍然基于它的词法父元素维护`**this**` 上下文。***

## *****2。我们能把参数绑定到一个箭头函数吗？*****

***箭头函数肯定没有自己的参数对象。arguments 对象允许常规函数接受动态参数。***

***但是，在箭头函数中也有一个接受动态参数的变通方法！***

***ES6 中引入的传播和休息算子。***

******展开运算符:将集合的内容展开为用逗号分隔的值。******

```
***var a = [1, 2, 3];
console.log(...a); // prints 1, 2, 3***
```

******Rest 运算符:将逗号分隔的值组合成一个集合。******

```
***function a(...args) {
 console.log(args); //prints [1, 2, 3]
}
a(1, 2, 3);***
```

***这两个运算符都用(…)表示，即三个点。Javascript 不希望你把它处理得太多，它会尝试自己处理大部分事情！🤩***

*****例:*****

```
***const gameOfThrones = () => {
  return `The song of ${arguments[0]} and ${arguments[1]}`;
};****console.log(gameOfThrones("ice", "fire"));***
```

***上面的代码会抛出一个错误，因为`**gameOfThrones**` 这个箭头函数没有参数对象。因此，代码将在第 2 行抛出一个引用错误。***

```
***const gameOfThrones = (...args) => {
   const values = [...args];
   return `The song of ${values[0]} and ${values[1]}`;
};****console.log(gameOfThrones("ice", "fire"));****const gameOfThrones = (...args) => {
  const values = [...args];
  return `The ${values[0]} of ${values[1]} and ${values[2]}`;
};****console.log(gameOfThrones("song", "ice", "fire"));***
```

***以上两个例子解释了如何使用 `**spread and rest operators**`将动态参数传递给 arrow 函数。***

***您也可以使用`**call/apply/bind**`和`**spread and rest operators**`向 arrow 函数动态发送参数，即使`**call/apply/bind**`不能用于向 arrow 函数附加新的`**this**`上下文。查看下面的示例，了解如何操作。***

```
***const gameOfThrones = (...args) => {
  const values = [...args];
  return `The ${values[0]} of ${values[1]} and ${values[2]}`;
};****gameOfThrones.apply(this, ["song", "ice", "fire"]);
gameOfThrones.call(this, "song", "ice", "fire");***
```

## *****3 .我们可以使用 arrow 函数作为构造函数还是使用带有 arrow 函数的新运算符？*****

***不，我们不能。构造函数应该有一个内置的`**[[Construct]]**`函数和一个附加的原型。`**[[Construct]]**`函数接受在创建函数的新实例时传递的参数，原型对象允许您修改/添加函数的属性。然而，箭头功能既没有`**[[Construct]]**`功能，也没有附带原型。***

```
***const annabelle = (claps, haunts) => {
    this.claps = claps || true;
    this.haunts = haunts ||true;
};
anabelle.prototype.forgets = false; //Throws an error.***
```

***当您试图将新属性绑定到 arrow 函数的原型时，上面这段代码将抛出一个错误，因为 arrow 函数没有原型。错误说明无法设置`**undefined**`的`**forgets**`属性。***

## *****随访问题-*****

*****基于以上的理解，你能区分正则函数和箭头函数吗？*****

***是的，您可以通过检查函数中的“原型”属性来区分常规函数和箭头函数。***

```
***annabelle.hasOwnProperty(“prototype”); //returns false***
```

## *****4。箭头函数可以用作生成器函数吗？*****

***不。箭头函数不支持 yield 语句，这就是为什么我们不能将它们用作生成器函数。此外，没有可用于创建生成器箭头函数的语法。虽然，有几个关于向箭头函数添加生成器功能的提议，我们可能很快就会看到。所以，敬请期待！***

## *****5。下面代码的输出会是什么？*****

```
***const greenArrow = () 
  => {
   return "I want peace and no war!";
 };***
```

***上面的代码将抛出一个语法错误，因为箭头函数不能在其参数和箭头之间包含换行符。但是，如果返回值没有左括号，可以通过在左花括号或箭头后添加一个换行符来解决这个问题***

```
***//valid**
**const greenArrow = () => {
   return "I want peace and no war!";
 };****//valid
const greenArrow = () => 
   console.log("I want peace and no war!");*** 
```

## *****6。为什么 arrow 函数声明会在下面的代码片段中抛出语法错误？*****

```
***let callback;
callback = callback || function() {}; // ok
callback = callback || () => {}; //throws syntax error***
```

***这是因为，尽管 arrow 函数中的 arrow 不是操作符，但 arrow 函数有特殊的解析规则，与常规函数相比，这些规则与操作符优先级的交互方式不同。因此，表达式会混淆||和= >符号，从而导致错误。***

## ***后续问题-***

*****这种情况可以解决吗？当然可以。*****

***我们可以通过在()中包含箭头函数声明，从而定义整个表达式优先于||操作符，来避免||和= >之间的交互混淆。***

```
***let callback;
callback = callback || function() {}; // ok
callback = callback || (() => {}); //ok***
```

## *****7。基于对上面问题的理解，下面代码的输出会是什么？*****

```
***const winner = “Green Arrow”;
function greenArrow() {
  console.log(“I want peace and no war!”);
}
const deathStroke = () => {
  console.log(“I want peace too but that comes after war!”);
}****const callback1 = winner || greenArrow(); // returns Green Arrow
const callback2 = winner || deathStroke(); //returns Green Arrow****const callback3 = greenArrow() || winner; // returns I want peace and no war!
const callback4 = deathStroke() || winner; //returns I want peace too but that comes after war!***
```

***如果箭头函数声明与另一个运算符内联编写，将会导致错误。也就是说，如果粗箭头(= >)和操作符都是内联的，并且箭头声明不是一个单独的单元(用()括起来),就会出现混淆，导致语法错误。***

## *****8。为什么是箭头函数？它们的目的是什么？*****

***既然我们已经读了这么多关于箭头函数的内容，你难道不知道这项发明的源头是哪一种特殊的需要吗？***

***如果有人问你这个问题，显然不是期待听到一个箭头函数的定义。他们想要更多！所以你给他们更多！***

***1.箭头函数可用于反复应用于项目列表的函数。这归因于 arrow 函数的高度直观性，因为它紧密绑定到其词法父对象的`**this**` 上下文。***

```
***const justiceLeague = ["SUPERMAN", "BATMAN", "FLASH", "GREENARROW", "WONDERWOMAN", "AQUAMAN"];****const appearedMoreThanOnce = justiceLeague.filter(hero => hero !== "GREENARROW");***
```

***在上面的`**filter**` 函数中，外部常规函数(过滤器)在列表`**justiceLeague**`上被调用。内部箭头功能与其外部常规功能`**filter**`紧密耦合。由于这个原因，内部箭头函数非常容易地在`**justiceLeague**`列表的条目上不断迭代，因为它不会对它所指的`**this**`上下文产生混淆。***

***2.当处理异步代码时，使用箭头函数是非常理想的。让我们考虑下面的例子来理解这句话。***

```
***this.greenArrow.then((shoots) => {
 this.deathStroke(shoots);
});***
```

***在上面的代码中，我们有一个常规函数`**greenArrow**` ，它在`**this**` 被调用——引用窗口对象。因此，常规函数的`**.then**`处理程序中的回调函数现在被绑定到正确的`**this**` 上下文，并将在整个异步操作中保持绑定。***

## *****9。何时不使用箭头功能？*****

***这个我们已经讲过了，还是再来重温一下吧。***

1.  ***当试图创建构造函数时。***
2.  ***当试图创建一个生成器函数时。***
3.  ***当创建深度调用链或嵌套函数时(深度超过一级)。如果处理不当，有时会很难维护“这个”上下文。***

# *****总结*****

***恭喜你！你有深入学习所需的耐心。跟上它，坐下来，观察它如何带你去不同的地方。😊***

***另外，我希望我没有冒犯任何超级英雄/哈利波特迷。本文中返回的语句和使用的函数名纯属虚构，是作者想象的产物。任何与真人、活人或死人、真实事件的相似之处纯属巧合。😆***

## ***那么告诉我——是箭头函数更好还是常规函数更好？***

***没有更好的了。这两种功能都有自己的使用案例和用途。当将常规函数作为对象属性附加时，创建生成器函数，或者访问函数中的外部`**this**`上下文时，应该使用常规函数。***

***然而，当您希望保持函数中`**this**` 上下文的神圣性，并且不希望它受到妨碍时，应该使用箭头函数，我们上面已经讨论过这种情况。***

> ***“愿最好的功能被选中！开始编码吧！”***

****更多内容尽在*[*plain English . io*](http://plainenglish.io/)***