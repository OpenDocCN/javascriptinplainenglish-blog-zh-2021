# 如何避免 JavaScript 中的对象突变

> 原文：<https://javascript.plainenglish.io/javascript-how-to-avoid-object-mutation-7cd733913a9f?source=collection_archive---------3----------------------->

## 避免 JavaScript 中对象变异的三种快速方法&免费的乔恩·斯图尔特 gif

![](img/b7870491c318580b6764c7f7deb3e0fd.png)

Photo by [Possessed Photography](https://unsplash.com/@possessedphotography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我最近写了 JavaScript 中的[可变数据和](/javascript-mutable-vs-immutable-1efb662d78c8)不可变数据。我用来展示对象可变性的例子是这样的:

```
let character = {
    firstName: 'Captain',
    lastName: 'America'
}let avenger = character;character.lastName = 'Marvel';console.log(avenger.lastName);
```

我让读者猜猜控制台上打印了什么(是`// Marvel` btw ),这让我想到了避免对象突变的方法。

这里有一些方法可以避免我们最初的`character`对象发生变异:

## 1.创建新对象

这似乎是显而易见的，但你总是可以创建一个新的对象！这可能需要多几行代码，但是这样，当你需要改变一个对象，并且在内存中有多个变量指向同一个对象时，你就可以避免麻烦。对于我们的对象，我们甚至可以将存储在`character.firstName`的值用于`avenger`指向的新对象。

```
let character = {
    firstName: 'Captain',
    lastName: 'America'
};let avenger = {
    firstName: character.firstName,
    lastName: 'Marvel'
};character.firstName === avenger.firstName;// true
```

## 2. [Object.assign( )](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)

随着 [ES6](https://en.wikipedia.org/wiki/ECMAScript#6th_Edition_%E2%80%93_ECMAScript_2015) 的引入，JS 给了我们使用这种方法将所有属性从一个对象复制到另一个对象的能力。**如果使用不当，该方法会使对象变异。我想说清楚这一点。通过在目标参数中提供一个空对象，可以很容易地避免改变对象。 [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign#description) 总是支持我们应对故障:**

> 如果目标对象中的属性具有相同的[键](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys)，则它们会被源中的属性覆盖。较新的源的属性会覆盖较早的属性。

为了避免分配给`character`变量的对象发生突变，使用`Object.assign()`方法，我们执行以下操作:

```
let character = {
    firstName: 'Captain',
    lastName: 'America'
};let avenger = Object.assign({}, character);
avenger.lastName = 'Marvel';
```

上面的代码将创建一个分配给`avenger`变量的新对象，然后我们将把`lastName`属性更改为字符串`‘Marvel’`，以获得我们想要的结果，而不改变分配给`character`变量的原始对象。但是，我们实际上可以通过执行以下操作，在`Object.assign()`方法中一举获得我们想要的结果:

```
let character = {
    firstName: 'Captain',
    lastName: 'America'
};let avenger = Object.assign({}, character, { lastName: 'Marvel' });
```

*边注:我想再迭代一次使用* `Object.assign()`时，传入空对象作为第一个参数(目标参数)的重要性。*使用该方法时，返回目标对象。所以，如果你给一个对象分配了属性，你就有可能改变这个对象。请看下面的例子来了解这一点:*

```
let character = {
    firstName: 'Captain',
    lastName: 'America'
};let avenger = Object.assign({}, character, { lastName: 'Marvel' });let newAvenger = Object.assign(avenger, { firstName: 'Ms.; });console.log(avenger);
console.log(newAvenger);// { firstName: 'Ms.',
     lastName: 'Marvel
   }// { firstName: 'Ms.',
     lastName: 'Marvel'
   }
```

*从乔恩的困惑中可以看出，我们对分配给* `avenger` *变量的目标对象进行了变异。我们现在有两个变量(*`avenger`*&*`newAvenger`*)分配给内存中的这个对象，这不是我们想要的结果。现在，当我们使用任何一个变量来分配新的属性或属性值时，我们都有可能在没有意识到的情况下改变这个对象。*

## 3.[传播语法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax#spread_in_object_literals)

最后，为了一些语法上的好处，我们使用了 spread 操作符。你看到的是同样的想法，但我觉得更悦目一些。

```
let character = {
    firstName: 'Captain',
    lastName: 'America'
};let avenger = { ...character };
avenger.lastName = 'Marvel';
```

这比前面的方法要简单得多，并且达到了相同的效果！但是，(*我打赌你已经预见到了这一点*)我们可以像这样使用 spread 运算符来获得相同的结果:

```
let character = {
    firstName: 'Captain',
    lastName: 'America'
};let avenger = { ...character, lastName: 'Marvel' };
```

# 结论

易变的对象，和突变，不必害怕。这可能会变得棘手，但总而言之，有许多不同的方法来避免变异对象。我希望这是有帮助的，如果你想到任何其他方法来避免突变，请告诉我。

快乐编码🤓