# JavaScript 中的高阶函数

> 原文：<https://javascript.plainenglish.io/higher-order-functions-in-javascript-12116b5b0bb1?source=collection_archive---------5----------------------->

![](img/f7c76b5d08ac794b00c2aa2037d40a95.png)

作为一名 JavaScript 开发人员，您会经常使用高阶函数。因此，对这些功能有一个适当的理解是至关重要的。

目前我看到人们在发现`reduce()`技术时经常感到困惑，然而我已经详细地阐明了一切，所以试着一点一点地理解它，我确信你将能够理解一切。

# 什么是高阶函数？

简单来说，高阶函数就是那些以其他函数为自变量或者返回其他函数的函数。在高阶函数中作为参数传递的函数称为回调函数。

为什么要用高阶函数？

*   它们帮助我们编写干净简单的代码
*   因为代码是干净的，所以调试起来会更容易

现在 JavaScript 有了一些内置的高阶函数。你可能已经使用过它们，甚至没有意识到这一点。这些都是类似`(filter(), reduce(), sort(), forEach())`的功能。

# 过滤器()

filter 方法返回一个新的元素数组，该数组通过了回调函数提供的特定测试。由于`filter`采用回调函数，因此`filter()`被称为高阶函数。现在传入`filter()`的回调函数被称为高阶函数。

*   `value of the element`(必选)
*   `index of the element`(可选)
*   `the array object`(可选)

```
let arr [1,2,3,4,5]; const resultant Array = arr.filter((element ) => {
    return element > 3; 
})console.log(resultantArray); // [4, 5]
```

在上面的例子中，所发生的是`arr`数组的元素被一个接一个地传递到`filter()`回调方法中，并且它们被测试用于特定的测试`element > 3`，那些通过测试的元素被推入`resultantArray`，这就是为什么输出是[4，5]，因为 4 和 5 是唯一通过测试的元素。

`element argument`正在逐个获取`arr`数组中元素的值，它将首先变为 1，然后它将测试`1>3`如果为真，1 将被推入结果数组，如果为假，它将被跳过到下一个元素。

示例:-

```
// filter age that is less than 18const ageArray = [10, 12, 35, 55, 40, 32, 15]; const filterAgeArray = ageArray.filter((age)=> {
    return age < 18; >
}); console.log(filterAgeArray); 
// [10, 12, 15]------------// /filter positive numbersconst numArray = [-2, 1, 50, 20, -47, -40]; const positiveArray = numArray.filter((num) => {
    return num > 0; 
}); console.log(positiveArray);
// [1, 50, 20]------------// filter names that contains `sh` in itconst namesArray = ["samuel", "rahul", "harsh", "hitesh"]; const filterNameArray = namesArray.filter((name) =>{
    return name.includes("sh"); 
}); console.log(filterNameArray); 
// ["harsh", "hitesh"]
```

# 地图()

顾名思义，`map()`方法用于将现有数组的值映射到新值，并将新值推送到新数组，然后返回新数组。现在，`map()`也采用回调函数，因此它被称为高阶函数。

传递给`map()`方法的回调函数有三个参数:-

*   `values of the element`(必需)
*   `index of the element`(可选)
*   `the array object`(可选)

```
const numArray = [1, 5, 3, 6, 4, 7]; const increasedArray = numArray.map((element) => {
    return element + 1; 
}); console.log(increasedArray);
[2, 6, 4, 7, 5, 8]
```

就像在`filter()`中一样，numArray 的元素将被一个接一个地传递给`map()`回调函数(作为元素参数),它们将被映射到一个新的值`element + 1`,然后它们将被推入`increasedArray`。

首先，1 将获得一个作为元素参数的传递，它将获得到新值`element + 1`的映射，这样 1 + 1(因为这里元素是 1)和 2 将被推入`increasedArray`中，以此类推，得到 5、3、6、4、7。

示例:-

```
// exponentiate every number on an arrayconst numArray = [2, 3, 4, 5, 15]; const poweredArray = numArray.map((number) => {
    return number * number; 
}); console.log(poweredArray); 
// [4, 9 ,16, 25, 144, 225]// extract the marks of studentconst studentsArray = [
    {
        name: "Rahul", 
        marks: 45, 
    }, 
    {
        name: "Samuel", 
        marks: 85, 
    }, 
    {
        name: "Chris", 
        marks: 25, 
    },
]; const ScoreArray = studentsArray.map((student) => {
    return student.marks; 
}); console.log(scoreArray); 
// [45, 85, 25]
```

# 减少()

`reduce()`方法用于将数组简化为单个值，就像`filter()`和`map()`一样，`reduce()`也将回调函数作为参数，因此它被称为高阶函数。酪`reduce()`除了回调函数之外还多了一个参数，那就是`initialValue`。同样，像`filter()`和`map()`一样，传入`reduce()`的回调函数接受一些参数，但传入 reduce 的回调函数接受 4 个参数，而不是 3 个。

*   `total`(必填)
*   `value of the elements`(必需)
*   `index of the element`(可选)
*   `the array object`(可选)

```
// A basic example reduce()const numArray = [1, 2, 3, 4, 5]; const sum = numArray.reduce((total, num) => {
    return total + num; 
}); console.log(sum);
```

让我们首先理解什么是 total 参数:- Total 参数是由`reduce()`函数返回的前一个值，现在当`reduce()`第一次运行时，将没有前一个返回值，因此`total argument`第一次等于 initialValue(还记得我们传递给`reduce()`的第二个参数)。

在我们的例子中，我们还没有使用 initialValue，所以当我们不传递 initialValue 时，reduce()方法跳过 numArray 的第一个元素，成为 total 参数的值。

在我们的例子中，我们没有传递 initialValue，所以 numArray 的第一个元素使得`1`将成为 total 参数的值，`numArray`的第二个元素将作为 num 参数传递，reduce 将返回`total + num`，使得`1+2 = 3`，3 将成为 total 的新值，现在来自`numArray`的第三个元素将作为 num 参数传递到`reduce()`回调中，reduce 将再次返回 total + num，即 3 + 3 = 6，6 将成为 total 的新值，依此类推。

(这个解释有点强硬和混乱。如果你试着循序渐进地学习，你会掌握的。

## 初始值参数

**initialValue** 顾名思义，是 total 参数的初始值，因为我们知道当`reduce()`第一次运行时，没有先前的返回值，因此来自现有数组的第一个元素(在我们的例子中是 numArray)成为 total 参数的值。所以不那么做，我们可以给 total 参数一个初值(记住 initial value 会是 total 参数的初值，total 参数后面会变成 reduce()之前的返回值)。

**注意:-** 当您使用 **initialValue** 参数时， **numArray** 不会跳过它的第一个元素，因此每个元素都会被传递到`reduce()`回调中。

具有初始值的 reduce()的语法:-

```
const resultantArray = existingArray.reduce((total,element,index.array)=> {
    // return something
}, initialValue);
```

感谢您的阅读！⚡

*更多内容请看*[*plain English . io*](http://plainenglish.io/)