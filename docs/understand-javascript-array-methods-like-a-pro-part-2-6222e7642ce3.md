# 像专家一样理解 JavaScript 数组方法

> 原文：<https://javascript.plainenglish.io/understand-javascript-array-methods-like-a-pro-part-2-6222e7642ce3?source=collection_archive---------20----------------------->

## JavaScript 数组方法的全面概述—第 2 部分

![](img/733882a12f5f523f6ae9a9053bb29495.png)

Photo by [Christina Morillo](https://www.pexels.com/@divinetechygirl?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/two-women-looking-at-the-code-at-laptop-1181263/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

欢迎回到我的系列**像专家一样理解 JavaScript 数组方法！**如果你错过了第一部分，我建议你在深入第二部分之前先检查一下。👇

[](/understanding-javascript-array-methods-like-a-pro-72be6153320f) [## 像专家一样理解 JavaScript 数组方法

### 如果你真的想成为 JavaScript 专家，那么你必须能够完全理解数组方法是如何工作的…

javascript.plainenglish.io](/understanding-javascript-array-methods-like-a-pro-72be6153320f) 

上次我们看了 JavaScript 提供的一些初学者数组方法，以及何时应该使用它们。在本系列的这一部分中，我们将深入探讨更高级的数组方法，如 **map()、some()和 reduce()** 。我倾向于使用这些方法，仅仅是因为它们在我的应用程序中使用时非常强大。读完这个系列，你也应该对这些方法的工作原理有一个专业的理解。

说够了，让我们开始吧…

# map()方法

欢迎使用地图方法！我非常兴奋地谈论这个方法，因为它是我的应用程序中最常用的方法。地图方法超级强大，非常容易理解。让我们来看看这个方法到底有多强大:

```
const galaxy = ['rick','morty','kate','jerry','summer','snowball'];let sub_world = [];for(let i = 0; i < galaxy.length; i++){
 sub_world.push({index: i, name: galaxy[i]})
}console.log({sub_world});//output
//[{index: 0, name: 'rick'},{index: 1, name: 'morty'},{index: 2,   name: 'jerry'},{index: 3, name: 'summer'},{index: 4, name: 'snowball'}]
```

在上面的代码中，我们循环遍历数组，并将一个新对象推送到我们的 **sub_world** 数组中，该数组包含元素的索引和元素的名称。在我们完成对数组的迭代后，我们记录新数组，以查看它返回了一个全新的对象数组。这看起来很简单，不是吗？

当然，但是如果你还记得这个系列的第一部分，因为循环很快就要灭绝了，仅仅是因为现在有了更简单的方法。

让我们看看如何使用 map 方法实现相同的代码

```
const galaxy = ['rick','morty','kate','jerry','summer','snowball'];const sub_world = galaxy.map((name,index) => ({index, name}))console.log({sub_world});//output
//[{index: 0, name: 'rick'},{index: 1, name: 'morty'},{index: 2,   name: 'jerry'},{index: 3, name: 'summer'},{index: 4, name: 'snowball'}]
```

看一下上面的代码。请注意 map 方法与我们在之前的故事中看到的 **forEach** 方法是多么的相似。这里的区别是 map 方法返回一个数组，而 forEach 不返回任何东西。

map 函数实际上是用来将一个数组映射到一个新的数组，我们可以做的事情是无限的。现在让我们看一个更复杂的例子。

```
const galaxy = ['rick','morty','kate','jerry','summer','snowball'];const friends = [
 {id: 0, name: 'bird man'},{id: 0, name: 'noob noob'},
 {id: 1, name: 'jessica'},{id: 1, name: 'morty jr.'},
 {id: 0, name: 'morty'},{id: 2, name: 'jerry'},
 {id: 4, name: 'morty'},{id: 4, name: 'rick'},
 {id: 4, name: 'ethan'},{id: 5, name: 'morty'},
 {id: 5, name: 'jerry'},{id: 3, name: 'snowball'}
]const sub_world = galaxy.map((name,index) => {
 const my_friends = friends.filter(friend => friend.id === index).map(friend => friend.name);
  return {
   name: name,
    friends: my_friends
  }
})console.log({sub_world});//output
//[{name: 'rick', friends:['bird man','noob noob','morty']},
// {name: 'morty', friends:['jessica','morty jr.']},
// {name: 'kate', friends:['jerry']},
// {name: 'jerry', friends:['snowball']},
// {name: 'summer', friends:['morty','rick','ethan']},
// {name: 'snowball', friends:['morty','jerry']}]
```

这可能看起来很难理解，但是相信我，当我们开始分解它时，它是相当简单的。在上面的例子中，我们迭代了星系数组中的每个元素。对于数组中的每个元素，我们过滤掉 **friends** 数组，并找到与当前元素的索引相匹配的元素。然后，我们将结果映射回一个名为 **my_friends** 的新数组。一旦完成，我们返回当前元素名称的对象，以及我们在 **friends** 数组中找到的它们的朋友。

这就是地图方法如此强大的原因💪。

# 何时使用 map()方法

map 方法是我最常用和最喜欢的 JavaScript 数组方法之一。这种方法在我发现自己处于的任何情况下都很方便。如上所述，我们可以使用 map 方法将一个旧数组转换成一个新的对象数组，或者基本上是任何与此相关的东西。当我们需要将两个数组合并成一个数组时，我们也可以使用这种方法(只有当两个数组的大小都相当小时，我才会推荐这种方法)。

所以 map 方法处理数组，但是对象呢？

很高兴你问了。map 方法不直接处理对象，但是我们总是可以使用 **Object.entries()** 方法将对象转换成数组(在本系列中我们不会讨论这个方法)，然后像以前一样使用它。

# reduce()方法

说到整合，reduce 方法就是为此而构建的。

这是我在编写应用程序时经常使用的另一个数组方法。这是最复杂的数组方法之一，但如果使用正确，它绝对是强大的。

```
const numbers = [1,10,44,21,19,2,3];let total = 0;for(let i = 0; i < numbers.length; i++){
 total += numbers[i];
}console.log({total});//output: 100
```

看上面的例子，我们可以看到一个简单的 for 循环，它取数组中所有数字的和。让我们继续用 reduce 方法替换 for 循环:

```
const numbers = [1,10,44,21,19,2,3];const total = numbers.reduce((sum,number) => sum + number,0)console.log({total});//output: 100
```

请注意 reduce 方法如何产生与之前相同的输出。好吧，我知道你在想什么，这看起来很混乱。相信我，我花了一段时间才明白这种方法是如何运作的。我会尽力解释，但事情是这样的:

reduce 方法的第一个参数叫做*累加器*，它的目的是……嗯，累加东西。在这种情况下，它将保存数组中数字的总和，我们可以初始化我们的总和，从我们喜欢的任何值开始，因此在 reduce 方法的末尾是“0”。第二个参数是我们的数组元素。这就像 forEach 和 map 一样，给我们当前所在的元素。最后，我们将当前总和与当前元素相加，并返回结果，直到访问完数组中的所有元素。

这个例子有点简单，所以让我们来看看 reduce 方法的一个更实际的用例。

```
const galaxy = ['rick','morty','rick','jerry','summer','summer','kate','noob noob','morty','rick','rick','summer','morty'];const character_count = galaxy.reduce((obj,name) => {
 obj[name] ? obj[name]++ : obj[name] = 1
  return obj;
},{})console.log({character_count});//output
//{jerry: 1, kate: 1, morty: 3, noob noob: 1, rick: 4, summer: 3}
```

在上面的例子中，我们试图计算一个特定的字符在数组中出现的次数。这里我们的累加器是一个对象而不是一个数字，我们的第二个参数和之前一样。我们在数组的第一次迭代中初始化一个空对象。如果一个字符已经存在于我们的对象中，那么我们增加该字符的计数，否则，我们用该字符的名称创建一个新的属性，并将其计数设置为 1。

正如你所看到的，似乎我们有一个额外的瑞克在我们的星系中翻找…

![](img/034850730de34a6b0010a977892cfa54.png)

rick and morty evil morty theme song — soundcloud.com

# 何时使用 reduce()方法

reduce 方法几乎在所有情况下都有用。如果我们需要得到一个快速的总数，如果我们需要创建一个具有唯一值的对象，或者像 map 方法一样产生另一个数组，我们可以使用它。我通常不使用 reduce 方法来生成另一个数组，原因很简单，因为 map 方法已经这样做了，使用 reduce 只会让它更难理解。

# some()方法

这种方法不像其他两种方法那么复杂，但我认为这是一种容易被大多数开发人员遗忘的方法。作为一个被遗忘的方法，它仍然在我的应用程序中有一些用处…

```
const products = ['potato','banana','strawberry','beans','coffee','cake']const check_avail = 'beans'
let available = false;for(let i = 0; i < products.length; i++){
 if(products[i] === check_avail){
   available = true;
  }
}console.log(`The product: ${check_avail} is ${available ? '' : 'not '}available`)//output: The product: beans is available
```

上面的例子演示了我们如何检查一系列产品的可用性。如果我们正在寻找的产品可用，那么我们将变量设置为 true 并记录输出。老实说，对于这种问题使用 for 循环有点大材小用，但是我们可以通过使用 some 方法来减少代码量。

```
const products = ['potato','banana','strawberry','beans','coffee','cake']const check_avail = 'beans'
const available = products.some(product => product === check_avail)console.log(`The product: ${check_avail} is ${available ? '' : 'not '}available`)//output: The product: beans is available
```

上面的代码片段演示了我们如何通过使用 some 方法获得相同的输出。与其他方法一样，这种方法的工作方式完全相同，只是它返回被检查的条件是真还是假。我们也可以用 **find()** 方法来做这个检查，但是这将导致我们进行额外的检查来确认是否找到了结果。

# 何时使用 some()方法

当我们需要检查数组中的条件是否满足时，some 方法变得非常有用，例如检查产品当前是否可用，或者我们是否需要检查某个数量是否存在。我经常使用这种方法，希望这能让其他人也用上它。

# 结论

好了，你知道了。理解这些方法是如何工作的确实有助于练习。你用得越多，你就越能理解如何以及何时正确使用它们。

不幸的是，这是这个系列的结尾，但我希望在不久的将来能做更多这样的事情。

一如既往，感谢再次阅读，不要忘记鼓掌，我会很快再见到你。👋

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)