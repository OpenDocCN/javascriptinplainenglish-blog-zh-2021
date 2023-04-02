# React 故事书入门

> 原文：<https://javascript.plainenglish.io/getting-started-with-storybook-for-react-c0785d4a47ba?source=collection_archive---------18----------------------->

![](img/25c7d144f3bfbe341831ed8a6439502c.png)

Photo by [Road Trip with Raj](https://unsplash.com/@roadtripwithraj?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Storybook 让我们可以用各种参数轻松地构建组件原型。

在这篇文章中，我们将看看如何开始与故事书。

# 入门指南

我们可以先用 Create React App 创建一个 React 项目。

为了创建它，我们运行:

```
npx create-react-app storybook-project
```

然后，我们可以通过运行以下命令向其添加故事书:

```
npx sb init
```

然后我们可以通过运行以下命令来运行它:

```
npm run storybook
```

运行故事书。

现在我们可以创造一个故事。

一个故事的组成部分可能需要一些参数来让我们调整它。

我们可以为这些参数提供默认值。

首先，我们创建一个需要一些道具的组件。

在`src/stories`文件夹中，我们创建了一个`Button.js`来创建一个接受一些道具的按钮:

```
import React from 'react';
import PropTypes from 'prop-types';
import './button.css';export const Button = ({ primary, backgroundColor, size, label, ...props }) => {
  const mode = primary ? 'button-primary' : 'button-secondary';
  return (
    <button
      type="button"
      className={['button', `button-${size}`, mode].join(' ')}
      style={backgroundColor && { backgroundColor }}
      {...props}
    >
      {label}
    </button>
  );
};Button.propTypes = {
  primary: PropTypes.bool,
  backgroundColor: PropTypes.string,
  size: PropTypes.oneOf(['small', 'medium', 'large']),
  label: PropTypes.string.isRequired,
  onClick: PropTypes.func,
};Button.defaultProps = {
  backgroundColor: null,
  primary: false,
  size: 'medium',
  onClick: undefined,
};
```

然后我们给它添加一个`button.css`样式:

```
.button {
  font-weight: 700;
  border: 0;
  border-radius: 3em;
  cursor: pointer;
  display: inline-block;
  line-height: 1;
}
.button-primary {
  color: white;
  background-color: #1ea7fd;
}
.button-secondary {
  color: #333;
  background-color: transparent;
}
.button-small {
  font-size: 12px;
  padding: 10px;
}
.button-medium {
  font-size: 14px;
  padding: 11px;
}
.button-large {
  font-size: 16px;
  padding: 12px;
}
```

我们的按钮需要一堆道具来让我们修改不同风格的按钮。

`primary`是布尔型道具。

`backgroundColor`是一串道具。

`size`让我们用一个枚举类型来改变大小。

让我们展示一个标签。

是一个让我们处理点击的函数。

为了让它在 Storybook 中显示，我们添加了`Button.stories.js`文件并添加了:

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
};export const Secondary = Template.bind({});
Secondary.args = {
  label: 'Button',
};export const Large = Template.bind({});
Large.args = {
  size: 'large',
  label: 'Button',
};export const Small = Template.bind({});
Small.args = {
  size: 'small',
  label: 'Button',
};
```

我们导出一个包含我们想要显示的东西的对象。

有我们想在故事书中显示的标题。

`component`是我们要预览的组件。

`argTypes`让我们设置各种道具的控制类型，以便我们可以在故事书中更改和预览它们。

下面是参数。args 允许我们将道具传递给组件，这样我们就可以更改它。

我们用`Template.bind`方法提供了一些默认值，并将`args`属性设置为我们想要的值。

# 结论

我们可以创建组件并用 Storybook 预览它们。

接受道具并用 args 绑定就可以换。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**