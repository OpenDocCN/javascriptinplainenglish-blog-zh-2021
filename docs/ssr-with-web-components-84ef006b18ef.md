# 带有 Web 组件的 SSR

> 原文：<https://javascript.plainenglish.io/ssr-with-web-components-84ef006b18ef?source=collection_archive---------4----------------------->

## 在木偶师中渲染阴影 DOM 和模板

![](img/8b1f0328b54b8c8627e7c72711db3ea7.png)

使用 Google 木偶师在服务器端呈现 web 组件是一个真正的挑战。影子 DOM 的序列化还处于试验阶段。[声明式阴影 DOM](https://web.dev/declarative-shadow-dom) 允许对阴影 DOM 进行序列化，只需几个简单的步骤就可以实现。如果不遵循这些步骤，在 Puppeteer 中渲染后，您将得到空的自定义元素。

## 启用影子根目录

对于要用实验特性序列化的 Shadow DOM，首先需要设置模板的`shadowroot`属性。

```
<template shadowroot="open">
```

## 启用实验性 Web 平台功能

为了在 Puppeteer 中序列化 Shadow DOM，我们将为元素使用一个提议的新函数:`getInnerHTML`。这个函数接受一个公开了`includeShadowRoots`属性的对象。

```
const html = await page.$eval('html', (element) => {
    return element.getInnerHTML({includeShadowRoots: true});
});
```

没有启用的实验特征，该功能是未定义的。要在浏览器中启用此功能，请转到:`chrome://flags/#enable-experimental-web-platform-features`。要在 Puppeteer 中启用此功能，您必须更改您的启动配置:

```
const args = puppeteer.defaultArgs();
// IMPORTANT: you can't render shadow DOM without this flag
// getInnerHTML will be undefined without it
args.push('**--enable-experimental-web-platform-features**');
const browser = await puppeteer.launch({
    args
});
```

## 定义等待方法

对于要包括在输出中的组件执行结果，您需要等待渲染完成。为此，我们查询 DOM 来检测影子根的存在。

```
await page.**waitForFunction**(selector => !!document.querySelector(selector)?.shadowRoot, {
    polling: 'mutation',
}, selector);
```

更多关于`waitForFunction`的信息，点击[这里](https://github.com/puppeteer/puppeteer/blob/main/docs/api.md#pagewaitforfunctionpagefunction-options-args)。

## 完整示例

下面是一个完整的功能示例。如果您试图让您的 web 组件呈现，复制示例并测试它。编码快乐！