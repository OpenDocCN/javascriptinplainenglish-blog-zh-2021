# 使用 Vue 测试工具对 Vue 应用进行单元测试——模拟项目

> 原文：<https://javascript.plainenglish.io/unit-test-vue-apps-with-vue-test-utils-mocking-items-b78833cde4?source=collection_archive---------8----------------------->

![](img/c16eec3a578fc89fb6f805036a7221cb.png)

Photo by [Helena Hertz](https://unsplash.com/@imperiumnordique?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有了 Vue Test Utils 库，我们可以轻松地为 Vue 应用编写和运行单元测试。

在本文中，我们将看看如何用 Vue Test Utils 库编写单元测试。

# 模拟注射

当我们挂载组件时，我们可以通过在`mocks`属性中传递它们来模仿注入的反应属性。

例如，我们可以写:

```
import { mount } from '@vue/test-utils'const Foo = {
  template: `
    <div>
      <p>{{$route.path}}</p>
    </div>
  `,
}const $route = {
  path: '/foo',
}test('should render the path', () => {
  const wrapper = mount(Foo, {
    mocks: {
      $route
    }
  })
  expect(wrapper.text()).toContain('/foo')
})
```

我们只是将`$route`属性设置为`mocks`对象中的`$route`对象，然后我们应该会看到它被渲染。

# 存根组件

我们可以通过使用`stubs`属性来编写存根全局组件:

```
import { mount } from '@vue/test-utils'const Foo = {
  template: `
    <div>
      <child-component></child-component>
    </div>
  `,
}test('should render child-component', () => {
  const wrapper = mount(Foo, {
    stubs: ['child-component']
  })
  expect(wrapper.find('child-component')).toBeTruthy()
})
```

我们在`Foo`中有没有注册的`child-component`，所以我们可以通过使用`stubs`属性用一个空组件来存根它。

# 测试按键、鼠标和其他 DOM 事件

我们可以用`trigger`方法触发组件上的事件。

例如，我们可以写:

```
import { mount } from '@vue/test-utils'const MyButton = {
  template: `
    <button @click='count++'>
      {{count}}
    </button>
  `,
  data() {
    return {
      count: 0
    }
  }
}test('shows latest count when button is clicked', async () => {
  const wrapper = mount(MyButton)
  await wrapper.trigger('click')
  expect(wrapper.text()).toContain('1');
})
```

我们挂载`MyButton`组件，并在返回的组件包装器上调用`trigger`。

然后我们可以用`text`方法检查`count`的最新值。

例如，我们可以写:

```
import { mount } from '@vue/test-utils'const MyButton = {
  template: `
    <div>
      <button @click='count++'>
        add
      </button>
      <p>{{count}}</p>
    </div>
  `,
  data() {
    return {
      count: 0
    }
  }
}test('shows latest count when button is clicked', async () => {
  const wrapper = mount(MyButton)
  await wrapper.find('button').trigger('click')
  expect(wrapper.find('p').text()).toContain('1');
})
```

用添加按钮创建`MyButton`组件。

当我们点击它时，它更新了`count`。

为了测试它，我们调用`find`来查找按钮。然后我们调用`trigger`来触发`click`事件。

然后我们用选择器`'p'`调用`find`来检查 p 元素的内容。

我们可以检查在元素上触发事件时是否调用了方法。

例如，我们可以写:

```
import { mount } from '@vue/test-utils'const Foo = {
  template: `
    <div>
      <button class="yes" @click="callYes">Yes</button>
      <button class="no" @click="callNo">No</button>
    </div>
  `,
  props: {
    callMe: {
      type: Function
    }
  },
  methods: {
    callYes() {
      this.callMe('yes')
    },
    callNo() {
      this.callMe('no')
    }
  }
}test('should call callMe with the right arguments when buttons are clicked', async () => {
  const spy = jest.fn();
  const wrapper = mount(Foo, {
    propsData: {
      callMe: spy
    }
  })
  await wrapper.find('button.yes').trigger('click')
  expect(spy).toHaveBeenCalledWith('yes');
  await wrapper.find('button.no').trigger('click')
  expect(spy).toHaveBeenCalledWith('no');
})
```

我们有一个`Foo`组件，它将一个`callMe`函数作为道具。

然后为了编写我们的测试，我们通过调用`jest.fn()`创建了一个`callMe`函数的 spy。

接下来，我们将它作为一个道具传递给我们 mount `Foo`。

最后，我们调用`trigger`来触发按钮上的点击，并检查渲染结果。

获取我们期望的函数的参数。

# 结论

我们可以用 Jest 和 Vue 测试工具模拟组件中的各种项目。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**