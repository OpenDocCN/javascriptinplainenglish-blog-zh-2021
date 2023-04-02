# 为反应式表单设置值的 6 种不同方式

> 原文：<https://javascript.plainenglish.io/6-different-ways-to-set-values-for-reactive-forms-a0686f3dca0a?source=collection_archive---------2----------------------->

## 角度基础备忘单 2021

## 如何设置数组的值？

![](img/efaae083ed0571c1b54aba6cdc8dfc27.png)

Photo by [inlytics | LinkedIn Analytics Tool](https://unsplash.com/@inlytics?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们可以在应用程序中每天使用反应式表单，因为它们支持不可变的特性、简单的错误处理和单元测试编写能力。

你知道在表单中设置值的所有方法吗？

> 在这篇文章中，我将介绍所有可以用来为单个表单控件或表单设置值的方法。

## 1.设置值()

```
this.testform.get("testcontrol").setValue(100);
```

我们也可以用不同的方法来控制。

```
this.testform.controls["testcontrol"].setValue(200);
```

## 2.patchValue()

```
this.testform.get('testcontrol').patchValue(testdata.id);this.testform.controls['testcontrol'].patchValue(testdata.id);
```

如果你想让表单自己找出补丁，我们可以这样做。

```
this.testform.patchValue({ testcontrol: testdata.id });
```

## 3.修补值可以与对象一起工作，如果响应对象中的键与表单控件匹配，则它将直接更新值。

```
this.testform.patchValue({
    "testcontrol": testdata.id,
    "desc": "testdata value"
});
```

## 4.如果响应中的键不同，并且您希望在补丁之前正确映射，那么…

```
const { key1, key2} = response;//response from service

this.testForm.patchValue({
  key1,
  key2
});
```

***或者我们可以创建一个新的对象本身并把它传递给表单。***

```
let obj = Object.assign({}, this.testform.getRawValue(), someClass);this.testform.patchValue(obj);
```

## 5.处理表单数组

我已经创建了一个表单数组，并尝试以这种方式修补它

```
this.testform = this._fb.group({
    test: this._fb.array([])
});let testformArray = this.testform.get('test') as FormArray;for (let i of [0, 1, 2, 3]) {
    testformArray.push(new FormControl(false));
}
const data = ['atit', 'patel', 'form', 'array'];testformArray.patchValue(data);}
```

# 准备面试？查看角度面试问题 2021

[](/top-100-questions-you-must-prepare-for-your-next-angular-interview-1-10-3e13d5fefab9) [## 你必须为下一次角度面试准备的 100 个问题(1-10)

### 最常见的角度面试问题 2021

javascript.plainenglish.io](/top-100-questions-you-must-prepare-for-your-next-angular-interview-1-10-3e13d5fefab9) [](/top-100-questions-you-must-prepare-for-to-ace-your-next-angular-interview-10-20-c3f5ab854be) [## 为赢得下一次面试，你必须准备的 100 个问题(10-20)

### 最常见的角度面试问题 2021

javascript.plainenglish.io](/top-100-questions-you-must-prepare-for-to-ace-your-next-angular-interview-10-20-c3f5ab854be) 

# 你可以看看我以前的文章

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)