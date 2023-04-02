# 什么是 WebAssembly，为什么它很重要？

> 原文：<https://javascript.plainenglish.io/what-is-webassembly-and-why-does-it-matter-2c1e5b5da60a?source=collection_archive---------7----------------------->

![](img/ae2019fd47d498181a64edcaa0971728.png)

WebAssembly logo by [Carlos Baraza](https://github.com/carlosbaraza/web-assembly-logo)

在过去的几年里，在 web 和其他领域有很多关于 WebAssembly 的讨论。如果你以前没有听说过，它是一种类似汇编语言的语言。它几乎可以在任何地方运行，包括 web、移动、桌面和服务器。很多语言都支持编译到 WebAssembly，比如 C/C++ (Emscripten)、Rust、Go (TinyGo)。其他的有解释器/JIT 编译器，可以编译成 WebAssembly，像 Python (Pyodide)和 C#。在 web 上和本机代码中使用它有很多好处，这将在后面讨论。首先，让我们回顾一下 WebAssembly 和其他类似东西的历史。

# 沙盒 web 运行时的历史

在网络发展之初，Java 非常流行，并且发展迅速。为了帮助人们在网络上使用 Java 和其他语言，浏览器引入了 Java 小程序。Java 小程序允许人们在网上使用 Java 和其他语言编写脚本。因为不可信的网站可以运行代码，所以它是沙箱化的，这意味着它是隔离的和安全的。然而，它需要一个浏览器之外的外部插件，并且对于小应用程序来说很笨重，所以另一种为网络构建的语言 JavaScript 应运而生。

随着 Java 和 Java 小程序开始衰落，JavaScript 开始流行起来。最终，因为它没有很好地集成到 web 中，并且有许多缺陷，Java 小程序被从大多数浏览器中删除。JavaScript 成为 web 上唯一的语言，虽然它运行良好，但它从未对其他语言的编码提供很大的支持，并且它的性能也不是最理想的。

2013 年，一个新的 JavaScript 子集诞生了，它被设计成可以快速运行，并且可以在多种语言中使用。它被称为 ASM . js。ASM . js 是为 web 实现低级汇编的一个很好的实验，但是还可以做一些改进。

为了修复 asm.js 的一些问题，比如更快的解析，2017 年发布了 WebAssembly。它很快获得了流行和浏览器的支持。目前，它受 Chrome、Edge、Firefox、Safari 等支持。

# WebAssembly 到底是什么？

WebAssembly 类似于 Assembly，只是它是跨平台的、隔离的，并且可以在浏览器中运行。许多人将其与 JVM 字节码相比较，JVM 字节码是 Java、Scala 和 Kotlin 等语言使用的跨平台字节码。

但是，也有一些不同之处。首先，WebAssembly 被设计成完全沙盒化和隔离的，不像 JVM。JVM 可以沙箱化，Java 小程序已经展示了这一点，但是因为 JVM 在设计时没有考虑到这一点，所以要困难得多。另一方面，WebAssembly 从一开始就是为此而设计的，所有主要的 WebAssembly 编译器/运行时都是沙箱化的。

此外，WebAssembly 内置于 web 中，比 JVM 更轻量级。你甚至可以使用像 [Wasmer](https://wasmer.io/) 这样的编译器提前将你的代码编译成一个非常小的可执行文件。

最后，WebAssembly 内置于 web 中，而不需要在 web 中使用插件。

# WebAssembly 的功能

## 支持多种语言

![](img/1dab07341cb58e43c0e23b5d374e6120.png)

Photo by [Graham Holtshausen](https://unsplash.com/@freedomstudios?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

WebAssembly 与本机汇编或 JVM 一样，可以与许多不同的语言一起工作。有些语言，比如 Rust 和 Go，天生支持编译成目标正确的 WebAssembly。其他的，像 C/C++，TypeScript 和 Swift，可以用另一个编译器编译成 WebAssembly。最后，有些语言不能直接编译成 WebAssembly，但是它们的运行时可以编译成 WebAssembly，比如 Python 和 C#。只需做一点工作，您就可以将更多的语言编译成 WebAssembly，因为许多编译器使用 LLVM，可以使用 Emscripten 将 LLVM 编译成 WebAssembly。

## 沙盒和安全

![](img/d3ef638f17fb8c3782e43b203ddc72a7.png)

Photo by [Markus Winkler](https://unsplash.com/@markuswinkler?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

默认情况下，WebAssembly 是完全沙箱化和隔离的，确保 WebAssembly 代码不能访问运行时不希望它访问的内容，即使您不使用容器或虚拟机。根据您使用的运行时，您可以测量 WebAssembly 脚本占用多少 RAM 和 CPU，并允许它访问有限的文件系统。这种沙盒结合提前将 WebAssembly 编译成本机代码，使得快速运行低开销的沙盒代码成为可能。

## 跨平台

![](img/066c5a48e24e1c2e19362b48e34a02af.png)

Photo by [AltumCode](https://unsplash.com/@altumcode?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

因为 WebAssembly 被设计成 web 的一部分，所以它是跨平台的，可以在所有现代浏览器上运行。它还可以编译到许多不同的平台上。WebAssembly 可以在桌面、移动和 web 上完全运行，无需太多工作。它甚至可以在具有特定运行时的平台上实现接近本机的性能。

# 如何使用 WebAssembly

## 在浏览器中运行 WebAssembly

大多数浏览器都支持 WebAssembly。你只需要`import()`或`fetch()`模块，然后运行`WebAssembly.instantiate(bytes, importObject)`。

Example usage of WebAssembly from MDN

关于如何在浏览器中使用 WebAssembly 和 JavaScript 的更多信息，这里有一个很好的 MDN 页面。

## 本机运行 WebAssembly

这有点复杂，但仍然不是很难。有许多不同的低开销 WebAssembly 解释器和编译器。最受欢迎的两个是 [Wasmtime](https://wasmtime.dev/) 和 [Wasmer](https://wasmer.io/) 。Wasmer 比 Wasmtime 有一些优势，比如支持 LLVM 后端以更快地执行代码，支持更多的语言。

然而，Wasmtime 得到了字节码联盟的支持，字节码联盟是一群像 Google 和 Mozilla 这样的公司，它们是 WebAssembly 的领导者。这完全取决于你需要什么，而且像 Lucet 这样的选择更多，所以在决定之前，你要对主题进行自己的研究。我推荐的一点是，如果你需要使用 WebAssembly 编译器 API，你可以使用 Rust 来构建本地使用 WebAssembly 的应用程序。许多流行的 WebAssembly 工具都内置了 Rust，所以使用相同的语言是最容易的。

# 结论

WebAssembly 是一种非常有前途的语言，它将继续发展和改进。希望你对 WebAssembly 有所了解，感谢阅读。

# WebAssembly 资源

## 语言编译器

Rust — [Wasm Bindgen](https://github.com/rustwasm/wasm-bindgen)

Go — [Wasm GOARCH](https://golang.org/cmd/go/#hdr-Environment_variables)

C/C++ — [Emcscripten](https://emscripten.org/)

斯威夫特— [斯威夫特 WASM](https://swiftwasm.org/)

C#-[Blazor](https://dotnet.microsoft.com/apps/aspnet/web-apps/blazor)用于 web 应用程序，或者[native aut](https://github.com/dotnet/runtimelab/tree/feature/NativeAOT)用于提前实验性地编译 c#到多个目标，包括 WASM

Python — [Pyodide](https://pyodide.org/en/stable/)

TypeScript—[AssemblyScript](https://www.assemblyscript.org/)(注意:与 TypeScript 语法相同，但 assembly script 使用的类型略有不同)

Java 或其他 JVM 语言— [JWebAssembly](https://github.com/i-net-software/JWebAssembly) 或 [TeaVM](https://github.com/konsoletyper/teavm)

哈斯克尔——阿斯特留斯

## 本机编译器的 web 程序集

[Wasmtime](https://wasmtime.dev/)

瓦斯默

[朗讯](https://github.com/bytecodealliance/lucet)

[Wasm2C](https://github.com/WebAssembly/wabt/blob/main/wasm2c/README.md)

[Wasm 微运行时](https://github.com/bytecodealliance/wasm-micro-runtime)

(更多精彩尽在[牛逼的 WASM 运行时](https://github.com/appcypher/awesome-wasm-runtimes)

## 其他的

[向导](https://github.com/bytecodealliance/wizer) —预初始化 WASM 模块

[binary en](https://github.com/WebAssembly/binaryen)——一组用于 WASM 的工具，其中一些已经提到过了

[牛逼的 WASM](https://github.com/kanaka/awesome-wasm)

[牛逼的 WASM 工具](https://github.com/vshymanskyy/awesome-wasm-tools)

[牛逼的 WASM 郎](https://github.com/appcypher/awesome-wasm-langs)

[超棒的 WASM 运行时间](https://github.com/appcypher/awesome-wasm-runtimes)

*更多内容看* [***说白了. io***](http://plainenglish.io/)