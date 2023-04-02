# JavaScript 中的不变性:为什么它很重要以及如何使用它

> 原文：<https://javascript.plainenglish.io/immutability-in-javascript-why-its-important-and-how-to-use-it-e7c4125cc58f?source=collection_archive---------6----------------------->

不变性在现代 JavaScript 中是一个超级热门的话题，其背后的原因当然是函数式编程范式。

![](img/19be5408e8aa497fe7c6c115f7df33bf.png)

不可变数据与函数方法紧密相连，在函数方法中，任何突变都被认为是不必要的副作用。但是首先，让我们深入了解可变性和不可变性的细节。

# 什么是可变性？

为了让事情变得清晰，如果代码是可变的，这没有什么错 JavaScript 的数组 API 是可变的，这没有什么错。然而，误用可变性会对你的软件产生副作用。让我们看看下面的示例代码:

```
const person = {
   name: 'Rodrigo',
   email: 'email@email.com'
} // Make a copy of person object 
const newPerson = person; // Changing the email of the new person 
newPerson.email = 'somethingelse@email.com'; console.log(newPerson === person); // true 
console.log(person);    //  { name: 'Rodrigo', email: 'somethingelse@email.com' } 
console.log(newPerson); //  { name: 'Rodrigo', email: 'somethingelse@email.com' }
```

您可以看到，我们正在将对象(person)复制到另一个对象(newPerson ),并在 newPerson 上做了一点小小的更改。这里的问题是，这种变化反映在两个对象中。

发生这种情况是因为当你在 JS 中将一个对象赋给一个变量时，你实际上是在给它赋一个内存引用，所以当你这样做时:

```
const newPerson = person;
```

你只是复制了那个引用，而不是真正的值。两个变量指向同一个地方。

# 变得不可改变

不变性是维护对象状态的艺术，使开发变得简单、可追踪、可测试并减少任何可能的副作用。主要思想是:更新不应该改变对象，而是用更新的数据创建一个新对象。

与其传递对象并对其进行变异，不如创建一个全新的对象:

```
const person = { name: 'Rodrigo', email: 'email@email.com' } 
const newPerson = Object.assign(
  {}, 
  person, 
  { email: 'somethingelse@email.com' }
);console.log(newPerson === person); // false console.log(person)    // { name: 'Rodrigo', email: 'email@email.com' } 
console.log(newPerson) // { name: 'Rodrigo', email: 'somethingelse@email.com' }
```

但是嘿，我们用的是 ES6，难道不能换一种方式吗？当然可以！我们可以使用 Spread 运算符！看一看:

```
const person = { name: 'Rodrigo', email: 'email@email.com' } 
const newPerson = { ...person, email: 'somethingelse@email.com' } console.log(newPerson === person); // false - really different objects
console.log(person)    // { name: 'Rodrigo', email: 'email@email.com' } 
console.log(newPerson) // { name: 'Rodrigo', email: 'somethingelse@email.com' }
```

整洁，对不对？同样的结果，甚至更干净的代码。首先，我们创建一个新的对象，将{}赋值给一个变量，然后使用“spread”操作符(…)将 person 中的所有属性复制到新对象中。然后，我们定义一个新的“电子邮件”属性来覆盖旧的属性。请注意，在这种情况下，顺序很重要，如果在传播 person 对象之前定义了 email: 'somethingelse@email.com '，它将被来自 person 对象的 email 的值覆盖。

# 数组

首先，我们来看一个如何改变数组的小例子:

```
const fruits = [ 'Orange', 'Apple' ];
const newFruits = characters newFruits.push('Banana');console.log(fruits === newFruits) // true :-(
```

数组的工作方式与对象相同，所以您也可以使用 spread 操作符在数组上实现不可变。你可以这样使用它:

```
const fruits = [ 'Orange', 'Apple' ];
const newFruits = [ ...fruits, 'Banana' ];console.log(fruits === newFruits) // false 
console.log(fruits)    // [ 'Orange', 'Apple' ] 
console.log(newFruits) // [ 'Orange', 'Apple', 'Banana' ]
```

如您所见，您可以使用简单的现代 JavaScript 轻松实现不变性！最后，这都是关于常识和理解你的代码实际上做什么。如果你不小心编程，JavaScript 可能是不可预测的。

*更多内容看*[***plain English . io***](http://plainenglish.io/)