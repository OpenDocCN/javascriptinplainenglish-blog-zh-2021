# 用例子解释 JavaScript 类

> 原文：<https://javascript.plainenglish.io/javascript-classes-explained-with-examples-c10d0426834b?source=collection_archive---------3----------------------->

## 通过实例了解 JavaScript 中的类语法。

![](img/b9d5b40461e38448319d53b1f911d3af.png)

Photo by [Fotis Fotopoulos](https://unsplash.com/@ffstop?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 介绍

类语法是 ES6 中引入的最好的特性之一。在 JavaScript 中，类为开发人员提供了一种简单的语法，而不是使用构造函数。它们通常被称为“语法糖”，因为它们提供了一种在 JavaScript 中进行面向对象编程的更干净的方式。

在本文中，我们将通过一些实例来学习 JavaScript 中的类。让我们开始吧。

# 定义一个类

正如我所说的，JavaScript 类引入了一种简单的方法和一种语法糖来编写构造函数。它们主要用于创建新对象。

为了在 JavaScript 中定义一个类，我们使用关键字`class`并给它一个首字母大写的名字。然后我们需要在类内部定义一个构造函数方法。

这里有一个例子:

```
**class** **U**ser{
  **constructor**(firstName, lastName){
    this.firstName = firstName;
    this.lastName = lastName;
  }

}
```

正如你在上面看到的，我们创建了一个名为`User`的类，它有一个带两个参数的构造函数方法，我们可以用它来创建我们的新对象。

现在，我们可以使用我们的类来创建包含用户的名字和姓氏的新对象。

看看下面的例子:

```
//Create the class
**class** **U**ser{
  **constructor**(firstName, lastName){
    this.firstName = firstName;
    this.lastName = lastName;
  }
}
//create a new object.
const newUser = **new** User('Mehdi', 'Aoussiad');console.log(newUser);
//output: {firstName: "Mehdi", lastNamee: "Aoussiad"}
```

为了从我们的类中创建一个新的对象，我们使用关键字`new`，后跟类名。然后我们替换在构造函数中使用的参数。每当调用关键字`new`时，将调用构造函数来创建一个新对象。

# 定义方法

JavaScript 类的好处是可以在类内部定义方法。

这里有一个例子:

```
class **U**ser{
  **constructor**(firstName, lastName){
    this.firstName = firstName;
    this.lastName = lastName;
  }//Adding a method.
 **fullName(){
    return `${this.firstName} ${this.lastName}`;
  }**}
const newUser = **new** User('John', 'Doe');console.log(newUser); //output: {firstName: "John", lastName: "Doe"}//access the method.
console.log(**newUser.fullName()**); //output: John Doe
```

如您所见，您可以在新创建的对象`newUser`中访问方法`fullName`。您可以在类中创建任意多的方法。

# 类继承

在 JavaScript 中，类可以从称为父类的其他类继承方法和属性。

假设我们想要创建一个名为`UsersAge`的新类，它继承了上面的类`User`的所有方法和属性。为此，我们使用关键字`extends`和方法`super()`。

看看下面的例子:

```
class UsersAge **extends** User{
  constructor(firstName, lastName, age){
    **super**(firstName, lastName);
    this.age = age;
  }
}
```

我们使用关键字`extends`来表明我们想要从父类`User`继承。另一方面，方法`super()`用于访问父类构造函数的所有属性。

现在我们使用了类继承，我们可以访问新创建的类中的类用户的所有方法。

这里有一个例子:

```
 //New Object.
const newUserAge = new UsersAge("Brad", "Traversy", 30); //Accessing the fullName method of the parent class(User).
console.log(**newUserAge.fullName()**);
//output: Brad Traversy
```

在上面的例子中，我们在一个使用子类`UsersAge`创建的新对象中访问了类`User`的方法`fullName`。那是因为我们使用了类继承。

# Getters 和 Setters

Getters 和 setters 只是两个类方法，它们允许我们获取和设置对象内部的属性值。

看看下面的例子:

```
class User{
  constructor(name){
    this.name = name;
  }

  //Getter
  **get** userName(){
    return this.name;
  }//setter
  **set** userName(updateName){
    this.name = updateName;
  }
}//Create object.
const newUser = **new** User('John');//Get name.
console.log(**newUser.name**); //John//Set name.
newUser.name = 'Mehdi';
console.log(newUser.name); //Mehdi
```

正如您所看到的，使用 getters 和 setters，您可以轻松地在类对象中获取和设置值。

# 结论

JavaScript 类作为 ES6 的一个特性来代替构造函数。它们提供了一种易于理解的语法糖，可以将 JavaScript 作为一种面向对象的语言来使用。

感谢您阅读这篇文章。希望你觉得有用。

# 更多阅读

[](https://js.plainenglish.io/5-useful-javascript-tips-to-speed-up-your-coding-38c54c42e911) [## 加速编码的 5 个有用的 JavaScript 技巧

### 用 JavaScript 更快编码的 5 种方法和技巧。

js .平原英语. io](https://js.plainenglish.io/5-useful-javascript-tips-to-speed-up-your-coding-38c54c42e911) 

*阅读更多尽在*[***plain English . io***](https://plainenglish.io/)