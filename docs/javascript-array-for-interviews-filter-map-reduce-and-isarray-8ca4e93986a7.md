# 用于面试的 JavaScript 数组:过滤、映射、简化和数组

> 原文：<https://javascript.plainenglish.io/javascript-array-for-interviews-filter-map-reduce-and-isarray-8ca4e93986a7?source=collection_archive---------1----------------------->

![](img/7ea5780abf1af58087aabd745093652d.png)

Javascript

## 数组的内置备忘单

作为一名 JavaScript 开发人员，我们经常想要从数组中操作或提取不同的数据，JavaScript 提供了各种内置函数来减轻我们的任务。这些函数可以帮助我们改进代码结构，用更简单的方式回答数组相关的面试问题。

## 我们将研究以下数组函数:

1.  Array.isArray
2.  地图
3.  过滤器
4.  减少

# 伊萨雷

我们经常要检查变量是否是数组，有多种方法可以做到这一点，最常见的方法是使用 ***instanceof。***

```
let a = [1,1,2,42]
let b = { "name": "Manan" }
console.log(a instanceof Array) //true
console.log(b instanceof Array) //false
```

让我们用阵的方式来做吧:

```
let a = [1,1,2,42]
let b = { "name": "Manan" }
console.log(Array.isArray(a)) //true
console.log(Array.isArray(b)) //false
```

# 地图()

如果你是 JavaScript 的初学者，你可能到现在都没有使用过 map 函数，但是学习 map 函数将会对你有长远的帮助。

假设您有一个对象数组，每个对象包含一个键***【id】***，现在您想要一个包含所有 id 的数组。

解决方法之一是初始化一个空数组并运行一个 for 循环，然后将每个对象的 id 放入数组中。

```
let employees = [
    {
        "id": 11,
        "name":"Abhinav",
        "salary":75000
    },
    {
        "id": 2131,
        "name":"Raj",
        "salary":62000
    },
    {
        "id": 3012,
        "name":"Raj",
        "salary":32000
    }]
let idsArray = []
for(let i = 0; i< employees.length; i++){
   idsArray.push(employees[i].id)
}
console.log(idsArray) //[11,2131,3012]
```

让我们使用地图:

```
let employees = [
    {
        "id": 11,
        "name":"Abhinav",
        "salary":75000
    },
    {
        "id": 2131,
        "name":"Raj",
        "salary":62000
    },
    {
        "id": 3012,
        "name":"Raj",
        "salary":32000
    }]
let idsArray = employees.map(employee => employee.id)
console.log(idsArray) //[11,2131,3012]
```

# 过滤器()

顾名思义 filter 是一个可以帮助你过滤数组元素的函数，假设有一个包含***【salary】***的对象数组，现在你想得到一个工资大于 40000 的员工的数组。

```
let employees = [
    {
        "id": 11,
        "name":"Abhinav",
        "salary":75000
    },
    {
        "id": 2131,
        "name":"Gaurav",
        "salary":62000
    },
    {
        "id": 3012,
        "name":"Raj",
        "salary":32000
    }]
let salaryAbove40K = employees.filter(employee => employee.salary > 40000)
console.log(salaryAbove40K) //Array will contain objects whose salary is greater than 40000.
```

# 减少()

这个内置函数有点复杂，但是我们将通过下面的问题来理解它。
假设上面的数组中每个对象都包含关键字***“salary”。现在试着找出所有薪水的总和。一个通用的解决方案是用 0 初始化一个变量，然后为数组的每个元素运行循环*的*,然后将值添加到数组中。***

```
let employees = [
    {
        "id": 11,
        "name":"Abhinav",
        "salary":75000
    },
    {
        "id": 2131,
        "name":"Gaurav",
        "salary":62000
    },
    {
        "id": 3012,
        "name":"Raj",
        "salary":32000
    }]
let totalSalary = 0
for(let i = 0; i < employees.length ; i++){
   totalSalary = totalSalary + employees[i].salary
}
console.log(totalSalary) //169000
```

> 让我们用 reduce 来做吧

```
let employees = [
    {
        "id": 11,
        "name":"Abhinav",
        "salary":75000
    },
    {
        "id": 2131,
        "name":"Gaurav",
        "salary":62000
    },
    {
        "id": 3012,
        "name":"Raj",
        "salary":32000
    }]
let totalSalary = employees.reduce((a,employee)=> a + employee.salary, 0)
console.log(totalSalary) //169000
```

现在让我们考虑我们想要找出工资最高的雇员。

```
let employees = [
    {
        "id": 11,
        "name":"Abhinav",
        "salary":75000
    },
    {
        "id": 2131,
        "name":"Gaurav",
        "salary":62000
    },
    {
        "id": 3012,
        "name":"Raj",
        "salary":32000
    }]let employeeWithHighest = employees.reduce((a,employee)=> (a.salary || 0 ) > employee.salary ? a  : employee, {} )
console.log(employeeWithHighest) //Answer will the object of Abhinav
```

现在让我们试着理解 reduce 的第一个参数是一个回调函数，它有两个参数—***【a】***和 ***“雇员”。*** 到现在你可能已经猜到了“employee”是数组中的一个不同的元素，但是什么是“*？它是一个局部变量，在遍历数组时使用。我已经将***‘a’***初始化为空{}，这是 reduce 函数的第二个参数。*

*简而言之，reduce 函数初始化一个局部变量并遍历每个元素，对于每个元素，它都存储其对该局部变量的回答，一旦遍历完所有元素，就返回该局部变量的最终值。*

## *结论*

*有许多内置函数的备选库，但是了解内置函数有助于我们更好地理解 JavaScript。*

*我希望你已经发现这是有用的。感谢您的阅读。*

**如果你想了解更多关于内置函数的信息，你可以参考:*[*https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Global _ Objects/Array*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)*