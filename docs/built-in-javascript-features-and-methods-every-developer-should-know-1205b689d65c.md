# 每个开发人员都应该知道的 JavaScript 特性

> 原文：<https://javascript.plainenglish.io/built-in-javascript-features-and-methods-every-developer-should-know-1205b689d65c?source=collection_archive---------28----------------------->

*为你的下一个 JavaScript 项目使用这些提示和技巧*

![](img/265fcd224770b669a8541963c4d5ef31.png)

在 JavaScript 诞生之前，网页只是静态的，缺乏动态行为的能力。然而，在 1995 年，网景公司的人决定解决这个问题，并开始在他们专有的网络浏览器中添加一种脚本语言。相反，他们想出了一种全新的编程语言，我们现在称之为 JavaScript。

今天，超过 97%的网站使用 JS 作为他们的客户端编程语言，它可以说是现存的最流行的编程语言。自从 1997 年成为 EMCA 标准以来，这种语言已经有了许多改进和更新；包括许多内置的特性和方法。虽然开发人员可能熟悉常用的操作符，如`.forEach()`、`.map()`、`.sort()`和递增/递减(`++` / `--`)操作符，但是有太多的这些功能有助于代码优化。

这里有几个是每个开发者都应该知道的。

## 逗号运算符

逗号运算符(`,`)从左到右计算其操作数，并返回最后一个操作数的值。它允许创建一个复合表达式，其中计算多个表达式，最终值是其成员表达式最右边的值。逗号操作符通常用于向一个`for`循环提供多个参数。

```
let num = 10num = (num--, num)
console.log(num)       *// expected output: 9*num = (20, 30)
console.log(num)       *// expected output: 30*let a, b, c
a = b = 3, c = 4
console.log(a)         *// expected output: 3 (left-most)*let x, y, zx = (y = 5, z = 6)
console.log(x)         *// expected output: 6 (right-most)*
```

## 一元加和求反运算符

一元加(`+`)和求反(`-`)运算符位于其操作数之前，并计算其操作数。加号(`+`)操作符试图将它的操作数转换成一个数字，如果它还不是的话。

```
+8               *// result: 8* +"8"             *// result: 8* +"-8"            *// result: -8* +"8.8"           *// result: 8.8* +"123e-4"        *// result: 0.0123* +true            *// result: 1* +false           *// result 0* +null            *// result: 0* +"Infinity"      *// result: Infinity* +"not a number"  *// result: NaN* +function(){}    *// result: NaN*
```

negation ( `-`)操作符做同样的事情，但是对结果求反。

```
-8               *// result: -8* -"8"             *// result: -8* -"-8"            *// result: 8* -"8.8"           *// result: -8.8* -"123e-4"        *// result: -0.0123* -true            *// result: -1* -false           *// result -0* -null            *// result: -0* -"Infinity"      *// result: -Infinity* -"not a number"  *// result: -NaN* -function(){}    *// result: -NaN*
```

## 三元运算符

当试图根据特定条件是否为真来执行代码块时，直觉是使用`if...else`语句。三元运算符也是如此，接受三个操作数；一个条件后跟一个`?`，如果条件为真则执行一个表达式，后跟一个`:`，如果条件为假则执行一个表达式。写出来的运算符是这样的:

条件`?`表达式真`:`表达式假

```
const age = 19let canDrink
    if (age >= 21) {
        canDrink = "yes"
    } else {
        canDrink = "no"
    }*// identical to the above if...else statement* canDrink = (age >= 21) ? "yes" : "no"console.log(canDrink) *// expected output: "no"*
```

使用三元运算符可以将几行代码压缩成一行。

## Switch 语句

虽然`if...else if...else`对于基于条件执行不同的动作来说非常好，但是如果有三个以上的条件，它很快就会变得混乱。在这些情况下，最好使用`switch`语句。

```
const expression = 'dog'switch (expression) {
    *//invoke the switch statement to evaluate an express
*    case 'cat':
        *//code to be executed when the result of the expression  
          matches 'cat'* console.log('The cat meows.');
        break;     
           *// break statement ensures that the program
              breaks out of switch once the matched statement is
              executed* case 'bird':
        console.log('The bird chirps.');
        break;
    case 'dog':
        console.log('The dog woofs.');
            *// expected output: "The dog woofs."* break;
    default:
        *// a default clause is executed if the value of the 
           expression doesn't match any of the cases* console.log(`There are no animals matching ${expression}`)
}
```

当使用一个`switch`语句时，表达式的值与每种情况下的值进行比较。如果匹配，则执行相关的代码块。如果不匹配，则执行默认代码块。

## For…Of 和 For…In 循环

`for...of`和`for...in`循环都是使用数字索引的标准`for`循环的有效替代。

