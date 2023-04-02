# 添加带有 Vue 3 和 JavaScript 的视频播放器

> 原文：<https://javascript.plainenglish.io/add-a-video-player-with-vue-3-and-javascript-4d342c3259e4?source=collection_archive---------8----------------------->

![](img/1e4329f16a7c55930a2082526cc0eb53.png)

Photo by [Jakob Owens](https://unsplash.com/@jakobowens1?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个视频播放器。

# 创建项目

我们可以用 Vue CLI 创建 Vue 项目。

要安装它，我们运行:

```
npm install -g @vue/cli
```

与 NPM 或:

```
yarn global add @vue/cli
```

用纱线。

然后我们运行:

```
vue create video-player
```

并选择所有默认选项来创建项目。

# 创建视频播放器

我们可以通过编写以下代码来创建视频播放器:

```
<template>
  <video width="320" height="240" ref="videoPlayer">
    <source
      src="https://www.learningcontainer.com/wp-content/uploads/2020/05/sample-mp4-file.mp4"
      type="video/mp4"
    />
    Your browser does not support the video tag.
  </video>
  <div>
    <button @click="play">play</button>
    <button @click="pause">pause</button>
    <button @click="stop">stop</button>
    <button @click="setSpeed(0.5)">0.5x</button>
    <button @click="setSpeed(1)">1x</button>
    <button @click="setSpeed(1.5)">1.5x</button>
    <button @click="setSpeed(2)">2x</button>
  </div>
</template><script>
export default {
  name: "App",
  methods: {
    play() {
      this.$refs.videoPlayer.play();
    },
    pause() {
      this.$refs.videoPlayer.pause();
    },
    stop() {
      const { videoPlayer } = this.$refs;
      videoPlayer.pause();
      videoPlayer.currentTime = 0;
    },
    setSpeed(speed) {
      this.$refs.videoPlayer.playbackRate = speed;
    },
  },
};
</script>
```

我们有一个分配了`ref`的`video`元素。

`width`和`height`设置视频的尺寸。

元素有视频源。

我们将它设置为我们想要播放的 MP4 剪辑的 URL。

在那下面，我们添加按钮让我们播放、暂停和停止视频。

我们也有按钮，让我们改变播放速度。

然后在下面，我们添加一些方法，当我们点击按钮时，这些方法就会被调用。

`play`方法让我们通过用`this.$refs.videoPlayer`获取`videoPlayer` ref 并对返回的 video 元素调用`play`方法来播放视频。

`pause`方法类似。我们获取包含元素的`videoPlayer` ref，并对其调用`pause`来暂停视频。

视频元素没有停止视频的方法。但是我们可以通过暂停它并将`currentTime`重置为 0 来实现。

要设置视频的速度，我们可以设置`playbackRate`属性。

0.5 是正常速度的一半。

任何高于 1 的速度都比正常速度快。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松地在我们的 web 应用程序中添加一个视频播放器。

*更多内容看* [***说白了. io***](https://plainenglish.io/)