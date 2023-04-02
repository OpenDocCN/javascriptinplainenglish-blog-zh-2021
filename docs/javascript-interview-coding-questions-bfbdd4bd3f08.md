# 基本的 JavaScript 面试编码问题

> 原文：<https://javascript.plainenglish.io/javascript-interview-coding-questions-bfbdd4bd3f08?source=collection_archive---------0----------------------->

![](img/ff9cbc950ca0fd9c9df5d0797205e1a2.png)

Photo by [Scott Graham](https://unsplash.com/@homajob?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 1)解释什么是回调函数，并举例说明。

**答案:**作为参数传递给另一个函数的函数称为`**callback** function`。这个回调函数将在某个操作完成后执行。

**代码:**

# 2)反转给定字符串的每个单词。

**示例:**

给定字符串— `Welcome to Hello World`

应该变成——`emocleW ot olleH dlroW`

**代码:**

# 3)写一些代码来检查一个对象是否是数组。

## **回答:**

`Array.isArray(object)`判断一个对象是否是数组。`Array.isArray`受 Chrome 5、Firefox 4.0、IE 9、Opera 10.5 和 Safari 5 支持

## 代码:

[](https://codechintan.com/how-to-get-started-with-mongo-db-atlas/) [## 如何入门 MongoDB Atlas？

### MongoDB 如何入门 MongoDB Atlas？“MongoDB 地图集”的云版本，用于创建和部署地图集…

codechintan.com](https://codechintan.com/how-to-get-started-with-mongo-db-atlas/) 

# JavaScript 中如何清空数组？

given Array-> arrayList =[' a '，' b '，' c '，' d '，' e '，' f ']；

# 答案-1:

```
arrayList = [];
```

当我们没有将这个数组引用到另一个变量时，上面的方法是很好的。

# 答案 1 中的问题:

# 答案-2:

```
arrayList.length = 0;
```

上面的代码将通过将现有数组的长度设置为`0`来清除该数组。这种清空数组的方式也更新了所有指向原始数组的引用变量。当您想要更新指向`arrayList`的所有其他引用变量时，这种清空数组的方式很有用。

# 答案-3:

```
arrayList.splice(0, arrayList.length);
```

这种清空数组的方式也将和答案 2 一样，这也将清空所有的引用。

# 答案-4:

```
while(arrayList.length) {
  arrayList.pop();
}
```

这种清空数组的方式也将和答案 2 一样，这也将清空所有的引用。但是不推荐这种方法，因为它是循环运行的。

# 5)如何检查一个数字是否是整数？

检验一个数是小数还是整数的一个非常简单的方法是看我们除以 1 时是否还有余数。

# 6)解决这个问题:

```
duplicate([1, 2, 3, 4, 5]); // Output: [1,2,3,4,5,1,2,3,4,5]
```

# 代码:

创建一个名为 duplicate()的函数，该函数将一个数组作为参数，并返回一个重复的数组。

# 7)编写一个“mul”函数，该函数应调用如下语法。

```
console.log(mul(2)(3)(4)); // output : 24
console.log(mul(4)(3)(4)); // output : 48
```

# 代码:

```
function mul (x) {
  return function (y) { // anonymous function
    return function (z) { // anonymous function
      return x * y * z;
    };
  };
}console.log(mul(2)(3)(4)); // output : 24
console.log(mul(4)(3)(4)); // output : 48
```

这里，`mul`函数接受第一个参数并返回一个匿名函数，它接受第二个参数，并返回一个匿名函数，它接受第三个参数并返回三个参数的乘积，这三个参数是按顺序传递的。

# JavaScript 中的闭包是什么？编写一个示例代码。

**答:**闭包是定义在另一个函数内部的函数。闭包函数是内部函数，父函数是外部函数。此外，闭包函数可以访问父函数作用域中定义的变量，因为闭包函数在父函数内部。

闭包函数可以访问三个范围内的变量:

*   变量在其自身范围内声明
*   父函数作用域中声明的变量
*   在全局命名空间中声明的变量

**说明** : `innerFunction`是定义在`outerFunction`内部的闭包函数，可以访问所有在 outerFunction 作用域声明和定义的变量。此外，闭包函数可以访问在`global namespace`中声明的变量。

上述代码的输出将是:

```
"outerArg = 4
outerFuncVar = x
innerArg = 3
innerFuncVar = y
globalVar = abc"
```

# 9)解决这个问题:

```
var addSeven = createBase(7);
addSeven(10); // output : 17
addSeven(21); // output : 28
```

# 代码:

您可以创建一个闭包来保存传递给函数`createBase`的值，即使在内部函数返回之后。被返回的内部函数是在外部函数中创建的，使它成为一个闭包，它可以访问外部函数中的变量，在本例中，变量是`baseNumber`。

```
function createBase(baseNumber) {
  return function(N) {
    // we are referencing baseNumber here even though it was declared
    // outside of this function. Closures allow us to do this in JavaScript
    return baseNumber + N;
  }
}var addSix = createBase(7);
console.log(addSix(10)); // output : 17
console.log(addSix(21)); // output : 28
```

# 10) FizzBuzz 挑战

编写一个 for 循环，迭代到`100`，同时以`3`的倍数输出 **"fizz"** ，以`5`的倍数输出 **"buzz"** ，以`3`和`5`的倍数输出 **"fizzbuzz"** 。

# 代码:

# 11)给定两个字符串，如果它们是彼此的变位词，则返回 true。

例如:`Mary`是`Army`的变位词

**阅读完整答案:**[https://codechintan . com/JavaScript-coding-questions-for-interview](https://blog.codechintan.com/javascript-coding-questions-for-interview)

# 12)使用闭包创建私有计数器。

**答:**闭包——是指我们在外部函数中创建一个函数。闭包允许我们更新私有变量，但是如果不使用帮助函数，这个变量就不能从函数外部访问。

**阅读完整答案:**[https://codechintan . com/JavaScript-coding-questions-for-interview](https://codechintan.com/javascript-coding-questions-for-interview)

# 13)假值和真值的列表，强制为布尔值。

**回答:**

# “假”值列表:

*   `""`(空字符串)
*   `0`、`-0`、`NaN`(无效数字)
*   `null`，`undefined`
*   `false`

# “真”值列表:

*   `"hello world"`
*   `42`
*   `true`
*   `[ ]`、`[ 1, "2", 3 ]`(数组)
*   `{ }`、`{ a: 42 }`(对象)
*   `function foo() { .. }`(功能)

# 14)解决这个问题:

**代码:**

```
(function() {
  var a = b = 5;
})();console.log(b);
```

**阅读完整答案:**[https://codechintan . com/JavaScript-coding-questions-for-interview](https://blog.codechintan.com/javascript-coding-questions-for-interview)

# 15)解决这个问题:

```
multiply(5)(6);
```

**阅读完整答案:**[https://codechintan . com/JavaScript-coding-questions-for-interview](https://blog.codechintan.com/javascript-coding-questions-for-interview)

# 16.写代码解释' this '关键字？

**阅读完整答案:**[https://codechintan . com/JavaScript-coding-questions-for-interview](https://blog.codechintan.com/javascript-coding-questions-for-interview)

# 17.如何在 JavaScript 中创建私有变量？

**阅读完整答案:**[https://codechintan . com/JavaScript-coding-questions-for-interview](https://blog.codechintan.com/javascript-coding-questions-for-interview)

# 18)解释以下代码的输出:

```
var output = (function(x) {
  delete x;
  return x;
})(0);console.log(output);
```

**阅读完整答案:**[https://codechintan . com/JavaScript-coding-questions-for-interview](https://blog.codechintan.com/javascript-coding-questions-for-interview)

# 19)解释以下代码的输出:

```
var Employee = {
  company: 'abc'
}
var emp1 = Object.create(Employee);
delete emp1.company
console.log(emp1.company);
```

**阅读完整答案:**[https://codechintan . com/JavaScript-coding-questions-for-interview](https://blog.codechintan.com/javascript-coding-questions-for-interview)

# 20)为什么(0.1 + 0.2 === 0.3)不等于真？

```
0.1 + 0.2 === 0.3
```

**回答:**这将令人惊讶地输出`false`，因为在内部表示某些数字时存在浮点错误。`0.1 + 0.2`不会很好地出现在`0.3`中，但结果实际上是`0.30000000000000004`，因为计算机无法在内部表示正确的数字。解决这个问题的一个办法是在用十进制数做算术时对结果进行舍入。

```
// this is what not expecting!
**x = 0.1 + 0.2
0.30000000000000004**

// this will solve our problem
**y = Math.round(x * 100) / 100
0.3**
```

# 21)什么时候使用`bind`功能？

**答:**`bind()`方法创建了一个新函数，它的`this`关键字被设置为我们提供给新函数的值。

`bind`函数的一个很好的用途是当你有一个特定的函数，你想用一个特定的`this`值来调用它。然后可以使用`bind`将一个特定的对象传递给一个使用`this`引用的函数。

**示例代码**:

[](https://codechintan.com/how-to-get-started-with-mongo-db-atlas/) [## 如何入门 MongoDB Atlas？

### MongoDB 如何入门 MongoDB Atlas？“MongoDB 地图集”的云版本，用于创建和部署地图集…

codechintan.com](https://codechintan.com/how-to-get-started-with-mongo-db-atlas/) 

> 请在评论框中随意评论…如果我错过了什么，或者什么是不正确的，或者什么对你不起作用:)
> 
> 更多文章敬请关注:
> [https://medium.com/@AnkitMaheshwariIn](https://medium.com/@AnkitMaheshwariIn)

如果你不介意给它一些掌声👏 👏如果这篇文章有所帮助，我将不胜感激。:)帮别人找文章，这样才能帮到他们！

永远鼓掌…

![](img/2f4712882de180d90c9dcdb0cb91ae69.png)

*更多内容请看*[***plain English . io***](http://plainenglish.io/)

阅读更多👇

[https://codechintan . com/JavaScript-coding-questions-for-interview](https://codechintan.com/javascript-coding-questions-for-interview)