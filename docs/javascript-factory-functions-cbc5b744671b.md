# 如何在 JavaScript 中使用工厂函数创建对象

> 原文：<https://javascript.plainenglish.io/javascript-factory-functions-cbc5b744671b?source=collection_archive---------1----------------------->

## 本文将介绍使用工厂函数在 JavaScript 中构建一个对象。

![](img/b297e312f46a086dc6f3f2b33b19429d.png)

Photo by [Alexander Tsang](https://unsplash.com/@alexander_tsang?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

当学习 JavaScript 和任何其他主题时，我倾向于问“为什么？”为什么要这样做？为什么我必须知道这些？为什么？

我承认，‘为什么？’可能是个烦人的问题。“因为我是这么说的”是我父母在成长过程中常说的一句话。令他们懊恼的是，这并没有阻碍我理解“为什么”的努力。

所有这些都是为了说明我正在试图理解我们是如何发展到 JavaScript 类的。我认为开发类似类的对象来展示我们现在所知的 JavaScript 类会很有趣。

本文将介绍如何使用工厂函数构建一个对象，接下来的一篇文章将介绍构造函数并使用 new 运算符来创建相同的对象，最后一篇文章将介绍作为类构建的相同对象。

# 工厂功能

> 在[面向对象编程(OOP)](https://en.wikipedia.org/wiki/Object-oriented_programming) 中，**工厂**是[创建其他对象](https://en.wikipedia.org/wiki/Object_creation)的[对象](https://en.wikipedia.org/wiki/Object_(computer_science))——形式上，工厂是从某个方法调用返回不同原型或类[【1】](https://en.wikipedia.org/wiki/Factory_(object-oriented_programming)#cite_note-1)对象的函数或方法，这被认为是“新的”。
> 
> — [维基百科](https://en.wikipedia.org/wiki/Factory_(object-oriented_programming))

如果上面的引用没有弄清楚什么是工厂函数，就把它想象成一个不使用[构造函数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new)或类而返回一个对象的函数。

我刚刚重新观看了 MCU 的第 1 阶段，所以我们的工厂函数将创建一个表示超级英雄的对象，因为这是我曾经使用的所有示例，所以为什么现在停止呢？

```
const avengers = [];const captainAmerica = {
   name: 'Steven Rogers',
   alias: 'Captain America',
   abilities: [
      'Enhanced strength, speed, stamina, durability, agility, reflexes, senses, and mental processing via the super soldier serum',
      'Master martial artist and hand-to-hand combatant',
      'Accelerated healing',
      'Immunity to diseases and toxins',
      'Slowed aging', 
      'Master tactician, strategist, and field commander',
      'Using Vibranium-steel alloy shield']
}
```

上面你会看到我们有一个代表美国队长的物体。现在，让我们创建一个工厂函数来为我们创建这个对象。

```
const makeHero = (name, alias, abilities) => {
  const hero = {};
  hero.name = name;
  hero.alias = alias;
  hero.abilities = abilities;
  return hero;
}
```

就是这样。那是工厂功能。它没有工厂函数那么激动人心，但它是一个不使用构造函数或类就返回对象的函数。要使用这个工厂创建一个新对象，我们应该编写:

```
const captainAmerica = makeHero('Steven Rogers', 'Captain America', ['Enhanced strength, speed, stamina, durability, agility, reflexes, senses, and mental processing via the super soldier serum',
'Master martial artist and hand-to-hand combatant',
'Accelerated healing',
'Immunity to diseases and toxins',
'Slowed aging',
'Master tactician, strategist, and field commander',
'Using Vibranium-steel alloy shield']);
```

但是这真的能节省我们的时间吗？不完全是。我们仍然需要手工输入所有的信息。但是，如果我们想把我们的复仇者组合成一个阵列呢？嗯，我们可以创建引用数组的变量，比如`const avengers = [];`。然后我们可以用 JS 给我们的数组方法添加和移除对象，比如`push()` & `pop()`。那将会起作用，但是更有趣的是如果我们在工厂内部创建函数来添加或删除`avengers`数组中的英雄？这将允许我们的对象使用相同的方法在`avengers`数组中添加和删除它们自己！

```
const makeHero = (name, alias, abilities) => {
  const hero = {};
  hero.name = name;
  hero.alias = alias;
  hero.abilities = abilities;
  hero.assemble = function () {
    avengers.includes(this)
      ? console.log(
          `${this.alias} has already been assembled into the
           Avengers`
        )
      : avengers.push(this);
    *return* avengers;
  };
  hero.disassemble = function () {
    const heroToRemove = avengers.findIndex(
      (hero) => hero === this
    );
    heroToRemove === -1
      ? console.log(
          `${this.alias} has already been disassembled from the
           Avengers`
        )
      : avengers.splice(heroToRemove, 1);
    *return* avengers;
  };
  *return* hero;
}
```

看那个！当我们用我们的工厂函数创建一个新对象时，它可以使用这些来自我们工厂的内置方法，节省我们大量的时间(好吧，也许不是大量的时间)。

工厂函数对创建对象非常有帮助，但是还有其他方法可以实现这一点。下周我将深入探讨这个问题。

编码快乐！

## 有趣的相关阅读

[1]埃里克埃利奥特。(2016) [JavaScript 工厂函数 vs 构造函数 vs 类](https://medium.com/javascript-scene/javascript-factory-functions-vs-constructor-functions-vs-classes-2f22ceddf33e)。

[2]埃里克·埃利奥特。(2017) [带 ES6+](https://medium.com/javascript-scene/javascript-factory-functions-with-es6-4d224591a8b1) 的 JavaScript 工厂函数。

[3] rajaraodv。(2016)[ES6 中的“类”是新的“坏”的部分吗？](https://medium.com/@rajaraodv/is-class-in-es6-the-new-bad-part-6c4e6fe1ee65)。

[*更多内容尽在 plainenglish.io*](http://plainenglish.io/)