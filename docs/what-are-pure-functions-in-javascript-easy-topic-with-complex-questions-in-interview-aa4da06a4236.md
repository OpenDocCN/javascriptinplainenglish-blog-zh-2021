# JavaScript 中的纯函数和不纯函数是什么？

> 原文：<https://javascript.plainenglish.io/what-are-pure-functions-in-javascript-easy-topic-with-complex-questions-in-interview-aa4da06a4236?source=collection_archive---------5----------------------->

![](img/8b141de0d63117c57cc47e791df90dac.png)

你们中的大多数人可能知道什么是纯函数，事实上最初我并没有打算写一篇关于这个主题的文章，因为它非常直接。但在一次采访中，有人问我纯函数的多种变体，我无法回答。所以我想写一个详细的解释来帮助观众。

## **什么是纯函数？**

简而言之，这些函数的输出严格依赖于传递的输入，并且没有副作用。例如:考虑下面的例子来计算正方形的面积。

```
function areaOfSquare(length, breadth){
    return length * breadth;
}
areaOfSquare(2,4); // output will be 8
```

无论你将相同的值传递给 **areaOfSquare** 函数多少次，输出都保持不变。**所以，我们可以断定纯函数是确定性的。**

现在你知道什么是不纯函数了，记住下面是它的定义。

## **什么是不纯函数？**

简而言之，不纯函数是那些输出不仅仅依赖于输入数据的函数。让我们考虑下面一个简单的例子。

```
function generateNumber(input){return input + Math.random();}
generateNumber(10)
```

在上面的 **generateNumber()** 函数中，返回值不依赖于输入，任何时候你调用相同编号的函数，输出都会不同。因此，我们可以断定**不纯函数是不确定的。**

在大多数面试中，面试官会知道你知道上述话题，所以他们会问一些小问题。

## **问题 1:拥有纯函数的优势是什么？**

1.  **我们可以避免副作用:**由于纯函数不修改任何全局状态或变量，所以纯函数内部不会有任何副作用。副作用越小，代码结构越好。
2.  **记忆化:**对于相同的输入，纯函数将总是返回相同的输出。因此，函数可以存储结果并在调用时返回，而不是一直计算输出。
3.  **更容易测试和调试:**因为输出是确定的，所以你总是可以预测输出并编写测试用例来测试功能。甚至调试代码也变得很容易，因为你不需要担心函数的行为会随着时间的推移而改变，它总是一样的。

## **问题二:console.log 是纯函数吗？**

现在你知道了纯函数的定义和例子，你能猜出 console.log(' ')是不是纯函数吗？

这里我们有两个方面:

**1。console.log(' ')是一个函数，它的返回值总是未定义的**，I **表示**

```
 let x = console.log('hello'); // This line will print hello
 console.log(x); // output will be undefined 
```

因此，console.log 函数总是返回 undefined，因此它是一个纯函数。

**2。如果你在一个纯函数里面有 console.log，那么这个函数还是纯函数吗？**

不，如果你在一个纯函数中使用 console.log，它会产生一些副作用，比如在函数范围之外向 console 打印值。所以，技术上低于功能是不纯的。

```
function areaOfSquare(length, breadth){
    console.log("Area is", length * breadth);
    return length * breadth;
}
areaOfSquare(2,4); // output will be 8
```

避免，在完成测试后在函数内部使用日志，这会使函数变得不纯。

## **问题 3:像滤波、映射这样的数组方法是纯函数吗？**

与上面的问题相比，这很容易，通过概念思考并猜测答案。为了给出上下文，过滤器和映射方法将迭代数组并返回新数组作为输出。

过滤器示例:

```
const words = ['spray', 'destruction'];
const result = words.filter(word => word.length > 6);
console.log(result); // Output will be ['destruction']
```

地图示例:

```
const array1 = [1, 4];
// pass a function to map
const map1 = array1.map(x => x * 2);
console.log(map1);
```

# 结论

如果您已经清楚地理解了这个概念，您的答案将是**是**。map 和 filter 方法都是纯的，无论您传递同一个数组和执行同一个任务多少次，输出都是相同的。

在面试中，你可能会被问到更棘手的问题，在这种情况下，你会想，如果你把一个输入传递给一个函数，你是否总是得到相同的输出？然后检查是否有副作用？如果否，则该函数是纯的，否则不是。

快乐阅读，在我的下一篇文章中找到你。

**同一作者更多文章:**

1.  [在 JavaScript 中，一切都是对象吗？](https://mevasanth.medium.com/how-everything-is-object-in-javascript-a4164d7e6a2d)
2.  [JavaScript 中的提升:访谈热点](https://mevasanth.medium.com/hoisting-in-javascript-hot-topic-for-interview-43b463a6a77?source=follow_footer---------0----------------------------)
3.  [JavaScript 记忆——面试热点](https://mevasanth.medium.com/memoization-in-javascript-hot-topic-for-interview-815475544ab0)

*多内容于* [***中***](http://plainenglish.io)