# 将 JavaScript 整合到 Rust 应用中

> 原文：<https://javascript.plainenglish.io/embed-javascript-in-rust-3f7d66221f52?source=collection_archive---------1----------------------->

*WasmEdge 融合了 Rust 的性能和 JavaScript 的易用性*

![](img/e0a6252d7a5bbf708e1d65bc97fb47f7.png)

Photo by [Mohammad Rahmani](https://unsplash.com/@afgprogrammer?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/rust-javascript?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

在我的[上一篇文章](/running-javascript-in-webassembly-883ec71438e1)中，我讨论了如何在 WebAssembly 沙箱中运行 JavaScript 程序。 [WasmEdge 运行时](https://github.com/WasmEdge/WasmEdge)为云原生 JavaScript 应用程序提供了一个轻量级、高性能和 OCI 兼容的“容器”。

然而，JavaScript 是一种“慢”语言。使用 JavaScript 的原因主要是因为它的易用性和开发效率，尤其是对于初学者。另一方面，WebAssembly 能够运行用 Rust 等语言编写的高性能应用程序。有没有结合 JavaScript 和 Rust 的解决方案？WasmEdge 提供了两个世界中最好的东西。

有了 [WasmEdge 和 QuickJS](https://github.com/second-state/wasmedge-quickjs/) ，开发者现在可以混合搭配这两种强大的语言来创建应用程序。它是这样工作的。

*   应用本身是用 Rust 写的，编译成 WebAssembly。它可以作为一个 wasm 字节码文件进行编译和部署。它可以通过 Docker Hub、CRI-O 和 k8s 等符合 OCI 标准的容器工具进行管理。
*   JavaScript 程序嵌入在 Rust 应用程序中。JavaScript 源代码可以在编译时包含，也可以在运行时通过文件、STDIN、网络请求甚至函数调用包含。这允许 JavaScript 程序由不同于 Rust 程序的开发人员编写。
*   Rust 程序可以处理应用程序中的计算密集型任务，而 JavaScript 程序可以处理“业务逻辑”。例如，Rust 程序可以为 JavaScript 程序准备数据。

接下来，我们来看几个例子。查看[wasmedge-quick js](https://github.com/second-state/wasmedge-quickjs/)Github repo，并转到`examples/embed_js`文件夹继续跟进。

```
$ git clone https://github.com/second-state/wasmedge-quickjs
$ cd examples/embed_js
```

您必须安装 [Rust](https://www.rust-lang.org/tools/install) 和 [WasmEdge](https://github.com/WasmEdge/WasmEdge/blob/master/docs/install.md) 来构建和运行本文中的示例。

`embed_js`演示展示了如何在 Rust 中嵌入 JavaScript 的几个不同的例子。您可以构建并运行所有示例，如下所示。

```
$ cargo build --target wasm32-wasi --release
$ wasmedge --dir .:. target/wasm32-wasi/release/embed_js.wasm
```

# 你好 WasmEdge

下面的 Rust 函数 [main.rs](https://github.com/second-state/wasmedge-quickjs/blob/main/examples/embed_js/src/main.rs) 在编译时嵌入了一行 JavaScript 程序。

```
fn js_hello(ctx: &mut Context) {
    let code = r#"print('hello quickjs')"#;
    let r = ctx.eval_global_str(code);
    println!("return value:{:?}", r);
}
```

由于嵌入式 JavaScript 程序不返回任何内容，您将看到如下执行结果。

```
hello quickjs
return value:UnDefined
```

# 返回值

当然，嵌入式 JavaScript 程序可以向 Rust 程序返回值。

```
fn run_js_code(ctx: &mut Context) {
    let code = r#"
      let a = 1+1;
      print('js print: 1+1=',a);
      'hello'; // eval_return
    "#;
    let r = ctx.eval_global_str(code);
    println!("return value:{:?}", r);
}
```

返回值是一个字符串`hello`。运行这个 Rust 程序的输出如下。注意，在 Rust 中，JavaScript 字符串值被包装在`JsString`中。

```
js print: 1+1= 2
return value:String(JsString(hello))
```

# 调用嵌入式 JavaScript 函数

从 Rust 程序中，您可以调用一个 JavaScript 函数，传入调用参数，并捕获返回值。第一个例子展示了如何将一个 Rust 字符串传递给一个 JavaScript 函数。

```
fn run_js_function(ctx: &mut Context) {
    let code = r#"
      (x)=>{
          print("js print: x=",x)
      }
    "#;
    let r = ctx.eval_global_str(code);
    if let JsValue::Function(f) = r {
        let hello_str = ctx.new_string("hello");
        let mut argv = vec![hello_str.into()];
        let r = f.call(&mut argv);
        println!("return value:{:?}", r);
    } ...
}
```

来自`ctx.eval_global_str(code)`的值`r`是一个映射到 JavaScript 函数的 Rust 函数。您可以调用 Rust 函数，并从调用 JavaScript 函数中获得预期的结果。

```
js print: x= hello
return value:UnDefined
```

您还可以将一个数组从 Rust 传递给 JavaScript 函数，并让 JavaScript 函数返回值。

```
fn run_js_function(ctx: &mut Context) {
    ... let code = r#"
      (x)=>{
          print("\nx=",x)
          let old_value = x[0]
          x[0] = 1
          return old_value
      }
    "#;
    let r = ctx.eval_global_str(code);
    if let JsValue::Function(f) = r {
        let mut x = ctx.new_array();
        x.set(0, 0.into());
        x.set(1, 1.into());
        x.set(2, 2.into()); let mut argv = vec![x.into()];
        println!("argv = {:?}", argv);
        let r = f.call(&mut argv);
        println!("return value:{:?}", r);
    }
}
```

结果如下。

```
argv = [Array(JsArray(0,1,2))]
x= 0,1,2
return value:Int(0)
```

# 使用 JavaScript 模块

嵌入式 JavaScript 程序可以将外部 JavaScript 文件作为模块加载。`examples/embed_js_module`项目展示了这个用例。 [async_demo.js](https://github.com/second-state/wasmedge-quickjs/blob/main/examples/embed_js_module/async_demo.js) 文件包含一个带有导出函数的 JavaScript 模块，我们将导入该模块并在嵌入式 JavaScript 中使用。

```
import * as std from 'std'async function simple_val (){
    return "abc"
}export async function wait_simple_val (a){
    let x = await simple_val()
    print("wait_simple_val:",a,':',x)
    return 12345
}
```

Rust 程序源代码按照 ES 规范的要求异步导入 [async_demo.js](https://github.com/second-state/wasmedge-quickjs/blob/main/examples/embed_js_module/async_demo.js) 模块。执行结果`p`是一个 Rust `Promise`，它将在异步函数返回后具有正确的值。Rust 中的`ctx.promise_loop_poll()`调用一直等到异步执行完成。然后我们可以从`Promise`接收返回值。

```
use wasmedge_quickjs::*;fn main() {
    let mut ctx = Context::new(); let code = r#"
      import('async_demo.js').then((demo)=>{
        return demo.wait_simple_val(1)
      })
    "#; let p = ctx.eval_global_str(code);
    ctx.promise_loop_poll();
    println!("after poll:{:?}", p);
    if let JsValue::Promise(ref p) = p {
        let v = p.get_result();
        println!("v = {:?}", v);
    }
}
```

结果如下。

```
wait_simple_val: 1 : abc
after poll:Promise(JsPromise([object Promise]))
v = Int(12345)
```

# 下一步是什么

在 Rust 中嵌入 JavaScript 是创建高性能云原生应用的一种强大方式。在下一篇文章中，我们将研究另一种方法:[使用 Rust 实现 JavaScript API](https://www.secondstate.io/articles/embed-rust-in-javascript/)。它允许 JavaScript 开发人员利用 WasmEdge 运行时中的高性能 Rust 函数。

本系列文章:

*   [用 WasmEdge 在 WebAssembly 中运行 JavaScript](https://www.secondstate.io/articles/run-javascript-in-webassembly-with-wasmedge/)
*   [将 JavaScript 整合到 Rust 应用中](https://www.secondstate.io/articles/embed-javascript-in-rust/)
*   [使用 Rust 创建高性能的 JavaScript APIs】](https://www.secondstate.io/articles/embed-rust-in-javascript/)
*   [从 JavaScript 调用本地函数](https://www.secondstate.io/articles/call-native-functions-from-javascript/)

云原生 WebAssembly 中的 JavaScript 仍然是下一代云和边缘计算基础设施中的新兴领域。我们才刚刚开始！如果您感兴趣，请加入我们的 [WasmEdge](https://github.com/WasmEdge/WasmEdge) 项目(或者通过提出功能请求问题告诉我们您想要什么)。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)