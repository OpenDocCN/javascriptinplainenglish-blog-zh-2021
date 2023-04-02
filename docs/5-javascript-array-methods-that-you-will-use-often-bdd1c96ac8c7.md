# 您将经常使用的 5 种 JavaScript 数组方法

> 原文：<https://javascript.plainenglish.io/5-javascript-array-methods-that-you-will-use-often-bdd1c96ac8c7?source=collection_archive---------19----------------------->

## 方便的 JavaScript 数组方法

![](img/3aa7297678bb37c0f5ba09fbf39b86b3.png)

Photo by [ThisisEngineering RAEng](https://unsplash.com/@thisisengineering?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在第一部分中，我们已经学习了从初始化到数组的创建、插入和删除的数组基础知识。

[](https://medium.com/dev-genius/a-practical-guide-to-array-in-javascript-d0acd16fb78d) [## JavaScript 数组实用指南

### 学习 JavaScript 数组中的关键方法

medium.com](https://medium.com/dev-genius/a-practical-guide-to-array-in-javascript-d0acd16fb78d) 

我们甚至在 Google 开发者工具中实践了数组的概念。因为我们知道实践的重要性及其在生活中的应用。

所以一定要读数组的第一部分，不要直接跳到第二部分。这将有助于你轻松地学习这个概念，并提高你编码的成功率。

那我们开始吧。

# 1.排序()

这是每个领域中最常用的方法之一。甚至一个普通人也用它来进行他们的活动。

顾名思义，它有助于排序数字，字母等。

## **有哪些应用？**

假设你有未排序的数据，想轻松排序。然后就可以用`.sort() method`。

例如:

```
let num = [2, 4, 3, 6, 0];
console.log(num.sort());//The ouput will be
[0, 2, 3, 4, 6]
```

当你打印初始数组时。

```
console.log(num);//The output will be 
[0, 2, 3, 4, 6]
```

因此。sort()方法将改变初始数组。

# 2.切片()

你知道吗:你在推特上只能发 280 个字符。为此，我们可以使用。slice 方法将 tweets 剪切成 280 个字符并打印出来。

## 它的应用有哪些？

它只是剪切数组或生成数组的切片。

例如:

```
let num =  [1, 2, 3, 4, 5];
console.log(num.slice(0,2));//The output will be
[1, 2]
```

简单来说。slice(0，2)表示从索引 0 到 2 对数组进行切片，不计算第二个索引。

当你打印初始数组时。

```
console.log(num);//The output will be 
[1, 2, 3, 4, 5]
```

因此。slice()方法不会改变初始数组。

# 3.for 循环

迭代是几乎每种编程语言都使用的过程。这是一个访问数组中包含的每一项的简单过程。

迭代数组最常用的方法之一是使用 for 循环。

for 循环的基本语法是`for(variable; condition; modification).`

## **它的应用是什么？**

假设我们有国家的数据，我们想把它存储在一个变量中。

然后我们用一个数组。

但是我们想查看每一个项目。所以我们会使用`for loop`。

让我们举个例子:

```
let countries = [“USA”, “India”, “England”];for( var i=0; i<=countries.length; i++){
console.log(countries[i]);
} //The Output will be
USA
India
England
```

这里我们定义了一个名为 countries 的变量数组。然后我们应用了一个`for loop`。

在 for 循环中，我们定义了一个等于 0 的变量`i`。然后我们将循环迭代到`countries.length-1`。最后，在我们打印输出后，每次增加`i`。

```
for( var i=0; i<=countries.length; i++)
```

在 for 循环中，我们逐个迭代国家元素。使用`console.log(countries[i]);`。

> 额外材料:
> 
> 永远不要使用无限 for 循环。这可能会给你带来几个问题。无限循环就是不终止的循环实例。

# 4.地图()

这是 JavaScript 和 Web 开发中最常用的方法之一。我不知道 Vue.js，Angular 但是 React 开发者大多用`.map() method`

它类似于 for 循环，只是它创建了一个新数组。我们也可以通过定义不同的方法来创建一个新的数组。

## **有哪些应用？**

假设我们有一个完整的数字数据集，我们想把它乘以 10。

我们要做什么？

访问单个元素。然后为每个元素创建一个新变量并乘以 10。

不，我们不会那么做。

我们将简单地使用。map()方法。

例如:

```
var num = [1, 2, 3, 4, 5];
var newarray = num.map((number) => number * 10);
console.log(newarray);//The output will be
[10, 20, 30, 40, 50]
```

这里，我们定义了一个名为`const num = [1, 2, 3, 4, 5];`的数组。

然后，我们通过映射每个`num`元素并将其乘以 10 来定义一个新数组。

许多人可能会发现不同的语法，如`(number) => number * 10`。[是 JSX](/a-beginners-guide-to-jsx-in-react-native-c50b4037440b) 。

# 5.过滤器()

基于特定条件创建新数组。简单来说，`.filter()` `method`根据应用的条件创建一个新的数组(过滤数组)。

## **有哪些应用？**

假设我们由大量数据组成。我们想知道孩子的数量和他们的年龄。

所以我们可以用。filter()方法。

例如:

```
var age = [12, 34, 65, 1, 55, 33, 8]; 
var childAge = age.filter( age => age < 18 );
console.log(childAge);// The Output will be
[12, 1, 8]
```

这里我们定义了一个数组为`var age = [12, 34, 65, 1, 55, 33, 8];`。

然后我们编写代码根据条件过滤年龄。最后打印过滤后的数组。

# 结论

拍拍自己的背，你已经学会了各种数组方法。

学习是困难的，但是你已经从中学到了一些东西。

恭喜你。

现在实施吧。

谢了。