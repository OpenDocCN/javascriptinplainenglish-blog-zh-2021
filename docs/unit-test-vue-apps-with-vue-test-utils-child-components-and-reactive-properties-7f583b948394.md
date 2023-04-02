# 使用 Vue 测试工具对 Vue 应用进行单元测试——子组件和反应属性

> 原文：<https://javascript.plainenglish.io/unit-test-vue-apps-with-vue-test-utils-child-components-and-reactive-properties-7f583b948394?source=collection_archive---------8----------------------->

![](img/7d1f74ff3a8c17f8f3cd0cd72dbbf02a.png)

Photo by [Caleb Woods](https://unsplash.com/@caleb_woods?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有了 Vue Test Utils 库，我们可以轻松地为 Vue 应用编写和运行单元测试。

在本文中，我们将看看如何用 Vue Test Utils 库编写单元测试。

# 从子组件发出事件

我们可以检查在子组件中发出的事件。

为此，我们调用`mount`来安装父组件和子组件。

然后我们可以在孩子身上发出我们想要的事件:

```
import { mount } from '@vue/test-utils'const ChildComponent = {
  template: `
    <div>
      <p>child</p>
    </div>
  `,
}const ParentComponent = {
  template: `
    <div>
      <child-component @custom="onCustom" />
      <p id='emitted' v-if="emitted">emitted</p>
    </div>
  `,
  data() {
    return { emitted: false }
  },
  methods: {
    onCustom() {
      this.emitted = true
    }
  },
  components: {
    ChildComponent
  }
}describe('ParentComponent', () => {
  it('shows emitted when child-component emits custom event', async () => {
    const wrapper = mount(ParentComponent)
    await wrapper.findComponent(ChildComponent).vm.$emit('custom')
    expect(wrapper.find('#emitted').text()).toContain('emitted')
  })
})
```

为了用`ParentComponent`挂载`ParentComponent`的子组件，我们调用`mount`方法。

`findComponent`方法将`ChildComponent`作为参数，这样我们可以使用返回的组件包装器通过`$emit`方法发出`custom`事件。

然后，为了检查“发出的”文本是否显示，我们调用`find`方法来检查它是否有`'emitted'`字符串。

# 操纵组件状态

我们可以用`setData`或`setProps`方法操作组件状态。

例如，我们可以写:

```
import { mount } from '@vue/test-utils'const Counter = {
  template: `
    <div>
      <p>{{count}}</p>
    </div>
  `,
  data() {
    return { count: 0 }
  },
}describe('Counter', () => {
  it('renders 10 for count', async () => {
    const wrapper = mount(Counter)
    await wrapper.setData({ count: 10 })
    expect(wrapper.find('p').text()).toContain(10)
  })
})
```

用我们想要设置的数据调用`setData`方法。

键是反应性属性的键，值是其值。

要设置道具，我们可以使用`setProps`方法:

```
import { mount } from '@vue/test-utils'const Foo = {
  template: `
    <div>
      <p>{{foo}}</p>
    </div>
  `,
  props: ['foo']
}describe('Foo', () => {
  it('renders bar for foo prop', async () => {
    const wrapper = mount(Foo)
    await wrapper.setProps({ foo: 'bar' })
    expect(wrapper.find('p').text()).toContain('bar')
  })
})
```

我们调用`setProps`方法将`foo`属性的值设置为`'bar'`。

然后我们检查它是否在测试的最后一行被渲染。

当我们安装组件时，也可以设置道具:

```
import { mount } from '@vue/test-utils'const Foo = {
  template: `
    <div>
      <p>{{foo}}</p>
    </div>
  `,
  props: ['foo']
}describe('Foo', () => {
  it('renders bar for foo prop', async () => {
    const wrapper = mount(Foo, {
      propsData: {
        foo: 'bar'
      }
    })
    expect(wrapper.find('p').text()).toContain('bar')
  })
})
```

`mount`方法的第二个参数使用`propsData`属性让我们模拟道具。

# 结论

我们可以在测试中模仿道具并设置反应属性的值，然后测试它们。

子组件事件也可以从父组件进行测试。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**