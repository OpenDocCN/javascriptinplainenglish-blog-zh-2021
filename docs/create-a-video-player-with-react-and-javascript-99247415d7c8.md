# 用 React 和 JavaScript 创建一个视频播放器

> 原文：<https://javascript.plainenglish.io/create-a-video-player-with-react-and-javascript-99247415d7c8?source=collection_archive---------4----------------------->

![](img/728771d1efb622fb4bd3fca1023b56ec.png)

Photo by [Jakob Owens](https://unsplash.com/@jakobowens1?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个视频播放器。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app video-player
```

和 NPM 一起创建我们的 React 项目。

# 创建视频播放器

为了创建视频播放器，我们编写:

```
import React, { useRef, useState } from "react";export default function App() {
  const videoPlayer = useRef();
  const [currentTime, setCurrentTime] = useState(0);
  const [seekValue, setSeekValue] = useState(0); const play = () => {
    videoPlayer.current.play();
  }; const pause = () => {
    videoPlayer.current.pause();
  }; const stop = () => {
    videoPlayer.current.pause();
    videoPlayer.current.currentTime = 0;
  }; const setSpeed = (speed) => {
    videoPlayer.current.playbackRate = speed;
  }; const onPlaying = () => {
    setCurrentTime(videoPlayer.current.currentTime);
    setSeekValue(
      (videoPlayer.current.currentTime / videoPlayer.current.duration) * 100
    );
  }; return (
    <div className="App">
      <video
        width="320"
        height="240"
        ref={videoPlayer}
        onTimeUpdate={onPlaying}
      >
        <source
          src="https://www.learningcontainer.com/wp-content/uploads/2020/05/sample-mp4-file.mp4"
          type="video/mp4"
        />
        Your browser does not support the video tag.
      </video>
      <br />
      <p>{currentTime}</p>
      <input
        type="range"
        min="0"
        max="100"
        step="1"
        value={seekValue}
        onChange={(e) => {
          const seekto = videoPlayer.current.duration * (+e.target.value / 100);
          videoPlayer.current.currentTime = seekto;
          setSeekValue(e.target.value);
        }}
      />
      <div>
        <button onClick={play}>play</button>
        <button onClick={pause}>pause</button>
        <button onClick={stop}>stop</button>
        <button onClick={() => setSpeed(0.5)}>0.5x</button>
        <button onClick={() => setSpeed(1)}>1x</button>
        <button onClick={() => setSpeed(1.5)}>1.5x</button>
        <button onClick={() => setSpeed(2)}>2x</button>
      </div>
    </div>
  );
}
```

我们创建一个分配给视频元素的`videoPlayer` ref。

然后我们定义`currentTime`状态来获取当前播放时间。

`seekValue`有职位可找。

接下来，我们定义了获取视频播放器元素的 ref 的`play`函数，并对其调用`play`。

同样，我们在`pause`中调用`pause`。

而在`stop`中，我们调用`pause`，将视频元素的`currentTime`设置为 0。

在`setSpeed`中，我们调用`setCurrenTime`来设置视频的当前播放时间。

我们调用`setSeekValue`来移动视频搜索滑块输入。

在此之下，我们添加视频元素。

我们设置大小并为它分配一个 ref，这样我们就可以在函数中使用它。

我们还将`onTimeUpdate`处理程序设置为`onPlaying`函数，以获取设置的当前播放时间和寻道值。

`source`元素有视频源。

下面，我们以秒为单位显示`currentTime`值。

在那下面，我们显示范围输入，让我们设置视频的进度。

`value`道具设置为`seekValue`以在视频播放时移动滑块点。

在`onChange`函数中，我们设置`currentTime`并调用`setSeekValue`来设置`seekValue`状态。

在它下面，我们有播放、暂停和停止按钮，当我们点击它们时，它们调用上面的函数。

当我们点击其他按钮时，它们会调用`setSpeed`。

# 结论

我们可以用 React 和 JavaScript 轻松创建一个视频播放器。