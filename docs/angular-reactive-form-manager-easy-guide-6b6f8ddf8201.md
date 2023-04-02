# 角度反应式表单管理器—简易指南

> 原文：<https://javascript.plainenglish.io/angular-reactive-form-manager-easy-guide-6b6f8ddf8201?source=collection_archive---------8----------------------->

## 使用表单管理器服务将大表单拆分成小的可重用表单组组件的简单解决方案。

![](img/c83609460a229fdfb52bc45138066fd5.png)

Photo by [Luca Bravo](https://unsplash.com/@lucabravo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

最近我在做一个大的 Angular 项目，它需要实现两个反应式表单，其中一个需要被分成单独的选项卡组件。所以我寻找一种解决方案，将表单分成更小的表单组，并在所有表单中重用它们。此外，我需要找到一种方法从不同的选项卡组件收集表单组值，并将它们合并成一个值。

所以，我想到了一个主意！我们需要实现一个表单管理器服务，来处理不同的表单组，并在一个大表单中管理它们的验证和值。这个想法很简单，创建带有表单组的组件(可以在表单之间重用)，并在表单管理器中注册每个表单组(每个表单有一个唯一的名称)。这样，您可以从应用程序中的任何地方访问这些表单组，并将多个表单组视为一个大表单。

一开始听起来可能很难，但实际上，这很容易实现。让我们看看我们是怎么做的。

首先，我们来做两个更小的表单组。为了简单起见，我不会展示模板代码。

因此，第一个表单组将包含客户姓名、姓氏和电话号码字段。

```
@Component({
  selector: 'app-client-form-group',
  templateUrl: './client-form-group.component.html',
  styleUrls: ['./client-form-group.component.less'],
})
export class ClientFormGroupComponent implements OnInit, OnDestroy {
  @Input() formName: string; formGroup: ForumGroup;constructor(formManager: FormManagerService, formBuilder: FormBuilder) {
    this.formGroup = this.buildForm(formBuilder );
  } ngOnInit(): void {
    this.formManager.register(this.formName, this.formGroup);
  }

  ngOnDestroy(): void {
    this.formManager.unregister(this.formName);
  } buildFormGroup(formBuilder: FormBuilder): FormGroup {
    return formBuilder.group({
      name: [],
      surname: [],
      phone: [],
    });
  }
}
```

第二个表单组将有两个字段:地址和邮政编码。

```
@Component({
  selector: 'app-address-form-group',
  templateUrl: './address-form-group.component.html',
  styleUrls: ['./address-form-group.component.less'],
})
export class AddressFormGroupComponent implements OnInit, OnDestroy {
  @Input() formName: string; formGroup: ForumGroup;constructor(formManager: FormManagerService, formBuilder:  FormBuilder) {
    this.formGroup = this.buildFormGroup(formBuilder);
  } ngOnInit(): void {
    this.formManager.register(this.formName, this.formGroup);
  }

  ngOnDestroy(): void {
    this.formManager.unregister(this.formName);
  } buildFormGroup(formBuilder: FormBuilder): FormGroup {
    return formBuilder.group({
      address: [],
      postCode: [],
    });
  }
}
```

让我们更深入地研究一下这段代码将会做什么。所以首先我们需要输入表单组名。表单组将在我们的表单管理器服务中以该名称注册。

```
@Input() name: string;
```

接下来，我们注入表单管理器(稍后解释)和 Angular 表单生成器。我们调用 buildFormGroup 方法来构建表单，并将结果保存为 FormGroup 类属性。

```
constructor(formManager: FormManagerService, formBuilder:  FormBuilder) {
  this.formGroup = this.buildFormGroup(formBuilder);
}
```

我们的方法 buildFormGroup 只是简单地使用 Angular form builder 构建反应式表单。

```
buildFormGroup(formBuilder: FormBuilder): FormGroup {
  return formBuilder.group({
    address: [],
    postCode: [],
  });
}
```

我们使用角度生命周期方法在初始化时将表单组注册到某个表单下的表单管理器服务，并在组件销毁时取消注册。

```
ngOnInit(): void {
  this.formManager.register(this.name, this.formGroup);
}

ngOnDestroy(): void {
  this.formManager.unregister(this.name);
}
```

好了，现在我们有了两个独立的表单组组件，可以很容易地在任何更大的表单中重用。让我们看看我们如何能做到这一点。为此，我们需要实现一个简单的表单管理器服务，将所有独立的组保存为一个表单。

```
@Injectable()
export class FormManagerService {
  private formGroup = new FormGroup({}); get(): FormGroup {
    return this.formGroup;
  }  register(name: string, formGroup: FormGroup): void {
    this.formGroup.addControl(name, formGroup);
  } unregister(name: string): void {
    this.formGroup.removeControl(name);
  }
}
```

现在，我们可以简单地将客户端和地址表单组组件插入到应用程序的不同位置，并提供唯一的名称，这样它们就可以在表单管理器服务中注册。

```
...<app-client-form-group name="clientFormGroup"><app-client-form-group/>...<app-address-form-group name="addressFormGroup"><app-address-form-group/>...
```

在需要访问完整表单数据或其控件的地方，我们可以从表单管理器中获取表单。

```
...constructor(private formManager: FormManagerService) {}...submit(): void {
  const form = this.formManager.get();

  if(form.valid) {
    form.value; // Get value and do something with it
  }
}...
```

## 结论

这是一个非常简单的例子，只是为了展示表单管理器的概念，您还可以为存储在表单管理器中的表单结构添加类型，为表单组组件添加额外的逻辑和验证器，使用异步方法来跟踪表单管理器中的表单更改，等等。

但是，通过这种简单而优雅的方式，您可以轻松地将大表单分成更小的可重用组件，并使用表单管理器服务将这些小组件组合成一个大表单。

这使您可以轻松地管理组件、统一的表单验证、统一的表单值，并且可以在应用程序的任何地方轻松访问表单。