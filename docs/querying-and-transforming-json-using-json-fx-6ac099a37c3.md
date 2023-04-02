# 使用 JSON-fx 查询和转换 JSON

> 原文：<https://javascript.plainenglish.io/querying-and-transforming-json-using-json-fx-6ac099a37c3?source=collection_archive---------17----------------------->

![](img/0ae8a0b25b3c2631282a127b830dc372.png)

**JSON-fx** 是 JavaScript 的对象查询和转换引擎。它定义了一种直观的声明性语法，用于将输出值表示为一个或多个输入值的函数。

用例可以包括任何场景，其中 JSON 数据的值查询或整个 JSON 对象的转换最好通过运行时配置实现，而不是硬编码到应用程序逻辑中。

JSON-fx 表达式嵌入在称为模板的 JSON 对象中，模板在运行时被解析和编译成表达式树。这些是它们执行的本地 JavaScript 代码的高效轻量级包装器。该库包括大量内置函数和操作符，并且易于扩展。

JSON-fx 核心库包括解析器/编译器和一组内置函数，没有外部运行时依赖性，占用空间非常小。

# 装置

像许多现代 JavaScript 库一样，JSON-fx 是作为 NPM 包分发的。将 JSON-fx 安装到 Node.js 项目或使用 NPM 的现代浏览器客户端项目(如 Angular 或 React 项目)中:

```
npm install @mindsung/json-fx
```

# 简单的例子

这将在后面解释，但是让我们从一个非常简单的例子开始，这个例子演示了这个库的基本用法。

```
import { JsonFx } from "@mindsung/json-fx";const myInput = { n1: 10, n2: 5, s: "world!" };const myTemplate = {
  mySum: "$.n1 + $.n2",
  myText: "'Hello, ' + $.s"
};const fx = new JsonFx();
const compiled = fx.compile(myTemplate);
const output = compiled.evaluate({ name: "$", value: myInput });
```

产生输出:

```
{
  mySum: 15,
  myText: "Hello, world!"
}
```

# 模板输入

模板评估通常包括一个或多个输入值。通常，只有一个输入，通常命名为`"$"`，如上面的基本用法示例所示。但是，可以提供任意数量的指定输入值。这些输入变量名必须以`"$"`开头，可以是任何类型。例如:

```
const inputs = [{
  name: "$myInput",
  value: 1000
}, {
  name: "$myOtherInput",
  value: {
    someProp: {
      anEvenDeeperProp: "some value"
    }
  }
}];
const output = compiled.evaluate(...inputs);
```

然后，所有输入都可以通过它们在模板中的变量名来引用:

```
{
  anOutputProp: "$myInput / 2",
  anotherOutputProp: "$myOtherInput.someProp.anEvenDeeperProp + ' was input'"
}
```

这将产生以下输出:

```
{
  anOutputProp: 500,
  anotherOutputProp: "some value was input"
}
```

# 模板表达式语法

模板可以由任何有效的 JavaScript 值或对象组成。模板可以是简单的单个常量值(当然，这是没有用的，因为不会发生任何类型的转换或计算)，或者单个 JSON-fx 字符串表达式，或者复杂的 JSON-fx 对象表达式。

# 字符串表达式

顾名思义，JSON-fx 字符串表达式是一个字符串值，它包含一个或多个函数调用和/或操作符，结果只产生一个输出值或对象。在编译模板时，JSON-fx 运行时将对其进行解析，从而创建一个高效的表达式树，可以根据任意数量的不同输入值对其进行评估。

```
const template = "math~floor($.someNumber / 10) % 10";
const compiled = fx.compile(template);
const input = {
  name: "$",
  value: { someNumber: 1234 }
};
const output1 = compiled.evaluate(input);
// output1 = 3
input.value = { someNumber: 2468 };
const output2 = compiled.evaluate(input);
// output2 = 6
```

在这个例子中，输入`$`是包含单个属性`someNumber`的对象。模板字符串定义了一个 JSON-fx 表达式`math~floor($.someNumber / 10) % 10`，它使用整数除法和模数运算符有效地输出了`$.someNumber`的十位数。模板被传递给`fx.compile(...)`，后者将字符串转换成编译后的表达式。接下来，`compiled.evaluate(input)`对提供的输入执行表达式并返回结果，在本例中是数字`3`。然后，输入的值被改变，表达式被再次计算，这次结果是数字`6`。

# 函数和运算符

函数调用是任何 JSON-fx 字符串表达式的核心组件。所有字符串表达式本质上都是一个或多个函数求值的组合。偶数运算符是一种语法快捷方式，表示对关联函数的调用。例如，表达式`$a + $b`只是函数调用`add($a, $b)`的简写表示。

