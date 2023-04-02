# 你应该知道的 10 个节省时间和精力的 JavaScript 技巧

> 原文：<https://javascript.plainenglish.io/10-javascript-tricks-you-should-know-to-save-time-and-effort-813379390881?source=collection_archive---------7----------------------->

JavaScript 是一种成熟的动态编程语言，可以增加网站的交互性。它是初学者友好的，并且提供了许多工具，如果使用正确的话，可以节省大量的精力和时间。这是你在使用 JavaScript 时应该知道的 10 个技巧。请继续阅读，获取一系列节省时间的建议。

![](img/8cc642643a3e8358c2e8ecda68e0cccb.png)

Photo by [Jexo](https://unsplash.com/@jexo?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

## 1.像专家一样记录控制台日志

调试代码时，通常会记录一个值来检查赋值的结果。虽然你可以像下面这样做，

```
console.log('name', name)
console.log('someOtherValue', someOtherValue)
console.log('etc', etc)
```

您可以使用对象析构来简化您的工作。

```
console.log({name, someOtherValue, etc})
```

## 2.对象简写属性

假设您已经初始化了变量 x 和 y 中的一些值，并且您想要创建一个具有属性 x 和 y 的对象。使用基本的文字语法，您将最终重复每个标识符

```
let x = 1, y = 2
const obj = {
   x: x,
   y: y
}
```

在 ES6 和更高版本中，您可以删除冒号和标识符的一个副本，最终得到更简单的代码:

```
let x = 1, y = 2
const obj = {
   x,
   y
}
obj.x + obj.y => 3
```

## 3.逻辑赋值运算符

你可能知道数学赋值操作符。它可以让你对一个变量执行一个数学运算。

```
let count = 1
count += 2 // 3
count -= 1 // 2
```

假设你想给变量赋值，如果变量的当前值是真的。

```
let obj = {}
obj['name'] && (obj['name'] = 'Joe') // {}
```

你可以用下面的线代替上面的线。请注意，如果属性不存在，它不会创建属性。

```
obj['name'] &&= 'Joe' // {}
obj['name'] = 'Joe' // assign property 'name' to obj {name: 'Joe'}
obj['name'] &&= 'Colin' // { name: 'Colin' }
```

你可以在这里阅读更多关于逻辑赋值操作符[的内容。](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_OR_assignment)

## **4。传播算子**

在 ES2018 和更高版本中，您可以使用“扩展运算符”将现有对象的属性拷贝到新对象中`...`在对象文字内部:

```
let x = { p: 1}
let y = { q: 2, r: 3}
let z  = {...x, ...y} // { p: 1, q: 2, r: 3}
```

在上面的代码中，x 和 y 的属性被展开到 z 中。三个点在其他 JavaScript 上下文中用于其他目的，但是对象文字是三个点导致一个对象插入另一个对象的唯一上下文。

另外，请注意，如果展开的对象中有重复的属性，则该属性的值将是最后一个值。

```
let user = { name: "Joe", city: "New York", age: "25" }
let updatedUser = { ...user, age: "26"} 
// { name: "Joe", city: "New York", age: "26" }
```

您也可以对数组使用此属性。

```
let arr1 = [2, 3, 4]
let arr2 = [5, ...arr1] // [5, 2, 3, 4]
```

## **5。自调用功能**

在 JavaScript 中，函数表达式可以自动调用。

```
(function() {
 // your code goes here
})();
```

自调用函数是一个匿名函数，它在被定义后就被直接调用。如果表达式后跟()，这些函数将自动执行。请注意，函数声明不能自行调用。

```
let sum = (function(a,b){
    var result = a+b;
    return result;
})(10,20)
// sum => 30
```

自调用函数的主要好处是变量范围。这些函数内部定义的变量在函数范围之外不可用。这可以防止全局名称空间被可能不再需要的变量和函数弄得乱七八糟。

## 6.将数字格式化为货币

JavaScript 提供了一种支持区分语言的数字格式的方法。

```
const number = 123456.789
let dollars = new Intl.NumberFormat('en-US', {
      style: 'currency',      
      currency: 'USD',    
}).format(number)
// $123,456.79
```

如果使用 API 时没有指定区域设置，则返回默认区域设置和默认选项中的格式化字符串。

```
const number = 1234
let dollars = new Intl.NumberFormat().format(number)
// will return number formatted with default locale
```

## **7。用===代替==**

尽管==和===完成了相似的事情，但是===对相等性进行了更严格的检查。==或者！=如果需要，执行自动类型转换。然而，当你使用三重相等时，它会检查操作数的类型和值(严格相等)以及引用值(引用相等)。

```
5 == '5' // true, type conversion from int to String
5 === '5' //falseconst user = { name: "Joe" }
const someNewUser = user
user === someNewUser // true, reference check
```

三重等于比较值和类型，可以认为比`==`更快。

## **8。交换变量**

我们都去过那里；我们在交换变量时使用了一个临时变量。但是在 JavaScript 中有一个更好更直观的方法……使用析构。

```
let x = 5, y = 4;
[ y, x ] = [ x, y ]
// y = 5, x = 4
```

## 9.使用长度清空数组或调整数组大小

在 JavaScript 中，您可以覆盖数组的 length 属性来调整大小或清空数组。

```
const array = [1, 2, 3, 4]
array.length = 0 // []array.length = 2 // [1, 2]
```

## 10.三元运算符(？)

这一点你们大多数人可能都知道。三元运算符可用于替换 if…else 语句。举个例子，

```
let x = 10;
if( x % 2 === 0 )
   console.log('Number is even.')
else
   console.log('Number is odd')
```

可以替换为

```
let x = 10;
x % 2 === 0 ? console.log('Number is even') : console.log('Number is odd.')
```

我希望你在读完这篇文章后学到了一些关于 JavaScript 的新东西。

如果你做了，给这篇文章一些爱。如果你在 JavaScript 中使用了任何技巧，请在评论中分享。:)

*更多内容请看*[***plain English . io***](http://plainenglish.io/)