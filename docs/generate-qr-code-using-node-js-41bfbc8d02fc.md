# 如何使用 Node.js 生成二维码

> 原文：<https://javascript.plainenglish.io/generate-qr-code-using-node-js-41bfbc8d02fc?source=collection_archive---------2----------------------->

![](img/279dbb99e0d51aed1cf7869b823d942e.png)

二维码已经成为生活中重要的一部分。QR 是“快速反应”的意思。它可以存储大量的数据。QR 扫描仪可以通过扫描即时处理数据。

随着数字设备的增加，你可以通过扫描来获取任何数据。二维码有各种各样的使用案例，比如在销售和市场营销中，你可以在二维码中存储产品的所有细节。

许多支付方式还允许你扫描二维码，向任何人付款。一些物流行业大量使用二维码来跟踪货物。

在今天的帖子中，我们将使用流行的节点包“二维码”来生成二维码。

## 步骤 1:通过 npm 安装二维码包

```
npm install --save qrcode
```

## 第二步:在 index.js 文件中导入二维码包

```
const QRCode = require('qrcode')
```

## **第三步:定义生成二维码的参数**

```
const opts = {
 errorCorrectionLevel: 'H',
 type: 'terminal',
 quality: 0.95,
 margin: 1,
 color: {
  dark: '#208698',
  light: '#FFF',
 },
}const qrImage = await QRCode.toString('Hi testing QR code', opts)
```

**一只**。纠错功能允许您成功扫描二维码，即使该符号是脏的或损坏的。根据操作环境，有四个级别可供选择。级别越高，抗错误能力越强，但会降低符号的容量。

**b** 。颜色指定 QR 码图像颜色。

**c** 。Type 指定预期的输出类型，如数据 URL 中的 image/png、image/jpeg、image/webp 和字符串中的 utf8、SVG、terminal。

**d.** 质量在 0–1 的范围内指定图像的质量。默认值为 0.92 &仅适用于 image/jpeg & image/webp 类型。

**e.** 对于文本，您可以指定文本模式，如数字、字母数字、字节&汉字。基于模式的类型，它将能够存储数据，如数字模式可以存储多达 7089 个字符&字节模式允许存储 2953 个字符。

**f.** 版本指定二维码版本，范围为 1–40。如果没有指定版本，将使用更合适的值。每个版本都有不同数量的模块(黑点和白点)，这些模块定义了符号的大小。对于版本 1，它们是 21x21，对于版本 2，它们是 25x25 e，依此类推。版本越高，可存储的数据就越多，当然，二维码符号也会越大。

![](img/28c52bc1b8f2404bda822d4d99a444b9.png)

Output of the above Code

有多种方法可以创建二维码，如生成:

1.toDataURL 要传入 HTML IMG 标签。
2。到文件以创建文件映像。
3。toString 来创建 QR 码的字符串表示。如果输出格式是 SVG，它将返回一个包含 XML 代码的字符串。
4。toCanvas 将 QR 码符号绘制到节点画布上。您必须传递应该绘制画布的文档 id。
5。创建以生成 QR 码符号并返回 QR 码对象。

点击查看示例[中二维码生成的不同方法。您可以使用该模块生成任何二维码。例如，您可以为您的电子商务产品详细信息生成一个二维码&并将其存储在 AWS S3 上。或者，您可以生成一个二维码到您的支付门户网站进行快速支付。](https://replit.com/@shraddhapaghdar/QRCode-generation#index.js)

***感谢阅读。***

[*更多内容看 plainenglish.io*](http://plainenglish.io/)