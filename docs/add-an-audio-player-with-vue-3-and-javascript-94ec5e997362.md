# 添加带有 Vue 3 和 JavaScript 的音频播放器

> 原文：<https://javascript.plainenglish.io/add-an-audio-player-with-vue-3-and-javascript-94ec5e997362?source=collection_archive---------10----------------------->

![](img/74ff1618f405307a6890c5ae7b94dd36.png)

Photo by [Alexey Ruban](https://unsplash.com/@intelligenciya?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

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
vue create audio-player
```

并选择所有默认选项来创建项目。

# 创建音频播放器

我们可以通过编写以下代码来创建音频播放器:

```
<template>
  <input
    type="range"
    min="0"
    max="100"
    step="1"
    v-model="seekValue"
    @change="onSeek"
  />
  <audio
    src="https://file-examples-com.github.io/uploads/2017/11/file_example_MP3_700KB.mp3"
    ref="audioPlayer"
    @timeupdate="onPlaying"
  >
    Your browser does not support the
    <code>audio</code> element.
  </audio>
  <p>{{ currentTime }}</p>
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
  data() {
    return {
      currentTime: 0,
      seekValue: 0,
    };
  },
  methods: {
    play() {
      this.$refs.audioPlayer.play();
    },
    pause() {
      this.$refs.audioPlayer.pause();
    },
    stop() {
      const { audioPlayer } = this.$refs;
      audioPlayer.pause();
      audioPlayer.currentTime = 0;
    },
    setSpeed(speed) {
      this.$refs.audioPlayer.playbackRate = speed;
    },
    onPlaying() {
      const { audioPlayer } = this.$refs;
      if (!audioPlayer) {
        return;
      }
      this.currentTime = audioPlayer.currentTime;
      this.seekValue = (audioPlayer.currentTime / audioPlayer.duration) * 100;
    },
    onSeek() {
      const { audioPlayer } = this.$refs;
      const seekto = audioPlayer.duration * (this.seekValue / 100);
      audioPlayer.currentTime = seekto;
    },
  },
};
</script>
```

我们有一个范围输入，我们可以滑动它来改变`seekValue`，

我们用`v-model`将它绑定到`seekValue`。

此外，我们将一个`change`事件处理程序附加到输入，该处理程序改变音频元素的`currentTime`来寻找音频。

`audio`元素有我们想要播放的音频。

我们监听`timeUpdate`事件，这样我们就可以得到当前时间。

我们给它分配一个引用，这样我们就可以在以后操作它。

在那下面，我们显示`currentTime`。

然后我们有几个按钮让我们播放、暂停、停止和改变音频的速度。

在模板下面，我们有返回了`currentTime`和`seekValue`反应属性的`data`方法。

`play`方法从 ref 获取音频播放器元素，并调用`play`播放音频。

`pause`方法从 ref 获取音频播放器元素，并调用`pause`暂停音频。

`stop`方法暂停音频，并将`currentTime`设置为 0，以将音频回放重置回起点。

`setSpeed`让我们通过改变`playbackRate`属性来设置速度。

当发出`timeUpdate`事件时，调用`onPlaying`方法。

我们将`this.currentTime`的无功属性设置为`audioPlayer`的`currentTime`属性。

此外，我们更新了`seekValue`，使其与`currentTime`同步。

这将更新范围滑块，使其与`currentTime`同步。

最后，我们有当范围输入发出`change`事件时运行的`onSeek`方法，这是在我们完成移动滑块时完成的。

我们得到了`seekValue`无功属性，并通过将其乘以`duration`并除以 100 来计算`seekTo`值。

然后我们将它设置为`currentTime`来改变当前时间。

# 结论

我们可以添加一个带有 Vue 3 和 JavaScript 的音频播放器。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)