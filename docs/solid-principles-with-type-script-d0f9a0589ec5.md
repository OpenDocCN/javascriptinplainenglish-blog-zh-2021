# 具有脚本类型的坚实原则

> 原文：<https://javascript.plainenglish.io/solid-principles-with-type-script-d0f9a0589ec5?source=collection_archive---------3----------------------->

## SOLID Principle 是一种编码标准，由 Robert C Martin 提出，并在整个面向对象编程领域得到实践。

![](img/1ba3ea47cc79c70ad0f6cfbceeb43c85.png)

TypeScript

## **什么是固体原理？**

在软件设计中，SOLID 是五个设计原则的首字母缩略词，所有开发人员都应该对这五个原则有一个清晰的概念，以便正确地开发软件，避免糟糕的设计。当开发人员正确应用坚实的原则时，它会使您的代码更具可扩展性、逻辑性和可读性。

五项坚实的原则是:

1.**单一责任原则:**每个类应该只有一个责任，或者一个类的改变不应该有一个以上的原因。

2.**开-闭原则:**对象应该对扩展开放，对修改关闭。

3.Liskov 替换原则:子类应该可以替换它们的超类。

4.**接口分离原则:**许多特定于客户端的接口比一个通用接口要好。

5.**依赖倒置原则:**依赖抽象，不依赖具体化。

## **单一责任原则**

```
Every class should have only one responsibility or There should not be more than one reason for a class to change.
```

假设我们有一个学校管理系统，它有不同的部门，例如，数学，英语，计算工资的文学，报告和教学时间。

```
class Department {
 public calculatePay (): number {
 // implement algorithm for Mathematics, English, Literature
 }
 public reportHours (): number {
 // implement algorithm for  Mathematics, English, Literature
 }
public techingHours (): Promise<any> {
 // implement algorithm for  Mathematics, English, Literature
 }
}
```

在上面的例子中，如果你看到我们编写了一个类来计算一个类中的工资、报告和教学时间，这显然违反了 SRP。

请查看下面**单一责任原则的实现。**

```
abstract class Employee {
 // This needs to be implemented
 abstract calculatePay (): number;
 // This needs to be implemented
 abstract reportHours (): number;
 // let’s assume THIS is going to be the 
 // same algorithm for each employee- it can
 // be shared here.
 protected teachingHours (): Promise<any> {
 // common teachingHours algorithm
 }
}class Math extends Employee {
  calculatePay (): number {
    // implement own algorithm
  }
  reportHours (): number {
    // implement own algorithm
  }

  teachingHoursHours (): number {
    // implement own algorithm
  }
}class Accounting extends Employee {
  calculatePay (): number {
    // implement own algorithm
  }
  reportHours (): number {
    // implement own algorithm
  }
 teachingHoursHours (): number {
    // implement own algorithm
  }}class IT extends Employee {
  calculatePay (): number {
    // implement own algorithm
  }
  reportHours (): number {
    // implement own algorithm
  }
   teachingHoursHours (): number {
    // implement own algorithm
  }
}
```

## **开闭原理**

```
**A Software object should be open for extension but closed for modification**
```

根据这种方法，软件对象应该对扩展开放，但对修改关闭。让我们举一个例子我们要计算矩形和圆形的面积，所以我们编写了下面的代码:

```
class Rectangle {
  public width: number;
  public height: number;
  constructor(width: number, height: number) {
    this.width = width;
    this.height = height;
  }
}
class Circle {
  public radius: number;
  constructor(radius: number) {
    this.radius = radius;
  }
}
function calculateAreasOfMultipleShapes(
  shapes: Array<Rectangle | Circle>
) {
  return shapes.reduce(
    (calculatedArea, shape) => {
      if (shape instanceof Rectangle) {
        return calculatedArea + shape.width * shape.height;
      }
      if (shape instanceof Circle) {
        return calculatedArea + shape.radius * Math.PI;
      }
    },
    0
  );
}
```

