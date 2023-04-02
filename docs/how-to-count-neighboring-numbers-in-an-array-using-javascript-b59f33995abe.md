# 如何使用 JavaScript 计算数组中相邻的数字

> 原文：<https://javascript.plainenglish.io/how-to-count-neighboring-numbers-in-an-array-using-javascript-b59f33995abe?source=collection_archive---------17----------------------->

## 日常 JavaScript 技巧、窍门和最佳实践

## 使用 JavaScript 计算数组中相邻的数字

![](img/aabe6d0d6e7251d6ea8775069ba82514.png)

Photo by [Djim Loic](https://unsplash.com/@loic?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我总是喜欢像报纸这样能在较短时间内提供足够信息的东西。在这里，我为日常前端开发创建了一些技巧。

在这里，我将带来一篇新文章，介绍一些基于属性值对数组进行排序的方法。这些技巧可以成为你 2021 年 JavaScript 编码面试中的一块小石头。

*我知道小石头没什么区别，但如果我们有成千上万的石头，那就有区别了，为此我明天会带来新的石头。敬请关注。*

# 开始今天的话题吧。

## 使用 Reduce

"`**reduce()**`方法对数组的每个元素执行一个**缩减器**函数(你提供的)，产生一个输出值。"(来源: [Mozilla](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce) )

```
let data = [1, 1, 2, 2, 4, 4, 6, 6, 5, 1, 9, 2, 7, 7];//using reduce
let output = data.reduce((acc, element) => {
    if (acc.length && acc[acc.length - 1].key == element) {
        acc[acc.length - 1].count++;
    } else {
        acc.push({
            key: element,
            count: 1
        });
    }return acc;
}, []).map(element => `${element.key}:${element.count}`)
```

## 输出将如下所示

```
console.log(output);//*["1:2", "2:2", "4:2", "6:2", "5:1", "1:1", "9:1", "2:1", "7:2"]*
```

## 使用地图:

“`**map()**`方法**创建一个新数组**，其中填充了调用数组中每个元素的函数的结果”(Source: [Mozilla](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce) )

```
let output2 = (function groupNeighbors([first, ...rest], output = [], last) {
    last === first ? output[output.length - 1].push(first) : output.push([first]);
    return rest.length ? groupNeighbors(rest, output, first) : output;
})(data).map(x => x.length > 1 ? [x[0], x.length].join(':') : x[0]);
```

## 输出将如下所示

```
console.log(output2);//*["1:2", "2:2", "4:2", "6:2", 5, 1, 9, 2, "7:2"]*
```

# **延伸阅读:**

*更多内容看* [***说白了. io***](http://plainenglish.io)