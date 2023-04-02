# 如何使某些属性在 TypeScript 中可选

> 原文：<https://javascript.plainenglish.io/how-to-make-certain-properties-optional-in-typescript-9b4f8e85c5de?source=collection_archive---------2----------------------->

![](img/22a5a275b3374eca80179c938cda4656.png)

Photo by [Kevin Ku](https://unsplash.com/@ikukevk?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

接口的声明是使一些属性可选的地方。您可以通过在属性名称旁边打一个问号来实现这一点。

```
interface Person {
    uuid: string;
    name: string;
    surname: string;
    sex: string;
    height: number;
    age: number;
    pet?: Animal;
}interface Animal {
    name: string;
    age: number;
}
```

在上面的例子中，`pet`是一个可选属性。这很有用，但是每次你想在`Person`的`pet`上执行一些操作时，你需要检查它是否被声明，因为`pet?: Animal;`是`pet: Animal | undefined;`语法的简写。

# 小案例研究

假设你想做一个像`J. Doe`一样返回姓名首字母和姓氏的函数。

```
function personShortName(name: string, surname: string): string {return `${name[0]} ${surname}`;
}const person1: Person = { /* Person properties */ };personShortName(person1.name, person1.surname);
```

我们可以使用`Person`类型对象作为函数参数，而不是每次调用`personShortName()`时都访问`name`和`surname`。

```
function personShortName(person: Person): string {return `${person.name[0]} ${person.surname}`;
}
```

当然，我们也可以使用析构来简化这个函数，如下所示:

```
function personShortName({name, surname}: Person): string {return `${name[0]} ${surname}`;
}
```

似乎不错，但看看它的局限性。你需要一个`Person`类型的对象来调用一个简单的函数。现在，如果您想在其他地方调用它，您需要创建一个新的`Person`。

```
❌ personShortName({ name: 'Robert', surname: 'Doe' })
```

由于`{ name: string, surname: string }`与`Person`类型不匹配，上述示例不适用。

# 那如何实现双赢呢？

Typescript 获得了一个`Partial<T>`实用程序类型，该类型简单地使得`T`的所有属性都是可选的。如果我们使用`Partial<Person>`而不是`Person`作为`personShortName()`中的参数类型，那么前面的例子就有效了:

```
function personShortName({name, surname}: Partial<Person>): string {return `${name[0]} ${surname}`;
}️personShortName({ name: 'Robert', surname: 'Doe' });
```

但是我们这里有个副作用，`{ name: string; surname; string }`变成了`{ name: string | undefined; surname: string | undefined; }`。

然后，为了防止返回像“u. undefined”这样奇怪的结果，我们需要在函数内部执行一些类型检查，确保每个需要的变量都被定义。

```
function personShortName({name, surname}: Partial<Person>): string | null {return name && surname ? `${name[0]} ${surname}` : null;
}
```

我们已经实现了…另一个副作用——现在我们的函数可能会返回`null`,这可能会在其使用的地方强制进行一些额外的检查。

但是不要担心——有更好的方法。TypeScript 还提供了另一个实用程序类型— `Pick<T, Keys>`，它从`T`中选择一些属性`Keys`。

```
function personShortName({ name, surname }: Pick<Person, 'name' | 'surname'>): string  {
    return `${name[0]} ${surname}`;
}
```

这样我们就实现了我们的目标——我们允许双向调用这个函数——传递一个有效的`Person`对象或者只传递需要的变量。

```
personShortName({ name: 'John', surname: 'Doe' });const someone: Person = { name: 'John', ... }
personShortName(someone);
```

# 更进一步

在上面的解决方案中，您无法访问`personShortName`函数中剩余的`Person`属性。让我们假设您想要实现一个仅在最简单的变体中使用`name`和`surname`的函数，但是您也想要访问其他`Person`属性。

```
function personShortName(person: Person): string  {
  const { name, surname, uuid } = person;
  if (uuid) {
    const userRole = getUserRole(uuid);
    return `${name[0]} ${surname}, ${userRole}`;
  } 

  /* some other operations on persons params */

  return `${name[0]} ${surname}`;
}
```

这种实现不允许您直接使用带有`name`和`surname`的简单调用。但是当没有`uuid`时，我们不需要所有的`Person`属性来返回短名称。我们需要访问所有的`Person`属性，但是应该只需要`name`和`surname`。也许然后让我们允许`person: Person | Pick*<*Person, 'name' | 'surname'*>*`。

```
function personShortName(person: Person | Pick<Person, 'name' | 'surname'>)): string  {
  ❌ const { name, surname, uuid } = person;
  if (uuid) {
    const userRole = getUserRole(uuid);
    return `${name[0]} ${surname}, ${userRole}`;
  }

  /* some other operations on persons params */

  return `${name[0]} ${surname}`;
}
```

这是个好主意，但还是行不通。编译器会说`property uuid don't exist on type { name: string, surname: string }`。

# 解决方案是结合

这种方法是一个很好的方向，因为我们已经声明我们需要一个完整的`Person`或`{ name, surname }`。但事实上，我们不想要整个`Person`或`{ name, surname }`。我们想要完成的事情是让所有的`Person`属性**可选**和`name, surname`成为**必需**。我们可以通过组合`Partial<T>`和`Pick<T, Keys>`实用程序类型来实现这一点。

```
function personShortName(person: Partial<Person> & Pick<Person, 'name' | 'surname'>)): string  {
  const { name, surname, uuid } = person;
  if (uuid) {
    const userRole = getUserRole(uuid);
    userRole = getUserRole(uuid);
    return `${name[0]} ${surname}, ${userRole}`;
  } /* some other operations on persons params */ return `${name[0]} ${surname}`;
}
```

上面的语法，`Partial<Person> & Pick<Person, 'name' | 'surname'>`给了我们这样的类型:

```
person: {
    uuid?: string;
    name: string; <- required
    surname: string; <- required
    sex?: string;
    height?: number;
    age?: number;
    pet?: Animal;
}
```

通过这种方式，我们可以拥有一些必需的属性，而其他的则变成可选的。希望你会觉得有用。

*~ Dawid Witulski @ evonica—2021*

*更多内容请看*[***plain English . io***](http://plainenglish.io/)