`for...of` 循环是一种迭代可迭代对象的方法，包括字符串、数组、集合和其他类似数组的对象。它调用一个定制的迭代钩子，为对象的每个不同的属性值执行语句。

```
// iterating over a string
const iterableStr = 'hello'

for (value of iterableStr) {
  console.log(value)
}
*// expected output:
// "h"
// "e"
// "l"
// "l"
// "o"*// iterating over an array
const iterableArr = [5, 10, 15, 20]

for (value of iterableArr) {
  value += 1
  console.log(value)
}
*// expected output:
// 6
// 11
// 16
// 26*
```

`for..in`循环是一种迭代对象“可枚举”属性的方法，适用于所有具有这些属性的对象。

```
const obj = { a: 'red', b: 'orange', c: 'yellow'};for (property in obj) {
  console.log(`${property}: ${obj[property]}`);
}// expected output:
// "a: red"
// "b: orange"
// "c: yellow"
```

***注意:*** *虽然* `*for...in*` *循环可以用来使用索引对数组和字符串进行迭代，但不建议这样做。一般的经验是数组和字符串用* `*for...of*` *，对象用* `*for...in*` *。*

## Number.prototype.toFixed()和 Number.prototype.toPrecision()

`.toFixed()`和`.toPrecision()`都接受一个数字对象，并返回一个表示数字对象的字符串。

`.toFixed()`使用定点符号格式化数字。将一个数字传递给该方法，该数字表示小数点后出现的位数。

```
const numObj = 12345.6789
numObj.toFixed()       *// result:  '12346'* numObj.toFixed(1)      *// result:  '12345.7'* numObj.toFixed(6)      *// result:  '12345.678900', zeros are added*(1.23e+20).toFixed(2)  *// result:  '123000000000000000000.00'* (1.23e-10).toFixed(2)  *// result:  '0.00'* 2.34.toFixed(1)        *// result:  '2.3'* 2.35.toFixed(1)        *// result:  '2.4'* 2.55.toFixed(1)        *// result:  '2.5' *unexpected rounding behavior*
```

***注意:*** *有一些奇怪的情况下* `*toFixed()*` *会出现意外的舍入行为。*

`.toPrecision()`与`.toFixed()`功能相似，但将数字对象格式化为指定的数字精度。

```
let numObj = 1.234567
numObj.toPrecision()    *// result:  '1.234567'* numObj.toPrecision(5)   *// result:  '1.2345'* numObj.toPrecision(2)   *// result:  '1.2'* numObj.toPrecision(1)   *// result:  '1'*numObj = 0.000123
numObj.toPrecision()    *// result:  '0.000123'* numObj.toPrecision(5)   *// result:  '0.00012300'* numObj.toPrecision(2)   *// result:  '0.00012'* numObj.toPrecision(1)   *// result:  '0.0001'*
```

这两种方法通常用于金融和科学数据，以获得更高的准确性。

## 数学对象

`Math`是一个内置在 JavaScript 中的对象，它具有数学属性和方法。使用`Math.*property*` 语法可以访问八个数学常数。然而，有 35 个内置的静态方法。一些最常用的是`Math.ceil()`、`Math.floor()`、`Math.round()`、`Math.max()`、`Math.min()`、`Math.pow()`和`Math.sqrt()`。

`Math.ceil()`函数总是将一个数向上舍入到下一个最大的整数；而`Math.floor()`函数总是返回小于或等于给定数字的最大整数。`Math.round()`但是，使用更传统的舍入方法，舍入到最接近的整数。

```
Math.ceil(.85)       *// result: 1* Math.ceil(6)         *// result: 6* Math.ceil(4.004)     *// result: 5* Math.ceil(-8.005)    *// result: -8*Math.floor(.85)      *// result: 0* Math.floor(6)        *// result: 6* Math.floor(4.004)    *// result: 4* Math.floor(-8.005)   *// result: -9*Math.round(1.05)     *// result: 1* Math.round(1.5)      *// result: 2* Math.round(1.95)     *// result: 2* Math.round(-1.05)    *// result: -1* Math.round(-1.5)     *// result: -1* Math.round(-1.95)    *// result: -2*
```

`Math.max()`函数返回作为参数给出的最大数值。`Math.min()`反其道而行之，返回传入数字中的最小值。如果没有参数传递给任何一个函数，结果将是`NaN`。

```
Math.max(3, 5, 1)       *// result: 5* Math.min(3, 5, 1)       *// result: 1*Math.max(-1, -3, -2)    *// result: -1* Math.min(-1, -3, -2)    *// result: -3*const array1 = [1, 3, 2, 8]
Math.max(...array1)     *// result: 8* Math.min(...array1)     *// result: 1*Math.max()              *// result: NaN* Math.min()              *// result: NaN*
```

