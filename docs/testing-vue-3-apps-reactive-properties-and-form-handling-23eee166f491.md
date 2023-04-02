# 测试 Vue 3 应用程序—反应属性和表单处理

> 原文：<https://javascript.plainenglish.io/testing-vue-3-apps-reactive-properties-and-form-handling-23eee166f491?source=collection_archive---------12----------------------->

![](img/62ab3eae954c263222c15d93bdbb0a29.png)

Photo by [Siora Photography](https://unsplash.com/@siora18?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

随着应用程序变得越来越复杂，自动测试它们变得非常重要。我们可以通过单元测试做到这一点，然后我们就不必手动测试所有的东西了。

在本文中，我们将通过编写一个简单的应用程序并测试它来看看如何测试 Vue 3 应用程序。

# 将数据传递给组件

我们可以将数据传递给组件。

例如，我们可以写:

```
import { mount } from '@vue/test-utils'const Name = {
  template: `
    <div>
      <input v-model="name">
      <div v-if="error">{{ error }}</div>
    </div>
  `,
  props: {
    minLength: {
      type: Number
    }
  },
  computed: {
    error() {
      if (this.name.length < this.minLength) {
        return `Name must be at least ${this.minLength} characters.`
      }
      return
    }
  }
}test('renders an error if length is too short', () => {
  const wrapper = mount(Name, {
    props: {
      minLength: 10
    },
    data() {
      return {
        name: 'short'
      }
    }
  })
  expect(wrapper.html()).toContain('Name must be at least 10 characters')
})
```

我们有一个带有输入字段和错误显示的`Name`组件。

`error` computed 属性检查`name`是否太短，如果太短，则显示一条错误消息。

在测试中，我们将`minLength`道具传递给组件。

而`data`方法设置了`name`无功属性。

然后我们显示错误消息，因为`name`值的长度小于 10。

# 使用`setProps`

我们也可以用`setProps`的方法来设置道具。

例如，我们可以写:

```
import { mount } from '@vue/test-utils'const Show = {
  template: `
    <div>
      <div v-if="show">{{ greeting }}</div>
    </div>
  `,
  props: {
    show: {
      type: Boolean,
      default: true
    }
  },
  data() {
    return {
      greeting: 'Hello'
    }
  }
}test('renders a greeting when show is true', async () => {
  const wrapper = mount(Show)
  expect(wrapper.html()).toContain('Hello')
  await wrapper.setProps({ show: false })
  expect(wrapper.html()).not.toContain('Hello')
})
```

我们测试`Show`组件并检查`'Hello'`是否在组件中呈现。

然后我们调用`setProps`将`show`道具设置为`false`。

然后我们检查`'Hello'`没有被渲染。

# 测试表单处理

我们可以通过与表单元素交互来测试表单处理。

例如，我们可以写:

```
import { mount } from '@vue/test-utils'const EmailInput = {
  template: `
    <div>
      <input type="email" v-model="email">
      <button @click="submit">Submit</button>
    </div>
  `,
  data() {
    return {
      email: ''
    }
  },
  methods: {
    submit() {
      this.$emit('submit', this.email)
    }
  }
}test('sets the value', async () => {
  const wrapper = mount(EmailInput)
  const input = wrapper.find('input')
  await input.setValue('abc@mail.com')
  expect(input.element.value).toBe('abc@mail.com')
})
```

我们有一个带有输入组件的`EmailInput`组件。

然后我们添加一个测试来安装`EmailInput`组件。

然后我们用`find`得到输入。

然后我们调用`input.setValue`来设置它的值。

然后我们用`input.element.value`从输入中得到值。

# 结论

我们可以传入道具的数据，并用 Vue 测试工具测试渲染的 Vue 3 组件。

同样，我们可以用它来测试表单输入。