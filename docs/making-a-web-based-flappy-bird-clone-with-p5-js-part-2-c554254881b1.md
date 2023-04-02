# 用 p5.js 制作基于 Web 的 Flappy Bird 克隆体|第 2 部分

> 原文：<https://javascript.plainenglish.io/making-a-web-based-flappy-bird-clone-with-p5-js-part-2-c554254881b1?source=collection_archive---------14----------------------->

![](img/76f346c8e4d0ec32b885df850db8c5e6.png)

## 概述

这是系列教程的第 2 部分，我将带您了解如何使用 p5.js 制作 flappy bird 克隆体。在第 1 部分中，我介绍了 p5.js 的基本概念，并向您展示了如何将背景对象渲染到 p5.js 画布中。如果您尚未完成第 1 部分[,您可以在此处](/how-to-make-a-web-based-flappy-bird-clone-with-p5-js-part-1-2913fde25c8a)找到它。如果你是来继续的，那我们就开始吧。

## 地面物体——假装无限

首先，让我们来看看地面物体。在 Flappy Bird 中，地面实际上是水平向后移动的物体，这就造成了鸟向前飞的错觉。现在棘手的部分是如何让地面看起来可以无限延伸。

让我们想想我们能做这件事的所有方法。我们真的可以有一个穿过屏幕的无限大的地面吗？嗯，也许吧，但是你需要一个非常长的图像。可以想象，一个无限长的图像在任何游戏中都不是很实用。那么我们如何让一个有限的物体无限地走下去呢？我们实际上不需要太多，因为我们在第 1 部分中定义的框架不是无限的，我们可以隐藏框架外发生的事情。

第一种我们可以伪造无限的方法是我们可以从两个地面物体开始，它们都和画布一样宽。第一个完全在屏幕上开始，第二个在屏幕外紧挨着第一个。然后我们可以开始移动地面，直到第二个完全适合屏幕，第一个离开屏幕。然后，我们可以删除第一个，然后在第二个后面的屏幕上添加一个新的，然后无限重复。

这很好，但我们可以做得更好。想想看，我们真的需要去掉第一个吗？那是一大堆我懒得做的烦人的数组操作。我们能不能只让第一个一过屏幕就出现在后面？你当然可以，这正是我们要做的。

创建一个名为 Ground.js 的新文件，不要忘记将脚本包含在 HTML 文件中——在索引脚本之前。

在 index.js 中，让我们定义 GROUND_HEIGHT 全局变量，因为我们将在其他几个地方使用该变量。我们还将在预加载函数中加载地面图像——在本例中，我将其定义为 BASE_IMG。

```
// index.js
const WIN_WIDTH = 400;
const WIN_HEIGHT = WIN_WIDTH * 1.62;
const GROUND_HEIGHT = 110;let BG_IMG;
let BASE_IMG;function preload() {
 BG_IMG = loadImage("assets/bg.png");
 BASE_IMG = loadImage("assets/base.png");
}
```

现在要制作实际的地面对象，在 Ground.js 中如下定义该对象:

```
// Ground.jsfunction Ground() {
 this.velocity = 5;
 this.x1 = 0;
 this.x2 = width; 
 this.y = height — GROUND_HEIGHT;
// width and height references the canvas's dimension provided my p5this.update = () => {
 this.x1 -= this.velocity;
 this.x2 -= this.velocity;
 if (this.x1 <= -width) {
  this.x1 = width;
 }
 if (this.x2 <= -width) {
  this.x2 = width;
 }
 };this.show = () => {
 // Just as before, we must explicitly tell p5 to render the ground object 
 image(BASE_IMG, this.x1, this.y, width, BASE_IMG.height);
 image(BASE_IMG, this.x2, this.y, width, BASE_IMG.height);
 };
}
```

地面的 y 属性(或垂直位置)是画布的高度减去地面的高度。这是因为 p5 定义了一个坐标系统，其中 y 位置越大，物体越低——我知道这有点奇怪。还应该注意，x 位置越大，对象在画布上就越靠右。

在 show 函数中，通过调用 p5 提供的 image 函数来渲染地面。这里，我们同时显示两幅图像。正如你可能看到的，从我们调用函数的方式，只有每个对象的 x 位置被更新，而所有其他变量保持不变。

