# 你应该知道的 6 个强大的 JavaScript 对象方法

> 原文：<https://javascript.plainenglish.io/the-6-powerful-javascript-object-methods-that-you-should-know-b2a659ddf3b5?source=collection_archive---------7----------------------->

## 实用的 JavaScript 对象方法和实例

![](img/890a8fa759f329f1916c0e6f3cb5c226.png)

Photo by [Cottonbro](https://www.pexels.com/fr-fr/@cottonbro) from [Pexels](https://www.pexels.com/).

像任何其他编程语言一样，JavaScript 有自己的数据类型，比如数字、字符串、数组、对象等等。这些数据类型允许开发人员处理数据，并在语言中实现许多有用的东西。

对象在 JavaScript 中是一种非常重要的数据类型，它们有很多有用的内置方法，我们可以使用和访问这些方法，使我们作为开发人员使用对象变得更加容易。

这就是为什么在这篇文章中，我们将学习一些有用的对象方法，你应该知道在 JavaScript 中。让我们开始吧。

# 1.对象键

方法`Object.keys()`(O 大写)用于返回一个数组，该数组包含我们作为参数传递给它的特定对象的所有键。

让我们看看下面的例子:

```
const employee = {
  name: "James",
  age: 25,
  available: true
}//Print the keys in the console
console.log(**Object.keys(employee)**);
//output: ["name", "age", "available"]
```

正如你在上面的例子中看到的，我们得到了一个包含关键字的数组作为输出。现在，您可以使用任何其他数组方法来访问和遍历这些键。

因为对象没有 length 属性，所以您也可以使用`Object.keys()`来获取对象的长度。

下面是一个例子:

```
Object**.**keys(employee)**.length;** //3
```

# 2.对象冻结

方法`Object.freeze()`防止对象中的数据突变。所以您不能添加、更新或删除作为参数传递给`Object.freeze()`的对象的属性。

看看下面的例子:

```
const employee = {
  name: "James",
  age: 25,
  available: true
}//Freezing the object.
**Object.freeze(employee);**//updating and adding properties.
employee.name = "Brad";
employee.newProp = "Hard Worker";console.log(employee);
//Output: {name: "James", age: 25, available: true}
```

如您所见，即使我们更新了属性，对象也没有改变。

# 3.对象密封

方法`Object.seal()`和`Object.freeze()`有点类似。它阻止向对象添加新属性，但允许更改和更新现有属性。

```
const user = {
  name: "Alex",
  age: 23,
  isOnline: false
}//Using Object.seal()
**Object.seal(user);**//updating a property.
user.isOnline = true;//Adding a property.
user.active = false;console.log(user);
//output:{name: "Alex", age: 23, isOnline: true}
```

属性`isOnline`得到了更新，但是我们无法将属性`active`添加到对象中，因为我们使用了`Object.seal()`来阻止它。

# 4.对象值

方法`Object.values()`允许你以数组的形式获取一个对象中的所有值。您只需将对象作为参数传递给方法`Object.values()`。

这里有一个例子:

```
const user = {
  name: "Alex",
  age: 23,
  isOnline: false
}console.log(**Object.values(user)**);
//output: ["Alex", 23, false]
```

如您所见，您获得了一个对象值数组。现在你可以用这个数组做任何事情。

# 5.对象条目

方法`Object.entries()`也是有用的。它允许你获得一个对象的键和值，并返回一个多维数组，其中包含每个键和值的其他数组。

让我们来看一个实际的例子:

```
const user = {
  name: "Alex",
  age: 23,
  isOnline: false
}console.log(**Object.entries(user)**);
//output: [["name", "Alex"], ["age", 23], ["isOnline", false]]
```

正如您在示例中看到的，方法`Object.entries()`允许我们以数组的形式获取键和值。

# 6.对象创建

方法`Object.create()`用于从另一个现有对象的原型创建一个新对象。

看看下面的例子:

```
const user = {
  firstName: "John",
  lastName: "Doe",
  age: 25,
  fullName(){
    return `${this.firstName} ${this.lastName}`;
  }
}//New Object.
let newObject = **Object.create(user)**;//Updating properties.
newObject.firstName = "Mehdi";
newObject.lastName = "Aoussiad";//We can also use the method fullName of user in this new object.
newObject.**fullName()**; //output: Mehdi Aoussiadconsole.log(newObject);
//Output: {firstName: "Mehdi", lastName: "Aoussiad"}
```

在上面的例子中，我们使用`Object.create()`来创建一个新对象，它具有用户对象的原型。这就是为什么我们能够在新对象中改变属性并使用对象`user`的方法。如果您不想在对象中复制代码，这非常有用。

# 结论

正如您所看到的，这些对象方法在 JavaScript 中非常有用，因为对于开发人员来说，它们使处理对象变得更加容易。在某些情况下，你肯定需要使用这些方法。

感谢您阅读这篇文章。希望你觉得有用。

**更多阅读**

[](/5-useful-javascript-features-that-nobody-is-talking-about-b630838dedba) [## 没有人谈论的 5 个有用的 JavaScript 特性

### 你应该知道的冷门 JavaScript 特性。

javascript.plainenglish.io](/5-useful-javascript-features-that-nobody-is-talking-about-b630838dedba) 

*还有，如果你对 JavaScript 和 web 开发相关的更有用的内容感兴趣，可以* [*订阅*](https://mehdiouss.ck.page/) *我的快讯。*