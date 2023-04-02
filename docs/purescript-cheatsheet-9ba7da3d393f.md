# PureScript:编译成 JavaScript 的函数式语言

> 原文：<https://javascript.plainenglish.io/purescript-cheatsheet-9ba7da3d393f?source=collection_archive---------10----------------------->

## PureScript 基础:对象、递归、映射等等

![](img/c951390e1006b2cc80d00a0f26b6652e.png)

我说过我有多爱 PureScript 吗？

该项目完全在 Node.js 上运行，代码被编译成 JavaScript——然而它使用了一种完全不同的编程语言:一种非常类似 Haskell 的语言。

只是在 Haskell 的传统中，PureScript 是一种纯函数式编程语言。正如我之前给出的介绍和安装指南一样，现在我将介绍这门语言的基础知识。

要了解 PureScript 是什么，如何安装和运行它，请查看以下内容:

[](/purescript-3ee759ce05aa) [## 用 PureScript 为 Web 带来强大的函数式编程

### 就像 JavaScript 的 Haskell

javascript.plainenglish.io](/purescript-3ee759ce05aa) 

然后，随时回来学习基础知识。如果您已经安装并运行了 PureScript，没有什么可以阻止我们——让我们学习 PureScript 的基础知识吧！

# 在控制台中打印东西

最强大的调试工具？肯定是主机！然而，由于 PureScript 不是那么容易使用，这可能会感觉很麻烦。让我们揭开主机的神秘面纱。

登录主函数就像这样简单:

```
main = log "Hello World!"
```

默认情况下，log 函数只能接收字符串。变量、数字和所有其他类型需要首先用 show-function 进行转换:

```
main = log (show(10))
```

打印一个函数调用(因此，它的返回值)也是一样的:

```
double x = x * 2

main = log (show (double 2))
```

用于打印的连接可以这样完成:

```
printNumber x = "Number: "<> (show (x)) <> "cool, "main = log (printNumber 2)
```

上面印着:“数字:2 酷，嗯？”。

但是如果登录一个不是主函数的函数呢？
这个有点麻烦。

重要的是要理解登录到控制台是一个副作用。引起副作用会使函数变得不纯，而不纯的函数违背了 PureScript 和 Haskell 的哲学。然而，我们可以从每个函数中记录日志——但是我们需要一个技巧来这样做。

要使用在终端中打印的日志功能，我们需要使用“效果单元”类型。我们可以将函数返回值的类型设置为:

```
saySomething :: String -> Effect UnitsaySomething msg = log msgmain = saySomething "My message"
```

# 记录—就像 JavaScript 对象一样

人们可以将 PureScript 中的记录看作对象。这些对象的行为就像在 JavaScript 中一样。唯一的区别是:记录是不可变的。

在初始化记录之前，最佳实践是首先提供它的类型。

```
type Person =
{ name :: String,
  age :: Int }

max :: Person
max = { name: "Max", age: 22 }

main = log (show max)
```

现在，变量“max”属于“Person”类型，它需要一个名字和一个年龄。main 函数记录该记录，我们可以看到与 JavaScript 中相同的输出:`{ age: 22, name: "Max" }`。

通过点运算符，访问属性也像在 JavaScript 中一样:

`max.name`会返回“Max”。

# 条件式

条件句？是啊，那个如果-否则-的东西。因为 PureScript 是围绕函数进行解析的，所以我们现在只关注它。

以下函数接收两个数字作为参数，并且只返回较大的一个:

```
greatestNum :: Int -> Int -> Int
greatestNum a b =
  *if* a > b
  *then* a
  *else* bmain = log (show (greatestNum 2 4))
```

我们可以将现有条件作为参数传递，而不是在函数体内编写比较:

```
test condition =
  *if* condition
  *then* "true"
  *else* "false"main = log (test(2 > 1))
```

因为 2 大于 1，所以该函数返回“真”。

# 数组

就像记录一样，数组在 PureScript 中是不可变的。

初始化数组的方法不止一种。我们可以使用每一个表达式，它返回一个数组来这样做——任何自定义函数，一个映射，一个过滤器，一个范围，或者只是硬编码的数组。我们来看两种方式。

硬编码:`nums = [1, 2, 3]`

使用范围生成数组:`nums = range 1 3`

两者都生成下面的数组:`[1, 2, 3]`。

确保首先导入必要的包。将此写在您的文件顶部:`import Data.Array`。

串联数组不会改变将被串联的数组。因此，函数返回的都是新数组。关于`concact`的特别之处在于，我们将想要添加的数组传递到一个数组中——结果是一个数组的数组作为函数参数。

```
nums = concat [[1, 2], [3, 4]]-- nums now is: [1, 2, 3, 4] 
```

# 地图和过滤器

这两个函数在函数式编程中都是绝对必要的。这两个函数都根据提供的模式转换数据结构——但是，它们不会改变原始结构。

地图可以想象成 for-each。过滤器可以想象成 for-each，只返回符合我们模式的条目。

让我们用 map 将数字数组中的每个值加倍:

```
map (\n -> n * 2) [1, 2, 3]-- [2, 4, 6]
```

变量“n”代表数组中的每一个值。我们在值翻倍后返回它。如您所见，函数图的第一个参数是我们使用的模式——这个模式就是函数本身。
第二个参数是我们要映射的数组。

让我们为所有偶数筛选一个数组:

```
filter (\n -> mod n 2 == 0) [1, 2, 3, 4, 5, 6]-- [2, 4, 6]
```

Filter 的工作原理是一样的:第一个参数是模式函数，第二个是数组。

# 高级函数概念

正如我在之前的文章中介绍了函数的基础一样，让我们来看看更高级的概念:递归和 do 关键字。

## 递归

所有开发人员都应该知道递归的概念。这是一种编写可读代码的强大技术。在 PureScript 中使用递归并不困难——它严重依赖于条件:

## do 关键字

为了理解这个关键字，让我们构建一个小函数来记录一些东西。由于登录到控制台会使我们的函数不纯，我们必须通过类型来注意这一点:效果单元类型。通过使用它，犯副作用作为回报是允许的。

```
saySomething :: String -> Effect Unit
saySomething n = log nmain = saySomething "My message"
```

这将在控制台中打印“我的消息”。但是如果我们想要做不止一件事呢？比如我们要多次登录？由于我们的函数基本上返回“log”函数，因此多次编写这样的代码是没有用的——函数只能返回一个函数。

do 关键字有助于解决这个问题。突然间，我们可以在“saySomething”的函数体中调用多个函数。

```
saySomething :: String -> Effect UnitsaySomething n = *do* log n
  log "Another message"main = saySomething "My message"
```

这就是 PureScript 的基础知识！

万一你有问题，记住语法和功能:
[这里有一个小的纯脚本备忘单](https://codingcheats.io/purescript/)

感谢您的阅读！

*更多内容尽在*[***plain English . io***](http://plainenglish.io)