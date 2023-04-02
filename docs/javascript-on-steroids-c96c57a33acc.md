# 类固醇上的 JavaScript？

> 原文：<https://javascript.plainenglish.io/javascript-on-steroids-c96c57a33acc?source=collection_archive---------14----------------------->

![](img/03ed9e77c7f13f27534a2fa600bddbde.png)

重载您的本地 JavaScript 对象，以获得更好的可重用性和更干净的代码。

**问题空间**

自从 ES6 推出以来，很多新的 JavaScript 方法出现了，比如 map、reduce、find。这些都是代码的函数助手，使您可以轻松地操作和使用 Javascript 数据结构。

在我们作为 JavaScript 开发人员的日常生活中，我们仍然一遍又一遍地编写相同的东西，这就是像 Lodash 这样的库发挥作用的地方。但是当人们争论为什么 React 的包大小是 145KB 而 Angular 的包大小是 2.4MB 时，真的需要这些吗？洛达什是一个令人印象深刻的图书馆，没有什么可以带走的。

**我的解决方案**

用我们已经知道的东西来扩展 JavaScript 对象是一个可行的选择。ES6 也提供了类，这只是语法上的糖，但是来自 OOP 背景会让你理解得更好，尽管 JavaScript 仍然有很多奇怪的地方。

在我的日常工作中，我经常需要找到数组中某个元素的唯一出现。我需要检查一个元素是否存在于一个数组中，我觉得这是正常工作流的一部分，没有任何异常。

```
class PowerArray  extends Array {

  checkIfExist(value){
   return !!this.find(val=>val==value)
  }
  unique(){
    console.log(this)
    return new PowerArray(...new Set(this))
  }
  sum(){
   return this.reduce((val,acc)=>val+acc,0)
  }
}const array=new PowerArray() 
```

在这个实现中，您拥有一个数组本身提供的所有函数，以及添加的 3 个不同的方法。

现在，我们可以像使用普通数组一样使用这个新数组，并将我们的方法与本机方法链接在一起。

```
array.push(1)
array.push(2)
array.push(2)
console.log(array.unique().sum())//3
console.log(array.sum())//5
console.log(array.checkIfExist(7))//false
```

谈到另一个重要的数据结构，它在 JavaScript 世界中被大量使用——对象。

```
class PowerObject extends Object{
  getKeys(){
   return Object.keys(this)
  }
  getValues(){
    return Object.values(this)
  }
  prettyPrint(){
    console.group('Object...')
    console.log('Object Values',this)
    console.groupEnd()
  }
  deepClone(){
    const temp=JSON.stringify(this);
    return Object.assign(new PowerObject(),JSON.parse(temp))
  }
}
```

我们在这里也使用了相同的概念，并且我们能够通过这段代码将 3 个更有用的方法附加到我们的应用程序中。

对于对象的克隆，我们经常使用扩展操作符

```
const a = {...b}//works only with first level keys, shallow copy
```

这种实现工作得非常好，除非你在 b 中有嵌套对象，当许多初学者希望这也能用于嵌套对象时，他们很难找到问题。

```
const myObject = new PowerObject();
myObject['a']=5;
myObject['b']={'m':'5'};
const normalObject={...myObject}normalObject.a=7;
normalObject.b.m=6;console.log(myObject)
//a: 5 , b:{m:6} so the value of m is changed despite using the //spread operator
```

**修复:**

这是如何工作的？当您将一个对象转换为字符串并解析回该对象时，它通过将它转换为通过值传递且不可变的原始类型来中断对初始对象的引用，这与通过引用传递的对象不同。

```
const normalObject = myObject.deepClone()//this will make a deep copy
console.log(normalObject)
normalObject.a = 7
normalObject.b.m = 6
myObject.prettyPrint()// the original object intact //YEAHHH 
```

现在，其他方法也更加语法化，使您的工作更加整洁，代码更具可读性。

```
myObject.getKeys() //["a", "b"]
myObject.getValues() //[5, {…}]
```

于是，我们来到了文章的结尾。关键要点是什么？总是试图让你的代码库对你自己和你的同事来说更容易；过度工程在编程中是真实存在的，所以尽量避免。您可以通过创建自己的方法来巩固您的理解，并使您的代码尽可能地去耦合。

**亲提示:**

您可以将该类添加到条目文件或任何脚本文件中的 window 对象中，这样它们就可以在整个项目中使用，而无需到处导入。

```
window.PowerClass=PowerClass 
```

避免使用与原生 JavaScript 中的函数或方法相同的名称。这对你可能弊大于利。

敬请关注更多内容。和平！

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)