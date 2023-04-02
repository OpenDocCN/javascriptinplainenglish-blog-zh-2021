# 理解固体:依赖倒置原则

> 原文：<https://javascript.plainenglish.io/understanding-solid-dependency-inversion-principle-ea271d5a53cd?source=collection_archive---------8----------------------->

## **依赖倒置原则是软件设计和开发的标准指导规则之一，以确保松耦合组件和组件可扩展性**

![](img/5d1fa55f277942c85e1643c927402fa6.png)

# 依赖倒置原理是什么？

依赖倒置原则声明我们需要依赖抽象而不是具体的实现。

# **什么是系统耦合？**

系统耦合被定义为系统中一个项目对另一个项目的约束状态。耦合发生在上下文信息上。例如，在空调中，压缩机被称为耦合到内部冷却制冷剂和冷却机构，因为这些部件一起构成冷却系统的整体。

# **紧耦合和松耦合的组件？**

联轴器有两种类型:**紧联轴器**和**松联轴器**。这些指的是在存在某个组件/模块的替代品的情况下，系统将如何反应。

在我们之前的例子中，如果空调的冷却机制与压缩机“紧密耦合”，那么其他公司制造的压缩机替代品**极有可能完全破坏冷却机制**。这是紧耦合组件系统的一个例子。紧密耦合的组件有具体的硬编码实现。

松耦合与上述示例中的*正好相反*，用一个功能相似但*构造* / *实现*不同的系统进行替换，将确保系统按照上述方式工作。

# **现在让我们看一个代码示例**

根据我们之前的类比，我们定义一个简单的**空调**类:

```
class CompressorV1 { constructor() { console.log(“Compressor V1”); } setup() { // perform some necessary setup task } turnOn() { this.setup(); // function code }} class AirConditioner { private compressor: Compressor = new CompressorV1(); constructor() {} public powerOn() { this.compressor.turnOn(); }}
```

**CompressorV1** 对象是该**空调**类中的**直接依赖**。如果根据我们的类比进行新的修改，这将破坏**空调**类，因为它没有办法扩展功能以与新的压缩机类型一起运行。在没有实现依赖性反转原则的情况下，如果新的压缩机 **CompressorV2** 被引入空调，这将是代码的未来快照:

```
class CompressorV2 { constructor() { console.log(“Compressor V2”); } setup() { // perform some necessary setup task } turnOn() { this.setup(); // function code }} class AirConditioner { private compressor: Compressor = new CompressorV1(); private compressor2: CompressorV2 = new CompressorV2(); constructor(private activeCompressor = 1) {} public powerOn() { if (activeCompressor == 1) { this.compressor.turnOn(); } else { this.compressor2.turnOn(); } }}
```

## 问题突然变得很明显。

代码**在添加大量不同的组件后将无法很好地扩展**，这些组件是**空调**级中的核心依赖项，将来可能需要被替换。而且即使组件不需要替换，以这种方式使用 **if-else** 块对生产代码也不好。众所周知，代码执行过程中遇到的决策分支越多，执行速度就越慢。

# **控制反转(IoC)**

从上面的例子中，我们看到 **AirConditioner** 类负责实例化和管理 compressor 对象。这导致了一种乏味的代码模式，每次引入新的**压缩机**时，都需要有人修改**空调**类来支持新的**压缩机**类型。

然而，让我们换个角度来看。我们没有让**空调**类来处理压缩机对象的生命周期，而是定义了一个*抽象*压缩机接口来为**空调**处理生命周期。我们将这个接口命名为 **ICompressor** (在前面加一个 **I** 只是接口的命名约定)。

你会问，为什么要有一个**接口**？接口允许我们*定义*一个特定类型的函数*，而不需要实际实现它*。因此，我们定义了一个压缩器的接口，它具有“设置”和“打开”的声明，但没有它的定义。

```
interface ICompressor { setup(config?: any): any; turnOn(): any;}
```

每个 compressor 类现在都会实现这个接口。产生的代码:

```
class CompressorV1 implements ICompressor { constructor() { console.log(“CompressorV1 is in system”); } setup(config?: any): any { // perform the very same setup tasks in this interface function } turnOn(): void { // same function code }}class CompressorV2 implements ICompressor { constructor() { console.log(“Compressor V2 is in system”); } setup(config?: any): any { // perform the same necessary setup task } turnOn(): void { // same function code as before }}
```

此外，**空调**级采用这种优雅的界面设计，看起来干净多了:

```
class AirConditioner { constructor(private compressor: ICompressor) {} public powerOn() { this.compressor.turnOn(); }}
```

如果我们现在运行我们的程序，它看起来是这样的:

```
class Main { static main(args: string[]): Number { const ac: AirConditioner = new AirConditioner(new CompressorV1()); ac.powerOn(); }}
```

我们刚才所做的被称为**控制反转**。这个过程消除了**空调**对**压缩机**类的依赖性。因此，概括地说，我们通过引入一个*甚至更高层次的抽象* ( **ICompressor** )，使**反转了**依赖控制流**，其中更高层次的模块(**空调**类)依赖于更低层次的模块(**压缩机 V1** / **压缩机 V2** 类)。**

# **再举一个例子**

在我们上面的空调案例中，引入复杂行为并不罕见。假设出现了第三种类型的压缩器，我们也需要在我们的 ACs 中提供对这种压缩器的支持。但是这个压缩器的设置过程有点不同。与前两种类型完全离线设置过程不同，这种类型有一个远程连接模块，需要在压缩机启动之前配置该模块，以便进行压缩机系统资源监控。

因此，第三个压缩器具有不同的内部设置行为，因为它依赖异步请求来完成其设置任务。

由于现在采用了更高层次的实现方式，这种新型压缩机可以非常容易地集成到我们的空调中。我们简单地以下面的方式实现了另外一个 **Compressor** 类，但是这次 **turnOn** 函数被实现为 **async** 函数。这是一个完全有效的修改，因为接口只关心函数的签名，从不关心函数是如何实现的。

```
class SmartCompressor implements ICompressor { constructor() { console.log(“Smart Compressor is in system”); } loadConfiguration(): any { //function to load connection configuration } setup(config?: any): Promise<any> { // perform the same necessary setup task } async turnOn(): void { const configObject = loadConfiguration(); try { await this.setup(configObject); // function code to turn on compressor } catch (err) { // catch error if connection fails console.log(err.message); } }}
```

尽管这次设置压缩器的过程非常不同，但是依赖反转确保了这个新添加的组件不需要对我们的系统进行完全的重新迭代(注意，这次我们甚至不需要使用我们的**空调**类)，从而节省了我们的时间和精力。借助于依赖倒置原则，这个系统现在已经被转换成一个松散耦合的系统。

# **结论**

总之，这就是**依赖倒置原则**陈述并打算实现的内容。显而易见，松耦合架构是如何以及为什么支持这一原则，以及为什么它会出现在 **S.O.L.I.D** 软件设计原则的列表中。

*更多内容请看*[***plain English . io***](http://plainenglish.io)