在 update 函数中——它也将在每个渲染周期运行——通过减去一个我们称为 velocity 的变量来更新 x 位置。请注意，速度不一定是 5，只是根据我自己的实验，我认为 5 似乎是一个很好的速度，但你当然可以通过改变这个变量来进行自己的实验。有趣的逻辑是，如果一个地面对象完全离开了屏幕，我们只需通过将 x 位置设置为等于屏幕的宽度来使它更新回屏幕的另一侧。

```
// index.js...let BG_IMG;
let BASE_IMG;let ground; //the global ground variablefunction preload() {
 BG_IMG = loadImage("assets/bg.png");
 BASE_IMG = loadImage("assets/base.png");
}function setup() {
 createCanvas(WIN_WIDTH, WIN_HEIGHT);
 ground = new Ground(); // Initialize the new ground here
}function draw() {
 background(BG_IMG); ground.update(); 
 ground.show();
}
```

What you should have now

## 管道物体——假装无限的另一种方式

现在让我们移动到管道对象。同样，在这里我们也想假装无穷大，因为只要游戏没有结束，管道就会一直出现。当然，我们可以使用与地面类似的策略。然而，在这里，我们将在不同的高度初始化管道，以使游戏更有趣，所以让我们使用前面讨论的第一个策略，当管道移出屏幕时，我们将立即删除管道，并将一个“新”管道添加到我们的管道数组中。

```
// Pipe.js
function Pipe() {
 this.SCALE = 1.75;
 this.velocity = 5; //velocity should be the same as the ground
 this.gap = 200; // distance between the top and bottom pipe this.x = width;
 this.y = random(200, 400); 

//The height that the pipe will have should be random and it's x position will start out from the right of the screen this.scaledWidth = this.SCALE * PIPE_UP_IMG.width;
 this.scaledHeight = this.SCALE * PIPE_UP_IMG.height; this.topPosition = this.y — this.scaledHeight — this.gap; this.show = () => {
  image(PIPE_UP_IMG, this.x, this.y, this.scaledWidth, this.scaledHeight);

  image(PIPE_DOWN_IMG, this.x, this.topPosition, this.scaledWidth, this.scaledHeight);
 }; this.update = () => {
  this.x = this.x — this.velocity;
 }; this.isOff = () => {
  return this.x < -this.scaledWidth;
 };
}
```

在 Pipe.js 中，我们包含了更新单个管道对象的逻辑。show 函数只显示顶部和底部管道，而 update 方法只是将管道向左移动速度量。最后，我们定义一个 isOff 方法来告诉我们这个特定的管道是否已经移动到屏幕左侧。

现在我们已经封装了一个管道的逻辑，接下来我们可以展示多个管道。在这个特殊的例子中，我在索引文件中编写了这个逻辑，但是您可以将这个相同的逻辑提取到一个名为 Pipes.js 之类的单独文件中。

```
// index.js...
let PIPE_UP_IMG;
let PIPE_DOWN_IMG;let ground; //the global ground variable
pipes = []; // the global pipes arrayfunction preload() {
 ...
 PIPE_UP_IMG = loadImage("assets/pipeUp.png");
 PIPE_DOWN_IMG = loadImage("assets/pipeDown.png");
}function setup() {
 createCanvas(WIN_WIDTH, WIN_HEIGHT).touchStarted(jumpEvent);
 ground = new Ground(); // Initialize the new ground here
}function draw() {
 background(BG_IMG); pipesUpdate() 
 pipes.forEach(pipe => pipe.show()) 
 //pipes must be shown before the ground so that the ground is rendered on top of the pipe ground.update(); 
 ground.show();
}function pipesUpdate() {
 if (frameCount % 60 === 0) {
  const pipe = new Pipe();
  pipes.push(pipe);
 } pipes.forEach((pipe, idx) => {
  pipe.update();
  if (pipe.isOff()) {
   pipes.splice(idx, 1);
  }
}
```

在 pipesUpdate 函数中，您可以看到 if 语句，其中我向数组添加了一个新管道。frameCount 是一个 p5 对象，它跟踪从画布初始化开始已经渲染了多少帧。这只是一种让添加新管道的时间间隔保持不变的方式，60 帧的倍数似乎对我来说最合适，但是您可以尝试这个值

Now we should have this

## 未完待续…

好的，接下来是鸟本身，这将比我们在这里做的要复杂一些。你可以在这里找到第三部。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)