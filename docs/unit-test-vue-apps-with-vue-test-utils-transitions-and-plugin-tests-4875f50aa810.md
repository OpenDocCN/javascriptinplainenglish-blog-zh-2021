# 使用 Vue 测试工具对 Vue 应用进行单元测试——过渡和插件测试

> 原文：<https://javascript.plainenglish.io/unit-test-vue-apps-with-vue-test-utils-transitions-and-plugin-tests-4875f50aa810?source=collection_archive---------13----------------------->

![](img/0139b03ddf45d3ac41d1d08edfc5c2dc.png)

Photo by [Green Chameleon](https://unsplash.com/@craftedbygc?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有了 Vue Test Utils 库，我们可以轻松地为 Vue 应用编写和运行单元测试。

在本文中，我们将看看如何用 Vue Test Utils 库编写单元测试。

# 模仿过渡

我们可以像测试其他组件一样测试带有转换的组件。

我们所要做的就是将反应属性设置为我们想要的值。

例如，我们可以写:

```
import { mount } from '@vue/test-utils'const Foo = {
  template: `
    <div>
      <transition>
        <p v-if="show">Foo</p>
      </transition>
    </div>
  `,
  data() {
    return {
      show: true
    }
  }
}describe('Foo', () => {
  it('renders bar for foo prop', async () => {
    const wrapper = mount(Foo)
    expect(wrapper.text()).toMatch(/Foo/)
    await wrapper.setData({
      show: false
    })
    expect(wrapper.text()).not.toMatch(/Foo/)
  })
})
```

我们调用`mount`来安装`Foo`组件。

然后，我们检查在将`show`反应属性设置为`false`之前显示了什么。

然后我们调用`setData`将`show`设置为`false`。

然后我们检查显示内容的模式，用`text`方法返回呈现的文本，用`toMatch`方法检查内容是否匹配给定的正则表达式模式。

我们也可以用`transitionStub`助手来存根化转换:

```
import { mount } from '@vue/test-utils'const Foo = {
  template: `
    <div>
      <transition>
        <p v-if="show">Foo</p>
      </transition>
    </div>
  `,
  data() {
    return {
      show: true
    }
  }
}const transitionStub = () => ({
  render(h) {
    return this.$options._renderChildren
  }
})describe('Foo', () => {
  it('renders bar for foo prop', async () => {
    const wrapper = mount(Foo, {
      stubs: {
        transition: transitionStub()
      }
    })
    expect(wrapper.text()).toMatch(/Foo/)
    await wrapper.setData({
      show: false
    })
    expect(wrapper.text()).not.toMatch(/Foo/)
  })
})
```

`transitionStub`只是一个用`render`方法返回一个对象来模拟渲染过渡的函数。

如果我们安装组件并在安装时设置电抗属性值，我们也可以避免使用`setData`:

```
import { mount } from '@vue/test-utils'const Foo = {
  template: `
    <div>
      <transition>
        <p v-if="show">Foo</p>
      </transition>
    </div>
  `,
  data() {
    return {
      show: true
    }
  }
}test('should render Foo', async () => {
  const wrapper = mount(Foo, {
    data() {
      return {
        show: true
      }
    }
  }) expect(wrapper.text()).toMatch(/Foo/)
})test('should not render Foo', async () => {
  const wrapper = mount(Foo, {
    data() {
      return {
        show: false
      }
    }
  }) expect(wrapper.text()).not.toMatch(/Foo/)
})
```

# 应用全局插件和混合插件

如果我们想要应用全局插件，那么我们必须使用`createLocalVue`来返回一个`Vue`构造函数的模拟版本。

这样，我们可以控制何时应用全局插件。

例如，我们可以写:

```
import { createLocalVue, mount } from '@vue/test-utils'const localVue = createLocalVue()const MyPlugin = {};
MyPlugin.install = function (Vue, options) {
  Vue.prototype.fooMethod = function () {
    this.foo = 'bar';
  }
}localVue.use(MyPlugin);
const Foo = {
  template: `
    <div>
      <p>{{foo}}</p>
    </div>
  `,
  data() {
    return {
      foo: ''
    }
  }
}test('should render bar', async () => {
  const wrapper = mount(Foo, {
    localVue
  })
  await wrapper.vm.fooMethod();
  expect(wrapper.text()).toContain('bar')
})
```

我们调用`createLocalVue`函数来创建`Vue`构造函数的模拟版本。

然后，我们通过定义`MyPlugin`对象并将`fooMethod`实例方法添加到插件中来创建插件。

接下来，我们调用`localVue.use(MyPlugin)`，这样我们就可以用`mount`组件`Foo`添加我们的插件。

然后在我们的测试中，我们在第二个参数`mount`的对象中设置了`localVue`属性。

我们调用我们的`fooMethod`来运行测试。

最后，我们检查文本是否被渲染。

# 结论

我们可以模仿过渡和插件，这样我们就可以用插件做测试。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**