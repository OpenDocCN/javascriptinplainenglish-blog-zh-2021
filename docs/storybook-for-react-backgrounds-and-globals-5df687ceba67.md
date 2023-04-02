# React 的故事书—背景和全局

> 原文：<https://javascript.plainenglish.io/storybook-for-react-backgrounds-and-globals-5df687ceba67?source=collection_archive---------9----------------------->

![](img/afff9335f73224177ba3e5949c3e3e87.png)

Photo by [Karina lago](https://unsplash.com/@karinalago?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Storybook 让我们可以用各种参数轻松地构建组件原型。

在这篇文章中，我们将看看如何使用 Storybook 来处理 globals。

# 背景

我们可以设置背景工具栏项来添加设置背景的选项。

我们可以通过在`.storybook/preview.js`文件中添加选项来实现这一点:

```
export const parameters = {
  backgrounds: {
    default: 'twitter',
    values: [
      {
        name: 'twitter',
        value: '#00aced'
      },
      {
        name: 'facebook',
        value: '#3b5998'
      },
    ],
  }
}
```

我们设置`backgrounds`属性来设置背景颜色的选择。

`values`有一系列我们可以设定的选择。

`name`是显示在下拉列表中的名称，`value`是背景颜色值。

`default`是选择要显示的名称。

我们也可以选择一组故事。

为此，我们写道:

`src/stories/Button.stories.js`

```
import React from 'react';import { Button } from './Button';export default {
  title: 'Example/Button',
  component: Button,
  argTypes: {
    backgroundColor: { control: 'color' },
  },
  parameters: {
    backgrounds: {
      default: 'twitter',
      values: [
        {
          name: 'twitter',
          value: '#00aced'
        },
        {
          name: 'facebook',
          value: '#3b5998'
        },
      ],
    }
  }
};
```

我们在`parameters`属性内的`Button`故事集中设置背景颜色。

此外，我们可以只为一个故事设置下拉背景色。

为此，我们写道:

`src/stories/Button.stories.js`

```
import React from 'react';import { Button } from './Button';export default {
  title: 'Example/Button',
  component: Button,
  argTypes: {
    backgroundColor: { control: 'color' },
  },
};const Template = (args) => <Button {...args} />;export const Primary = Template.bind({});
Primary.args = {
  primary: true,
  label: 'Button',
};Primary.parameters = {
  backgrounds: {
    default: 'twitter',
    values: [
      {
        name: 'twitter',
        value: '#00aced'
      },
      {
        name: 'facebook',
        value: '#3b5998'
      },
    ],
  }
};
```

也可以将`disable`属性设置为`true`来禁用背景:

```
import React from 'react';import { Button } from './Button';export default {
  title: 'Example/Button',
  component: Button,
  argTypes: {
    backgroundColor: { control: 'color' },
  },
};const Template = (args) => <Button {...args} />;export const Primary = Template.bind({});
Primary.args = {
  primary: true,
  label: 'Button',
};Primary.parameters = {
  backgrounds: { disable: true }
};
```

我们禁用了带有`Primary`故事的背景下拉菜单。

# 工具栏和全局

我们可以创建自己的故事书工具栏来控制特殊的全局变量。

全局变量是对故事呈现的非特定于故事的输入

它们不会作为参数传递到故事中。

我们可以通过在`.storybook/preview.js`文件中放置一些属性来添加我们自己的工具栏:

```
export const globalTypes = {
  theme: {
    name: 'Theme',
    description: 'Global theme for components',
    defaultValue: 'light',
    toolbar: {
      icon: 'circlehollow',
      items: ['light', 'dark'],
    },
  },
};
```

我们有带有一些属性的`theme`属性。

`toolbar`属性具有`icon`属性来设置下拉选项的图标。

有一系列可供选择的项目。

# 创建一个装饰器

我们可以用装饰器来消费`theme`全局。

例如，我们可以写:

`.storybook/preview.js`

```
import React from 'react';
import { ThemeProvider } from 'styled-components';export const globalTypes = {
  theme: {
    name: 'Theme',
    description: 'Global theme for components',
    defaultValue: 'palevioletred',
    toolbar: {
      icon: 'circlehollow',
      items: ['palevioletred', 'white'],
    },
  },
};const withThemeProvider = (Story, context) => {
  return (
    <ThemeProvider theme={{ main: context.globals.theme }}>
      <Story {...context} />
    </ThemeProvider>
  )
}
export const decorators = [withThemeProvider];
```

我们用`toolbar`属性添加了一些主题选择。

我们用`context.globals.theme`属性得到选择的值。

我们用`ThemeProvider`包装了`Story`组件，也就是我们在故事中显示的任何组件。

然后我们导出我们创建的`withThemeProvider`,放入一个数组中。

现在我们可以通过从下拉菜单中选择来设置主题。

# 结论

我们可以为背景添加选项，并设置装饰者使用的全局变量。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**