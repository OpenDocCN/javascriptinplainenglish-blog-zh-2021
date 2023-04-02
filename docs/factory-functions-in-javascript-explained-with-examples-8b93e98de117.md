# 用例子解释 JavaScript 中的工厂函数

> 原文：<https://javascript.plainenglish.io/factory-functions-in-javascript-explained-with-examples-8b93e98de117?source=collection_archive---------4----------------------->

## 通过示例了解 JavaScript 中的工厂函数。

![](img/f47280107b58bc431a8097fe53ff5539.png)

Photo by [Cottonbro](https://www.pexels.com/fr-fr/@cottonbro) on [Pexels](https://www.pexels.com/).

工厂函数在 JavaScript 中一直很有吸引力，因为它们提供了在不使用`new`关键字或类的情况下轻松生成对象实例的能力。

在本文中，我们将通过一些实例来学习 JavaScript 中的工厂函数。让我们开始吧。

# 什么是工厂功能？

工厂函数只是一个返回新对象的*函数*。

工厂函数不需要使用`new`关键字，但是仍然可以用来初始化对象，就像构造函数一样。

让我们来看看一些实际的例子:

首先，让我们创建一个对象`user1`，它给出了一个用户的信息:

```
let user1 = {
    name: 'Mehdi',
    age: 19,
    getInfo() {
        return **this.name** + ' is ' + **this.age** + ' years old.';
    }
};console.log(**user1.getInfo()**);
//Mehdi is 19 years old.
```

如您所见，对象`user1`有两个属性:姓名和年龄。用一个方法`getInfo()`以字符串的形式返回这些属性。

比方说，您需要为另一个用户创建另一个对象`user2`。您需要重新开始并复制代码，如下所示:

```
let user2 = {
    name: 'John',
    age: 29,
    getInfo() {
        return **this.name** + ' is ' + **this.age** + ' years old.';
    }
};console.log(**user2.getInfo()**);
//John is 29 years old.
```

如果你必须为另外 100 个用户做同样的事情呢？需要再创建 100 个对象吗？

为了避免再次复制相同的代码，我们将需要使用 JavaScript 工厂函数**来为我们创建对象，而不需要使用`new`关键字或深入复杂的类。**

下面的例子显示了一个创建用户对象的工厂函数`createUser`:

```
function **createUser(name, age)** {
    return {
        name: name,
        age: age,
        getInfo() {
            return **name** + ' is ' + **age** + ' years old.';
        }
    }
}
```

如你所见，函数`createUser`返回一个对象，这就是为什么我们称它为工厂函数。现在我们可以使用它来创建用户的对象。

下面的代码使用`createUser()`工厂函数创建三个对象`Mehdi`、`John`和`Anna`:

```
let mehdi = createUser('Mehdi', 19);
let john = createUser('John', 29);
let anna = createUser('Anna', 25);console.log(**mehdi.getInfo()**); //Mehdi is 19 years old.
console.log(**john.getInfo()**); //John is 29 years old.
console.log(**anna.getInfo()**); //Anna is 25 years old.
```

如您所见，使用工厂函数，您可以创建任意数量的`user`对象，而无需重复代码。

如果你不喜欢 ES5，下面是使用 ES6 语法的相同代码:

```
const createUser = (**name, age**) =>{
    return {
        **name**,
        **age**,
        getInfo() {
            return `${**name**} is ${**age**} years old.`;
        }
    }
}
let mehdi = createUser('Mehdi', 19);
let john = createUser('John', 29);
let anna = createUser('Anna', 25);console.log(mehdi.getInfo());
console.log(john.getInfo());
console.log(anna.getInfo());
```

*输出:*

![](img/ba59419f4e345866e8e3aa089f994b6c.png)

The output from the console.

# 内存空间问题

上面例子的唯一问题是，当你创建一个用户对象并把它存储在一个变量中时，这个对象需要一个内存空间，如果我们有数千个对象，它会影响代码的性能。

然而，所有对象都有相同的方法`getInfo()`。所以我们可以将这个方法从工厂函数中移除，并将其存储在另一个单独的变量中，以避免重复使用。我们只会在需要的时候使用它。

我们将该方法从工厂函数中移除:

```
function **createUser(name, age)** {
    return {
        name: name,
        age: age,
    }
}
```

然后，我们将它存储在一个单独的变量中:

```
const separated = {   
  getInfo() {   
      return `${this.name} is ${this.age} years old.`;
 } 
}
```

在用户对象上调用`getInfo()`方法之前，您可以将对象`seperated`的方法分配给用户对象，如下所示:

```
let john = createUser('John', 29);
let anna = createUser('Anna', 25);**john.getInfo = separated.getInfo;
anna.getInfo = separated.getInfo;**console.log(john.getInfo());
console.log(anna.getInfo());
```

*输出:*

![](img/e63cd8ca57cb676ac9b30f15a523b6a8.png)

The output from the console.

这没问题，但是如果我们有很多对象，这又会变得更加困难和低效。这就是为什么你需要使用`Object.create()`。

# 方法“Object.create()”

方法`Object.create()`使用现有对象作为新对象的原型来创建新对象。

我们可以如下使用`Object.create()`:

```
const separated = {   
  getInfo() {   
      return `${this.name} is ${this.age} years old.`;
 } 
}function createUser(name, age) {
     **let person = Object.create(separated);**
     person.name = name;
     person.age = age;
     return person;
 }
```

现在，您可以创建`person`对象并调用`separated`对象的方法:

```
let john = createUser('John', 29);
let anna = createUser('Jane', 25);**console.log(john.getInfo());
console.log(anna.getInfo());**
```

*输出:*

![](img/e63cd8ca57cb676ac9b30f15a523b6a8.png)

The output from the console.

# 结论

正如您所看到的，使用工厂函数可能是一种很好的技术，它允许您在不使用`new`关键字或类的情况下生成对象实例。但是当你有很多对象时，事情就变得更难了。这就是为什么我会推荐使用构造函数或者类。

感谢您阅读本文，希望您觉得有用。

# 更多阅读

*如果你对 JavaScript 和 web 开发相关的更有用的内容感兴趣，也可以* [*订阅*](https://mehdiouss.ck.page/) *我的快讯。*

这里有另一篇有用的文章，请点击下面的链接:

[](https://medium.com/javascript-in-plain-english/5-powerful-ides-that-nobody-is-talking-about-c20ed0ae83ee) [## 没有人谈论的 5 个强大的 IDEs

### 一些你可能需要使用的有用的文本编辑器。

medium.com](https://medium.com/javascript-in-plain-english/5-powerful-ides-that-nobody-is-talking-about-c20ed0ae83ee)