`Math.pow()`需要两个参数。第一个是基数，第二个是指数。它返回指数幂的底数。

```
Math.pow(7, 2)     *// result:  49* Math.pow(2, 10)    *// result:  1024* Math.pow(4, 0.5)   *// result:  2 (square root of 4)*Math.pow(8, 1/3)   *// result:  2 (cube root of 8)* Math.pow(2, 1/3)   *// result:  1.2599210498948732 (cube root of 2)*Math.pow(-4, 2)    *// result:  16 (squares are positive)* Math.pow(-4, 3)    *// result:  -64 (cubes can be negative)* Math.pow(-4, 0.5)  *// result:  NaN (negative numbers don't have a  
                      real square root)*
```

`Math.sqrt()`简单地返回传递给方法的数字的平方根。

```
Math.sqrt(9)      *// result:  3* Math.sqrt(2)      *// result:  1.414213562373095* Math.sqrt(1)      *// result:  1* Math.sqrt(0)      *// result:  0* Math.sqrt(-1)     *// result:  NaN* Math.sqrt(-0)     *// result:  -0*
```

## String.prototype.replace()

`.replace()`是一个带两个参数的字符串方法；一个模式和一个替代品。模式可以是子字符串或 RegExp，方法在字符串中搜索它。所有匹配都将被第二个参数替换。

```
const string = "Sally fed her dog vegetables. Her dog was happy."
console.log(string.replace("dog", "monkey"))
*// expected output: "Sally fed her monkey vegetables. Her monkey was 
   happy."*let regex = /dog/i
const newString = string.replace(regex, "son")
console.log(newString)
*// expected output: "Sally fed her son vegetables. Her son was
   happy."*
```

## String.prototype.localeCompare()

`.localeCompare()`方法返回一个数字，指示一个引用字符串在排序顺序中是在给定字符串之前、之后还是相同。这在按字母顺序对字符串进行排序时特别有用。

```
const arrayOfStrings = ['cat', 'dog', 'chicken', 'fish', 'bird']const sortedArr = arrayOfStrings.sort((a, b) => a.localeCompare(b))
console.log(sortedArr)
// *expected output: ['bird', 'cat', 'chicken', 'dog', 'fish']*
```

使用`.localeCompare()`，还可以选择包含`locales`和`options`参数。这些参数将改变方法的行为，并指定应该使用的语言和格式约定。

## String.prototype.slice()

`.slice()`方法从一个字符串创建一个子字符串，而不修改原始字符串。它可以接受一个或两个参数，指示原始字符串的开始和结束索引。如果只传入一个参数，子字符串将从该索引开始，一直延续到原始字符串的末尾。如果有两个参数，子字符串从起始索引开始提取字符，直到*，但不包括*结束索引。

另外，如果参数为负，则被视为`str.length + index`。(例如，如果开始索引是`-5`，则被视为`str.length - 5`。)如果结束索引参数在开始索引参数之前，则返回一个空字符串。

```
const str = "JavaScript"let substr = str.slice(3)
console.log(substr)        // *expected output: "aScript"*substr = str.slice(2,8)
console.log(substr)        // *expected output: "vaScri"*substr = str.slice(-3)
console.log(substr)        // *expected output: "ipt"*substr = str.slice(-7,-1)
console.log(substr)        // *expected output: "aScrip"*substr = str.slice(3, 1)
console.log(substr)        // *expected output: ""*substr = str.slice(-3, 1)
console.log(substr)        // *expected output: ""*
```

## Array.prototype.slice()

当在一个数组上调用`.slice()`时，它从原始数组返回一个元素的浅层副本。类似于`.slice()` string 方法，它也需要一个或两个参数，代表起始和结束索引。原始阵列不受影响。

```
const fruitsArr = ['Banana', 'Orange', 'Lemon', 'Apple', 'Mango']let newFruitsArr = fruitsArr.slice(3)
console.log(newFruitsArr) *// expected output: ['Apple', 'Mango']*newFruitsArr = fruitsArr.slice(1, 3)
console.log(newFruitsArr)
// *expected output: ['Orange', 'Lemon']*newFruitsArr = fruitsArr.slice(-4)
console.log(newFruitsArr)
// *expected output: ['Orange', 'Lemon', 'Apple', 'Mango']*newFruitsArr = fruitsArr.slice(-4,-2)
console.log(newFruitsArr)
// *expected output: ['Orange', 'Lemon', 'Apple']*newFruitsArr = fruitsArr.slice(4,2)
console.log(newFruitsArr)
// *expected output: []*
```

## Array.prototype.some()

