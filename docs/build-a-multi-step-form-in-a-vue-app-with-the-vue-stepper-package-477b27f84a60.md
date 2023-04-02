# 使用 vue-stepper 包在 Vue 应用程序中构建多步表单

> 原文：<https://javascript.plainenglish.io/build-a-multi-step-form-in-a-vue-app-with-the-vue-stepper-package-477b27f84a60?source=collection_archive---------7----------------------->

![](img/3bff00619d39b7f1aacc5bc79df7ef1c.png)

Photo by [Yusuf Evli](https://unsplash.com/@yusufevli?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

要在 Vue 应用中轻松构建多步表单，我们可以使用 vue-stepper 包来帮助我们。

在本文中，我们将了解如何使用 vue-stepper 包将多步表单添加到我们的应用程序中。

# 装置

要安装库，我们运行:

```
npm i vue-stepper
```

# 创建多步表单

为了创建一个多步表单，我们需要一个容器组件。

此外，我们需要一个组件来显示步骤内容。

例如，我们可以写:

`App.vue`

```
<template>
  <div id="app">
    <horizontal-stepper
      :steps="demoSteps"
      @completed-step="completeStep"
      @active-step="isStepActive"
      @stepper-finished="alert"
    ></horizontal-stepper>
  </div>
</template><script>
import HorizontalStepper from "vue-stepper";
import StepOne from "./components/StepOne";
import StepTwo from "./components/StepTwo";export default {
  name: "App",
  components: {
    HorizontalStepper
  },
  data() {
    return {
      demoSteps: [
        {
          icon: "mail",
          name: "first",
          title: "Step 1",
          subtitle: "Step 1",
          component: StepOne,
          completed: false
        },
        {
          icon: "report_problem",
          name: "second",
          title: "Step 2",
          subtitle: "Step 2",
          component: StepTwo,
          completed: false
        }
      ]
    };
  },
  methods: {
    completeStep(payload) {
      this.demoSteps.forEach(step => {
        if (step.name === payload.name) {
          step.completed = true;
        }
      });
    },
    isStepActive(payload) {
      this.demoSteps.forEach(step => {
        if (step.name === payload.name) {
          if (step.completed === true) {
            step.completed = false;
          }
        }
      });
    },
    alert(payload) {
      alert("end");
    }
  }
};
</script>
```

`StepOne.vue`

```
<template>
  <div>
    <input placeholder="email" v-model="email" @input="onChange">
  </div>
</template><script>
export default {
  data() {
    return {
      email: ""
    };
  },
  beforeMount(){
    if (this.email){
      this.$emit("can-continue", { value: true });
    }
  },
  methods: {
    onChange() {
      this.$emit("can-continue", { value: true });
    }
  }
};
</script>
```

`StepTwo.vue`

```
<template>
  <div>
    <input placeholder="problem" v-model="problem" @input="onChange">
  </div>
</template><script>
export default {
  data() {
    return {
      problem: ""
    };
  },
    beforeMount(){
    if (this.problem){
      this.$emit("can-continue", { value: true });
    }
  },
  methods: {
    onChange() {
      this.$emit("can-continue", { value: true });
    }
  }
};
</script>
```

在`App.vue`中，我们有步骤的容器。

该模板具有`horizontal-stepper`组件，该组件具有表单的图标、标题和副标题。

当我们单击 next 时，会发出`completed-step`事件。

`active-step`是我们转到不同步骤时发出的。

当所有步骤完成时，发出`stepper-finished`。

`StepOne.vue`和`StepTwo.vue`是我们的步骤组件。

我们用数组`demoSteps`中的`component`属性将它们设置为内容。

当我们在输入中键入一些内容时，就会发出`input`事件。

当发出`input`方法时，运行`onChange`方法，因此发出`can-continue`事件。当它与一个属性设置为`true`的对象一起发出时，下一步按钮被激活。

现在我们可以继续其他步骤。

一旦我们单击 Finish 按钮，就会发出`stepper-finished`事件，我们可以看到一个警告，因为`alert`方法正在运行。

# 结论

我们可以使用 vue-stepper 包将多步表单添加到我们的 Vue 应用程序中。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**