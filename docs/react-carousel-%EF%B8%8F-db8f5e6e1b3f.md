# 如何创建一个反应转盘⚛️🎠

> 原文：<https://javascript.plainenglish.io/react-carousel-%EF%B8%8F-db8f5e6e1b3f?source=collection_archive---------13----------------------->

![](img/b756d0387c27aa2a8ced7ae03fad2589.png)

在这篇博客中，我们将探讨如何在 React 中实现一个旋转滑块。我为一家为许多企业提供产品的科技初创公司重建了一个网站，并自豪地在其网站上展示这些品牌标志。当重新创建网站时，我决定在一个转盘上显示品牌，也就是说，它是自动的，无限的，并允许手动滑动。

## 安装 React Slick📥

我使用了一个名为 React Slick 的库来实现转盘滑块。我们需要首先通过在命令行中键入以下命令来安装库:

```
npm install react-slick --save
```

或者

```
yarn add react-slick
```

一旦成功安装 React Slick，您将需要通过在命令行中添加以下内容来将 CSS 包含在您的项目中:

```
npm install slick-carousel --save
```

然后在 CSS 文件中添加这两行代码:

```
[@import](http://twitter.com/import) "~slick-carousel/slick/slick.css";
[@import](http://twitter.com/import) "~slick-carousel/slick/slick-theme.css";
```

## 让我们开始破解⚒️

现在，我们将开始构建我们的滑块，我将它命名为`BrandSlider`，并从`react-slick`导入`Slider`，如下所示:

```
import React, { useState } from 'react';
import Slider from 'react-slick';
import '../../styling/brandslider.css';const BrandSlider = () => { return ( )}
```

正如你在上面看到的，我们还使用了`{ useState }`钩子，因为我们将使用 state 来跟踪图像索引，并在滑块上设计中心图像的样式。

## 调用所有图像！🖼️

对于每个品牌，我在谷歌上找到了 png 格式的商标文件，并在 photoshop 上把它们做成大致相同的大小和颜色，以符合公司的主题。我导入了每个图像，然后创建了一个数组，我将在组件内部映射该数组。在下面的例子中，我没有添加品牌名称，只是在*品牌*后面加了一个数字。

```
import React, { useState } from 'react';
import Slider from 'react-slick';
import brandOne from '../../assets/Brand1Logo.png';
import brandTwo from '../../assets/Brand2Logo.png';
import brandThree from '../../assets/Brand3Logo.png';
import brandFour from '../../assets/Brand4Logo.png';
import brandFive from '../../assets/Brand5Logo.png';
import brandSix from '../../assets/Brand6Logo.png';
import brandSeven from '../../assets/Brand7Logo.png';
import brandEight from '../../assets/Brand8Logo.png';
import '../../styling/brandslider.css';const images = [brandOne, brandTwo, brandThree, brandFour, brandFive, brandSix, brandSeven, brandEight];const BrandSlider = () => { return ( )}
```

## 🗳️的州和地图🗺️

我们现在将声明一个新的状态变量，我们称之为" *imageIndex"* ，并将其设置为 0。然后，我们将添加主代码，该代码将映射整个数组，如下所示:

```
import React, { useState } from 'react';
import Slider from 'react-slick';
import brandOne from '../../assets/Brand1Logo.png';
import brandTwo from '../../assets/Brand2Logo.png';
import brandThree from '../../assets/Brand3Logo.png';
import brandFour from '../../assets/Brand4Logo.png';
import brandFive from '../../assets/Brand5Logo.png';
import brandSix from '../../assets/Brand6Logo.png';
import brandSeven from '../../assets/Brand7Logo.png';
import brandEight from '../../assets/Brand8Logo.png';
import '../../styling/brandslider.css';const images = [brandOne, brandTwo, brandThree, brandFour, brandFive, brandSix, brandSeven, brandEight];const BrandSlider = () => {
  const [imageIndex, setImageIndex] = useState(0); return (
    <div className='slider'>
      <p>Empowering leading global brands</p>
      <Slider>
        {images.map((img) => (
          <div className='temp'>
            <img src={img} alt={img} />
          </div>
        ))}
      </Slider>
     </div>
  )}
```

这里需要注意几件事。首先，我们还没有完成`BrandSlider`组件的工作，因为我们需要研究如何处理每个图像索引。如你所见，每个`img`的`className`是`'temp'`，因为我们将添加一个三元运算符来设计中心徽标图像的样式。

## 设置和样式⚙️ 🖌️

我们将为`div`添加`className`作为三元运算符，以表示哪些图像是*‘活动’*(居中)的，哪些图像不是。我们还将添加设置来配置我们的滑块(这可能在您的项目中有所不同)。

```
import React, { useState } from 'react';
import Slider from 'react-slick';
import brandOne from '../../assets/Brand1Logo.png';
import brandTwo from '../../assets/Brand2Logo.png';
import brandThree from '../../assets/Brand3Logo.png';
import brandFour from '../../assets/Brand4Logo.png';
import brandFive from '../../assets/Brand5Logo.png';
import brandSix from '../../assets/Brand6Logo.png';
import brandSeven from '../../assets/Brand7Logo.png';
import brandEight from '../../assets/Brand8Logo.png';
import '../../styling/brandslider.css';const images = [brandOne, brandTwo, brandThree, brandFour, brandFive, brandSix, brandSeven, brandEight];const BrandSlider = () => {
  const [imageIndex, setImageIndex] = useState(0); const settings = {
    infinite: true,
    lazyload: true,
    speed: 500,
    slidesToShow: 5,
    centerMode: true,
    centerPadding: 0,
    autoplay: true,
    beforeChange: (current, next) => setImageIndex(next)
  }; return (
    <div className='slider'>
      <p>Empowering leading global brands</p>
      <Slider {...settings}>
        {images.map((img, idx) => (
          <div className={idx === imageIndex ? "slide activeSlide" : "slide"}>
            <img src={img} alt={img} />
          </div>
        ))}
      </Slider>
    </div>
  )}
```

现在我们转到 CSS 文件来设计居中品牌标志的样式，以增加其`scale`并将其`opacity`设置为`1`，而非居中标志则设置为`0.2`，如下所示:

```
.slide {
  transform: scale(0.5);
  transition: transform 300ms;
  opacity: 0.2;
}.activeSlide {
  transform: scale(1.5);
  transition: transform 300ms;  
  opacity: 1;
}
```

现在你知道了。希望这个演练是有帮助的，并且您能够为您的项目创建一个无缝的旋转滑块！

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)