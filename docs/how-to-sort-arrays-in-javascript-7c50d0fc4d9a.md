# 如何在 JavaScript 中对数组排序

> 原文：<https://javascript.plainenglish.io/how-to-sort-arrays-in-javascript-7c50d0fc4d9a?source=collection_archive---------20----------------------->

## 字符串、数字和对象的排序列表。构建一个通用的比较函数。

![](img/afeccd1254ab27e1d38a12471495eb73.png)

在本文中，我们将了解如何对数字、字符串和对象的数组进行排序。最后，我们将尝试创建一个通用函数，它可以根据任意数量的属性对数据对象列表进行排序。

# 对字符串数组排序

`sort`方法将元素转换成字符串，并按字母顺序排序。当然，这对于排序字符串非常有用。

```
const fruits = ["Lemon", "Apple", "Mango"];
fruits.sort()console.log(fruits);
//["Apple", "Lemon", "Mango"]
```

记住`sort`方法是不纯的。它改变输入数组。

# 对数字数组排序

如前所述,`sort`在排序之前将值转换成字符串。这对我们排序字符串很有用，但对数字不起作用。看看下面的例子。

```
const numbers = [-1, -3, -2];
console.log(numbers.sort());
//[-1, -2, -3]
```

当数字按字符串排序时，`'-2'`在`'-1'`之后。

然而，我们可以通过提供一个比较函数来解决这个问题。

```
function asc(a, b){
  if(a > b) return 1;
  if(a < b) return -1;
  return 0;
}const numbers = [-1, -3, -2];
console.log(numbers.sort(asc));
//[-3, -2, -1]
```

比较函数定义了排序顺序。它取两个元素`a`和`b`，如果`a`在`b`之前，则返回`-1`，如果`b`在`a`之后，则返回`1`，如果顺序保持不变，则返回`0`。

`asc`是比较功能。

这是前面 compare 函数的一个简短版本，可以用来对数字进行升序排序。

```
function asc(a, b){
  return a - b;
}
```

# 排序对象数组

接下来，让我们看看如何对对象数组进行排序。

考虑购物清单。对于列表中的每个水果，我们都有`name`和`quantity`属性。

```
const shoppingList = [
 {name: 'Lemon', quantity: 3},
 {name: 'Apple', quantity: 2},
 {name: 'Mango', quantity: 1}
]
```

下面是我们如何根据水果名称对列表进行排序。

```
shoppingList.sort(function (objA, objB) {
  const a = objA.name;
  const b = objB.name;
  return a === b 
    ? 0 
    : a > b 
      ? 1 
      : -1;
});console.log(shoppingList);
//[
//{name: "Apple", quantity: 2},
//{name: "Lemon", quantity: 3},
//{name: "Mango", quantity: 1}
//]
```

compare 函数从两个对象中获取名称，然后用它来决定返回的结果。

我们可以通过提取 compare 函数并给它一个揭示意图的名称来提高可读性。

```
function byName(objA, objB) {
  const a = objA.name;
  const b = objB.name;
  return a === b 
    ? 0 
    : a > b 
      ? 1 
      : -1;
}shoppingList.sort(byName);
```

# 创建通用比较函数

之前的比较函数`byName`只能按 name 属性排序。根据任何包含字符串或数字的属性进行排序将非常有用。

如果我们创建一个接受属性名并使用该属性返回比较函数的函数会怎么样？这是它可能的样子。

```
function by(propName){
  return function(objA, objB){
    ...
  }
}
```

`by`是返回另一个函数的函数。`by`是高阶函数。

下面是我们如何实现它。

```
function by(propName){
  return function(objA, objB){
    const a = objA[propName];
    const b = objB[propName];
    return a === b 
      ? 0 
      : a > b 
        ? 1 
        : -1;
  }
}shoppingList.sort(by("name"));
```

括号符号用于读取 sort 属性的值。然后基于这些值，返回升序的正确结果`-1`、`0`或`1`。

compare 函数适用于字符串和数字。下面是一个根据数量对列表进行排序的示例。

```
shoppingList.sort(by("quantity"));
//[
//{name: "Mango", quantity: 1},
//{name: "Apple", quantity: 2},
//{name: "Lemon", quantity: 3}
//]
```

# 按任意数量的属性排序

前面的比较函数适用于基于一个属性的排序，但是如果我们想要使用多个属性进行排序呢？

考虑下一个例子。

```
const shoppingList = [
 {name: 'Broccoli', quantity: 1, type:'Vegetables'},
 {name: 'Lemon', quantity: 2, type: 'Fruits'},
 {name: 'Apple', quantity: 2, type: 'Fruits'},
 {name: 'Orange', quantity: 1, type: 'Fruits'},
 {name: 'Mango', quantity: 1, type: 'Fruits'}
];
```

在这种情况下，我们有几个对象具有相同的`type`和`quantity`。

我们想先按`type`排序。如果两个元素有相同的`type`，那么我们将按`quantity`排序。如果两个元素具有相同的数量，那么我们将按照`name`对它们进行排序。

下面是一个可能的实现
`by`函数使用 rest 参数对所有属性进行排序。rest 参数是一个数组。

```
function by(...props){    
  return function(objA, objB){
    const propName = props[0];
    const otherProps = props.slice(1);

    const a = objA[propName];
    const b = objB[propName];

    return a === b 
      ?  otherProps.length
        ? by(...otherProps)(objA, objB)
        : 0
      : a > b 
        ? 1 
        : -1;
  }
}
```

事情是这样的。

`slice()`从`start`到`end` indexs 返回一部分现有数组的新副本。如果省略`end`，则`slice`提取到数组末尾，表示`arr.length`。

`props.slice(1)`返回包含除第一个值之外的所有当前值的新数组。

带有所有属性的数组中的第一个属性用于排序。当两个元素具有相同的值时，列表中的下一个属性用于排序。这种行为是通过对当前两个元素的剩余排序属性调用`by`函数实现的:`by(...otherProps)(objA, objB)`。当两个值相等，并且没有更多属性要排序时，返回`0`，因此顺序保持不变。

下面是结果。

```
shoppingList.sort(by("type", "quantity", "name"));
console.log(shoppingList);//[
//  {name: "Mango", quantity: 1, type: "Fruits"},
//  {name: "Orange", quantity: 1, type: "Fruits"}, 
//  {name: "Apple", quantity: 2, type: "Fruits"},
//  {name: "Lemon", quantity: 2, type: "Fruits"},
//  {name: "Broccoli", quantity: 1, type: "Vegetables"},
//]
```

# 结论

正如您所看到的，对字符串进行排序与`sort`方法的默认行为配合得很好，但是对于其他值类型，可能需要一个比较函数。您在本文中找到的比较函数可能对您在不同的项目中有用。感谢阅读。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)