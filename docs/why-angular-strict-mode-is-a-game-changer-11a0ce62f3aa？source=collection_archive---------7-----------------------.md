# 为什么角度严格模式是游戏规则的改变者

> 原文：<https://javascript.plainenglish.io/why-angular-strict-mode-is-a-game-changer-11a0ce62f3aa?source=collection_archive---------7----------------------->

## 什么是严格模式，为什么要使用它？

![](img/63dbff3c1fe5f7540b253e6f3974b816.png)

如果你过去使用 TypeScript，它是一种促进严格数据类型的编程语言，可以帮助开发人员避免许多在开发过程中可以避免的生产问题。由于在最新的 angular (v.12)中默认启用严格模式，我们将研究为什么在您的应用程序中启用该功能是一个好主意，以及我们如何编写类型安全的代码。

# 为什么是严格模式？

在 angular 应用中启用严格模式的目的是提醒开发人员确保变量、方法和类已经被分配给特定的数据类型。严格模式设置将有助于:

*   早点抓虫子
*   减小包的大小，避免分配不必要的内存。
*   遵循最佳实践
*   获得更好的 IDE 支持

尽管启用严格模式会降低您更快编写代码的速度，但是开发人员需要认识到严格模式带来的好处对我们代码开发人员和维护人员来说是绝对有益的。

# 如何编写类型安全的代码

下面是为数据声明类型定义的一些常用方法

## 显式声明类型

可以将类型附加到变量上，以防止类型不明确。

*   *原始类型*

```
const a:**number** = 0;const b:**boolean** = false;const c:**string** = 'a';
```

*   *对象类型*

```
const e:**{x: number, y: string}** = {x: 1, y: 'text'};
const f = e.x **as number**;
```

💡如果您的变量接受 null 引用，您应该将 null 作为另一种类型添加到您的变量中。

```
const g: **number | null** = null;
```

💡如果你 100%确定你的变量不能为空或未定义，你应该加上**感叹号**，**！**，明确告诉 TS 编译器跳过空值检查。

```
const h**!**: number;
```

## 分配初始值

如果变量设置了初始值，也可以隐含数据类型。

```
const a = 0;     // a is a numberconst b = false; // b is a booleanconst c = 'a';   // c is a stringconst d = {x: 1, y: 'text'} 
// d is an object that has attribute x as number and attribute y as // a string
```

## 析构对象文字

当析构一个对象文本时，也可以用两种方法声明类型:

*   *显式声明*

```
const a = {x: 1, y: undefined}
const {x: **number**} = a;
console.log(x); // 1
```

*   *分配默认值*

```
const a = {x: 1, y: undefined}
const {y = **'text'** } = a;
console.log(y); // 'text'
```

## 声明 void 或返回一些值

对于方法和函数，类型可以在方法签名中设置，也可以通过返回值来暗示。

*   *方法签名*

```
methodA(a: string, b: number): **void** {...}
//methodA doesn't have a return typemethodB(): **string** {...}
//methodB returns a stringmethodC = (a: string, b: number): **number** => {...}
//methodC returns a number
```

*   返回值

```
methodD(a: string, b: number) {
  **return 'text'**;
} 
//methodD returns a stringmethodE = (a: string, b: number) => **b > 0**
//methodE returns a boolean
```

# 结论

数据类型在编程中的重要性不可低估，必须始终如一地遵循，以保持应用程序更安全和更易维护。希望这篇文章能带来一个不同的视角，关于启用严格模式，以及为什么从长远来看强制数据类型会对开发人员有所帮助。

*更多内容看* [***说白了. io***](http://plainenglish.io)