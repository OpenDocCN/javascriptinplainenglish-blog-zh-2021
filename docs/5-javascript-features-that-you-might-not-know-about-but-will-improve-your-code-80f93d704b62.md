# 5 个鲜为人知的 JavaScript 特性将改善您的代码

> 原文：<https://javascript.plainenglish.io/5-javascript-features-that-you-might-not-know-about-but-will-improve-your-code-80f93d704b62?source=collection_archive---------10----------------------->

![](img/699d67ccb0cc6aea4b794b9c82765ca8.png)

Image by Jonathan Fielding

今天，我想分享一些 JavaScript 特性，这些特性你应该在日常代码中使用，但是在过去几年中 JavaScript 的许多更新中可能已经错过了。

# 1.JavaScript 字符串填充

如果你在 2016 年从事 JavaScript 生态系统的工作，你可能会记得`left-pad`事件。

总之，NPM 上有一个 JavaScript 包，可以用来填充字符串和额外的字符，它从 NPM 被删除了，因为它被许多包所依赖，它引起了多米诺骨牌效应，破坏了全世界的软件构建。

虽然 NPM 修复了这个问题，但在 TC39 上，人们发现很多人更喜欢使用库来填充字符串，而不是自己编写代码，因此作为 ES2017 的一部分，他们引入了`.padStart()`和`.padEnd()`。

要将 0 添加到字符串的开头，我们将使用`.padStart()`，传递字符串的目标长度和填充当前字符串的字符串。在下面的例子中，我填充了字符串“1 ”,使其长度为“5”。

```
let str = "1";
str = str.**padStart(5,0)**;
console.log(str) // output is **00001**
```

或者，我们可能想要填充字符串的末尾，为此我们使用`.padEnd()`。类似地，我们传递字符串的目标长度和用来填充当前字符串的字符串。在下面的例子中，我填充了字符串“1 ”,使其长度为“5”。然而，这一次它将在末尾添加填充。

```
let str = "1";
str = str**.padEnd(5,0)**;
console.log(str) // result is 1**0000**
```

# 2.传播算子

Spread 操作符并不是最新最闪亮的 JavaScript 特性，它在 2015 年作为 ES2015 规范的一部分出现，但是它的一些用例经常被忽略。

spread 运算符的第一个用例是将一个数组中的项目添加到另一个数组中。在下面的例子中，我有一个包含 3 个水果的数组，但是我想要第二个包含第四个水果的数组，所以我使用 spread 操作符来复制原始水果，并添加第四个水果。

```
const arr1 = ["Apple", "Orange", "Pear"]
const arr2 = [...arr1, "Banana"]
console.log(arr2) // ["Apple", "Orange", "Pear", "Banana"]
```

我们可以对对象做类似的事情，但是额外的好处是我们可以覆盖原始对象中的值。

```
const personA = {
  name: "Jonathan",
  age: 21,
}
const personB = {
  ...personA,
  name: 'Charlie'
}
console.log(personB) // {name: "Charlie", age: 21}
```

# 3.休息参数

从 Spread 操作符开始，我们有了`Rest`参数，有点像它的反义词。`rest`语法收集多个元素并将它们“浓缩”成一个元素。

`rest`参数的一个很好的用例是当一个数组被析构时将它的剩余元素分组。在下面的例子中，我们销毁了一些水果，所以苹果是独立的，剩下的水果放在水果数组中。

```
const [apple, ...fruits] = ["apple", "orange", "pear"];
console.log(apple); // output is "apple"
console.log(fruits); // output is ["orange", "pear"]
```

# 4.数组.原型.包含

我要讲的下一个特性是`Array.prototype.includes`，这个特性允许你发现一个数组是否包含一个项。

在`Array.prototype.includes`之前，这可以通过循环数组并在找到项目时将变量设置为 true 来实现，见下文:

```
const fruits = ["Dragonfruit", "Kiwi", "Mango", "Pear", "Starfruit"];
let found = false;fruits.forEach(function(fruit) {
  if (fruit === 'Kiwi') {
    found = true;
  }
});console.log(found); // Outputs `true`
```

现在，有了`Array.prototype.includes`，我们可以将这个显著地减少到如下

```
const fruits = ["Dragonfruit", "Kiwi", "Mango", "Pear", "Starfruit"];
const found = fruits.includes("Kiwi");
console.log(found); // Outputs `true`
```

注意:作为开发者，我们不需要担心这个搜索是如何实现的，所以浏览器有机会自己优化这个行为。

# 5.可选链接

我想说的第五个也是最后一个特性是可选链接。

可选链接允许我们尝试检索对象中嵌套很深的数据，而不必处理数据可能不存在的情况。

让我们看看下面的例子，在这个例子中，我们用一些元数据来定义`Jonathan`。

```
const jonathan = {
  name: "Jonathan",
  meta: {
    age: 21
  }
}const age = jonathan.meta.age;
const gender = jonathan.other.gender; // Will throw errorconsole.log(age);
console.log(gender);
```

如果我们运行这段代码，它会导致一个错误，因为对象的`other`部分不存在。

![](img/722a44a3baee2633cf14a507188bf02c.png)

使用可选链接，我们可以通过这样的方式来防止这个错误:如果一个属性不存在，就不要在对象树中继续操作。我用可选链接更新了下面的代码。

```
const jonathan = {
  name: "Jonathan",
  meta: {
    age: 21
  }
}const age = jonathan?.meta?.age;
const gender = Jonathan?.other?.gender;console.log(age); // outputs 21
console.log(gender); // outputs "undefined"
```

如果我们现在运行这个，将不再有错误，性别将简单地不确定，我们可以单独处理。

# 包扎

JavaScript 正以前所未有的速度快速发展，每年都有更新，这种语言保持着新鲜感，人们很容易忘记我们可以用仅仅几年前的特性做的所有很酷的事情。

根据我自己的经验，写这篇文章实际上让我对我谈到的每个特性有了更多的了解。帮助我巩固自己的知识。

感谢您抽出时间阅读，如果您想阅读类似的帖子，请在 Medium 上跟随我。