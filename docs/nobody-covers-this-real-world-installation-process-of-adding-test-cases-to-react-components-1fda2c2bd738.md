# 没有人讨论过添加测试用例来反应组件的真实安装过程

> 原文：<https://javascript.plainenglish.io/nobody-covers-this-real-world-installation-process-of-adding-test-cases-to-react-components-1fda2c2bd738?source=collection_archive---------11----------------------->

使用已经安装的第三方库(如 Redux)为 React 组件编写测试用例。

![](img/3debfa5947c186db3b420539b4edeafe.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 在后台

我最近得到了一个新工作机会的测试任务。编码任务通常与拖放功能有关，需要添加一些基本的测试用例。我通常面临的问题是安装 React 测试库。安装之后，我在运行测试用例时遇到了一个问题，我的存储库中已经安装了 Next.js 和 Redux。

最后，我用 react-testing-library 阅读并研究了一下 Redux 在 Next.js 中的安装过程。最后，我在这里阐明了安装 Jest 和 React 测试库的过程，这些测试库带有预先安装的库，比如 Next.js 中的 Redux。

# 入门指南

测试 React 组件最常用的 npm 包和测试库是`[**@testing-library/react**](https://testing-library.com/docs/react-testing-library/setup)` [**。**](https://testing-library.com/docs/react-testing-library/setup)

这个库依赖 Jest 来运行测试用例，但是我们确实需要更多的这个 party 插件和包来让它在 Next.js 中工作。

```
yarn add @testing-library/dom @testing-library/jest-dom 
    @testing-library/react babel-jest jest jest-dom 
    identity-obj-proxy
```

运行测试用例需要这些包。

*   Jest——主要帮助运行捕获所有 test.js 文件的测试用例
*   **巴别塔**——需要传输我们的代码
*   **@ testing-library/react**—这是帮助编写测试用例的库

下一步是安装 jest 的设置来捕获所有的 test.js 前缀文件，并运行所需的测试用例。

根控制器内部创建两个文件，分别命名为`**jest.config.js**` **&** `**jest.setup.js**`

在 **Jest** 配置文件中，通过添加以下代码来添加配置 Jest 设置的配置。

在 jest 设置文件中，我们将导入测试库，它将帮助我们编写测试用例。在我们的例子中，我们使用@testing-library/react，因此我们将导入它。

一旦 Jest 的设置完成，我们只需要在根目录下的`**.babelrc**`文件中为下一个 JS 添加 babel 预置。

据此，你的笑话和巴别塔设置准备就绪。

# 使用 React 测试库

我们可以在测试目录中添加第一个示例测试，并运行我们的第一个测试。但这里的主要问题是我们已经包装的第三方，如 Redux 或 Material UI 以及更多的提供者。

这些提供者是应用程序根的包装器。为了测试任何 UI 组件，我们还需要在将该组件传递到测试库之前用这个包装器包装该组件。

我们目前只使用 redux 作为第三方提供者，所以我们将只使用 Redux 提供者包装每个测试组件。

在根目录下的 test 文件夹中，我们添加了`**test-utils.jsx**`文件。我们通过用 redux provider 包装每个呈现方法来创建一个用于测试库的定制呈现方法。

上面的代码基本上包装了通过与我们的第三方提供者一起测试库而提供的呈现方法，以创建我们的定制呈现方法。

现在，我们不得不使用这个定制的 render 方法，而不是测试库来测试任何 react 组件。我们将传递给这个 render 方法的每个 react 组件都将包装在我们的 Redux 提供程序中。

此外，不要忘记通过任何其他提供者自定义渲染，否则你的测试用例将失败，这是必要的，以提供每个需要的道具给我们的包装提供者在我们的情况下，我们已经通过存储和后端道具给我们的提供者。

因此，可以使用您的带有 Redux 和其他第三方的 Next.js 中的 React 测试库。

# 总结方法

*   安装所有需要的包，如 Jest，testing-library 和 Babel 插件
*   通过添加设置文件来初始化 Next.js 存储库中的 Jest。
*   在 Next.js 中添加 babel 来传输代码。
*   通过包装第三方提供者，为测试库创建自定义呈现方法。
*   导出并使用自定义呈现方法来测试 React 组件。

# 结论

我们已经在 Next.js 中介绍了如何将 React 测试库与第三方库一起使用。这篇文章应该会有更多的读者，因为这种用例大多发生在专业经验中。

作为前端开发人员，您也必须为 React 组件编写测试用例。如果您已经在使用 Redux 和 Material UI 以及其他第三方库，那么这篇文章一定会帮到您。

代码:

[](https://github.com/shreyvijayvargiya/iHateReadingLogs/tree/main/TechLogs/InstallingReduxWithTestingLibrary) [## shreyvijayvargiya/iHateReadingLogs

### 本报告给出了为已经安装的第三方 React 组件编写测试用例的基本理解…

github.com](https://github.com/shreyvijayvargiya/iHateReadingLogs/tree/main/TechLogs/InstallingReduxWithTestingLibrary) 

下次见。祝大家愉快！

[*更多内容尽在 plainenglish.io*](http://plainenglish.io/)