在 JSON-fx 表达式中，可以使用标准 JavaScript 函数调用语法调用函数，即函数名、左括号、逗号分隔的参数和右括号。

`add($a, $b)`

也可以使用中缀`:`运算符将函数链接到其他值、函数或表达式:

`$a:add($b)`相当于`add($a, $b)`

左边的值`$a`被隐式传递给`add($b)`作为第一个参数，取代其他参数。当将函数调用链接在一起时，中缀运算符在许多情况下可以提供更好的清晰度:

`toString(add($a, $b))`最好表述为`add($a, $b):toString()`，甚至`$a:add($b):toString()`

如果右边的函数只需要一个参数(由左边的操作数隐式提供)，则可以省略括号:

`$a:add($b):toString`

一组全面的内置 JSON-fx 函数提供了核心功能，公开并扩展了许多最有用的 JavaScript 函数。此外，通过向`JsonFx`类构造函数传递一组定义，可以注入扩展函数和操作符来扩展模板语言。

[点击这里查看所有 JSON-fx 内置函数和操作符](https://github.com/mindsung/json-fx/tree/develop/json-fx/src/fx/functions)

# 扩展功能

函数定义是一个具有两个属性的对象，`name`和`evaluate`。`name`属性是将在表达式中使用的函数名，`evaluate`属性是 JavaScript 函数定义。(JSON-fx 函数定义也可能包含一个`operator`属性，参见 JSON-fx 源代码中的示例。自定义扩展函数通常不包含运算符定义，因为大多数常用的运算符符号已经被内置函数使用。)

```
const fx = new JsonFx([
  {
    name: "addFive",
    evaluate: n => n + 5
  }
]);
```

# 值文字

字符串表达式可能包含值文字，包括数值、字符串和布尔值。数字文字不需要任何特殊的符号。字符串文字必须包含在单引号`'`中。布尔值可以是`true`或`false`。此外，可以使用特殊值`null`和`undefined`。

使用开/闭方括号`[]`，数组文字也可以嵌入到字符串表达式中。

```
const template = "(1.5 + 3):toString + ['hello', 2, true, null]:first";
```

在对任何输入进行评估时产生值`"4.5hello"`(该表达式不包含输入变量)。

# 属性访问器点标记法

与 JavaScript 和许多其他编程语言一样，在字符串表达式中使用点符号来访问对象属性。

```
const compiled = fx.compile("$.someProp.someDeeperProp");
const output = compiled.evaluate({
  name: "$",
  value: {
    someProp: {
      someDeeperProp: "hello"
    }
  }
});
```

产生输出`"hello"`

# 空条件运算符

JSON-fx 定义了一个内置的空条件操作符，该操作符允许许多模板看起来更清晰、更易读，并避免使用频繁、冗长的条件逻辑来检查和处理空值。空条件运算符`?`可以在任何属性点访问器或函数调用之前内联使用。如果紧接在`?`符号之前的表达式的值为空或未定义，表达式将返回空。

```
const template = "$.someProp?.someMissingProp?:substr(0, 3)?:toUpperCase";
```

当针对任何输入`$`进行评估时，如果输入值不包括属性`someProp`或属性`someProp.someMissingProp`，则表达式将愉快地返回 null 值，而不是抛出运行时错误。当输入对象可能具有不同的结构或可选属性时，这种行为特别有用。

# 匿名(λ)函数

有些函数需要的参数本身就是函数，例如 array `find`函数，它需要一个谓词函数的参数，并查找数组中与指定函数检查的条件相匹配的第一个成员。当调用这样的函数时，函数类型参数可以使用匿名函数或 lambda 语法来表达。

与许多编程语言一致，JSON-fx lambda 语法由一个或多个函数参数变量组成，这些变量必须以`"$"`开头，后面是`=>`，再后面是一个表达式。如果声明了多个参数，逗号分隔的参数列表必须用括号括起来。当只声明一个参数时，括号是可选的。

```
const template = "[2, 4, 6, 8]:find(($n) => $n > 5)"
```

当对任何输入进行评估时，产生值`6`。

# 对象表达式

JSON-fx 对象表达式提供了一种强大的方法，通过它可以转换和查询几乎任何复杂性的对象。对象表达式是一个 JavaScript 对象，包括表示 JSON-fx 变量声明、JSON-fx 运行时用户定义函数声明和输出的某种组合的属性。对象的每个属性值可以是常量(单值、对象或数组)、JSON-fx 字符串表达式或另一个 JSON-fx 对象表达式。

除了下面讨论的带有特殊符号的属性，对象的所有属性也将出现在结果输出值中。

```
const compiled = fx.compile({
  someProp: "$ + 1",
  anotherProp: {
    deeperProp: "$ * 2"
  }
});
const output = compiled.evaluate({ name: "$", value: 5 });
```

产出产值`{ someProp: 6, anotherProp: { deeperProp: 10 } }`

# 变量

除了传递到模板评估中的命名输入变量之外，还可以声明局部变量。对象表达式中的变量是以符号`"$"`开头的属性，可以在后续表达式中的任何地方使用。分配给变量属性的值可以是任何常量或表达式值。

```
const template = {
  "$pi": 3.14159,
  "$radiusSquared": "$radius * $radius", radius: "$radius",
  area: "($pi * $radiusSquared * 100):math~round / 100"
};
```

当使用值为`3`的输入`$radius`进行评估时，将产生`{ radius: 3, area: 28.27 }`

# 运行时用户定义的函数

虽然在行为上类似于扩展和内置函数，但运行时用户定义函数是在表达式模板中声明和实现的。这允许您的模板的功能被进一步扩展，而无需重新构建和重新部署您的应用程序，并且还提供了一种在您的模板中重用表达式逻辑的更紧凑和有效的方法。

对象表达式中的运行时用户定义函数是以符号`"@"`开头的属性，可以在后续表达式中的任何地方使用。从技术上讲，分配给属性的值可以是任何常量或表达式值，尽管只有表达式值才能使函数比变量更有用。类似地，虽然函数参数不是严格必需的，但是没有参数的函数并不比简单地声明一个变量更有优势。与所有 JSON-fx 变量一样，函数参数必须以`"$"`开头。

```
const template = {
  "@rectArea($length, $width)": "$length * $width",
  area: "@rectArea($.length, $.width)"
};
```

当使用值为`{ length: 3, width: 4 }`的输入`$`进行评估时，将产生`{ area: 12 }`。

注意，如上例所示，当调用运行时用户定义的函数时，函数名必须包含开头的`@`符号。

也可以使用用户定义的函数代替 lambda 函数，作为需要函数类型参数的其他函数(内置函数、扩展函数或运行时用户定义的函数)的参数。在这种情况下，函数名，包括`@`，作为参数值传递。

```
const template = {
  "@isBigNumber($n)": "$n >= 100",
  "$numbers": [50, 75, 100, 200],
  firstBigNumber: "$numbers:find(@isBigNumber)"
};
```

当对任何输入进行评估时，产生值`{ firstBigNumber: 100 }`。

# 变量和用户定义的函数范围

对象表达式中任何变量或用户定义函数的作用域是声明它的对象，包括任意级别的内部嵌套对象。因为模板是在计算之前编译的，所以对象上属性的实际声明顺序并不重要。换句话说，只要在相同(或嵌套)的对象范围内，声明变量或用户定义函数的属性就不必在使用之前出现(尽管这通常会提高可读性)。

```
const template = {
  rectInfo: {
    // @rectArea is in scope here because it was declared in
    // the parent object.
    area: "@rectArea($.length, $.width)"
  },
  // Valid to declare @rectArea here, even though it is used
  // above this in the logical property order.
  "@rectArea($length, $width)": "$length * $width"
};
```

# 目标价值提升

除了变量`"$"`和用户定义的函数`"@"`符号，属性名`"()"`(空括号)将该属性的单个值提升为其父属性的值。当需要单个值而不是对象值时，值提升很有用，但通过使用更复杂的对象表达式来获得该值是必要的或有帮助的，因此可以使用变量和/或用户定义的函数。

```
const template = {
  "$pi": 3.14159,
  "@area($radius)": "$pi * $radius:pow(2)",
  "()": "@area($)"
};
```

当使用输入值`3`对上述模板进行评估时，结果只是数字`28.27431`(不是对象)。值提升可用于对象表达式的任何嵌套级别，而不仅仅是模板对象的顶级。

注意，当使用值提升表示法时，除了变量和用户定义的函数声明之外，`"()"`属性必须是对象上唯一的属性。如果在特殊值提升属性旁边的对象表达式中存在其他普通对象属性，将导致编译时错误。

# 结论

JavaScript 空间中有几个工具和库可用于查询和转换 JSON 数据。JSON-fx 旨在提供其他产品所不具备的性能、全面的功能和可扩展性。本文中展示的例子将帮助您入门，但仅仅代表了可能的一小部分。我希望你能够使用这个工具，并从你的工作中获得和我一样多的价值！

*披露:我是* [*JSON-fx 项目*](https://github.com/mindsung/json-fx) *的撰稿人。*