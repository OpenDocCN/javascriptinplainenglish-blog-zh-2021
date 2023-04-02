# 为什么应该停止使用循环

> 原文：<https://javascript.plainenglish.io/why-you-should-stop-using-loops-88a6a789106e?source=collection_archive---------9----------------------->

如果你和我一样，你在 JavaScript 中使用 for 和 while 循环的时间最长。我是说，如果它能完成任务，那还有什么问题呢？嗯，虽然它完成了工作，但是当应用程序的规模和复杂性增加时，它可能会成为一个问题。

有 3 个很好的理由说明为什么你应该停止使用循环。我们还将看看循环的各种替代方案，它们将帮助我们以更好的方式完成任务。

# 1.易于阅读和维护

![](img/23f75a8b5070149310be846a8ad179fb.png)

[The cleaner it is the easier it is to maintain it.](https://pixabay.com/photos/fittings-water-polo-construction-2784899/)

函数式编程是一个概念，应用程序中的一切都可以归结为纯粹的函数。一个纯函数是这样的，它接受一组参数，进行一些计算并返回一个结果。它不访问函数之外的任何东西， ***它自己就是纯粹的*** 。更重要的是，它只做一件事。功能越简单越好。好处是:减少冗余，模块化和易于维护。

这和循环有什么关系？让我们看一个简单的例子。假设我们需要一个数组，把所有的数字加进去，然后把它连接成一个字符串:

***非函数式编程方式同 For 循环:***

```
var numberArray = [1,2,3,4,5,6];
var stringToConcatTo = "Total:";function addNumbersAndConcat(arr, str){
  var total = 0;
  for (var index = 0; index < arr.length; index++){
    total += arr[index];      ***// Add total***
  }
  str += total.toString();    ***// Concatenate to the string*** return str;
}
***// Function Call***
this. addNumbersAndConcat(numberArray, stringToConcatTo);
```

在上面的例子中，代码按照我们希望的那样工作，但是，它偏离了函数式编程的概念。该函数执行不止一次计算(加法代码块和级联代码块)。我们可以通过将加法部分放在不同的函数中，然后在这里调用它来解决这个问题。这样，这个函数只接受加法函数的输出，并进行连接。所以在这种情况下，它只是为连接做“计算”。

***功能编程方式同 For 循环:***

```
var numberArray = [1,2,3,4,5,6];
var stringToConcatTo = "Total:";function addArray(arr) {
  var total = 0;
  for (var index = 0; index < arr.length; index++){
    total += arr[index];      ***// Add total***
  }
  return total.toString();
}function concatToTotal(arr, str){
  str += this.addArray(arr);    ***// Concatenate to the string*** return str;
}concatToTotal(numberArray, stringToConcatTo); ***// Function Call***
```

这很好，但如果我们只是消除循环，我们可以做得更好。在 JavaScript 中我们可以使用 ***映射、归约和过滤。*** 这些功能就是为此而设计的。使用它们，我们使我们的代码更容易阅读，理解，并保持其功能性编程。在我们的特例中，我们将使用 ***减少*** 来改进我们的代码。

***无循环功能编程方式:***

```
var numberArray = [1,2,3,4,5,6];
var stringToConcatTo = "Total:";function concatToTotal(arr, str){
  str += arr.reduce((acc, currVal) => acc + currVal).toString();
  return str;
}concatToTotal(numberArray, stringToConcatTo);
```

我们已经重构了我们的 be 严格函数，reduce 帮助我们消除了循环，使它更紧凑，更易于阅读，更易于将来维护。

***注:*** *由于 reduce 的函数被很好地定义，代码更容易阅读，因此，看到 reduce 你就已经知道它应该做什么了。不像 loop，需要检查每一行才能了解循环在做什么。还要注意，在这种情况下使用 reduce over for-loop 不会显著提高性能。*

你可以在这里阅读更多关于 reduce [的内容。这是我迄今为止发现的对 reduce 最好的解释之一。](https://levelup.gitconnected.com/one-reduce-to-rule-them-all-504e1b790a83)

# **2。可组合性**

![](img/5c9337e708a7c4a03f176040be9601af.png)

[Composability is chain-like](https://pixabay.com/photos/chain-stainless-steel-metal-iron-4049725/)

例如，JavaScript array 类提供的函数 map、reduce 和 filter 是通用的，并且支持可组合性。可组合性简单地说就是，你可以在一个函数中做一件事，然后将输出传递给下一个函数，再传递给下一个函数以获得最终输出。这就像链接多个循环，但更漂亮。

让我们举一个例子:你应该在你的 web 应用程序中创建一个特性。它返回销售额最高的销售人员的姓名。

```
var nameList = [
  {
    "name": "Alice", "role": "Accountant", "papers_sold": 0
  },
  {
    "name": "Bob", "role": "Sales", "papers_sold": 1000
  },
  {
    "name": "Charles", "role": "Accountant", "papers_sold": 0
  }
  {
    "name": "Dan", "role": "Sales", "papers_sold": 1200
  }
  {
    "name": "Emily", "role": "Sales", "papers_sold": 1600
  } 
]
```

首先我们需要把销售和会计分开。然后，我们需要找出售出论文数量最多的销售人员。

传统上，我们会使用 for 循环来遍历数组。制作一个只有销售人员的新阵列。然后我们检查一下，找到销售额最高的人。它最终看起来会比实际需要的更丑陋、更复杂。

然而，通过组合 filter 和 reduce，我们可以这样做

```
function bestRecordInDept(nameList, role){ 
  return nameList
      .filter(record => record.role === role)
      .reduce((acc, value) => { 
        ***// Replace with the greater value***  
        acc = acc.papers_sold > value.papers_sold ? value : acc; 
        return acc.name;                     
      }, {})
}
```

在这里，我们使用 filter 过滤掉只有 Sales 作为角色的记录，然后将数据减少到销售量最大的销售人员的姓名。在这里，我们能够在不修改原始数组的情况下构造 filter 和 reduce，这将我们带到下一点。

***注意:*** *实际上，对于这个特定的用例，我们将避免使用 filter，而只在 reduce 中使用 if 语句。这将通过过滤器为我们节省一次数组迭代。我们在这里使用 filter 只是作为可组合性的一个例子。关于可组合性更详细的例子，你可以看这里的*[](https://code.tutsplus.com/tutorials/how-to-use-map-filter-reduce-in-javascript--cms-26209)

# *3.不变*

*![](img/f969320cffc4b52a8a452fdc2b269d73.png)*

*[That’s a mutant](https://pixabay.com/photos/parrot-kitty-ara-cat-bird-animal-3762988/)*

*通常，通过使用循环，我们最终会修改我们正在循环的原始数组。这可能会导致难以跟踪的错误。如果不小心的话，通过在多个地方改变数组的内容，我们可能会导致一些严重的不希望的“特性”。*

*使用固有的 JavaScript 原型函数，如 map，我们消除了这种可能性。这是因为，map 从不修改原始数组。它总是返回一个新的数组。这使得您的原始数组不可变，从而防止了未来在这方面出现任何错误的可能性。*

*比方说，你需要看看给每个人加薪 2%是什么样子。这意味着您需要保持原始记录不变。你只需要看到一些数据来为未来做准备。*

*如果您使用传统的循环来实现这一点，它可能看起来像这样:*

```
*var newNameList = nameList;
for (var index = 0; index < newNameList.length; index++){
  newNameList[index].salary = newNameList[index].salary*0.25;
}
console.log(newNameList);*
```

*问题就在这里。当您将一个数组分配给另一个数组时，它会通过引用创建一个副本。也就是说，当您修改 newNameList salary 时，NameList(您的原始数组)中的 salary 也会发生变化。这可不好。*

*一种方法是通过值创建数组的副本。可以通过在数组上使用 slice 来实现这一点，如下所示:name list . slice()；*

*然而，我们可以通过简单地使用这样的映射来避免整个问题:*

```
*console.log(nameList.map(x => x.salary += x.salary* 0.02));*
```

*干净多了，没有变异。:)*

# *性能问题*

*如果使用得当，传统循环与映射、减少和过滤之间的性能差异可以忽略不计。*

*有两个主要因素需要考虑:*

***迭代:** *与传统的循环相比，只要你使用 map、reduce 和 filter 来保持相同或更少的迭代次数，你应该是不错的。**

***数据的大小:** *对于非常大的数据，比如 100 万条数据记录，你最好使用一个 For 循环，必要时中间要有一个断点。在我的测试中，大约有 0.2-0.3 秒的微小差异，不会更多。当然，数据越大，差异就越显著。**

# ***那么什么时候应该使用循环呢？***

*大多数程序员习惯于考虑一个需要迭代的问题，并直接使用循环，因为这是我们最开始使用的，而且用得很多。这篇文章，最重要的是，在你思考问题的时候，努力让你远离这种思维定势。这并不意味着您需要完全丢弃循环。*

*我问自己两个简单的问题来决定是否需要一个循环:*

1.  *性能是否受到显著影响？*
2.  *我只是想让我的代码看起来更酷吗？*(我们都经历过)*目标是让未来的你读起来简单。过度设计只会使维护更加困难。*

*如果这两个问题的答案都是肯定的，那么我就去循环。*

# *结论*

*我希望有助于影响您将来编码和思考问题的方式。我很想听听你的想法。你同意吗？不同意？请在评论中告诉我。*

***一些有用的链接:**
[JavaScript 中的 Map 函数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
[JavaScript 中的 Reduce 函数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)
[JavaScript 中的 Filter 函数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)*

**更多内容看*[***plain English . io***](https://plainenglish.io/)*