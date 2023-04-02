# 如何创建自己的开源私人社交虚拟现实平台

> 原文：<https://javascript.plainenglish.io/how-to-create-your-own-open-source-private-social-vr-platform-897d90e43630?source=collection_archive---------8----------------------->

![](img/2a5982071f9a24ec640651305c293741.png)

也许你想要自己的虚拟现实办公室。自从上世纪 90 年代我读了一些很酷的科幻小说后，这一直是我的一个梦想。或者你是一名艺术家，你想向世界各地的人展示你的作品？或者也许你想要一个私人虚拟空间，去和其他有类似想法的人见面，在你自己的私人虚拟现实论坛上讨论？

假设你“不想拥有一个脸书控制的虚拟空间”，而是你自己的空间。您已经决定不将其建立在其他社交虚拟现实平台的[围墙花园](https://www.google.com/search?q=walled+garden+meaning&rlz=1C1SQJL_enUS858US858&oq=walled+garden&aqs=chrome.1.69i57j0i512l9.8283j0j7&sourceid=chrome&ie=UTF-8)上。有越来越多的人可以肯定。老实说，他们的许多功能集将比本文中的基础知识更先进。参见[中枢](https://hubs.mozilla.com/)、 [VRland](https://vrland.io/) 、[车架](https://developer.mozilla.org/en-US/docs/Web/API/WebXR_Device_API)等。

![](img/3622cc24643acb08591885520988978a.png)

你为什么想自己做这件事？答:因为你想要控制。控制您的内容，控制谁可以访问它。成本控制。控制，控制，控制！我知道，我听起来像一个[控制狂](https://www.google.com/search?q=what+is+a+control+freak&rlz=1C1SQJL_enUS858US858&oq=what+is+a+control+freak&aqs=chrome..69i57j0i512l6j0i22i30l3.5607j0j7&sourceid=chrome&ie=UTF-8)，但也许我不是唯一一个在外面的人。因此，本文。

然后，以下是如何使用[开源软件](https://opensource.com/resources/what-open-source)、VPS(虚拟专用服务器)以及几个多小时的设置和定制编码完成的？技能水平要求中等-高级-非常高级。除非你熟悉一些基本的东西，否则不要尝试这样做。网络开发，服务器安装/网络配置，图形技能，如 photoshop minimum，JavaScript，以及一些 3D 建模等。

![](img/950a783cc2f6451333c3e8afeb2d038f.png)

首先，为了便于管理，让我们限制一下范围。我不会向您展示如何配置私人登录系统。[或者如何设置自定义头像创建系统](https://readyplayer.me/)。或者甚至如何为你自己的虚拟空间做广告，或者建立电子商务，在你们都完成之后。有很多方法可以做这些事情，网上也有很多解释如何做的文章。

在我写这篇文章的时候，还没有很多文章解释如何建立你自己的社交虚拟空间。

为本文设置好所有的先决条件和期望后，现在让我们开始讨论我们的解决方案中涉及的一些软件技术。

WebXR -相对较新，是一个稳定且仍在发展的规范。这是我们在浏览器中做虚拟现实时要用到的。 [WebRTC](https://webrtc.org/) -更成熟的规范。这是我们将用于游客之间的交流。音频甚至视频。[A-frame](https://aframe.io/)——这是一种创建虚拟现实网页的奇妙且更简单的方法。

Three.js .用 JavaScript 处理我们的大部分图形，比 [WebGL](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API) 更高级。由于 A-frame 包含了 [Three.js](https://threejs.org/) ，我们不需要降低到这个细节级别来做我们想要做的事情，简化了大多数事情。

[Node.js](https://nodejs.org/en/) —服务器端 JavaScript 胶水处理我们几乎所有的通信。[网络化的 A-frame](https://github.com/networked-aframe)——或者有时被称为 NAF，神奇的开源代码用于将所有这些部分整合在一起。WebXR、WebRTC、A-frame、Three.js 和 Node.js 整合成一个功能性的私有开源[社交 VR 平台](https://www.google.com/search?q=social+VR+platform&rlz=1C1SQJL_enUS858US858&oq=social+VR+platform&aqs=chrome..69i57j69i60l3&sourceid=chrome&ie=UTF-8)。

如果你不熟悉其中的一些技术，你可能应该[钻研一下](https://www.merriam-webster.com/dictionary/bone%20up)，然后在这条路上继续前进。我也不得不这么做。

现在你需要做一些决定。你的[域名](https://www.cloudflare.com/learning/dns/glossary/what-is-a-domain-name/)会是什么？您将使用什么服务器技术？Linux，Windows，cloud， [VPS](https://www.dreamhost.com/blog/beginners-guide-vps/) ？你愿意花多少钱，金钱和时间，一个月保持这个运行？

每月大约 20 美元，我就可以安装和配置我自己的 windows VPS。我货比三家，花了很多时间配置和解决服务器上的问题。[我在这里的一篇文章中详细介绍了这一切。如果你安装的是 Linux 版本，可能会更容易、更便宜，但你需要在](https://michael-mcanally.medium.com/multi-user-vr-office-space-using-a-frame-and-naf-cab1409800ce)[网络版 github](https://github.com/networked-aframe/networked-aframe) 的说明中找到答案。

所以现在，终于在一些严肃的配置工作之后，我们有了我们的社交 VR 服务器设置。我们实际上能做什么？对于这一部分，我将提供一些链接，然后是金银岛示例的源代码。我不会提供资产，因为其中一些是我定制的，请你也这样做。但是，HTML 代码示例应该对您非常有用。因为它会显示完成了多少事情。为此，你需要[阅读我之前的一些解释文章](https://michael-mcanally.medium.com/a-four-year-writing-project-in-vr-13d3d8b821a7)。

**注意:**我已经标准化掉了 [A 帧版本 1.0.4](https://github.com/aframevr/aframe/releases/tag/v1.0.4) [，因为 aframe-extras 中的 navmesh 库仍然工作](https://github.com/n5ro/aframe-extras/tree/master/src/controls)。[更新版本的 A 型架打破了这个](https://discord.com/channels/758943204715659264/759166287901098024/880135266147385384)。此外，大多数都已针对 Oculus Quest 2 VR 耳机进行了调整。这篇文章的复杂性比它初看起来要高；由于大量的工作投入到建立这一点，并解释它，但鼓掌将不胜感激。[玩得开心](https://funbit64.com/)！请耐心等待所有要加载的内容。。。

我们开始吧:

[](https://funbit64.com:3025/VROffice2.html) [## VR 办公-正在加载用户空间，请稍候。

### 虚拟现实办公空间

funbit64.com](https://funbit64.com:3025/VROffice2.html) [](https://funbit64.com:3025/IslandComplex.html) [## 岛屿艺术综合体-正在加载用户空间，请稍候。

### 岛屿艺术虚拟现实画廊和会议由迈克尔麦卡纳利，VRArtscape-2021 年 5 月 31 日。

funbit64.com](https://funbit64.com:3025/IslandComplex.html) [](https://funbit64.com:3025/TeleportMindPalace.html) [## 心灵宫殿瞬间移动。。。请稍候

### 传送蜂巢房间-2021 年 8 月 27 日

funbit64.com](https://funbit64.com:3025/TeleportMindPalace.html)  [## 虚拟现实艺术景观

### 画廊艺术空间被颠覆的时机已经成熟。虚拟现实和降低成本的虚拟现实耳机提供了一个新的…

vrartscape.com](https://vrartscape.com/) 

```
<!DOCTYPE html>
<html>
  <head>
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta http-equiv="content-type" content="text/html; charset=utf-8">
    <title>Treasure Island Art Complex - Loading in 45 seconds</title>
    <meta name="description" content="Island Art VR Gallery and Meeting Complex by Michael McAnally, VRArtscape - May 31, 2021.">
    <meta name="viewport" content="width=device-width, user-scalable=no, minimum-scale=1.0, maximum-scale=1.0, shrink-to-fit=no">
    <meta name="mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-capable" content="yes" />
    <meta name="apple-mobile-web-app-status-bar-style" content="gray-translucent" />
    <script src="VRCore/aframe-master.min.js"></script>
    <script src="VRCore/aframe-extras.min.js"></script>
    <script src="VRCore/aframe-teleport-controls.min.js"></script>
    <script src="VRCore/aframe-text-geometry-component.min.js"></script>
    <script src="VRCore/aframe-alongpath-component.min.js" ></script>
    <script src="VRCore/aframe-curve-component.min.js"></script>
    <script src="VRCore/aframe-thumb-controls-component.min.js"></script>
    <script src="VRCore/aframe-lensflare-component.min.js"></script>
    <script src="VRCore/aframe-particle-system-component.min.js"></script>
    <script src="VRCore/socket.io.slim.js"></script>
    <script src="/easyrtc/easyrtc.js"></script>
    <script src="/dist/networked-aframe.js"></script>
    <script src="VRCore/aframe-randomizer-components.min.js"></script>
    <script src="/js/spawn-in-circle.component.js"></script>
    <script src="/js/info-message3.js"></script>
    <style type="text/css">
      #video-permission {
          position: fixed;
          top: 0;
          left: 0;
          width: 100%;
          height: 100%;
          background: white;
          z-index: 10000;
          display: none;
      }
      #video-permission-button {
        position: fixed;
        top: calc(50% - 1em);
        left: calc(50% - 60px);
        width: 120px;
        height: 2em;
      }
    </style><script type="text/javascript">
      var Speech = true;
      var audio1 = new Audio('assets/wav/action.wav');
      var audio2 = new Audio('assets/wav/swoosh.wav');
      var not360video = false;AFRAME.registerComponent('click-listener', {
        init: function () {
            this.el.addEventListener('click', function (evt) {
            });
        }
      });
      AFRAME.registerComponent('audiohandler', {
        init:function() {
            let playing = false;
            let audio = document.querySelector("#playAudio");
            this.el.addEventListener('click', () => {
                if(!playing) {
                    audio.play();
                } else {
                    audio.pause();
                    audio.currentTime = 0;
                }
                playing = !playing;
            });
        }
      })
     AFRAME.registerComponent('navigate', {
        schema: {url: {default: ''}},
        init: function () {
        var data = this.data;
            this.el.addEventListener('click', function () {
                window.location = data.url;
            });
        }
     });
      function speakInfo(narration) {
        var audio_msg = new SpeechSynthesisUtterance(narration);
        if (Speech === true) {
            window.speechSynthesis.speak(audio_msg);
        }
      }
      function changeOrb(orb_num) {
        document.getElementById('orbSky').setAttribute('material', 'src: #orb' + orb_num.toString());
        removeScene();
      }
      function removeScene() {
        document.getElementById('MeetingBuildings').setAttribute('visible', false);
        document.getElementById('RocketVirtualTXT').setAttribute('visible', false);
        document.getElementById('RocketVirtualTXT2').setAttribute('visible', false);
        document.getElementById('The_Island').setAttribute('visible', false);
        document.getElementById('ourOcean').setAttribute('visible', false);
        document.getElementById('artworkPosition1').setAttribute('visible', false);document.getElementById('artworkPosition3').setAttribute('visible', false);
        document.getElementById('artworkPosition4').setAttribute('visible', false);
        document.getElementById('artworkPosition5').setAttribute('visible', false);document.getElementById('artworkPosition11').setAttribute('visible', false);
        document.getElementById('artworkPosition12').setAttribute('visible', false);
        document.getElementById('artworkPosition13').setAttribute('visible', false);
        document.getElementById('artworkPosition17').setAttribute('visible', false);
        document.getElementById('ShootRaygun').setAttribute('visible', false);
        document.getElementById('Pedistal').setAttribute('visible', false);
        document.getElementById('Bust').setAttribute('visible', false);
        document.getElementById('Pedistal2').setAttribute('visible', false);
        document.getElementById('Palm_Tree1').setAttribute('visible', false);
        document.getElementById('Palm_Tree2').setAttribute('visible', false);
        document.getElementById('Palm_Tree3').setAttribute('visible', false);
        document.getElementById('Palm_Tree4').setAttribute('visible', false);
        document.getElementById('Palm_Tree6').setAttribute('visible', false);
        document.getElementById('Palm_Tree7').setAttribute('visible', false);
        document.getElementById('bridge-3').setAttribute('visible', false);
        document.getElementById('bridge-7').setAttribute('visible', false);
        document.getElementById('bridge-8').setAttribute('visible', false);
        document.getElementById('Foundation').setAttribute('visible', false);
        document.getElementById('FishA').setAttribute('visible', false);
        document.getElementById('FishB').setAttribute('visible', false);
        document.getElementById('FishC').setAttribute('visible', false);
        document.getElementById('FishD').setAttribute('visible', false);
        document.getElementById('FishE').setAttribute('visible', false);
        document.getElementById('FishF').setAttribute('visible', false);
        document.getElementById('FishG').setAttribute('visible', false);
        document.getElementById('FishH').setAttribute('visible', false);
        document.getElementById('video-screen').setAttribute('visible', false);
        document.getElementById('control-back').setAttribute('visible', false);
        document.getElementById('control-play').setAttribute('visible', false);
        document.getElementById('control-volume').setAttribute('visible', false);
        document.getElementById('progress-bar').setAttribute('visible', false);
        document.getElementById('progress-bar-track').setAttribute('visible', false);
        document.getElementById('progress-bar-fill').setAttribute('visible', false);
        document.getElementById('flare').setAttribute('visible', false);
        document.getElementById('cylinder1').setAttribute('visible', false);
        document.getElementById('sphere1').setAttribute('visible', false);
        document.getElementById('cylinder2').setAttribute('visible', false);
        document.getElementById('sphere2').setAttribute('visible', false);
        document.getElementById('modelSculpture').setAttribute('visible', false);
        document.getElementById('cylinder3').setAttribute('visible', false);
        document.getElementById('waterfountain').setAttribute('visible', false);
        document.getElementById('cylinder4').setAttribute('visible', false);
        document.getElementById('cylinder5').setAttribute('visible', false);
        document.getElementById('water').setAttribute('visible', false);
        document.getElementById('water-bridge').setAttribute('visible', false);
        document.getElementById('Treasure').setAttribute('visible', false);
        document.getElementById('fillWithGold').setAttribute('visible', false);document.getElementById('MovementControls').setAttribute('visible', false);
        document.getElementById('ReturnIsland').setAttribute('visible', true);
      }
      function restoreScene() {
        document.getElementById('orbSky').setAttribute('material', 'src: #orb1');
        document.getElementById('MeetingBuildings').setAttribute('visible', true);
        document.getElementById('RocketVirtualTXT').setAttribute('visible', true);
        document.getElementById('RocketVirtualTXT2').setAttribute('visible', true);
        document.getElementById('The_Island').setAttribute('visible', true);
        document.getElementById('ourOcean').setAttribute('visible', true);
        document.getElementById('artworkPosition1').setAttribute('visible', true);document.getElementById('artworkPosition3').setAttribute('visible', true);
        document.getElementById('artworkPosition4').setAttribute('visible', true);
        document.getElementById('artworkPosition5').setAttribute('visible', true);document.getElementById('artworkPosition11').setAttribute('visible', true);
        document.getElementById('artworkPosition12').setAttribute('visible', true);
        document.getElementById('artworkPosition13').setAttribute('visible', true);
        document.getElementById('artworkPosition17').setAttribute('visible', true);
        document.getElementById('ShootRaygun').setAttribute('visible', true);
        document.getElementById('Pedistal').setAttribute('visible', true);
        document.getElementById('Bust').setAttribute('visible', true);
        document.getElementById('Pedistal2').setAttribute('visible', true);
        document.getElementById('Palm_Tree1').setAttribute('visible', true);
        document.getElementById('Palm_Tree2').setAttribute('visible', true);
        document.getElementById('Palm_Tree3').setAttribute('visible', true);
        document.getElementById('Palm_Tree4').setAttribute('visible', true);
        document.getElementById('Palm_Tree6').setAttribute('visible', true);
        document.getElementById('Palm_Tree7').setAttribute('visible', true);
        document.getElementById('bridge-3').setAttribute('visible', true);
        document.getElementById('bridge-7').setAttribute('visible', true);
        document.getElementById('bridge-8').setAttribute('visible', true);
        document.getElementById('Foundation').setAttribute('visible', true);
        document.getElementById('FishA').setAttribute('visible', true);
        document.getElementById('FishB').setAttribute('visible', true);
        document.getElementById('FishC').setAttribute('visible', true);
        document.getElementById('FishD').setAttribute('visible', true);
        document.getElementById('FishE').setAttribute('visible', true);
        document.getElementById('FishF').setAttribute('visible', true);
        document.getElementById('FishG').setAttribute('visible', true);
        document.getElementById('FishH').setAttribute('visible', true);
        document.getElementById('video-screen').setAttribute('visible', true);
        document.getElementById('control-back').setAttribute('visible', true);
        document.getElementById('control-play').setAttribute('visible', true);
        document.getElementById('control-volume').setAttribute('visible', true);
        document.getElementById('progress-bar').setAttribute('visible', true);
        document.getElementById('progress-bar-track').setAttribute('visible', true);
        document.getElementById('progress-bar-fill').setAttribute('visible', true);
        document.getElementById('flare').setAttribute('visible', true);
        document.getElementById('cylinder1').setAttribute('visible', true);
        document.getElementById('sphere1').setAttribute('visible', true);
        document.getElementById('cylinder2').setAttribute('visible', true);
        document.getElementById('sphere2').setAttribute('visible', true);
        document.getElementById('modelSculpture').setAttribute('visible', true);
        document.getElementById('cylinder3').setAttribute('visible', true);
        document.getElementById('waterfountain').setAttribute('visible', true);
        document.getElementById('cylinder4').setAttribute('visible', true);
        document.getElementById('cylinder5').setAttribute('visible', true);
        document.getElementById('water').setAttribute('visible', true);
        document.getElementById('water-bridge').setAttribute('visible', true);
        document.getElementById('Treasure').setAttribute('visible', true);
        document.getElementById('fillWithGold').setAttribute('visible', true);document.getElementById('MovementControls').setAttribute('visible', true);
        document.getElementById('ReturnIsland').setAttribute('visible', false);
      }
      function sqrImg(imgNum) {
        document.getElementById('orb_2Dimg' + imgNum).setAttribute('visible', true);
        document.getElementById('OrbName_place' + imgNum).setAttribute('visible', true);
      }
      function dspImg(dimgNum) {
        document.getElementById('orb_2Dimg' + dimgNum).setAttribute('visible', false);
        document.getElementById('OrbName_place' + dimgNum).setAttribute('visible', false);
      }
      function playSwoosh() {
        audio2.play();
      }function playBlip() {
        audio1.play();
      }
      function playSound() {
      }
      function play360() {
          document.getElementById('vrVideo360').setAttribute('visible', true);
          document.getElementById('orbSky').setAttribute('visible', false);
          document.querySelector("#video-src").components.material.material.map.image.play();
          document.getElementById('video-screen').setAttribute('visible', false);
      }
      function STOPplay360() {
          document.getElementById('vrVideo360').setAttribute('visible', false);
          document.getElementById('orbSky').setAttribute('visible', true);
      }</script>
  </head>
  <body>
    <div id="video-permission">
    <button id="video-permission-button">Allow VR Video</button>
    </div>
    <button id="playButton" type="button">Play Music</button>
    <audio id="playAudio" autoplay loop>
        <!-- <source src="[https://rocketvirtual.com/A-Frame_WebXR/assets/mp3/Romanzeandante.mp3](https://rocketvirtual.com/A-Frame_WebXR/assets/mp3/Romanzeandante.mp3)" type="audio/mpeg"> --->
    </audio>
    <a-scene networked-scene="
      room: ArtIslandComplex;
      debug: true;
      adapter: easyrtc;
      audio: true;
      video: true;
    " info-message="htmlSrc: #messageText" shadow="type: pcfsoft" renderer="antialias: true; highRefreshRate: true"> 
      <a-assets timeout="30000">
        <a-asset-item crossorigin="anonymous" id="Island" src="assets/gltf/IslandSmooth.glb"></a-asset-item>
        <img crossorigin="anonymous" src="assets/img/floor1.jpg" id="floor" >
        <img crossorigin="anonymous" id="orb1" src="assets/360/image/skyland2.jpg">
        <img crossorigin="anonymous" id="flare-asset" src="assets/img/adjustflare.jpg">
        <a-asset-item id="MeetingComplex" src="assets/gltf/finalBuildingArtComplex2.glb" nav-agent="speed: 1.0; active: true"></a-asset-item>
        <a-asset-item crossorigin="anonymous" id="Palm" src="assets/gltf/PalmMinimal.glb"></a-asset-item>
        <video crossorigin="anonymous" id="video-src" src="assets/video/ArtProcessFinal.mp4"></video>
        <a-asset-item id="messageText" src="ControlsMessage.html" response-type="text"></a-asset-item>
        <a-asset-item id="optimerBoldFont" src="assets/fonts/optimer_bold.typeface.json"></a-asset-item><a-asset-item id="fountain" src="assets/gltf/marble_fountain.glb"></a-asset-item><img crossorigin="anonymous" src="assets/img/play2.png" id="play" >
        <img crossorigin="anonymous" src="assets/img/pause.png" id="pause" >
        <img crossorigin="anonymous" src="assets/img/volume-normal.png" id="volume-normal" >
        <img crossorigin="anonymous" src="assets/img/volume-mute.png" id="volume-mute" >
        <img crossorigin="anonymous" src="assets/img/seek-back.png" id="seek-back" ><img crossorigin="anonymous" id="artwork1" src="artwork/DSC_0137med6.jpg"><img crossorigin="anonymous" id="artwork3" src="artwork/DSC01280rmed6.jpg">
        <img crossorigin="anonymous" id="artwork4" src="artwork/DSC01693med6.jpg">
        <img crossorigin="anonymous" id="artwork5" src="artwork/DSC01361.jpg">

        <img crossorigin="anonymous" id="artwork11" src="artwork/DSC00921med6.jpg">
        <img crossorigin="anonymous" id="artwork12" src="artwork/DSC01255r.jpg">
        <img crossorigin="anonymous" id="artwork13" src="artwork/DSC01428med6.jpg">
        <img crossorigin="anonymous" id="artwork17" src="artwork/DSC00580med6.jpg"><img crossorigin="anonymous" id="blog" src="assets/img/wallInfo1.jpg">
        <img crossorigin="anonymous" id="writings" src="assets/img/wallInfo2.jpg">
        <img crossorigin="anonymous" id="server" src="assets/img/VRArtScapeCover3Final.png">
        <img crossorigin="anonymous" id="movementInstructions" src="assets/img/movementControl.jpg"><img crossorigin="anonymous" id="orb5" src="assets/360/image/theBeach.jpg">
        <img crossorigin="anonymous" id="orb7" src="assets/360/image/SAM_101_0152.jpg">
        <img crossorigin="anonymous" id="orb8" src="assets/360/image/SAM_101_0128.jpg">
        <img crossorigin="anonymous" id="orbthumb5" src="assets/360/image/thumb/theBeach_thumb.jpg">
        <img crossorigin="anonymous" id="orbthumb7" src="assets/360/image/thumb/SAM_101_0152_thumb.jpg">
        <img crossorigin="anonymous" id="orbthumb8" src="assets/360/image/thumb/SAM_101_0128_thumb.jpg">
        <img crossorigin="anonymous" id="imgthumb5" src="assets/360/image/imgthumb/theBeach.jpg">
        <img crossorigin="anonymous" id="imgthumb7" src="assets/360/image/imgthumb/SAM_101_0152_imgthumb.jpg">
        <img crossorigin="anonymous" id="imgthumb8" src="assets/360/image/imgthumb/SAM_101_0128_imgthumb.jpg">
        <img crossorigin="anonymous" id="ReturnBack" src="assets/img/ReturnBack.png">
        <a-asset-item id="fish1" src="assets/gltf/fishes/fish1.glb"></a-asset-item>
        <a-asset-item id="fish2" src="assets/gltf/fishes/fish2.glb"></a-asset-item>
        <a-asset-item id="fish3" src="assets/gltf/fishes/fish5.glb"></a-asset-item>
        <a-asset-item id="fish4" src="assets/gltf/fishes/fish15.glb"></a-asset-item><a-asset-item id="ShapeSculpture" src="assets/gltfSculpture/ShapesScuplture3.glb"></a-asset-item>
        <a-asset-item id="Raygun" src="assets/gltf/raygun4/raygun.glb"></a-asset-item>
        <a-asset-item id="MeBustAvatar" src="assets/gltf/FinalMeBustAvatar.glb"></a-asset-item>
        <a-asset-item id="Chest" src="assets/gltf/testChest2.glb"></a-asset-item>
        <img crossorigin="anonymous" src="assets/img/coins.jpg" id="coins">
        <a-mixin id="marble" geometry="primitive: sphere" scale=".30 .30 .30" animation__rotation="startEvents: mouseenter; pauseEvents: mouseleave; resumeEvents: mouseenter; property: rotation; to: 0 360 0; loop: true; dur: 10000" animation__mouseenter="startEvents: mouseenter; pauseEvents: mouseleave; resumeEvents: mouseenter; property: components.material.material.color; type: color; to: white;  dur: 500; " animation__mouseleave="property: components.material.material.color; type: color; to: gray; startEvents: mouseleave; dur: 500;" shadow ></a-mixin>
        <a-mixin id="spin" animation="property: rotation; to: 0 360 0; loop: true; dur: 100000; easing: linear"></a-mixin><a-asset-item id="RobotHead" src="assets/gltf/FinalEditRoboHead.glb"></a-asset-item>
        <a-asset-item id="LHand" src="assets/gltf/leftHandLow.glb"></a-asset-item>
        <a-asset-item id="RHand" src="assets/gltf/rightHandLow.glb"></a-asset-item>
        <template id="avatar-template">
          <a-entity networked-audio-source><a-box color="#FFF" position="0 1.4 0" material="" networked-video-source="" geometry="" scale="0.325 0.325 0.325"></a-box></a-entity>
        </template>
        <template id="head-template">
          <a-entity class="cam" gltf-model="#RobotHead" scale="0.004 0.004 0.004"></a-entity>
        </template>
        <template id="hand-left">
          <a-entity class="leftController">
            <a-entity gltf-model="#LHand" ></a-entity>
          </a-entity>
        </template>
        <template id="hand-right">
          <a-entity class="rightController">
            <a-entity gltf-model="#RHand" ></a-entity>
          </a-entity>
        </template>  
      </a-assets><a-entity id="The_Island" gltf-model="#Island" position="-208.88164 -9.83526 -154.40424" scale="140 140 140" visible="" shadow="cast: false; receive: true"></a-entity>
      <a-entity id="ambientlight" light="type: ambient; intensity: .95"></a-entity>
      <a-box id="Foundation" position="-3.32823 -0.09738 -7.89352" rotation="-90.00021045914971 90 0" scale="13.29474 10.89561 0.32555" width="4" height="4" color="#FFFFFF" shadow="receive: true" material="src: #floor; color: white; transparent: true; repeat: 50 50" geometry=""></a-box>
      <a-ocean id="ourOcean" position="-47.35699 -2.58219 40.11002" scale="6 6 6" width="50" depth="50" opacity=".55" ocean="color: #06C6CB; density: 45; amplitude: -0.2; speed: 0.95; speedVariance: 0.2"></a-ocean>
      <a-sky id="orbSky" material="src: #orb1" rotation="0 0 0" ></a-sky>
      <a-sphere id="flare" radius="0.05" color="yellow" lensflare="createLight:false; relative: true; src: #flare-asset; lightColor:yellow; intensity: 5; lightDecay: 500" position="-303.76151 57.79742 4.88911"></a-sphere>
      <a-entity id="MeetingBuildings" gltf-model="#MeetingComplex" position="9.89561 0.07 9.46907" rotation="0 90 0" scale="0.2 0.2 0.2" shadow=""></a-entity>
      <!-- Bridges allowing us to move around the island and on multiple levels.  -->
      <a-box id="water-bridge" position="-44.05655 -4.30731 -22.47425" rotation="-72.20929796254252 179.95229246350846 89.64325775278321" scale="6.0626 0.868 0.143" width="4" height="4" color="#FFFFFF" shadow="" material="" geometry="" opacity=".35"></a-box>
      <a-box id="bridge-3" position="-31.82349 5.17492 28.89981" rotation="-72.60521179897792 142.80400085840637 -82.01718949959195" scale="13.92453 1 0.143" width="4" height="4" color="#FFFFFF" opacity=".35" material="" geometry=""></a-box>
      <a-box id="bridge-7" position="-36.59874 -0.42997 -9.33153" rotation="-89.12816869496059 -90.00021045914971 90.00021045914971" scale="7.25388 0.868 0.143" width="4" height="4" color="#FFFFFF" shadow="" material="" geometry="" opacity=".35"></a-box>
      <a-box id="bridge-8" position="-91.33488 -0.62497 -42.07341" rotation="-89.66732198017871 44.930204378568895 -55.969382217354465" scale="8.09068 0.868 0.143" width="4" height="4" color="#FFFFFF" shadow="" material="" geometry="" opacity=".35"></a-box>
      <a-entity id="Palm_Tree1" gltf-model="#Palm" position="-122.21544 1.35503 -25.99071" rotation="0 0 0" scale=".002 .004 .002" shadow></a-entity>
      <a-entity id="Palm_Tree2" gltf-model="#Palm" position="26.89416 -0.91787 0.262" rotation="0 78.26 0" scale=".002 .004 .002" shadow></a-entity>
      <a-entity id="Palm_Tree3" gltf-model="#Palm" position="-53.19211 -1.21051 -11.23701" rotation="0 78.26 0" scale="0.002 0.003 0.002" shadow=""></a-entity>
      <a-entity id="Palm_Tree4" gltf-model="#Palm" position="0.36459 -0.13506 -41.8833" rotation="-6.868045090233179 61.74422383447803 5.194435370656045" scale="0.002 0.003 0.002" shadow=""></a-entity>
      <a-entity id="Palm_Tree6" gltf-model="#Palm" position="3.31197 0.23619 -4.07842" rotation="0 78.26 0" scale="0.002 0.003 0.002" shadow></a-entity>
      <a-entity id="Palm_Tree7" gltf-model="#Palm" position="-4.80875 0.18785 -12.51019" rotation="-0.7522935850067709 58.93100106038569 7.000971298703528" scale="0.002 0.003 0.002" shadow></a-entity>
      <a-entity id="RocketVirtualTXT" position="-12.68773 1.86857 -4.77643" rotation="0 90 0" text-geometry="value:Treasure Island VR Art Gallery; font: #optimerBoldFont" scale="0.25 0.25 0.25" material="color: #1C93EE"></a-entity><a-entity id="RocketVirtualTXT2" position="-18.286 1.06533 -9.08848" rotation="0 90 0" text-geometry="value: VR &amp; Art by Michael McAnally; font: #optimerBoldFont" scale="0.1 0.1 0.3" material="color: #1C93EE"></a-entity><a-entity id="TextSpot" position="-12.32473 1.90418 -5.60294" rotation="-1.4169246273585259 84.1428629195273 -86.78649018626092" light="angle: 75; decay: 0.65; distance: 1; type: spot; intensity: 0.35; color: #d57cbd"></a-entity>
      <a-entity id="TeleportingOrbsTXT" position="-16.02098 0.28739 1.42069" rotation="0 -180 0" text-geometry="value: Teleporting Orbs; font: #optimerBoldFont" scale="0.2 0.2 0.2" material="color: #F9CF45"></a-entity><a-cylinder id="cylinder1" position="3.27909 0.08504 -4.09886" scale="1.372 0.113 1.372" radius="0.5" height="1.5" color="#E3E3E3" shadow="" material="" geometry=""></a-cylinder>
      <a-sphere id="sphere1" position="3.29485 -0.0407 -4.11462" scale="0.457 0.307 0.457" radius="1.25" color="#51A727" shadow="" material="" geometry=""></a-sphere>
      <a-cylinder id="cylinder2" position="-4.82067 0.08504 -12.49902" scale="1.372 0.113 1.372" radius="0.5" height="1.5" color="#E3E3E3" shadow="" material="" geometry=""></a-cylinder>
      <a-sphere id="sphere2" position="-4.81461 -0.0407 -12.5219" scale="0.457 0.307 0.457" radius="1.25" color="#51A727" shadow="" material="" geometry=""></a-sphere>
      <a-entity id="waterfountain" gltf-model="#fountain" position="-1.46323 -0.14203 -9.20374" scale="2 .75 2" shadow=""></a-entity>
      <a-entity id="water" position="-1.46256 1.416 -9.20641" particle-system="color:#000, #FFF;duration:NaN;velocitySpread:2 3 2;velocityValue:0 9 0;accelerationSpread:1 0 1;particleCount:45;maxAge:1.5;texture: [https://funbit64.com:3025/assets/img/dot2.png](https://funbit64.com:3025/assets/img/dot2.png)" visible="true"></a-entity><!-- Our Treasure Chest in glTF format Link to license: [https://creativecommons.org/licenses/by/4.0/](https://creativecommons.org/licenses/by/4.0/)  Location: [https://sketchfab.com/3d-models/old-chest-efc357374ecf4d17a36e85f1237e624c](https://sketchfab.com/3d-models/old-chest-efc357374ecf4d17a36e85f1237e624c) -->
      <a-entity id="Treasure" gltf-model="#Chest" position="-36.36444 -9.686 -2.52202" rotation="0 -48.819441891916924 0" scale="0.01 0.01 0.01" visible="true"></a-entity><a-plane id="fillWithGold" position="-36.36285 -9.226 -2.50207" rotation="-89.67878113608133 66.30955154608043 -113.66164852466733" width="4" height="4" color="#EBE3B6" material="src: #coins" visible="true" scale="0.261 0.117 0.407"></a-plane><a-cylinder id="cylinder4" position="-1.45858 0.07067 -9.22259" scale="2.292 0.207 2.292" radius="0.5" height="1.5" color="#18C7D2" shadow="" material="" geometry="" opacity=".35"></a-cylinder><a-cylinder id="cylinder5" position="-1.45858 1.01776 -9.22259" scale="1.36 0.00668 1.36" radius="0.5" height="1.5" color="#18C7D2" shadow="" material="" geometry="" opacity=".35"></a-cylinder><a-sound id="alert-sound" src="src: url(assets/wav/action.wav)" autoplay="false" position="0 0 0"></a-sound>
      <a-video id="video-screen" src="#video-src" position="-12.6735 2.02774 -9.17445" rotation="0 90 0" scale="0.50761 0.49394 1" width="8" height="4" rotation="0 0 0" visible="true"></a-video> 
      <a-image class="clickable" id="control-back" width="0.4" height="0.4" src="#seek-back" position="-12.6735 0.655 -9.71611" rotation="0 90 0" visible="false" scale="0.85 0.85 0.85"></a-image>
      <a-image class="clickable" id="control-play" width="0.4" height="0.4" src="#play" position="-12.6735 0.655 -9.16072" rotation="0 90 0"></a-image>
      <a-image class="clickable" id="control-volume" width="0.4" height="0.4" src="#volume-mute" position="-12.6735 0.655 -8.59696" rotation="0 90 0" visible="false" scale="0.75 0.75 0.75"></a-image>
      <a-entity id="progress-bar" geometry="primitive:plane;height:0.1;width:4" material="opacity:0;transparent:true" position="-12.6735 0.93157 -9.17777" rotation="0 90 0" visible="false">
      <a-plane id="progress-bar-track" width="4" height="0.1" color="gray" position="" opacity="0.2" material="" visible="false" geometry=""></a-plane>
      <a-plane id="progress-bar-fill" width="2.496982785433659" height="0.1" color="#7198e5" position="-0.7515086072831705 0 0" geometry="" visible="false" material=""></a-plane>
      </a-entity><a-plane id="MovementControls" position="-1.36776 1.949 1.94834" scale="2 1 2" rotation="0 180 0" material="src: #movementInstructions; color: white; transparent: true; side: double" geometry="" ></a-plane><a-plane id="artworkPosition1" position="-13.11489 1.9 -5.99867" scale="1.33 1 1" rotation="0 -90 0" material="src: #artwork1; color: white; transparent: true; side: double" geometry="" ></a-plane>

      <a-plane id="artworkPosition3" position="-13.11958 1.949 -9.1733" scale="2.113 1.5 1" rotation="0 -90 0" material="src: #artwork3; color: white; transparent: true; side: double" geometry="" ></a-plane>
      <a-plane id="artworkPosition4" position="-17.80046 1.9 -20.07479" scale="1.33 1 1" rotation="0 0 0" material="src: #artwork4; color: white; transparent: true; side: double" geometry="" ></a-plane>
      <a-plane id="artworkPosition5" position="-16.021 1.89725 -20.06922" scale="1 1 1" rotation="0 0 90" material="src: #artwork5; color: white; transparent: true; side: double" geometry="" ></a-plane><a-plane id="artworkPosition11" position="-13.12109 1.9 -12.52271" scale="1.33 1 1" rotation="0 -90 0" material="src: #artwork11; color: white; transparent: true; side: double" geometry="" ></a-plane>
      <a-plane id="artworkPosition12" position="-13.10936 1.9 -17.81295" scale="1.33 1 1" rotation="0 -90 0" material="src: #artwork12; color: white; transparent: true; side: double" geometry="" ></a-plane>
      <a-plane id="artworkPosition13" position="-14.233 1.9 -20.07479" scale="1.33 1 1" rotation="0 0 0" material="src: #artwork13; color: white; transparent: true; side: double" geometry="" ></a-plane>
      <a-plane id="artworkPosition17" position="-13.11489 1.9 -0.33735" scale="1.33 1 1" rotation="0 -90 0" material="src: #artwork17; color: white; transparent: true; side: double" geometry="" ></a-plane><a-entity id="Bust" gltf-model="#MeBustAvatar" position="-18.19386 1.04973 -9.46061" rotation="-8.10105026535471 68.5767455414131 1.267382642829381" scale="0.003 0.003 0.003" shadow visible=""></a-entity>
      <a-box id="Pedistal2" position="-18.44864 0.55738 -9.53211" rotation="0 45 0" color="#FFFFFF" visible="" shadow="" material="" geometry=""></a-box>
      <a-entity id="PedistalSpot2" position="-18.06221 1.61283 -9.53659" rotation="-32.965126742851915 84.53533900919192 94.74716579180858" light="angle: 55; decay: 0.65; distance: 0.6; type: spot; intensity: 5; color: #d57cbd"></a-entity><a-entity id="ShootRaygun" gltf-model="#Raygun" position="-18.19039 0.92387 -14.97825" rotation="77.82714914380024 -84.96276552435951 0" scale="0.2 0.195 0.195" shadow visible=""></a-entity>
      <a-box id="Pedistal" position="-18.44864 0.55738 -14.90843" rotation="0 45 0" color="#FFFFFF" visible="" shadow="" material="" geometry=""></a-box>
      <a-entity id="GunPedistalSpot" position="-18.44864 1.398 -14.90843" rotation="-90.680 -0.538 4.844" light="angle: 55; decay: 0.5; distance: 1; type: spot"></a-entity><a-entity id="modelSculpture" position="-18.449 1.313 -4.08966" rotation="0 0 0" scale="0.0001 0.0001 0.0001" gltf-model="#ShapeSculpture" mixin="spin" shadow="recieve: false; cast: true"></a-entity>
      <a-cylinder id="cylinder3" position="-18.449 0.52434 -4.08966" radius="0.5" height="1.5" scale=".7 0.660 .7" color="#FFFFFF" shadow></a-cylinder>
      <a-entity id="SculptureSpot" position="-18.449 1.967 -4.08966" rotation="-88.61766329949904 -119.47201352508898 123.77091586195557" light="angle: 75; decay: 0.7; distance: 1.5; type: spot; intensity: 0.7"></a-entity><a-sphere id="orb_place5" class="clickable" mixin="marble" position="-15.2652 0.83949 1.28868" rotation="0 45 0" material="src: #orbthumb5" onclick="playSwoosh();changeOrb(5);STOPplay360();"  onmouseenter="sqrImg(5);" onmouseleave="dspImg(5);"></a-sphere>
      <a-sphere id="orb_place7" class="clickable" mixin="marble" position="-17.84266 0.83949 1.28868" rotation="0 45 0" material="src: #orbthumb7" onclick="playSwoosh();changeOrb(7);STOPplay360();"  onmouseenter="sqrImg(7);" onmouseleave="dspImg(7);"></a-sphere>
      <a-sphere id="orb_place8" class="clickable" mixin="marble" position="-16.52535 0.83949 1.28868" rotation="0 45 0" material="src: #orbthumb8" onclick="playSwoosh();changeOrb(8);STOPplay360();"  onmouseenter="sqrImg(8);" onmouseleave="dspImg(8);"></a-sphere>
      <a-entity id="OrbName_place5" material="color: #F9CF45" class="clickable" position="-15.9627 2.8206 1.78232" rotation="0 180 0" text-geometry="value: The Beach; size: 0.12; font: #optimerBoldFont" onclick="playBlip();speakInfo('The Beach');" visible="false"></a-entity>
      <a-entity id="OrbName_place7" material="color: #F9CF45" class="clickable" position="-15.9627 2.8206 1.78232" rotation="0 180 0" text-geometry="value: Pier and Bridge; size: 0.12; font: #optimerBoldFont" onclick="playBlip();speakInfo('Pier and Bridge');" visible="false"></a-entity>
      <a-entity id="OrbName_place8" material="color: #F9CF45" class="clickable" position="-15.9627 2.8206 1.78232" rotation="0 180 0" text-geometry="value: Downtown SF; size: 0.12; font: #optimerBoldFont" onclick="playBlip();speakInfo('San Francisco Market Street');" visible="false"></a-entity>
      <a-plane id="orb_2Dimg5" position="-16.55312 1.85704 1.7512" scale="2.168 1.8 0.1" rotation="0 180 0" material="src: #imgthumb5; side: double"  visible="false"></a-plane>
      <a-plane id="orb_2Dimg7" position="-16.55312 1.85704 1.7512" scale="2.168 1.8 0.1" rotation="0 180 0" material="src: #imgthumb7; side: double" visible="false"></a-plane>
      <a-plane id="orb_2Dimg8" position="-16.55312 1.85704 1.7512" scale="2.168 1.8 0.1" rotation="0 180 0" material="src: #imgthumb8; side: double" visible="false"></a-plane>
      <a-box id="ReturnIsland" class="clickable" position="-17.44352 0.29908 1.42523" rotation="-27.12095723251752 -180 0" material="src: #ReturnBack" scale="0.3 0.3 0.3" onclick="restoreScene();" shadow visible="false"></a-box><a-entity id="shadowcamera" light="intensity: 0.25; castShadow: true; shadowCameraLeft: -100; shadowCameraBottom: -100; shadowCameraRight: 100; shadowCameraTop: 100; shadowCameraVisible: false; angle: 180; decay: 0.5; shadowCameraFar: 100; shadowMapHeight: 1024; shadowMapWidth: 1024" position="-30.43253 34.92862 0.12768"></a-entity><a-entity id="mouseCursor" cursor="rayOrigin: mouse"></a-entity>
      <a-entity id="navmesh-walls" gltf-model="assets/gltf/FURTHERIslandNavmesh.gltf" visible="false" nav-mesh=""></a-entity>
      <a-entity id="avatar" networked="template:#avatar-template;attachTemplateToLocal:false;"
        movement-controls="constrainToNavMesh: true;" spawn-in-circle="radius:1">
        <a-entity class="cam" networked="template:#head-template;attachTemplateToLocal:false;" camera="active: true"
          position="0 1.6 0" look-controls></a-entity>
        <a-entity class="leftController" networked="template:#hand-left;attachTemplateToLocal:false;"
          hand-controls="hand: left; handModelStyle: lowPoly; color: #15ACCF"  teleport-controls="cameraRig: #avatar; teleportOrigin: #cam; button: trigger; type: line; curveShootingSpeed: 10; collisionEntities: #navmesh-walls; landingMaxAngle: 60" visible="true" ></a-entity>
        <a-entity class="rightController" networked="template:#hand-right;attachTemplateToLocal:false;"
          hand-controls="hand: right; handModelStyle: lowPoly; color: #15ACCF" laser-controls raycaster="showLine: true; far: 10; interval: 0; objects: .clickable, a-link;" line="color: #7cfc00; opacity: 0.5" visible="true"></a-entity>
      </a-entity><a-curve id="tracA" >
        <a-curve-point position="-33.15232 -3 -1.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-35.15232 -3 -2.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>  
        <a-curve-point position="-37.15232 -3 -5.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-35.15232 -3 -7.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-33.15232 -3 -9.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-36.15232 -3 -7.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>  
        <a-curve-point position="-38.15232 -3 -5.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-36.15232 -3 -2.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-33.15232 -3 -1.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
    </a-curve>
    <a-curve id="tracB" curve="">
        <a-curve-point position="-33.15232 -3 -3.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-36.15232 -3 -4.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>  
        <a-curve-point position="-37.15232 -3 -5.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-36.15232 -3 -3.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-33.15232 -3 -1.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-30.15232 -3 -4.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>  
        <a-curve-point position="-29.15232 -3 -5.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-30.15232 -3 -3.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-33.15232 -3 -3.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
    </a-curve>
    <a-curve id="tracC" curve="">
        <a-curve-point position="-31.15232 -3.5 -4.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-32.15232 -3.5 -2.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>  
        <a-curve-point position="-33.15232 -3.5 -5.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-30.15232 -3.5 -6.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-33.15232 -3.5 -3.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-35.15232 -3.5 -1.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>  
        <a-curve-point position="-32.15232 -3.5 -3.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-30.15232 -3.5 -4.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-31.15232 -3.5 -4.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
    </a-curve>
    <a-curve id="tracD" curve="">
        <a-curve-point position="-30.15232 -3.5 -4" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-30.15232 -3.5 -2" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>  
        <a-curve-point position="-32.15232 -3.5 -5.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-31.15232 -3.5 -2.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-30.15232 -3.5 5" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-32.15232 -3.5 -2.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>  
        <a-curve-point position="-30.15232 -3.5 -5.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-32.15232 -3.5 -2" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-30.15232 -3.5 -4" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
    </a-curve>
    <a-curve id="tracE" curve="">
        <a-curve-point position="-33.15232 -3 -2" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-35.15232 -3 -4" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>  
        <a-curve-point position="-33.15232 -3 -3" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-30.15232 -3 -4.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-30.15232 -3 -5.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-30.15232 -3 -6.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>  
        <a-curve-point position="-30.15232 -3 -6" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-29.15232 -3 -1" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-33.15232 -3 -2" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
    </a-curve>
    <a-curve id="tracF" curve="">
        <a-curve-point position="-29.15232 -3 -3" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-31.15232 -3 -2" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>  
        <a-curve-point position="-33.15232 -3 -4" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-36.15232 -3 -2" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-38.15232 -3 -3" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-34.15232 -3 -3" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>  
        <a-curve-point position="-30.15232 -3 -3" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-29.15232 -3 -3" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
    </a-curve>
    <a-curve id="tracG" curve="">
        <a-curve-point position="-32.15232 -3 -4" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-36.15232 -3 -3" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>  
        <a-curve-point position="-34.15232 -3 -3" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-34.15232 -3 -3" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-36.15232 -3 -2" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-37.15232 -3 -4.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>  
        <a-curve-point position="-36.15232 -3 -5.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-33.15232 -3 -3" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-32.15232 -3 -4" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
    </a-curve>
    <a-curve id="tracH" curve="">
        <a-curve-point position="-35.15232 -3 -5.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-37.15232 -3 -2" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>  
        <a-curve-point position="-33.15232 -3 -4" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-35.15232 -3 -2" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-37.15232 -3 -5.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-35.15232 -3 -2.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>  
        <a-curve-point position="-33.15232 -3 -1.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-34.15232 -3 -2.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
        <a-curve-point position="-35.15232 -3 -5.87581" geometry="height:0.1;width:0.1;depth:0.1" material="color:#ff0000" curve-point="" visible="false"></a-curve-point>
    </a-curve>
    <a-entity id="FishA" gltf-model="#fish1" alongpath="curve:#tracA;loop:true;dur:12000;rotate:true" scale="0.001 0.001 0.001" position="-4.27 1 -6" shadow="receive:false" rotation="-24 -90 90"></a-entity>
    <a-entity id="FishB" gltf-model="#fish2" alongpath="curve:#tracB;loop:true;dur:12000;rotate:true" scale="0.001 0.001 0.001" position="-4.27 1 -6" shadow="receive:false" rotation="-24 -90 90"></a-entity>
    <a-entity id="FishC" gltf-model="#fish3" alongpath="curve:#tracC;loop:true;dur:12000;rotate:true" scale="0.001 0.001 0.001" position="-4.27 1 -6" shadow="receive:false" rotation="-24 -90 90"></a-entity>
    <a-entity id="FishD" gltf-model="#fish4" alongpath="curve:#tracD;loop:true;dur:12000;rotate:true" scale="0.001 0.001 0.001" position="-4.27 1 -6" shadow="receive:false" rotation="-24 -90 90"></a-entity>
    <a-entity id="FishE" gltf-model="#fish1" alongpath="curve:#tracE;loop:true;dur:12000;rotate:true" scale="0.001 0.001 0.001" position="-4.27 1 -6" shadow="receive:false" rotation="-24 -90 90"></a-entity>
    <a-entity id="FishF" gltf-model="#fish2" alongpath="curve:#tracF;loop:true;dur:12000;rotate:true" scale="0.001 0.001 0.001" position="-4.27 1 -6" shadow="receive:false" rotation="-24 -90 90"></a-entity>
    <a-entity id="FishG" gltf-model="#fish3" alongpath="curve:#tracG;loop:true;dur:12000;rotate:true" scale="0.001 0.001 0.001" position="-4.27 1 -6" shadow="receive:false" rotation="-24 -90 90"></a-entity>
    <a-entity id="FishH" gltf-model="#fish4" alongpath="curve:#tracH;loop:true;dur:12000;rotate:true" scale="0.001 0.001 0.001" position="-4.27 1 -6" shadow="receive:false" rotation="-24 -90 90"></a-entity>
    </a-scene>
    <script>
      NAF.schemas.add({
        template: '#avatar-template',
        components: [
          'position',
          'rotation',
        ]
      });
      NAF.schemas.add({
        template: '#head-template',
        components: [
          'position',
          'rotation',
        ]
      });
      NAF.schemas.add({
        template: '#hand-left',
        components: [
          'position',
          'rotation',
        ]
      });
      NAF.schemas.add({
        template: '#hand-right',
        components: [
          'position',
          'rotation',
        ]
      });
      function onConnect() {
        console.log("connected to a room!");
      }
window.onload = function() {
  var context = new AudioContext();
}
document.querySelector('button').addEventListener('click', function() {
  context.resume().then(() => {
    console.log('Playback resumed successfully');
  });
});
      var AVideoPlayer = function() {
      this.duration         = 0;
      this.current_progress = 0;
      this.progressWidth    = 4;
      this.paused           = true;
      this.elProgressBar   = null;
      this.elProgressTrack = null;
      this.elProgressFill  = null;
      this.elAlertSound    = null;
      this.elVideo         = null;
      this.elVideoScreen   = null;
      this.elControlBack   = null;
      this.elControlPlay   = null;
      this.elControlVolume = null;
      this._initElements = function() {
        this.elProgressBar   = document.getElementById('progress-bar');
        this.elProgressTrack = document.getElementById('progress-bar-track');
        this.elProgressFill  = document.getElementById('progress-bar-fill');
        this.elAlertSound    = document.getElementById('alert-sound');
        this.elVideo         = document.getElementById('video-src');
        this.elVideoScreen   = document.getElementById('video-screen');
        this.elControlBack   = document.getElementById('control-back');
        this.elControlPlay   = document.getElementById('control-play');
        this.elControlVolume = document.getElementById('control-volume');
      }this.setProgress = function(progress) {
        var new_progress = this.progressWidth*progress;
        this._setProgressWidth(new_progress);
        var progress_coord = this._getProgressCoord();
        if (progress_coord != undefined) {
         progress_coord.x = -(this.progressWidth-new_progress)/2;
         this._setProgressCoord(progress_coord);
        }
      }
      this._getProgressCoord = function() {
        return AFRAME.utils.coordinates.parse(this.elProgressFill.getAttribute("position"))
      }
      this._getProgressWidth = function() {
        return parseFloat(this.elProgressFill.getAttribute("width"));
      }
      this._setProgressCoord = function(coord) {
        this.elProgressFill.setAttribute("position", coord);
      }
      this._setProgressWidth = function(width) {
        this.elProgressFill.setAttribute("width", width);
      }
      this.isProgressBarVisible = function(isVisible) {
        this.elProgressTrack.setAttribute("visible", isVisible);
        this.elProgressFill.setAttribute("visible", isVisible);
      }
      this.isControlVisible = function(isVisible) {
        this.elControlBack.setAttribute("visible", isVisible);
        this.elControlVolume.setAttribute("visible", isVisible);
        this.elVideoScreen.setAttribute("visible", isVisible);
      }
      this._addPlayerEvents = function() {
        var that = this;
        this.elVideo.pause();
        this.elVideo.onplay = function() {
          that.duration = this.duration;
        }
        this.elVideo.ontimeupdate = function() {
          if (that.duration > 0) {
            that.current_progress = this.currentTime/that.duration;
          }
          that.setProgress(that.current_progress);
        }
      }
      this._addControlsEvent = function() {
        var that = this;
        this.elControlPlay.addEventListener('click', function () {
          that._playAudioAlert();
          if (that.elVideo.paused) {
            this.setAttribute('src', '#pause');
            that.elVideo.play();
            that.paused = false;
            that.isProgressBarVisible(true);
            that.isControlVisible(true);
          } else {
            this.setAttribute('src', '#play');
            that.elVideo.pause();
            that.paused = true;
            that.isProgressBarVisible(false);
            that.isControlVisible(false);
         }
        });
        this.elControlVolume.addEventListener('click', function () {
          that._playAudioAlert();
          if (that.elVideo.muted) {
            that.elVideo.muted = false;
            this.setAttribute('src', '#volume-normal');
          } else {
            that.elVideo.muted = true;
            this.setAttribute('src', '#volume-mute');
          }
        });
        this.elControlBack.addEventListener('click', function () {
          that._playAudioAlert();
          that.elVideo.currentTime = 0;
        });
      }
      this._addProgressEvent = function() {
        var that = this;
        this.elProgressBar.addEventListener('click', function (e) {
          if (e.detail == undefined || e.detail.intersection == undefined || that.duration === 0) {
            return;
          }
          let seekedPosition = (e.detail.intersection.point.x+(that.progressWidth/2))/that.progressWidth;
          try {
            let seekedTime = seekedPosition*that.duration;
            that.elVideo.currentTime = seekedTime;
          } catch (e) {
          }
        });
      }
      this._playAudioAlert = function() {
        if (this.elAlertSound.components !== undefined && this.elAlertSound.components.sound !== undefined) {
         this.elAlertSound.components.sound.playSound();
        }
      }
      this._mobileFriendly = function() {
        if (AFRAME.utils.device.isMobile()) {
          var that = this;
          let video_permission        = document.getElementById('video-permission');
         let video_permission_button = document.getElementById('video-permission-button');
          video_permission.style.display = 'block';
          video_permission_button.addEventListener("click", function() {
            video_permission.style.display = 'none';
            that.elVideo.play();
            that.elVideo.pause();
          }, false);
        }
      }
      this.init = function() {
        this._initElements();
        this.setProgress(this.current_progress);
        this._addPlayerEvents();
        this._addControlsEvent();
        this._addProgressEvent();
        this._mobileFriendly();
      }
      this.init();
    }
      let scene = document.querySelector('a-scene');
      var cursor = document.querySelector('a-cursor');
      scene.lightOff = function() {
        scene.islightOn = true;
        scene.removeAttribute('animation__fogback');
        scene.setAttribute('animation__fog', "property: fog.color; to: #0c192a; dur: 800; easing: easeInQuad;");
      }
      scene.lightOn = function() {
        scene.islightOn = false;
        scene.removeAttribute('animation__fog');
        scene.setAttribute('animation__fogback', "property: fog.color; to: #dbdedb; dur: 800");
      }
      var videoPlayer = new AVideoPlayer();
      document.querySelector('#control-play').addEventListener('click', function () {
        if (videoPlayer.paused) {
          scene.lightOn()
        } else {
          scene.lightOff();
        }
      });
    </script>
  </body>
</html>
```

*更多内容请看*[***plain English . io***](http://plainenglish.io/)