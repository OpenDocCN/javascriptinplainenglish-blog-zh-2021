# NativeScript Vue —日期选择器、框架、html 视图和图像

> 原文：<https://javascript.plainenglish.io/nativescript-vue-date-picker-frame-htmlview-and-images-a6e8b5555ebb?source=collection_archive---------9----------------------->

![](img/580510cd832c54b55ff545457fe8ac0e.png)

Photo by [Alev Takil](https://unsplash.com/@alevtakil?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 是一个易于使用的构建前端应用的框架。

NativeScript 是一个移动应用程序框架，它允许我们使用流行的前端框架构建原生移动应用程序。

在本文中，我们将了解如何使用 NativeScript Vue 构建一个应用程序。

# 日期选择器

NativeScript Vue 带有一个日期选择器组件。

为了使用它，我们添加:

```
<template>
  <Page>
    <ActionBar title="NativeScript App"></ActionBar>
    <FlexboxLayout flexDirection="column">
      <DatePicker v-model="selectedDate" />
      <Label :text="selectedDate" style="text-align: center" />
    </FlexboxLayout>
  </Page>
</template><script >
export default {
  data() {
    return {
      selectedDate: undefined,
    };
  },
};
</script>
```

我们将`DatePicker`和`v-model`指令相加，将选择的值绑定到`selectedDate`反应属性。

此外，我们可以限制使用`minDate`和`maxDate`属性选择的日期范围。

他们会设置我们可以选择的最小和最大日期。

`date`获取或设置完整的日期。

`day`、`month`和`year`分别获取或设置日、月和年。

# 基本框架

组件是我们应用程序的根元素。

每个 app 至少需要一个`Frame`。

我们也可以有不止一个`Frame`。

例如，在`main.js`中，我们有:

```
import Vue from 'nativescript-vue'
import App from './components/App'
import VueDevtools from 'nativescript-vue-devtools'if(TNS_ENV !== 'production') {
  Vue.use(VueDevtools)
}// Prints Vue logs when --env.production is *NOT* set while building
Vue.config.silent = (TNS_ENV === 'production')new Vue({

  render: h => h('frame', [h(App)])
}).$start()
```

来渲染帧。

# html 视图

我们可以添加`HtmlView`组件来显示 NativeScript Vue 应用程序中的静态 HTML 内容。

例如，我们可以写:

```
<template>
  <Page>
    <ActionBar title="NativeScript App"></ActionBar>
    <FlexboxLayout flexDirection="column">
      <HtmlView html="<div><h1>HtmlView</h1></div>" />
    </FlexboxLayout>
  </Page>
</template><script >
export default {};
</script>
```

添加`HtmlView`以在`html`属性中显示原始 HTML。

# 图像

`Image`组件让我们显示图像。

例如，我们可以写:

```
<template>
  <Page>
    <ActionBar title="NativeScript App"></ActionBar>
    <FlexboxLayout flexDirection="column">
      <Image
        src="https://i.picsum.photos/id/23/200/200.jpg?hmac=IMR2f77CBqpauCb5W6kGzhwbKatX_r9IvgWj6n7FQ7c"
        stretch="none"
      />
    </FlexboxLayout>
  </Page>
</template><script >
export default {};
</script>
```

我们将`src`属性设置为图像的 URL。

`stretch`设置为`'none'`禁用拉伸。

我们还可以把`src`项目中的一条路径。例如，我们可以写:

```
<template>
  <Page>
    <ActionBar title="NativeScript App"></ActionBar>
    <FlexboxLayout flexDirection="column">
      <Image src="~/assets/images/NativeScript-Vue.png" stretch="none" />
    </FlexboxLayout>
  </Page>
</template><script >
export default {};
</script>
```

我们可以用这个路径引用`/src/assets/images`文件夹中的图像。

此外，我们可以引用一个图标:

```
<template>
  <Page>
    <ActionBar title="NativeScript App"></ActionBar>
    <FlexboxLayout flexDirection="column">
      <Image src="res://icon" stretch="none" />
    </FlexboxLayout>
  </Page>
</template><script >
export default {};
</script>
```

base64 字符串也适用:

```
<template>
  <Page>
    <ActionBar title="NativeScript App"></ActionBar>
    <FlexboxLayout flexDirection="column">
      <Image
        src="data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/4QDeRXhpZgAASUkqAAgAAAAGABIBAwABAAAAAQAAABoBBQABAAAAVgAAABsBBQABAAAAXgAAACgBAwABAAAAAgAAABMCAwABAAAAAQAAAGmHBAABAAAAZgAAAAAAAAA4YwAA6AMAADhjAADoAwAABwAAkAcABAAAADAyMTABkQcABAAAAAECAwCGkgcAFQAAAMAAAAAAoAcABAAAADAxMDABoAMAAQAAAP//AAACoAQAAQAAAMgAAAADoAQAAQAAAMgAAAAAAAAAQVNDSUkAAABQaWNzdW0gSUQ6IDIzAP/bAEMACAYGBwYFCAcHBwkJCAoMFA0MCwsMGRITDxQdGh8eHRocHCAkLicgIiwjHBwoNyksMDE0NDQfJzk9ODI8LjM0Mv/bAEMBCQkJDAsMGA0NGDIhHCEyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMv/CABEIAMgAyAMBIgACEQEDEQH/xAAbAAACAwEBAQAAAAAAAAAAAAAABAECAwUGB//EABcBAQEBAQAAAAAAAAAAAAAAAAABAgP/2gAMAwEAAhADEAAAAU21WN8nGVGZGmVWZGK040ej1Q6GbMxM0BBJATBCFZolFdVdRfkdfmdLxyw0wwswjbSbKMspsZjHA7XFV70KTGW851zrSPI+msZiCArVLYi1grKm0IaKaqhUa33U2HWEtkd2Q1ke4XUTH/SfMfe4rmHMQTP0jaoxXOsl6ZZVKkqbQvC9srxi1mVJddFLj107o5tz9rHxfQ812lol18z9J8FL7TvfM+5M+ory9rlnFfKtVKrW6Lxi0YmUtjIibYaKzda1jOi1xm6kpHPnnTX0Ticj0jPkm1tWqeo8N2k7eWFdTbLPOL4mS2zjOWxmFrZSb3WuMXXua525wpUtNR1OUJ2kmVrEiCad6XB3s7FKVZvmZrNChJQWxAWtnJtOOJuhBAys0ZZMrK5og4kdTq+kZ830OzVlTxHt9F+d0tldWrEKEBcoGk52IVaWiCRY2y1Jw0oQWsT9E+eVk9+nzudc9xHl7U3zdJVWuuKyQAVks4r209Zx+I1MzqnFvS8t7Txcu3YS9ynE26XBR1fbvx8ltfG9G8MxN653JiYqSAi+ZHpUuRROhitCt78+CdcNQ994GU7LCOdnb5STJXlOLNUAlLVkuRNkARUBYgCSAkIL3rZDHbJejVHSzrc9QhyFQrIKTAXKygARALAAAAEl5qJfK9SImFJgJmJIAIkAmJAAiAAAAAkCZAKgQAAASAAAAABIB//EACcQAAICAgIBBAIDAQEAAAAAAAECAAMEEQUSIBATITAUMRUiMiRg/9oACAEBAAEFAhFggggm53gO/sJjGPLBGgiwQQQRv09pDY7dl+tjDDLI8EWLBBBD+rk22KWSA7HoT5kwmMYzSwxoIIIPQGE/D2asqVWTXWA7juFD8j3ya27L4EwtC0ZoxjRoDAYDAZuBp2mUNHjb+y+jL7os4/2b6vhZubhMZozQtC0JhMb0EBgM3AZuZA7Ji3ezkfkqUvyOlfHcgruwDD9Tc3CYWjNGaEwmEwmGbgMBnadoGnaH5GSvR8Ww9MpmsUEo/H8h3Wydp2haFoxjGEwmEzcM3Nzc3NwGAztMhexDdK8GlXxsyv28qr5FfIECrIDgvO0LwvC0JhMJm5ubm4DN+vadpY3zdZ8cVkBqOVq/6K26NevZMW8o/fYLTtO0JhMJm5vx3Nzc3O0ss+XbZwMg1W5xFgsXRR9ofhsfI+O03Nzc35bm/GxtJv0B0fySa2/sv+fVMgiLZ2m/p3AZub9L38aTuu7wrJB8N+W5ubj26n79FEYelDaN8THd5VxlrxeKCluPpx0s4yuyq2tqbNzf0u/gn6b1D9xw1tfuZZtxpbVXn42Nki6e6eOszsavModSjfQx+PCv9ufAMQeO5ZcgX+5xV2XfVmj+SZqkutxjbdXkRkK/QyMRrwT9v/qanWdGhBU08mwqsr+Rdue0dd67I3aqMUYeOPV712VRRi4HE8eltZxFyeU5XDqxVXhj+KBo1Ve668Y0/jBXXh42PlBfxhyHM4C11xWKnujz/DF2dvJVLn2/xVtyrs2JyD49OPf+KTe+ZlZnLD8cTBuFOdzFHu8fw94yMHDb+O5fnKSllNiclx9iGq36VALV5OLhI/fILWd5/iLW1ke5VUnsYZhcituDiZP8fnclZ+Sxz/y8DBy2w7cz+z/Xv1LsfQehlVhre9Pcqx32GU49t6C1EPcMvVvuMHhjXdDfX7NoZcmiq72jeEFj2CxPvHj7jMv/AJb/xAAeEQACAgICAwAAAAAAAAAAAAAAAREwECACMSFQYf/aAAgBAwEBPwHRWLE1o6w7OI1WkdPDV0WNs8nVkEasjCGRRGjR9wrI9B//xAAcEQADAAMAAwAAAAAAAAAAAAAAAREQIDACQFD/2gAIAQIBAT8BykPZC1R5YmUhbtELcQXFkJ1Xt0vRcqUv2v/EADIQAAECBAIIBQMFAQAAAAAAAAEAAgMREiExMgQQEyJAQVFhICMwUnFCYLEUYoGRodH/2gAIAQEABj8C+0wVbVMqgYcJNU65IOGB4aY1GG8/GqXCTV0aV3QhxDfqp8NMjFPHdTGKpfircLQp9dVQUlPhAmu1S1UnhaSp+C/AS4i3ilqsFggHm6rfgvLMjyRY8SI9OQ9CRRgxM30pseHeG3Ozsg6G7ux45I6PHEozbOb1VESZ0Y5XexVslVyIUjwYINwhBjyETryctrBFWjvzM6JsWEaXt/sLY6UJ/uXkPmw/Sril3ozlb0sNWx0jfh9eYVcF1uylECqgGse1SiinurOa9hUxNp6eINTnEYC3yjGic8E6DDyNxKhhmZy2jjvSnJFFvNXsO6L3YC6OzM5Yr9IYZB6lNjwxhZ2qxW/Y+4Ldd/IVTjM+OQxUzYqT3eU1UQseSLp75xK28TKxbNoucdUNzsuBTiBdm8tm65Zun4T4Dsjt3/ihaUyxwJ/Cv9Yk7sU5jsQZekATLuV5Q20b3HALbaS+ln5VMNsmDksZu6rozmSqGZR4KIuYCk90fYbH4W1AkWoQombAlOYcrsVtOuPryJ8Mwg9qpK7LasVBUjwlLsqm3A3CLSZPbcKXJThmxur5x/vChpNh9r//xAAnEAEAAgEEAgIBBQEBAAAAAAABABEhECAxQVFhMHHwQIGRsdGhwf/aAAgBAQABPyGVHHHHMCBvSD8TrGZpGmDe9rUom5UqV8C6Dj08tg4xRxS2CUl8QrDUCDey4u2ltj0OOODpZs5LiEwloVoj6InU2VrpcWLu6F3FtKzWGoTPXJOpYXAe2Gck2gpJcYYw7w7lCPWDSkgkU84uBSZls3mUnFcmUlh/FpfioHpNQkmkIzyJSiAqDVkl1FAz64qiKpofg6pjC0EkEGpSCCBigy8xgzELM0Zf/DvzMmaD7wN1IMOgagMGGpKKELWyQbk4RIkHPBacMxhosuwowwsGDBhBBoYEHTWRMQyzOksHMipbdzG0YZZYWLFly4QRcGXLlkxaxjWEqE4gD9IucW24KNkxeRANjGFlxYsWXLlw0BBAy5rDmVbEqXMP4hrWpg91LaixYuhZely4QaFGlmKq2HMslTpbruZBABwM7nUKiLgZ1o8viXbAWuo0CJ0Liy5ey4uwd+xDoNNkHt4wI7W7jAb2Iz7Eq+v3CAHmscHyepXXP5H0fUFsgX3iJjpJcvW5etG0qnNWx+g1iRueGL8LhfaFr29eIqnjPEL4NsBOfuO3yg4n7qtzmOPOy5cuXKGUWuolStfklQTL+IM4UoKUzPZij8twygeip2r5g67Y9j/YZAXj1KY8DI3PtgeR/fZcuNwYuYFni9ukBe7UZh6Svo5nNGceiHqzLXWkEM9oCmvmdS2eKyHUafZuoMp+jicTCSVX9M6l+Y/9nDL9xFbcg4eOrfyvcou63FTtQZP2sokmX89y0LfB8e43nF4ILDiAlhgdKLE5vz/JByNgrx3PDZj2uJZGnyfHaYs1qdJlRa0yl+H3Dipy2EvaSEv0EzzToqXPsyHf0Ji9An+1iieRHqaIANcJ5fLFtYOnlDlPSIgz/mGYrDprslYrp9o4Yujxjw9MPu4bRuuKaFccS0MLCA2U8R4nLThOhHCeYLoUzidvP9kOpzyeyFOSskzp9e4zdWw+B0OdA0Z3KHkf8Y1j3MHEbJGVZfJMiYcOmBePb8w2nmdRuU4JwxhH9AadR2n6E0uP6l+b/9oADAMBAAIAAwAAABAEaVWwRTwUKLAwnwNJzS5iYaakFCC4W+ZRDynGjAxqkTf7PkO1hw9r2C/Lit8jNUY8sYobBvmSB9acLqCgGfYJJHTsLBwi8BbjwJKc5wHkMfXYPHXy9dU0Ofvp8OnWgDwn/CgQQ9qTIOARvNiADgdNSyACDjByACCJzzzwADwD/8QAHxEAAwACAwADAQAAAAAAAAAAAAERECEgMUEwUWFA/9oACAEDAQE/EGPCRQqUo2N4QhjyTa2RKNu7KN5Sw0NEOw9hJsouEJCWIQmHtDeD/CEEhISzCEwNMf0tshCEzMJbw0mLuYac4JQYhrdKIh12xPkWGLDSZ22QhKa4N4ikojd/EO3tjOxFesSmzsnFCE+8UWEXXjNNfHN0+hP7/wD/xAAeEQADAAMAAwEBAAAAAAAAAAAAAREQICEwMUFAUf/aAAgBAgEBPxAYygkc2TQxijJsg3S0E1hBzdRaVHCEEE0pcoZN8+Et3BLelGxLtw2Lu3hOZT8FEMRUnC/YmsezwhkGr7E+nJwt0SI57I6hX6NEX1DfjxdqURFekVJwf98KGXhS+J/l/8QAJhABAAICAQQCAgMBAQAAAAAAAQARITFBEFFhcSCBkaGxwfDRMP/aAAgBAQABPxB5Jqmua5ojYhn3BUWUhGJBly/gsWLFKBl9wXM3yxmaWhcS84TjGjTtKEazFpDiGEKPQkuXLlxYsqJunlhIkpmEtNpwg1EEVMxEJQ9o6d7iYLApN9QbWoAuXFlxjHKTp0LKrzMqXLHmZpXU09KrbLKHiUQ9oUZsle8jtKBqorVAuFFcBqeQyXHqEQ3PNPPN+ZfeZSczZ0tGZTXU/JCwneMvdBfsy40xdyoI5uFiOjbhezLu7dNE8sAhs5jl5jXuJ3mzMvuZGPMpmCeWeeXcyrmOnNQuabIUFRqBt4WGbsWfqIgESZVbhjyTySo3BpzCbzN2YneeaZdxWQ+jXzKOZm3PPLuZmHJAuNuKooOYWAMYhThO7w6GBTN+GIDjW5SrGUcwe8s5lg5lK5g7+F1pCj0ryeSUO5rzC7wK3FiuZRVTUNlc3GHoGnqMOwcQ26mhcJgS3kzAzmArcAEuM3TEWY9zy/AgjNCrcIvlfM7DBd5YCV7RFU1HSMAeaLmFIF4i47vxC6MJFOY17lpPJE7/ADaSp1EvfWCnMyG9RDp1H8RBKwnvF/GzMZoInsqXsKRxBKgO8AWNnRqNyznp39dYOoic+5ruDmWqajpXfSKakZZw2xNhLik2XfcwUiJyRsXyQaKeTptzp2SiM7Q6DyShnlgpdwQe63MhLwsVBEr05wlUrnpUF2gyiXEGKiLFuU89NiyML0kUMFJhzAW5/GOUtYqEOyzIx3DVUa+4FHESE6GMjR3JNvbRlgA24rMeb4h2w8ysYj/wpHnyeOmy26D1LqDCspWe2Kra9TcgWY7iElJpmGpXD3lm7y/nPc/3+iCs7QtCgpSPf7wk9aDLrzo44jrijLT+bt5JcHWQnavkjn1UjERhWL0EGYYiu8sW2/gynclQO9vU3BBoWpE0jKLJxZ7eDw0xNVqTXO/47MEkdg2vNbIEojRPR38xtCrbj9dopacLa/ETsXxGosuL0EFYXgRAc1BKBXtFVIjLhaQLlRr2mT+YJmkGFtK/EBD/AKliQcMcZKLP/J7zLnE3+q8PhmqjdKv5OH1K4bt36jh6zFgjxXdvMGL6GB8JsfDEAi2H0OH3L6CdR1NJbxL3oe4mB+YZO5/NYtY+P9H3iLy2i+XkfyhBXgMCrp81C1mmoLqjAOSFWxwR+450PbABaweoYAI21iX9e2FmRXhNRWgQXA/2Y/ENiLlrhDXscyyabBp9m0ie3lAX5HDHRUKRftW3zKqAPcjOelwYpllARvtQzio29eDgvu9/4QdukFlsYfxM4YK82dvnf2zBIXtAZB7q5YnlxGytffPj3ECuVysLoL+6DC/ppgBHx0Y/Rv6hBS3lsi34s+omMrarN/uD7lhgWwV/YPqUwAX7efw0PFSsQR8jUdx7y7I6YWly+0uDGL9Td9lRon3Pni8sXEkR9H9zHqu9MH7TF5OwMh4Imt2b1j/r2COs9o5vNLI2rErDUbQ9oua/3LShfZh9RJEdDym/YP8AcAigu224fpgEghG/7H+YI4Wdj/KenxHLbUvPD+Oh05ixL6alwY4S7ECgt0eJdgBwg7lru8nMCArZbA+piAguC8TJkGM29JBOsgGU5P7/ADLxqRoebZ9Qml/KmT2QVDeHIb++fzFDLqkun/YOmVvud/gofFYbiuGDpK3ExXKbgw3HEC7VcP8AjEFMGpuvE4iMgKbD3M1K9D3hwIgOVsiedQBgdSG4MuXLlxYRnEVRyw43L5uKo5mMXDU9I8QXAp66NYPiPwY/AhuLHeDHshzDUMMdxyR1H4nwfkdF0y3eO5eOjOIfE6v/AIBDXTXzEfidP//Z"
        stretch="none"
      />
    </FlexboxLayout>
  </Page>
</template><script >
export default {};
</script>
```

我们还可以显示一个字体图标:

```
<template>
  <Page>
    <ActionBar title="NativeScript App"></ActionBar>
    <FlexboxLayout flexDirection="column">
      <Image src.decode="font://&#xf004;" class="fas" />
    </FlexboxLayout>
  </Page>
</template><script >
export default {};
</script>
```

我们添加了`decode`修改器来解码图标字体。

# 结论

我们可以使用 NativeScript Vue 在应用程序中添加日期选择器、HTML 视图、框架和图像。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**