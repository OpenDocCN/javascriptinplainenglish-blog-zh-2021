# JavaScript 纯净的力量

> 原文：<https://javascript.plainenglish.io/the-power-of-javascript-purity-220a28339caa?source=collection_archive---------12----------------------->

## 深入探讨如何、为什么以及何时使用纯函数

![](img/9de90d08b264512b5ca12582c357fcc1.png)

Photo by [Adam Jaime](https://unsplash.com/@arobj?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/bar?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

一个男人走进一家酒吧，服务员给他拿来一杯水。喝完水后，男人点了一杯酸威士忌。服务员没有用新杯子盛酒，而是用苏格兰威士忌、柠檬汁和糖给水杯续杯。难以置信，对吧？当我点一杯饮料时，我希望它是直接从洗碗机里拿出来装在干净的玻璃杯里的。我不想重复使用已经喝过的杯子。这样，我知道我可以继续点饮料，而且里面的东西和以前点的没有任何区别。

用计算机科学的术语来说，廉价酒吧的水变成威士忌的场景可以被看作是一种*突变*或者是一种*副作用*。一些功能——served link——直接改变男人杯子里的内容。顾客的玻璃变异了。

相比之下，大多数酒吧用单独的杯子提供每一种新饮料，对吗？这个过程可以和一个纯函数*相媲美。功能**served link**不会直接影响客户的玻璃。相反，它提供了一个全新的杯子，不管要求如何，给任何想要的人(并且愿意付钱！).*

理解这些差异对于开发人员来说很重要，因为它鼓励我们编写更简洁、可重用的代码。此外，决定何时(何时)应用纯函数的能力是一个真正务实的程序员的标志。如果你还没有完全理解这个概念，没问题。让我们深入研究一下，看一些例子。

# 首先，什么是纯函数？

纯函数相当简单。它们是函数或方法。他们可能会接受争论。他们不修改他们的论点。他们不修改他们[功能范围](https://www.w3schools.com/js/js_scope.asp)之外的任何东西。每次给定相同的参数，它们都返回相同的值。这里有几个*专业*的定义。

根据[测点](https://www.sitepoint.com/functional-programming-pure-functions/):

> *“纯函数是返回值仅由其输入值决定的函数，没有可观察到的副作用。”*

维基百科说它遵循这两条规则:

> *1。对于相同的参数，函数返回值是相同的(没有局部静态变量、非局部变量、可变引用参数或输入流的变化)。*
> 
> *2。函数应用程序没有副作用(没有局部静态变量、非局部变量、可变引用参数或输入/输出流的突变)。*

如果您仍然没有理解什么是纯函数，不要担心，让我们看几个使用 JavaScript 的例子:

# 示例 1:一个简单的连接

假设我们正在编写一些 JavaScript 应用程序，在与我们正在处理的模块相同的目录中，我们有一组 png 图像。每个图像的名称都与我们在当前作用域中使用的一些字符串变量的名称相匹配。现在，我们需要编写一个附加文件扩展名的函数。png "到字符串的末尾。让我们使用三种不同的功能设计风格来尝试一下:突变、副作用和纯粹。

# 突变(不纯)

```
function appendPng(image){ 
    image += ".png"
}
```

在这里，我们取一个字符串，只是将字符串 *"png"* 附加到它的末尾。这种方法实际上会*改变*所提供的论点。换句话说，它在内存中的值会发生变化。没错，每次我们调用 *appendPng* 并传入一个变量*，*那个变量的值就会追加字符串*。png"* 并且永远不会相同(当然，除非您将它重新赋值或重新变异为其初始值)。

在许多语言中，这种变异有时会很有成效。这真的取决于场景。我们可能不希望重用某个值，这就是为什么我们要使用这个策略。然而，它不是一个纯粹的函数，因为它改变了所提供的参数。此外，该函数不返回值。根据经验， [void](https://www.cs.fsu.edu/~cop3014p/lectures/ch7/index.html#:~:text=Void%20functions%20are%20created%20and,does%20not%20return%20a%20value.) 函数通常是不纯的。

# 副作用(不纯)

```
let animal = "cat"function appendPng(){
    animal += ".png"
}
```

这个函数不纯有两个原因。首先，它变异了一个全局/局部范围的变量， *animal，*，这意味着它执行了一个**副作用** *。*其次，它不返回值。最后，这个方法完成了我们添加的目标。png”转换为字符串，但是，这远远不符合纯功能性的规则。

关于这种方法，我想提到的另一点与内存管理有关。JavaScript 使用了一个[垃圾收集器](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Memory_Management)，它通常会拾取我们用完的变量以节省一些内存，然而，它可能无法在这里完成它的工作。JavaScript 可能会忽略垃圾收集*动物*，因为它在 *appendPng* 中被引用。换句话说，只要*附肢*还在记忆中，那么*动物*也一定在记忆中。这很不幸，因为如果我们继续遵循这种编写函数的策略，那么我们的应用程序可能无法随着增长而扩展并保持最佳性能。

在这种情况下，我认为最好养成编写如下函数的习惯:

# 纯函数(纯！)

```
function appendPng(image){
    return `${image}.png`
}//or with arrow functions...const appendPng = (image) => `${image}.png`//or using the + operatorconst appendPng = (image) => image + ".png"
```

这些都是纯函数，因为无论我们调用它们多少次，无论我们何时调用它们，给定相同的输入，它们总是返回相同的输出。此范围内使用的值是一个参数(图像)和一些字符(。png)。此外，它不会改变其函数范围之外的任何变量。取而代之的是，它返回一个新的值。png”到它的参数，它没有变异。

# 3 之间最突出的区别

```
let animal = "cat"---Mutation---const animal_image = appendPng(animal) 
animal_image //"cat.png"
animal //"cat.png"---Side effect---const animal_image = appendPng(animal) 
animal_image //"cat.png"
animal //"cat.png"---Pure function---const animalImage = appendPng(animal) 
animal_image //"cat.png"
animal //"cat"
```

这是最显著的差异发挥作用的地方，纯粹的功能闪耀登场。假设我们想要声明一个新变量， *animal_image* ，它包含图像的引用，而不改变我们的原始字符串。在我们描述的选项中，使用 pure 函数是我们可以做到这一点的唯一方法。

> P-U-R-E …不是… P-U-R-R

![](img/85add678f279e39b97e9233be588effd.png)

Photo by [Corina Rainer](https://unsplash.com/@corinarainer?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/purr?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

# 示例 2:使用 Array.prototype.filter

Javascript 数组固有地拥有支持纯函数实践的方法，如 map、filter 和 reduce。让我们通过创建一个从数组中删除字符串的函数来看看 filter 的作用。

```
const removeStrings = (arr) => 
    arr.filter(el => typeof el !== "string")
```

同样，我们遵循相同输入相同输出的规则。此外，这里需要注意的一件重要事情是 Array.prototype.filter 方法创建了一个新的*数组，并没有修改现有的数组。*

行动中:

```
let a = [ 1, "by", true]
let b = removeStrings(a) b.push("something else")a // [1, "by", true]
b // [1, true, "something else"]
```

正如你所看到的， *a* 保持了它原来的形式，而 *b* 有点像是建立在 *a* 之上的。这些变量和它们的内容在内存中拥有不同的地址，除了它们的值相似之外，彼此没有关系。您可以通过修改其中一个继续工作，而不会无意中更改另一个。

# 例 3 对象和数组，命运的转折

![](img/0d0be80e50ab198bf1a032066a62ec57.png)

Photo by [Marcus Ganahl](https://unsplash.com/@marcus_ganahl?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/interstellar?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

假设我们生活在一个未来世界，几个世纪后，人类终于变成了星际人。不仅如此，我们经常乘坐一些瑞克&莫蒂级别的宇宙飞船。为了在太空深处导航，我们需要在车辆中存储一些空间地图数据。出于例证和高度简化的目的，让我们假设我们的地图是一组对象，例如:

```
{
    id: 324234,
    name: "Zorgon 34C",
    government: "Zorgonthian Empire", 
    passport_required: true, 
    parallax_angle: 67.2982,
    distance: 654656,
}
```

为了扩展我们的地图，我们可以冒险进入新的领域(不推荐，因为许多文明对加入星际联盟犹豫不决)，或者我们可以在一家名为 Map Express 的商店购买新的地图数据(推荐)。随着星际联盟的成长和宇宙的扩张,《地图快递》不断增加它在宇宙中的领土清单😂。让我们来看看他们如何将购买的数据加载到您的车辆上的两种方式:

## 纯方法(可能未被 Map Express 使用)

由于星际地图黑客水平很高，Map Express 决定将其所有地图数据保存在本地。换句话说，他们不会将它存储在单独的数据库中。因此，不再是每次顾客提出请求时由*获取*数据，而是商店简单地将顾客指向适当的功能，如下所示:

```
const buy_Cheshire_92B = (customer_map) => 
    [ 
        ...customer_map, 
        {
            id: 20919302,
            name: "Cheshire 92B",
            government: "Cheshire Cat Kingdom", 
            passport_required: true, 
            parallax_angle: 67.2982,
            distance: 654656,
        }
    ]
```

如您所见，每次调用该函数时，它都会使用[扩展语法](/the-secret-to-es6-spread-syntax-4066140678e0)克隆客户的地图，并将请求的区域附加到该克隆中。这是一种纯粹的方法，因为它不会改变它的参数，也不会导致任何副作用。

尽管它很纯粹，但对于像 Map Express 这样的新兴企业来说，这可能不是最好的做法。随着他们的库存越来越大，他们将需要通过编写越来越多的函数来进行扩展。更好的方法可能是编写一个通用(非纯)函数，并利用安全的现代 API 和数据库技术来存储他们的地图数据。

## 非纯方法(更可能使用)

```
const buy_territory_map = async (customer_map, requested_territory) => {
    const territory_map = await fetch(MapExpressAPI, requested_territory);
    return [ ...customer_map, territory_map ]
}
```

演示的方法 *buy_territory_map* 是**而不是纯粹的**，因为它向 Map Express 构建的一些外部 api 发出网络请求。虽然很有可能这个请求确实会返回相同的数据，但总是有可能外部数据库中的某些内容被更新。因此，尽管使用了一些纯代码原则，如使用 spread 语法进行克隆，但不能认为这个函数是纯函数。

也就是说，这就引出了一个关于**的重要话题，当** **不**使用纯函数时。Map Express 平台的架构师应该已经决定使用这种非纯粹的方法，因为它的可扩展性更好。例如，每次 Map Express 添加一个新的地图到它的目录中，它不需要为它编写一个全新的函数！

让我们来看看最后一种方法，它结合了我们刚刚看到的两种方法。(如果你对高阶函数不感兴趣，跳过这一步。)

## 好处# 1——几乎是一种纯粹的方法，但不完全是(可能使用过！)

```
const buy_map_territory = async (requested_territory) => {
    const territory_map = await fetch(MapExpressAPI, requested_territory);
    return (customer_map) => 
        [ 
            ...customer_map, 
            territory_map
        ]
}
```

这是一种有趣的方法。基本上，我们创建一个名为 *buy_map_territory* 的通用函数，它返回另一个函数！函数 *buy_map_territory* 从我们的外部 *MapExpressAPI* 异步存储请求的区域地图。返回的函数(未命名)只是通过扩展(克隆)客户的旧地图并向其追加新的区域来返回新定义的地图。

哇，等等，什么！？酷，我知道。

这些类型的函数通常以下列方式使用:

```
const buy_earth_map = await buy_map_territory("Earth")const JohnsNewMap = buy_earth_map(JohnsMap)const SallysNewMap = buy_earth_map(SallysMap)const CindysNewMap = await buy_map_territory("Morag")(CindysMap)
```

首先，声明一个新函数，该函数只执行我们的网络请求一次，并将结果存储在 *territory_map* 中。这有助于避免对同一地区的进一步网络请求。换句话说，每次我们调用 *buy_earth_map* 时，我们不需要再次执行我们的请求。

其次，为了快速获得我们的最终返回值，一个新的区域地图数组。

[高阶函数](https://developer.mozilla.org/en-US/docs/Glossary/First-class_Function)方法很有用，因为有时我们可能想要执行前者，而其他时候可能想要执行后者。

## 好处# 2——深度嵌套克隆

如果我们打算编写纯函数，特别重要的是密切关注对象和/或类似对象的数据类型(如数组和函数)，因为它们在内存中的处理方式。让我们以我们的星系际场景为例。假设，不是我们最初演示的类型，而是像这样存储区域地图:

```
{
    id: 324234,
    name: "Zorgon 34C",
    government: "Zorgonthian Empire", 
    passport_required: true, 
    location: { 
        parallax_angle: 67.2982,
        distance: 654656 
    }
}
```

在这种情况下，重要的是要知道如何按照我们之前的方式分布客户的地图阵列:

```
[ ...customer_map ]
```

会不会**不**保持纯函数属性为真。这是因为常用的克隆方法如 spread 语法和 Object.assign [执行**浅**克隆(或一级深)](https://stackoverflow.com/questions/38416020/deep-copy-in-es6-using-the-spread-syntax)。换句话说， *customer_map* 数组及其对象的第一层将被成功克隆，但是，更深层次的嵌套对象(如 *location* )仍将引用它们在内存中的原始位置。这可能会也可能不会导致问题，具体取决于您的代码的其余部分。如果我在一个函数中结合了纯方法和非纯方法，我最常遇到的问题是，我可能会使用像 redux 这样的库，当你尝试改变状态值时，它真的不喜欢。

# 回到酒吧

让我们使用纯函数方法在 JavaScript 中实现我们的 bar 类比，并最终完成它！

```
const customer1 = {
    drink: "Water",
    name: "John",
    amountOwed: 0
}function serveDrink(order, customer){
    return { 
        ...customer, 
        drink: order.drink, 
        amountOwed: customed.amountOwed + order.price 
    }
}const customer1AfterDrink = serveDrink({ drink: "Tequila", price: 5 }, customer1);
```

你现在应该明白这是怎么回事了。

## 结论

的确，纯函数并不总是一个选项。事实上，我作为 JavaScript 开发人员编写的大多数应用程序都是建立在副作用之上的。用户界面通常是基于副作用构建的。副作用和突变使我们的屏幕表现得很棒！我发现纯函数在创建 *utility-* 这样的旨在全面使用的方法时，以及在处理 React 和 Redux 这样的库时最有用。

总之，让我们不要直接改变顾客杯子里的东西(除非是一杯接一杯的水),而是为每一杯点的饮料提供一个新杯子。我们最终可能会得到更好的小费！

*更多内容看*[***plain English . io***](http://plainenglish.io/)