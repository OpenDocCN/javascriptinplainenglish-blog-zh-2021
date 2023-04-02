# 用 Phaser 和 Web Sockets 构建一个多人浏览器游戏

> 原文：<https://javascript.plainenglish.io/develop-your-first-multiplayer-browser-game-io-99931c7d3a5b?source=collection_archive---------2----------------------->

浏览器游戏不需要安装任何客户端软件或任何东西。有些人绝对喜欢它，是了不起的游戏玩家，而对另一些人来说，这可能是消除紧张和转移注意力的好方法(我属于后一类)。没有任何麻烦—您需要做的只是打开网络浏览器，与朋友或网上的人一起玩您喜欢的任何游戏。

![](img/78258687b80833b5d6db455c37583a49.png)

一款撞球游戏或者射击游戏，通常免费玩，多人浏览器游戏值得一试。说到这里，在这篇文章中，我将指导你开发你的第一个多人浏览器游戏。在开始开发游戏之前，确保你有下面提到的东西:

*   这是一个服务器环境，我们将使用它来提供文件和处理 Web 套接字。(下载:【https://nodejs.org/en/download/ 
*   [**http://localhost**](http://localhost)—这是计算机的本地主机地址，用于运行只能从您的机器访问的服务器。
*   这是一个桌面和移动 HTML5 游戏框架，我们用于客户端游戏逻辑。(下载:[https://phaser.io/download/stable)](https://phaser.io/download/stable))从此链接下载 JS 文件。
*   **NPM** —这是一个软件包管理器，使得管理软件包和从终端下载项目变得更加容易。(下载:[https://www.npmjs.com/get-npm)](https://www.npmjs.com/get-npm))
*   **Express JS framework**—帮助我们托管服务器并将文件从服务器发送到客户端。(“npm 快速安装”)
*   **web sockets**—NPM:“NPM 安装 socket.io”

一旦我们安装完上面提到的东西，我们现在就可以开始编码了。

## 设置服务器

打开你的 VS 代码，新建一个名为“Game”的文件夹。在游戏文件夹中，创建一个名为 **server.js** 的文件。该将成为服务器的主入口，即**主文件**。我们将处理从这里开始的所有服务器。下面是 server.js 的代码:

```
// loading all dependencies**var express = require(‘express’);
var http = require(‘http’);
var path = require(‘path’);
var socketIO = require(‘socket.io’);**//setting the port**var port = 8080;**//initializing framework**var players = {};**// instancing**var app = express();** //default constructor
**var server = http.Server(app);** //to launch Express
**var io = socketIO(server);** //passing ‘server’ so that it runs on IO server
**app.set(‘port’, port);**//used ‘public’ folder to use external CSS and JS**app.use(‘/public’, express.static(__dirname + “/public”));**//port listening**server.listen(port, function() {
console.log(“listening…”);
});**//handling requests and responses by setting the Express framework**app.get(“/”, function (req, res) {
res.sendFile(path.join(__dirname, “landing.html”));
});****io.on(‘connection’, function (socket) {** //returns socket which is a piece of data that talks with server and client**console.log(“Someone has connected”);
players[socket.id] = {
player_id: socket.id,
x: 500,
y: 500
};
socket.emit(‘actualPlayers’, players);** //sends info back to that socket and not to all the other sockets
**socket.broadcast.emit(‘new_player’, players[socket.id]);**// when player moves send data to others**socket.on(‘player_moved’, function(movement_data) {
players[socket.id].x = movement_data.x;
players[socket.id].y = movement_data.y;
players[socket.id].angle = movement_data.angle;**// send the data of movement to all players**socket.broadcast.emit(‘enemy_moved’, players[socket.id]);
});**//synchronizing shooting**socket.on(‘new_bullet’, function(bullet_data) {
socket.emit(‘new_bullet’, bullet_data);
socket.broadcast.emit(‘new_bullet’, bullet_data);
});
socket.on(‘disconnect’, function () {
console.log(“someone has disconnected”);
delete players[socket.id];
socket.broadcast.emit(‘player_disconnect’, socket.id);
});
});**
```

在上面的代码中，我们使用了一个名为**landing.html**的 HTML 文件，它包含了建立基本网页结构的代码。这个 html 文件是在游戏文件夹中创建的。landing.html 的代码如下所示:

```
<!DOCTYPE html>
<html lang=”en”>
<head>
<meta charset=”UTF-8">
<meta name=”viewport” content=”width=device-width, initial-scale=1.0">
<meta http-equiv=”X-UA-Compatible” content=”ie=edge”>
<script src=”/public/js/phaser.js”></script>
<script src=”/public/js/player.js”></script>
<script src=”/public/js/shot.js”></script>
<script src=”/public/js/enemy.js”></script>
<script src=”/socket.io/socket.io.js”></script>
<script src=”/public/js/main_game.js”></script>
<title>Document</title>
<style>
body, html {
margin: 0;
padding: 0;
}
</style>
</head>
<body>
</body>
</html>
```

现在，在游戏文件夹里面新建一个文件夹，命名为“Public”。此外，在公共文件夹中创建一个新文件夹，并将其命名为 **js** 。将 phaser.js 文件放入该文件夹。我们现在已经创建了主 JS 文件，它将在浏览器中启动我们的游戏。

## 文件和服务器配置

现在，我们必须创建一个管理整个游戏的文件。我们将在这个文件中初始化游戏和画布。因此，在 js 文件夹中创建一个新的 JS 文件，并将其命名为 main_game.js。

## 扩展类，创建玩家类。

Phaser 框架提供了基本功能和基本游戏对象。为了让代码尽可能的像**一样干净和模块化**，我们需要**扩展类**。扩展**意味着向已经存在的类添加功能**，比如变量、方法和事件。

我们为玩家使用的游戏对象被称为精灵。 **Sprite** 是一个可以分配物理碰撞器及其**更多功能图像**的类。如果我们想要创建一个类“player”，**我们需要扩展我们将使用的类**(这是 Sprite 类)。

首先，在 js 文件夹中创建一个“player.js”文件。在 JavaScript 中，我们能够通过**定义一个类**来扩展类:

```
class Player {
}
```

如您所见，第一个关键字是“class ”,表示我们正在创建一个类。第二个关键字是我们的类的名称，它必须与所有其他类不同。

现在，让我们**延伸一下:**

```
class Player extends Phaser.Physics.Arcade.Sprite {
}
```

我们现在已经**定义了**一个叫做 Player 的类，这个类**继承了**Phaser 类的功能。物理.街机.雪碧”。

我们还需要为我们的类定义一个构造函数。构造函数是当我们创建一个类的对象时执行的主入口函数。这可以通过键入**构造函数(参数)**来完成:

```
class Player extends Phaser.Physics.Arcade.Sprite {
constructor (scene, x, y){
}
}
```

我们需要输入 **3 个参数→** **场景**在我们已经在 main_game.js 中创建的场景上创建一个玩家， **x** 和 **y** 为我们玩家的位置。我们需要调用 **super** ，这是一个调用扩展类的构造函数的函数，当从我们的 player 类创建一个对象时，我们会调用它:

```
class Player extends Phaser.Physics.Arcade.Sprite {
constructor (scene, x, y){
super(scene, x, y, "player");
}
}
```

在超级函数中，我们需要通过**场景**、 **x** 和 **y 坐标**，因为 Sprite 类的构造函数需要它们。sprite 类构造函数**也需要一个图像**，它将用于渲染 Sprite。我们可以通过键入图像的名称来实现(可以是您选择的任何名称)。

最后，我们需要调用的最后一个函数是“add”→一个现有的函数，它将类发送到游戏的渲染部分，并将它渲染到显示器上，以便我们可以看到它。

```
class Player extends Phaser.Physics.Arcade.Sprite {
constructor (scene, x, y){
super(scene, x, y, "player");
scene.add.existing(this);
}
}
```

我们需要在 create 函数中将一个对象从 player 类初始化到 Player 变量

**`this.player = new Player(this, 500, 500);`**

**因此，我们在 main_game.js 中创建了一个播放器。**

## **球员运动**

**我们将让我们的玩家移动，但是因为我们必须扩展这个职业，我们可能还需要编辑我们的主游戏循环。那么，这个**主游戏循环**是什么？主游戏循环基本上是由函数表示的循环**，该函数**在每个 **CPU 滴答**时执行**。这个**导致**T21 玩家移动**，每秒渲染**新帧**。这确实是我们游戏中最重要的功能。正如我之前所说的，我们希望**有一个干净的代码**，为此我们将**在我们的玩家类中创建一个伪主** **游戏**循环。这是一个名为“更新”的功能，但它本身并不执行。所以，我们必须在 main_game.js 的更新函数中执行它。**

```
class Player extends Phaser.Physics.Arcade.Sprite {
constructor (scene, x, y){
super(scene, x, y, "player");
scene.add.existing(this);
}
update () { // pseudo update loop in Player class
}
}
```

在这个更新函数中，我们将制作玩家的运动逻辑。但是有一个先决条件，即**在主游戏更新**循环中调用它。我们将通过打开 main_game.js 和**在 **update** 函数中调用我们的玩家变量**的 update 方法来做到这一点。

```
function update() {
this.player.update();
}
```

现在我们已经理解了大部分内容，我们终于可以为 player.js 文件编写代码了。player.js 文件的代码是:

```
**class Player extends Phaser.Physics.Arcade.Sprite {
constructor (scene, x, y) {**// super**super(scene, x, y, “player”);**// render**scene.add.existing(this);**// physics rendering to move around and shoot with our players**scene.physics.add.existing(this);
this.player_speed = 600;
this.depth = 5;**// holds scene**this.scene = scene;
this.setInteractive();
this.setCollideWorldBounds(true);** //to ensure that the player stays in the window
**self = this;**// input handlers**this.keyUp = scene.input.keyboard.addKey(‘W’);
this.keyDown = scene.input.keyboard.addKey(‘S’);
this.keyLeft = scene.input.keyboard.addKey(‘A’);
this.keyRight = scene.input.keyboard.addKey(‘D’);**//scene.bullets is a group**scene.physics.add.collider(this, scene.bullets, function() {
alert(“You’re dead”);
});**// set the players to rotate towards the cursor**scene.input.on(“pointermove”, function(pointer) {**//convert the x and y axis from pointer to world axis**this.angle = Phaser.Math.RAD_TO_DEG * Phaser.Math.Angle.Between(this.x, this.y, pointer.x, pointer.y);
this.setAngle(this.angle);
}, this);**//shoot with the player on pressing F**scene.input.keyboard.on(‘keydown-F’, function() {**// player method shoot**var x = self.x;
var y = self.y;
var angle = self.angle;
self.scene.io.emit(‘new_bullet’, {x: x, y: y, angle: angle});** //for synchronizing shooting
**});
this.old_x = this.x;
this.old_y = this.y;
this.old_angle = this.angle;
}****update() {
this.setVelocity(0, 0);** //with every CPU tick, reset velocity to 0 since we don’t want it to forever move upwards or downwards**if (this.keyUp.isDown) {
this.setVelocityY(this.player_speed * -1);
}else if(this.keyDown.isDown){
this.setVelocityY(this.player_speed);
}
if (this.keyRight.isDown) {
this.setVelocityX(this.player_speed);
}else if(this.keyLeft.isDown){
this.setVelocityX(this.player_speed * -1);
}**//synchronizing enemy movement**var x = this.x;
var y = this.y;
var angle = this.angle;****if (x != this.old_x || y != this.old_y || angle != this.old_angle) {** //this if statement exists only when the player moves// send socket to server**this.scene.io.emit(‘player_moved’, {x: x, y: y, angle: angle});** //the object contains the movement data//assigning new movement data after the player has moved**this.old_x = x;
this.old_y = y;
this.old_angle = angle;
}
}
}**
```

现在，我们需要在 js 文件夹中创建一个名为 shot.js 的 JavaScript 文件，其中包含发射子弹的代码。shot.js 的代码如下所示:

```
**class Shot extends Phaser.Physics.Arcade.Sprite {
constructor (scene, x, y, angle) {**// super**super(scene, x, y, “bullet”);**// render**scene.add.existing(this);**// physics rendering**scene.physics.add.existing(this);**// set angle to shoot in the right direction**this.setAngle(angle);
this.setCollideWorldBounds(true);
this.bullet_speed = 800;
scene.bullets.add(this);**// layer depth**this.depth = 0;**// DEG TO RAD**angle = angle * (Math.PI / 180);
this.vx = this.bullet_speed * Math.cos(angle);
this.vy = this.bullet_speed * Math.sin(angle);
this.setVelocity(this.vx, this.vy);
}
}**
```

这是一个多人浏览器游戏，很明显会有敌人。每个客户都认为自己是玩家，其余的是敌人或对手。因此，敌人. js 文件的代码是:

```
**class Enemy extends Phaser.Physics.Arcade.Sprite {
constructor (scene, x, y, id) {**// super**super(scene, x, y, “enemy”);**// render**scene.add.existing(this);**// physics rendering**scene.physics.add.existing(this);
this.depth = 5;
this.id = id;
}
shoot() {**//this function will initialize a shooting from the player. It will spawn a bullet and send it somewhere**new Shot(this.scene, this.x, this.y, this.angle);
}
}**
```

我们已经完成了玩家创建、敌人移动、子弹方向和整体配置。现在是时候将所有内容合并到最终的主游戏中了，即 main_game.js 文件。main_game.js 文件的代码如下所示:

```
//storing height and width of the client’s browser**var window_height = window.innerHeight;
var window_width = window.innerWidth;**//since we’re using a phaser, we have to create a variable that holds the config data for the phaser.**var config = {
type: Phaser.AUTO,
width: window_width,
height: window_height,
backgroundColor: ‘#000000’,**//this object will hold configuration for arcade physics**physics: {
default: ‘arcade’,
arcade: {
gravity: {
y: 0,
},**//this means it will not cross 60**fps: 60,
}
},
scene: {**//function where the statements and the comments will be executed pre initializing the game**preload: preload,**//create function works when the game is initialized only once at a time**create: create,**//main game loop that executes every CPU tick since we are modifying it upto 60 only**update: update,
}
}**// holds a game instance**var game = new Phaser.Game(config);
var player;
var player_init = false;
function preload() {**// loading images**this.load.image(‘player’, ‘public/img/player.png’);
this.load.image(‘bullet’, ‘public/img/bullet.png’);
this.load.image(‘enemy’, ‘public/img/enemy.png’);
}
function create() {
this.io = io();** //initializing a new io server
**self = this;** //because we have an event handler
**this.enemies = this.physics.add.group();
this.bullets = this.physics.add.group();
this.io.on(‘actualPlayers’, function(players) {
Object.keys(players).forEach(function (id) {** //looping through the players**if (players[id].player_id == self.io.id) {**//we are in the array**createPlayer(self, players[id].x, players[id].y);
}else {**// we are creating other players**createEnemy(self, players[id]);
}
});
});
this.io.on(‘new_player’, function (pInfo) {** //we’re sending info about the new player from the server. So, we accept the info by pInfo
**createEnemy(self.scene, pInfo);
});**//synchronizing enemy movement**enemies_ref = this.enemies;** //holds the reference to the enemy’s group
**this.io.on(‘enemy_moved’, function(player_data) {
enemies_ref.getChildren().forEach(function(enemy) {
if (player_data.player_id == enemy.id) {** //set a new position for the enemy because the player data and enemy id in the enemy’s group match together**enemy.setPosition(player_data.x, player_data.y);
enemy.setAngle(player_data.angle);
}
});
});**//synchronizing shooting**this.io.on(‘new_bullet’, function(bullet_data) {
new Shot(self.scene, bullet_data.x, bullet_data.y,
bullet_data.angle);
});
}
function update() {
if (this.player_init == true) {
this.player.update();
}
}
function createPlayer(scene, x, y) {**//creating the player on the scene i.e making the new players visible**scene.player_init = true;
scene.player = new Player(scene, x, y);
}
function createEnemy(scene, enemy_info) {
const enemy = new Enemy(scene, enemy_info.x, enemy_info.y, enemy_info.player_id);
scene.enemies.add(enemy);
}**
```

我们完了。玩游戏很有趣，但是开发自己的游戏太有趣了。当您最终开始使用“node server.js”运行节点服务器，并在浏览器的两个选项卡中键入“localhost:8080”时(扮演两个玩家)，您的游戏是这样运行的:

## 结论

我希望这篇文章对你们在这个单调的时代做一些有趣的事情有足够的帮助。谢谢你阅读它。祝你今天开心！玩的开心！

*更多内容看*[***plain English . io***](https://plainenglish.io/)