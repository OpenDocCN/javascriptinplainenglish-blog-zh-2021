# 你应该知道的 8 种 JavaScript 数组方法

> 原文：<https://javascript.plainenglish.io/8-javascript-array-methods-you-should-know-81947c9e46de?source=collection_archive---------17----------------------->

## JavaScript 中的数组方法你需要用例子来了解。

![](img/4b9b40a25b8b345960793dc5b105f3bb.png)

Photo by [Marcus Urbenz](https://unsplash.com/@marcusurbenz?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

数组几乎是任何编程语言不可或缺的一部分。理解数组对于揭示编程的概念是非常重要的。

根据 [Wikipedia](https://en.wikipedia.org/wiki/Array_data_structure) 的说法，数组可以定义为由元素集合组成的数据结构，每个元素至少由一个数组索引或键标识。存储数组，使得每个元素的位置可以通过数学公式从其索引元组中计算出来。

在本文中，我们将研究 JavaScript 数组方法以及如何使用它们。

简而言之，数组只是一个变量，能够在给定时间保存多个值。

还要注意的是，几乎所有主流浏览器都支持这些数组方法。

## **地图()方法**

map()方法是一个数组方法，它通过对父数组中的每个元素调用函数来创建数组。

此方法不会对没有值的数组元素执行函数。

map()数组方法的行为就像一个纯函数，不会改变原始数组。

**举例:**

```
const users = [
{name:’John’, age:33},
{name:’Philip’, age:40},
{name:’Carl’, age:30},
{name:’Frank’, age:27},
{name:’Florin’, age:25},
{name:’Debby’, age:21},
{name:’Liam’, age:26}]
const userAge=users.map((user)=>{
return user.name
})console.log(userAge)
```

这将返回给定数组中的所有名字

## **过滤()方法**

filter() array 方法返回一个给定的数组，该数组传递来自原始数组的给定计算。在过滤器内部，我们提供了如下所示的函数。

filter()函数不能在没有值的数组元素中使用。

filter()函数不会改变原始数组，因此它的行为就像一个纯函数。

**举例:**

```
const users = [
{name:’John’, age:33},
{name:’Philip’, age:40},
{name:’Carl’, age:30},
{name:’Frank’, age:27},
{name:’Florin’, age:25},
{name:’Debby’, age:21},
{name:’Liam’, age:26}]const filterUsers = users.filter((user)=>{
return user.age <=27
})console.log(filterUsers)
```

## **find()方法**

find() array 方法用于在数组中查找给定的对象。

此方法返回通过给定语句测试的第一个元素的值。

该方法对数组中的每个元素执行一次给定的函数。

find()方法不会改变提供的原始数组。

**示例:**

```
const users = [
{name:’John’, age:33},
{name:’Philip’, age:40},
{name:’Carl’, age:30},
{name:’Frank’, age:27},
{name:’Florin’, age:25},
{name:’Debby’, age:21},
{name:’Liam’, age:26}]const findUser= users.find((user)=>{
return user.name === ‘Debby’
})console.log(findUser)
```

## **forEach()方法**

forEach()数组方法用于为数组中的每个元素调用特定的函数。

**例如:**

```
const users = [
{name:’John’, age:33},
{name:’Philip’, age:40},
{name:’Carl’, age:30},
{name:’Frank’, age:27},
{name:’Florin’, age:25},
{name:’Debby’, age:21},
{name:’Liam’, age:26}]users.forEach((user)=>{
console.log(user.name)
})
```

该函数将返回给定数组中的所有名字。forEach()方法使得在大多数情况下使用数组变得非常容易。

## **某种()方法**

some() array 方法用于检查数组中给定的一组元素是否通过了特定的测试。

some()数组方法的行为就像一个纯函数。

如果它传递值，它将返回 true(并且不检查剩余的值)，否则，它将返回 false。

**例子:**

```
const users = [
{name:’John’, age:33},
{name:’Philip’, age:40},
{name:’Carl’, age:30},
{name:’Frank’, age:27},
{name:’Florin’, age:25},
{name:’Debby’, age:21},
{name:’Liam’, age:26}]const midUsers = users.some((user)=>{
return user.name <= 27
})console.log(midUsers)
```

## **每()方法**

every()方法执行并检查给定数组中的所有元素是否都通过了提供的测试。

它的行为就像一个纯函数，不改变原始数组。

**举例:**

```
const users = [
{name:’John’, age:33},
{name:’Philip’, age:40},
{name:’Carl’, age:30},
{name:’Frank’, age:27},
{name:’Florin’, age:25},
{name:’Debby’, age:21},
{name:’Liam’, age:26}]
const everyUsers = users.every((user)=>{
return user.name <= 25
})console.log(everyUsers)
```

## **减少()方法**

顾名思义，它将原始数组简化为单个对值，并对每个给定的值执行给定的函数。

**举例:**

```
const users = [
{name:’John’, age:33},
{name:’Philip’, age:40},
{name:’Carl’, age:30},
{name:’Frank’, age:27},
{name:’Florin’, age:25},
{name:’Debby’, age:21},
{name:’Liam’, age:26}]const totalAge= users.reduce((curr, user)=>{
return user.age + curr
}, 0)console.log(totalAge)
```

## **包含()方法**

includes()数组方法检查数组中是否包含给定的元素。

**例子:**

```
const ages = [19,56,45,54,30,32,21,33,21,18,23,23]const hasTwentyThree=ages.includes(23)
```

如果给定的测试通过，它将返回 true，否则，它将返回 false。

## **最终想法**

如果你喜欢读这篇文章，并且认为其他人也会喜欢，不要犹豫，分享它。

## **更多阅读量**

[](/vue-js-best-practices-you-should-adopt-3f3b3a8abace) [## Vue.js 您应该采用的最佳实践

### 使用 Vue.js 时的最佳实践

javascript.plainenglish.io](/vue-js-best-practices-you-should-adopt-3f3b3a8abace) [](/what-i-learned-while-building-my-portfolio-as-a-developer-26a20873517b) [## 作为一名开发人员，我在构建投资组合时学到了什么

### 你也可以从中学习。

javascript.plainenglish.io](/what-i-learned-while-building-my-portfolio-as-a-developer-26a20873517b) 

*更多内容看* [***说白了. io***](http://plainenglish.io/)