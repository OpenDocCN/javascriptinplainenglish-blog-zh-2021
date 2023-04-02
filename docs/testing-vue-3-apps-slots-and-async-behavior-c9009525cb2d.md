# 测试 Vue 3 应用—插槽和异步行为

> 原文：<https://javascript.plainenglish.io/testing-vue-3-apps-slots-and-async-behavior-c9009525cb2d?source=collection_archive---------11----------------------->

![](img/d258d3700aa08904bc62218b59d2430f.png)

Photo by [CDC](https://unsplash.com/@cdc?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

随着应用程序变得越来越复杂，自动测试它们变得非常重要。我们可以通过单元测试做到这一点，然后我们就不必手动测试所有的东西了。

在本文中，我们将通过编写一个简单的应用程序并测试它来看看如何测试 Vue 3 应用程序。

# 使用渲染功能测试插槽

我们可以用渲染函数和单文件组件来测试插槽。

例如，我们可以写:

`Header.vue`

```
<template>
  <div>Header</div>
</template>
```

`example.spec.js`

```
import { mount } from '[@vue/test-utils](http://twitter.com/vue/test-utils)'
import { h } from 'vue'
import Header from './Header.vue'const Layout = {
  template: `
    <div>
      <header>
        <slot name="header" />
      </header>
      <main>
        <slot name="main" />
      </main>
      <footer>
        <slot name="footer" />
      </footer>
    </div>
  `
}test('layout full page layout', () => {
  const wrapper = mount(Layout, {
    slots: {
      header: Header,
      main: h('div', 'Main Content'),
      footer: '<div>Footer</div>'
    }
  }) expect(wrapper.html()).toContain('<div>Header</div>')
  expect(wrapper.html()).toContain('<div>Main Content</div>')
  expect(wrapper.html()).toContain('<div>Footer</div>')
})
```

我们有带几个插槽的`Layout`组件。

我们还添加了一个测试，通过使用单个文件组件作为头的填充槽来测试它。

`main`槽填充了一个渲染函数。

`h`是一个渲染组件的函数。第一个参数是标记名，第二个参数是 div 的内容。

`footer`有一个 HTML 字符串作为它的值。

然后我们用`expect`调用检查它的内容。

# 作用域插槽

我们可以用 Vue 测试工具测试作用域插槽。

例如，我们可以写:

```
import { mount } from '@vue/test-utils'const ComponentWithSlots = {
  template: `
    <div class="scoped">
      <slot name="scoped" v-bind="{ msg }" />
    </div>
  `,
  data() {
    return {
      msg: 'world'
    }
  }
}test('scoped slots', () => {
  const wrapper = mount(ComponentWithSlots, {
    slots: {
      scoped: `<template #scoped="params">
        Hello {{ params.msg }}
        </template>
      `
    }
  })
  expect(wrapper.html()).toContain('Hello world')
})
```

我们的`ComponentWithSlots`组件有一个名为`scoped`的插槽。

它向父对象公开了`msg`属性。

在测试中，我们将其呈现在`template`标签中。

我们在测试的最后一行检查呈现的内容。

# 异步行为

我们可以在测试中测试异步行为。

例如，我们可以写:

```
import { mount } from '@vue/test-utils'const Counter = {
  template: `
    <div>
      <p>Count: {{ count }}</p>
      <button @click="handleClick">Increment</button>
    </div>
  `,
  data() {
    return {
      count: 0
    }
  },
  methods: {
    handleClick() {
      this.count += 1
    }
  }
}test('increments by 1', async () => {
  const wrapper = mount(Counter)
  await wrapper.find('button').trigger('click')
  expect(wrapper.find('p').text()).toMatch('Count: 1')
})
```

我们安装`Counter`组件。

然后我们得到`button`并在其上触发`click`事件。

然后我们检查`p`元素的文本，看看它是否是我们所期望的。

等价地，我们可以写:

```
import { mount } from '@vue/test-utils'
import { nextTick } from 'vue'const Counter = {
  template: `
    <div>
      <p>Count: {{ count }}</p>
      <button @click="handleClick">Increment</button>
    </div>
  `,
  data() {
    return {
      count: 0
    }
  },
  methods: {
    handleClick() {
      this.count += 1
    }
  }
}test('increments by 1', async () => {
  const wrapper = mount(Counter)
  wrapper.find('button').trigger('click')
  await nextTick()
  expect(wrapper.find('p').text()).toMatch('Count: 1')
})
```

我们以同样的方式触发按钮上的 click 事件。

但是我们调用`nextTick`来等待最新的`count`被渲染。

然后我们可以用同样的方法做检查。

# 结论

我们可以在 Vue 3 组件中测试命名和限定范围的插槽。

此外，我们可以测试异步行为，如组件中触发的点击。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)