如果我们想计算一个新形状的面积，那么我们必须修改上面的代码**calculatareasofmultipleshapes()**来适应这些变化。

我们可以通过遵循 SOLID 原则来避免上述情况。请查看下面的代码:

```
interface Shape {
  getArea(): number;
}
class Rectangle implements Shape {
  public width: number;
  public height: number;
  constructor(width: number, height: number) {
    this.width = width;
    this.height = height;
  }
  public getArea() {
    return this.width * this.height;
  }
}
class Circle implements Shape {
  public radius: number;
  constructor(radius: number) {
    this.radius = radius;
  }
  public getArea() {
    return this.radius * Math.PI;
  }
}
```

## **利斯科夫替代原则**

```
Sub classes should be substitutable for their super classes.
```

这个原则是芭芭拉·利斯科夫在 1980 年提出的。如果我们用最简单的方式来解释，那就是我们应该能够用一个物体和另一个物体交换。我们可以通过使用一个**接口**和一个**抽象** **类来实现这个原理。**

## **界面偏析原理**

```
**Many Client specific interfaces are better than one general purpose interface.**
```

如果我们用最简单的方式来定义这个原则，那就是防止软件对象依赖其他它们不需要的对象，我们可以通过使用**接口**和**抽象类来实现这个原则。**

假设我们有三个不同的**用户**类，它们在同一个操作类上使用三个不同的，每个用户类依赖于两个额外的操作，这是我们不需要的。

## **依存倒置原则**

**依赖倒置原则**建议在我们的高层和低层对象之间引入一个抽象层，这样高层和低层对象就不应该互相依赖；相反，高级和低级对象都依赖于抽象层。

让我们讨论下面的例子:

```
 interface person {
  introduceSelf(): void;
}class doctor implements Person {
  public introduceSelf() {
    console.log('I am a Doctor');
  }
}class itEngineer implements Person {
  public introduceSelf() {
    console.log('I am an IT Engineer');
  }
}
```

上面的例子在理论上和学术上是正确的，但是在介绍的实时实现中可能是复杂的，我们可能需要为它创建一个单独的服务，如下:

```
interface introductionService {
  introduce(): void;
}
class introduceShelf implements introductionService {
  public introduce() {
    console.log('I am an engineer');
  }
}
class Engineer implements Person {
  private introductionService = new introduceShelf();
  public introduceSelf() {
    this.introductionService.introduce();
  }
}
```

不幸的是，上面的代码打破了依赖反转原则，我们应该反转 **Engineer** 和**intruse shelf**object 之间的依赖，如下所示:

```
class engineer implements person {
  public introductionService: EngineerIntroductionService;

  constructor(introductionService: IntroductionService) {
    this.introductionService = introductionService;
  }

  public introduceSelf() {
    this.introductionService.introduce();
  }
}
const engineer = new Engineer(new EngineerIntroductionService());
```

有了上面的代码，我们不需要为 **Engineer** 和**I Engineer**类创建任何子类。

```
public introductionService: IntroductionService;

  constructor(introductionService: IntroductionService) {
    this.introductionService = introductionService;
  }
  public introduceSelf() {
    this.introductionService.introduce();
  }
}
const engineer = new Person(new EngineerIntroductionService());
const itEngineer= new Person(new itEngineerIntroductionService());
```

上面的代码是一个**合成而不是继承的例子。这使得我们的类更容易进行单元测试，因为我们可以很容易地在构造函数中注入服务。**

通过上面的例子，我们已经学会了通过使用 TypeScript 来实现 SOLID 原理的不同原理。

***亲爱的读者，感谢您的支持和您宝贵的时间。我希望这是有用的，并有助于发现角度应用的基础。如果你喜欢这篇文章并在评论中留下你的想法，请鼓掌。***

***请关注我并成为会员在*** [***中******获取更多文章。干杯！！***](https://medium.com/@technicadil_001/membership)