# 我无法在 WebRTC 中使用 JavaScript 访问我的摄像头和麦克风。

> 原文：<https://javascript.plainenglish.io/cant-access-camera-or-microphone-in-webrtc-apps-solve-using-navigator-mediadevices-web-api-c0ffe5cbd32c?source=collection_archive---------2----------------------->

## 如何用 navigator.mediaDevices Web API 解决这个问题

![](img/bc9ceec756e24c8d573e3a0c00a84dc5.png)

Photo by [Surface](https://unsplash.com/@surface?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时在 WebRTC 应用程序中会出现浏览器无法访问摄像头或麦克风的情况。可能它正在被另一个软件使用，或者它根本没有摄像头。

在这篇文章中，我想向你展示如何使用 [Web API MediaDevices](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices) 来检查这一点。这超级简单，让我们开始吧。在文章的最后，如果你是一个懒惰的开发者，你可以使用我的代码(*你应该是*😅).

# 列出媒体输入和输出设备

作为开发者，我们不能做出为什么不能接入用户麦克风或摄像头的假设。使用`navigator.mediaDevices.enumerateDevices()`方法，我们可以获得媒体输入和输出设备的列表。

这个方法返回一个`Promise`，所以得到那个列表超级简单！

```
navigator.mediaDevices.enumerateDevices()
  .then(function(devices) {
    console.log('devices: ', devices);
  })
  .catch(function(err) {
    console.log(err.name + ": " + err.message);
  });
```

这是我此刻的结果。

```
[
   {
      "deviceId":"default",
      "kind":"audioinput",
      "label":"Default - MacBook Pro Microphone (Built-in)",
      "groupId":"8e16639392cc33ed9421836432166375ff23720fe41cfab2bf1d350b8f83f5f5"
   },
   {
      "deviceId":"6e06241b89f9043e7101d5dbd2bdf91f7ba9ea78c0e5aa5efc58927e1f28c6f6",
      "kind":"audioinput",
      "label":"ray’s AirPods Pro (Bluetooth)",
      "groupId":"48357ddc7bab573800fd4db4c1d9dac1d0fb800d1fb9fd21cd2608c330db9a20"
   },
   {
      "deviceId":"2108da4a847ad10cf90c85af7cb29a29db54bf810afb18e58639e345fbe2abd7",
      "kind":"audioinput",
      "label":"MacBook Pro Microphone (Built-in)",
      "groupId":"8e16639392cc33ed9421836432166375ff23720fe41cfab2bf1d350b8f83f5f5"
   },
   {
      "deviceId":"default",
      "kind":"audiooutput",
      "label":"Default - ray’s AirPods Pro (Bluetooth)",
      "groupId":"48357ddc7bab573800fd4db4c1d9dac1d0fb800d1fb9fd21cd2608c330db9a20"
   },
   {
      "deviceId":"dd51ddd88220fda9209daf2dba9608b960a7539d1deac7007af734b3d30580fc",
      "kind":"audiooutput",
      "label":"ray’s AirPods Pro (Bluetooth)",
      "groupId":"48357ddc7bab573800fd4db4c1d9dac1d0fb800d1fb9fd21cd2608c330db9a20"
   },
   {
      "deviceId":"985ba2f44a8db0d1ef0b50f8e6f7a0b682535b91ea631cad24ae483e871cebfd",
      "kind":"audiooutput",
      "label":"U32J59x (DisplayPort)",
      "groupId":"91b72f113dc19f56739a74dcd2d8a422a4e5abef6a1efa0fd2e9f17ac2216bf0"
   },
   {
      "deviceId":"223700057fcf336336b3d6ab9f8dc7a281cb52b2409bec081aaeed8aa68c518a",
      "kind":"audiooutput",
      "label":"[Samsung] Soundbar J-Series (Bluetooth)",
      "groupId":"f1b0ba1e49bf6873ee2cb14193d5e6fa29fa3fc86e4b858734d2f15e0103bd66"
   },
   {
      "deviceId":"67d7d9cddb6f0cdc0fd7d13c9dd4f85f466be86d0a55c7ae572155d1383a1371",
      "kind":"audiooutput",
      "label":"MacBook Pro Speakers (Built-in)",
      "groupId":"8e16639392cc33ed9421836432166375ff23720fe41cfab2bf1d350b8f83f5f5"
   }
]
```

所以你会得到所有媒体设备的完整列表。但有一点是清楚的；列表中没有相机。(*我的新 M1 有一个有缺陷的网络摄像头，应该被修复*)如果我没有这个问题，我可能不会调查这个问题，也不会从用户的角度尝试修复它。

现在我们知道了计算机连接了哪种类型的输入设备，我们可以为用户编写一条错误消息。请注意，这与访问无关；这只是连接到我的计算机的媒体设备列表。

# 拿到摄像机和麦克风。

但是我们想区分它是否与访问问题有关，媒体设备是否由不同的软件使用，或者是否没有连接摄像头。

让我们检查一下是否可以访问用户电脑的摄像头和麦克风。

为此，我们可以使用`navigator.mediaDevices.getUserMedia(constraints)`。这个方法还返回一个`Promise`，这使得它很容易实现。

```
async function getMedia(constraints) {
  let stream = null;
  const constraints = {audio: true, video: true} try {
    stream = await navigator.mediaDevices.getUserMedia(constraints);
    /* use the stream */
  } catch(err) {
    /* handle the error */
  }
}
```

通过这个功能，我们可以看到我们是否可以访问麦克风和摄像头。但是由于我的电脑没有连接摄像头，我们得到了一个`NotFoundError`，但是我们看不到是麦克风还是摄像头的问题。

因此，我们必须为音频和视频分别运行该功能。

# 音频和视频访问

因此，我创建了一个功能来发现是否有音频和视频设备连接到计算机，以及我们是否可以访问它。该函数返回一个带有完整结果的`Promise`。

```
function getMediaDevices() {
  /*
   * This function checks the device if it has any audio and video input.
   * This is purely to check, not to check if the user has allowed the application to use an audio or video input device.
   * The function returns a Promise with an object of what types of input devices the computer has.
   * Documentation can be found: [https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/enumerateDevices](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/enumerateDevices)
   */
  let hasVideo = false;
  let hasAudio = false;
  let audioAccess = false;
  let videoAccess = false; return new Promise(async (resolve, reject) => {
    if (navigator.mediaDevices) {
      let devices = null; try {
        devices = await navigator.mediaDevices.enumerateDevices();
        console.log(JSON.stringify(devices));
        devices.forEach(function (device) {
          if (device.kind === "audioinput") {
            hasAudio = true;
          }
          if (device.kind === "videoinput") {
            hasVideo = true;
          }
        });
      } catch (error) {
        console.error("There are no media devices available in this device.");
      } try {
        audioAccess = await navigator.mediaDevices.getUserMedia({
          audio: true
        });
      } catch (error) {
        console.error(
          "The browser has no access to the microphone of the device."
        );
      } try {
        videoAccess = await navigator.mediaDevices.getUserMedia({
          video: true
        });
      } catch (error) {
        console.error("The browser has no access to the camera of the device.");
      } resolve({
        hasAudio: hasAudio,
        hasVideo: hasVideo,
        audioAccess: audioAccess,
        videoAccess: videoAccess
      });
    } else {
      reject({ error: "The media devices could not be checked" });
    }
  });
}
```

但是如果其中一个设备有问题，我们想给用户一个消息。例如，如果摄像机已经被团队使用。然后我们可以看到一个视频设备，但我们无法访问它。

对于错误处理程序，我创建了一个函数，如果您愿意，可以使用它。

```
function mediaDevicesAvailable() {
  console.log("Check Media!");
  getMediaDevices().then((media) => {
    const errorWrapper = document.querySelector(".error-on-initialize");
    let errorMessage = null; if (!media.hasAudio && media.hasVideo) {
      errorMessage = "Could not find your microphone.";
    } else if (!media.hasVideo && media.hasAudio) {
      errorMessage = "Could not find your camera.";
    } else if (!media.hasVideo && !media.hasAudio) {
      errorMessage = "Could not find your camera and microphone. ";
    } if (!media.audioAccess && media.videoAccess) {
      errorMessage = deviceErrorMsg("microphone");
    } else if (media.audioAccess && !media.videoAccess) {
      errorMessage = deviceErrorMsg("camera");
    } else if (!media.audioAccess && !media.videoAccess) {
      errorMessage = deviceErrorMsg("camera and microphone");
    } if (errorWrapper) {
      errorWrapper.innerHTML = errorMessage;
    }
  });
}function deviceErrorMsg(device) {
  return `We can not use your ${device}. Please turn off any other software that is using your ${device}.`;
}
```

确保为 DOM 中的现有元素定义了选择器。如果有的话，它会显示一个错误。否则，它不会显示任何内容。

如果您想在示例中看到这一点，请检查下面的[代码栏](https://codepen.io/devbyrayray/pen/vYypaEJ)。

# 结论

也许这不是您的确切用例，但是使用我的代码作为灵感来找出为什么您不能访问音频或视频设备。

如果你有问题，请让我知道。😉

*编码快乐！🚀*