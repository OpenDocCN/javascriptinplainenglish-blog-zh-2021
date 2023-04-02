# 使用 Vue 测试工具对 Vue 应用进行单元测试——键盘和鼠标事件

> 原文：<https://javascript.plainenglish.io/unit-test-vue-apps-with-vue-test-utils-keyboard-and-mouse-events-26e77d73399f?source=collection_archive---------11----------------------->

![](img/15899ce8015c31072f6802255864c80b.png)

Photo by [Aryan Dhiman](https://unsplash.com/@mylifeasaryan_?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有了 Vue Test Utils 库，我们可以轻松地为 Vue 应用编写和运行单元测试。

在本文中，我们将看看如何用 Vue Test Utils 库编写单元测试。

# 键盘事件测试

我们可以在代码中测试键盘事件。

例如，我们可以写:

```
import { mount } from '@vue/test-utils'const KEY_DOWN = 40
const KEY_UP = 38
const ESCAPE = 27const QuantityComponent = {
  template: `
    <div>
      <input type="text" [@keydown](http://twitter.com/keydown).prevent="onKeydown" v-model="quantity" />
    </div>
  `,
  data() {
    return {
      quantity: 0
    }
  },
  methods: {
    increment() {
      this.quantity += 1
    },
    decrement() {
      this.quantity -= 1
    },
    clear() {
      this.quantity = 0
    },
    onKeydown(e) {
      if (e.keyCode === ESCAPE) {
        this.clear()
      }
      if (e.keyCode === KEY_DOWN) {
        this.decrement()
      }
      if (e.keyCode === KEY_UP) {
        this.increment()
      }
      if (e.key === 'a') {
        this.quantity = 10
      }
    }
  },
  watch: {
    quantity(newValue) {
      this.$emit('input', newValue)
    }
  }
}describe('Key event tests', () => {
  it('Quantity is zero by default', () => {
    const wrapper = mount(QuantityComponent)
    expect(wrapper.vm.quantity).toBe(0)
  }) it('Up arrow key increments quantity by 1', async () => {
    const wrapper = mount(QuantityComponent)
    await wrapper.find('input').trigger('keydown.up')
    expect(wrapper.vm.quantity).toBe(1)
  }) it('Down arrow key decrements quantity by 1', async () => {
    const wrapper = mount(QuantityComponent)
    wrapper.vm.quantity = 2
    await wrapper.find('input').trigger('keydown.down')
    expect(wrapper.vm.quantity).toBe(1)
  }) it('Escape sets quantity to 0', async () => {
    const wrapper = mount(QuantityComponent)
    wrapper.vm.quantity = 3
    await wrapper.find('input').trigger('keydown.esc')
    expect(wrapper.vm.quantity).toBe(0)
  }) it('Magic character "a" sets quantity to 10', async () => {
    const wrapper = mount(QuantityComponent)
    await wrapper.find('input').trigger('keydown', {
      key: 'a'
    })
    expect(wrapper.vm.quantity).toBe(10)
  })
})
```

在每次测试中触发键盘事件。

`QuantityComponent`有一个输入元素，它监听`keydown`事件并相应地更新`quantity`。

`onKeydown`方法更新`quantity`反应属性，根据按下的键设置值。

在我们的测试中，我们用`find`方法获得了`input`元素。

然后我们调用`trigger`来触发各种`keydown`事件。

`keydown.up`模拟按下向上箭头。

`keydown.up`模拟按下向下箭头。

`keydown.up`模拟按下 esc 键。

最后一个测试模拟按下`'a'`键。

一旦我们这样做了，我们就可以检查`quantity`的反应属性以获得最终结果。

# 测试异步行为

我们可以使用与上一个例子相同的原理来测试异步行为。

例如，我们可以写:

```
import { mount } from '@vue/test-utils'const Counter = {
  template: `
    <div>
      <button @click='count++'>add</button>
      <p>{{count}}</p>
    </div>
  `,
  data() {
    return {
      count: 0
    }
  },
}describe('Counter tests', () => {
  it('count is set to 1 after click', async () => {
    const wrapper = mount(Counter)
    expect(wrapper.text()).toContain('0')
    const button = wrapper.find('button')
    await button.trigger('click')
    expect(wrapper.text()).toContain('1')
  })})
```

我们有一个`Counter`组件，当我们单击 add 按钮时，它会更新`count` reactive 属性。

然后在我们的测试中，我们用`text`方法检查呈现的内容。

然后我们点击按钮，再次进行检查。

# 结论

我们可以在测试中模拟点击和键盘事件，并测试呈现的内容。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**