`.some()`方法需要一个回调函数作为参数，并检查数组中是否至少有一个元素通过了由提供的函数实现的测试。如果数组中有符合条件的元素，则返回 true 否则返回 false。它不会修改数组。

```
const array = [1, 2, 3, 4, 5]*// checks whether an element is odd*
const odd = (element) => element % 2 !== 0console.log(array.some(odd))
*// expected output: true**// checks whether an element is greater than or equal to 10*
const tenOrMore = (element) => element >= 10console.log(array.some(tenOrMore))
*// expected output: false*
```

## Array.prototype.splice()添加元素

虽然`.splice()`是修改和缩短数组最常用的方法之一，但它也可以通过包含附加参数来添加元素。当使用`.splice()`移除元素时，只需要两个参数；第一个是开始更改数组的索引，第二个是指示要移除的元素数量的整数。但是，前两个参数后面的任何附加参数都是要添加到数组中的元素，从起始索引(第一个参数)开始。

```
let cars = ['Honda', 'Toyota', 'BMW', 'Mercedes', 'Ford']// *using only two parameters, remove two elements starting at index  
   2*
cars.splice(2,2)
console.log(cars)            
*// expected output: ['Honda', 'Toyota', 'Ford']**// remove 0 elements starting at index 1 and insert 'Chevy' and 
   'Volkswagon'* cars.splice(1,0,'Chevy','Volkswagen')
console.log(cars)
*// expected output after the array has been modified by the previous 
   splice: ['Honda', 'Chevy', 'Volkswagen', 'Toyota', 'Ford']*
```

## 数组. from()

`Array.from()`是一个静态方法，它从一个类似数组或可迭代的对象创建一个新的数组实例。当用两个参数调用时，第二个参数充当映射函数。

```
console.log(Array.from('foo'))
// expected output: ["f", "o", "o"]console.log(Array.from([1, 2, 3]))
// expected output: [1, 2, 3]console.log(Array.from([1, 2, 3], x => 2 * x))
// expected output: [2, 4, 6]
```

## object . prototype . hasownproperty()

可以在对象上调用`hasOwnProperty()`方法，并返回一个布尔值，指示该对象是否将指定的属性作为自己的属性。

```
const obj = { color: 'red', number: 4, language: "Spanish" }obj.hasOwnProperty('color')          * // result: true*
obj.hasOwnProperty('meal')            *// result: false*obj.drink = null
obj.hasOwnProperty('drink')          * // result: true*
```

此外，因为`Object`的所有后代都继承了`hasOwnProperty`方法，所以也可以在数组上调用它来检查索引是否存在。

## 对象.分配()

`Object.assign()`方法将一个或多个源对象的所有可枚举的和自己的属性复制到一个目标对象。它返回已被修改的目标对象。

```
const target = { a: 2, b: 6 }
const source = { b: 8, c: 9 }const returnedTarget = Object.assign(target, source)console.log(target)
// expected output: { a: 2, b: 8, c: 9}console.log(returnedTarget)
// expected output: { a: 2, b: 8, c: 9}
```

## Object.freeze()和 Object.seal()

方法冻结一个对象，防止它被改变。冻结对象可防止添加新特性，并防止删除或更改现有特性的值。任何这样做的尝试都将失败，要么无声地失败，要么抛出一个`TypeError`异常(最常见的，但不是唯一的，在严格模式下)。`.isFrozen()`方法可用于检查对象是否冻结。

```
const obj = { prop: 42 }console.log(Object.isFrozen(obj))
// expected output: falseObject.freeze(obj)obj.prop = 33;
// Throws an error in strict modeconsole.log(Object.isFrozen(obj))
// expected output: true
```

`Object.seal()`行为类似，但它允许更改现有属性，同时防止添加新属性和删除现有属性。`.isSealed()`方法可用于检查对象是否密封。

```
const obj = { prop: 42 }console.log(Object.isSealed(obj))
// expected output: falseObject.seal(obj)console.log(Object.isSealed(obj))
// expected output: trueobj.prop = 33        // the object's existing property is changeable
console.log(obj.prop)
// expected output: 33delete object1.property1      // cannot delete when sealed
console.log(obj.prop)
// expected output: 33
```

`Object.freeze()`和`Object.seal()`都是用来创建不可扩展的对象，但是 ***需要注意的是*** *对象一旦被冻结或者封存，就不能被撤销*。

# 结论

今天，JavaScript 的使用已经远远超出了其 web 浏览器的范围，并继续革新计算。无论您是这门语言的新手，还是已经使用 JS 多年的人，希望您能在下一个项目中实现这里分享的一些特性和方法。虽然可能要花一生的时间来完全探索 JavaScript，但好处是它似乎不会有任何进展。

*更多内容看* [***说白了. io***](http://plainenglish.io)