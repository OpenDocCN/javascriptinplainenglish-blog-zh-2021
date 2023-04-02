# 如何轻松使用 JavaScript 和 ArcGIS 创建精美丰富的地图

> 原文：<https://javascript.plainenglish.io/how-to-easily-use-javascript-and-arcgis-to-create-beautiful-rich-maps-94e9354e387b?source=collection_archive---------13----------------------->

## 在本教程中释放 GIS 的力量。

![](img/a40a0e1b7633c25ab16e504d4ee794d5.png)

A working example of showing volcanoes in the world with Bloom effect in ArcGIS

# **目的**

几周前， [Esri](https://www.esri.com/en-us/home) 举办了他们的年度(虚拟)[开发者大会](https://www.esri.com/content/dam/esrisites/en-us/media/brochures/2021-developer-summit-attendee-guide.pdf)，展示了他们 ArcGIS 平台开发的最新成果。

此次峰会旨在展示如何使用他们先进的地图技术构建尖端应用。不仅如此，他们还有技术研讨会和会议，以及一个讨论学习发展最佳实践的场所。

在本文中，我将解释什么是 GIS，您可以在 Esri 的开发人员门户浏览教程，还可以使用一个 JavaScript 示例来快速加载动态地图。

# 什么是 GIS

“GIS”代表 G **地理信息系统**。维基百科是这样解释的:

> “一个[概念化的](https://en.wikipedia.org/wiki/Concept)框架，提供捕获和分析[空间](https://en.wikipedia.org/wiki/Spatial_analysis)和[地理数据](https://en.wikipedia.org/wiki/Geographic_data_and_information)的能力。GIS 应用程序(或 GIS 应用程序)是基于计算机的工具，允许用户创建交互式查询(用户创建的搜索)、存储和编辑空间和非空间数据、分析空间信息输出，以及通过将这些操作的结果显示为地图来直观地共享它们。——维基百科”

换句话说，它是一个基于计算机的系统，用于分析和呈现空间数据。

目前，主要的公司是开发这个软件的大狗是 Esri。他们是 GIS 软件、web GIS 和地理数据库管理应用程序的国际供应商。

# 发展链接

令人欣慰的是，Esri 的[开发网站](https://developers.arcgis.com)充满了例子，你可以随心所欲地测试和演示。

仅举几个例子，他们的 Web APIs 可以用于 [JavaScript](https://developers.arcgis.com/javascript/latest/) 、[传单](https://developers.arcgis.com/esri-leaflet/)、[地图框](https://developers.arcgis.com/mapbox-gl-js/)和 [OpenLayers](https://developers.arcgis.com/openlayers/) 。

您也可以查看他们的[文档](https://developers.arcgis.com/documentation/)，查看可以利用他们的 ArcGIS 技术的完整技术列表。

# 工作示例

我从他们的开发者门户网站选择了这个[例子](https://developers.arcgis.com/javascript/latest/sample-code/intro-effect-layer/)来展示如何将效果层应用到地图上。

应用图层时，您可以向要素图层添加`bloom`效果。此功能允许您将 CSS 滤镜功能应用于图层，以提高地图的质量。

在这个特别的例子中，你将会看到一个巨大的光晕效果。用户可以通过复选框选择或取消火山爆发效果。

下面的代码是在一个**index.html**文件中制作的实例。

## 1.设置它

首先，您将创建一个 HTML 容器来显示地图和包含 bloom 效果的滑块。

## 2.创建配置

接下来，您需要设置**地图**和**视图**作为配置。您还可以将**效果**滑块设置在屏幕的左上角。

当点击 applyBloomEffect 时，它将调用 **updateMapEffects** 函数。

> **注意**:注意**活动门**的数值。这是 ArcGIS 免费提供的数值！

我们将在下一节实现 **updateMapEffects()** 。

## **3。最后，实现两个重要的功能**

最后，您将创建 **updateMapEffects()** 和 **createSlider()** 函数。跟随下面粘贴的`gist`中的评论，看看发生了什么。

> **注意:****create slider**()有很多默认值可以设置。你可以在这里阅读更多关于它的[。](https://developers.arcgis.com/javascript/latest/api-reference/esri-widgets-Slider.html)

# 在 index.html 把所有东西放在一起

现在我们已经创建了设置、配置和函数，我们只需将所有的 JavaScript 复制到**index.html 中。**

如果需要，可以随意将 JavaScript 函数放在一个单独的文件中！

# 运行您的地图

只需在浏览器中打开你的**index.html**文件，就能看到显示的地图。

就这么简单！

# 概括一下

*   GIS 代表**地理信息系统**，它是一个基于计算机的系统，用于分析和呈现空间数据。
*   Esri 是创建 ArcGIS 以增强 GIS 的开发者。
*   您在 Esri 的开发人员门户中创建了一个简单的示例，该示例显示了世界上所有的火山并应用了盛开效果。这些都是使用免费的 JavaScript API 完成的。

我仍然是 ArcGIS 的新手，正在探索它的全部潜力，因此如果您希望我继续展示更多示例，请随时给我留言。

干杯！

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)