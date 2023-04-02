# JavaScript 中的记忆化介绍及示例

> 原文：<https://javascript.plainenglish.io/intro-to-memoization-in-javascript-with-examples-e1a2b7f44575?source=collection_archive---------1----------------------->

![](img/185832cd3a831f1cd4b293cc818c85a9.png)

Photo by [Markus Spiske](https://www.pexels.com/@markusspiske)

在我的第一次现场编码面试中，我遇到了一个我从未见过的概念。我不记得这个问题的逐字逐句，但它大致是这样的:

*创建一个 memoize 函数，它能记住以前的输入，并将它们存储在缓存中，这样它就不必多次计算相同的输入。该函数将接受未指定数量的整数输入和一个 reducer 方法。参见:*

```
//Given reducer method: 
function add(a,b){
 return a+b
}//Create a method called memoize such that: 
const memoizeAdd = memoize(add);//then calling…
memoizeAdd(100,100); //returns 200
memoizeAdd(100); //returns 100
memoizeAdd(100,200) //returns 300
memoizeAdd(100,100) //returns 200 without computing
```

所以我在想… *sh*t.* 我以前从未使用过缓存，我该怎么回答这个问题呢！？然后我想起我听说过这个术语*记忆化*，甚至在我最近的【React 本地项目中使用了它。如果我没记错的话，我当时遇到了性能问题，在 StackOverflow 上搜索了一些可能的解决方案，发现[*react . memo*](https://reactjs.org/docs/react-api.html#reactmemo)*是一个有效的解决方案。不过，我一定是下意识地忽略了记忆实际上是如何工作的。*

*谢天谢地，这是一次风投面试，所以我花了几秒钟在谷歌上查了一下，“什么是 memoize 函数？”*(嗯……差不多吧)*。我找到了下面的[示例代码](https://www.freecodecamp.org/news/understanding-memoize-in-javascript-51d07d19430e/)，并将其作为参考来帮助回答问题的其余部分。*

```
*// a simple function to add something
const add = (n) => (n + 10);
add(9);
// a simple memoized function to add something
const memoizedAdd = () => {
  let cache = {};
  return (n) => {
    if (n in cache) {
      console.log('Fetching from cache');
      return cache[n];
    }
    else {
      console.log('Calculating result');
      let result = n + 10;
      cache[n] = result;
      return result;
    }
  }
}
// returned function from memoizedAdd
const newAdd = memoizedAdd();
console.log(newAdd(9)); // calculated
console.log(newAdd(9)); // cached*
```

*首先，让我们了解记忆化是做什么的。然后我们将检查上面显示的示例代码。最后，我们将看看它是如何帮助解决上述面试问题的。*

## *记忆有什么作用*

*下面是我发现的关于函数记忆的一个简单而准确的解释:*

*“记忆化是一种优化技术，在这种技术中，代价高昂的函数调用被缓存起来，这样下次用相同的参数调用函数时，结果可以立即返回”。—乔纳森·莱曼， [*JavaScript 函数记忆化*](http://inlehmansterms.net/2015/03/01/javascript-memoization/)*

****注意:*** *这种场景下不需要应用浏览器缓存。**

*我可能会这样详细说明:内存化通过将先前计算的结果存储在一个 JavaScript 对象(也称为缓存)中来帮助加速函数调用。换句话说，每次执行 memoize 方法时，都会发生以下两种情况之一:*

1.  ***如果输入之前被使用过，在缓存中找到它并立即返回存储的值，而不执行任何进一步的计算。***
2.  ***使用输入执行任何必要的计算，将结果存储在缓存中，返回结果。***

## *一个简单的记忆例子*

*为了进行演示，让我们构建一个简单的 memoize 函数，类似于上面显示的函数。*

*首先让我们用 ES6 定义我们的函数。作为一个参数，它将接受一个函数， *fn* ，用于计算。*

```
*const memoize = (fn) => {}*
```

*接下来，让我们声明一个初始缓存对象。*

```
*const memoize = (fn) => {
   let cache = {}
}*
```

*太好了。现在让我们实际返回一些东西。我们将首先实现可能性# 1—“*如果输入以前被使用过，在缓存中找到它，并立即返回存储的值，而不执行任何进一步的计算。”**

```
*const memoize = (fn) => {
   let cache = {}
   return (n) => {
      if (n in cache){
         return cache[n]
      }
}*
```

*我们来复习一下。首先， *memoize* 已经正式成为[高阶函数](https://medium.com/javascript-scene/higher-order-functions-composing-software-5365cf2cbe99#:~:text=A%20higher%20order%20function%20is,return%20a%20function%20as%20output.)，因为它将一个函数作为输入和/或返回一个函数作为输出。更详细地说，如果我们调用 *memoize* ，我们将得到另一个函数，该函数检查给定的参数 ***n*** 是否是 ***缓存*** 中的一个键，并将返回其相应的值。这有什么特别的？事实上，返回的函数在其作用域内有 ***缓存*** ，可以访问或添加属性！向前看，这可以证明是非常强大的。*

*现在，缓存对象将保持为空，因此让我们实现规则#2 来改变这种情况—“*使用输入来执行任何必要的计算，将结果存储在缓存中，返回结果。”**

```
*const memoize = (fn) => {
   let cache = {}
   return (n) => {
      if (n in cache){
         return cache[n]
      }else{
         let result = fn(n);
         cache[n] = result;
         return result;
      }
   }
}*
```

*厉害！现在，如果参数 ***n*** 没有存储在 ***缓存*** 中， *memoize* 将执行计算***【fn(n)***， ***结果*** 将存储在 ***缓存*** 中，如下:*

```
**/* Given n=5 and result=15, cache will contain the 
key:value pair of: */*"5" : 15*
```

*让我们看看它的实际效果。*

*首先，给定一个函数 *add10**

```
*const add10 = (n) => n + 10*
```

*我们可以像这样声明*

```
*const memoizeAdd10 = memoize(add10);*
```

*使用， *memoizeAdd10* ，我们可能会进行以下函数调用*

```
*memoizeAdd10(15); //returns 25
memoizeAdd10(20); //returns 30
memoizeAdd10(25); //returns 35*
```

*在这些调用之后， *memoizeAdd10* 的 ***缓存*** 将如下所示:*

```
*{
   "15" : 25,
   "20" : 30,
   "25" : 35
}*
```

*如果我们称之为*

```
*memoizeAdd10(15); //returns 25 without arithmetic computations*
```

*另一次，不是计算结果， *memoizeAdd10* 将只是潜入 ***缓存*** ，找到键“***15***”*并返回 ***25*** ，而不必执行任何计算。你可能会想，*“但这只是一个加法函数，几乎不会给我们的机器带来任何压力，谁在乎呢？”当然，但是当算法从简单的加法发展到递归运算时，例如，记忆化可以证明是一个巨大的优势。***

## **解决我们的面试问题**

**让我们运用目前所学的知识来解决文章开头提到的面试问题。我们可以使用上面定义的相同的 memoize 函数，只是做了一些调整:**

**在这个例子中，我们改变了 3 件事。让我们复习一下:**

1.  *****【n】***➡️***……args”(line 3)******—***返回函数现在接受未指定数量的参数，可以通过使用数组 *args* 或[*args*object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments)来访问这些参数。**
2.  *****"cacheKey "(第 4、5、6、9 行)—*** 我们声明了一个名为"*" cache key "*的变量，它代表了键的名称*(以前为" n")* ，该键将用于访问缓存或声明一个新的缓存属性。进行这种改变是为了跟踪多个输入。我们通过映射"***【args】***"数组并返回一串"***【n】***和一个" ***+*** "来形成*。比如调用 *memoizeAdd(10，20，30)* 的时候****cacheKey****会是*“10+20+30+”。******
3.  *****【fn(n)】***➡️***" args . reduce((ACC，curr) = > fn(acc，curr)，0)——***由于 *memoizeAdd* 可以接受任意未指定数量的参数，为了求所有参数之和我们可以使用[*array . prototype . reduce*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)**

***使用我们新翻新的 memoize 函数，在进行以下函数调用后***

```
***memoizeAdd(10, 20, 30, 40); //returns 100
memoizeAdd(1, 2, 3, 4); //returns 10
memoizeAdd(5, 10) //returns 15***
```

***我们的缓存看起来像这样:***

```
***{
   "10+20+30+40+" : 100,
   "1+2+3+4+" : 10,
   "5+10+" : 15
}***
```

***如果我们再打电话:***

```
***memoizeAdd(1, 2, 3, 4); //returns 10 without arithmetic computations***
```

***我们的函数 *memoizeAdd* 将返回 10，不需要算术运算。最终，随着更复杂的功能“*”这种技术被证明是极其有用的。然而，重要的是要记住什么时候不使用它。****

## ***结论***

***我们刚刚展示了 JavaScript 中函数记忆化的强大功能。我希望你喜欢阅读，并会考虑在你的下一个项目中使用这种方法！谢谢！***