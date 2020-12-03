---
title: Phaser 3 Snippets
author: liurongqing
date: 2020-11-11 10:00:00 +0800
categories: [Phaser3]
tags: [Phaser3, Snippets]
---

> 一些常用的代码片段

## Starter Snippets

### Html File

> 基本 html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, user-scalable=0, initial-scale=1, minimum-scale=1, maximum-scale=1, minimal-ui=1">
    <title>Game Title</title>
</head>
<body>
    <div id="root"></div>
    <script src="js/phaser.min.js"></script>
    <script src="js/main.js"></script>
    <script src="js/SceneMain.js"></script>
</body>
</html>
```

### Game Config File

> 游戏配置
> Example:var config = { type: Phaser.AUTO, width: 480, height: 640, parent: 'phaser-game', scene: [SceneMain] };

```js
var config = {
    type: Phaser.AUTO,
    width: game_width,
    height: game_height,
    parent: 'div-id',
    scene: [SceneName]
};
```

### Game Object

> 创建 Phaser 游戏

```js
var game = new Phaser.Game(config);
```

### Blank Scene

> 空白场景 

```js
class SceneMain extends Phaser.Scene {
    constructor(){
        super('SceneMain');
    }
    init(){}
    preload(){}
    create(){}
    update(){}
}
```

---

## Sprite Snippets

### Preload an Image

> 在场景中的 preload 周期中加载资源

```js
this.load.image('face', 'images/face.png');
```

### Add An Image

> 在场景中的 create 周期中添加图像

```js
this.face = this.add.image(x, y, 'key');
```

### Add A Sprite

> 在场景中的 create 周期中添加精灵

```js
this.face = this.add.sprite(x, y, 'key');
```

---

## Time Snippets

### Phaser Timer

> 计时器，函数在设置的秒内被调用
> Example:this.time.addEvent({ delay: 1000, callback: onTick, callbackScope: this, loop: true });


```js
this.timeEventName = this.time.addEvent({ delay: secs, callback: myFunction, callbackScope: this, loop: true});
```

### Remove timed event

> 移除计时器

```js
this.timeEventName.remove();
```

---

## Tween Snippets

### Y Tween

> Y轴动画

```js
this.tweens.add({ targets: child, duration: time, y: targetY });
```

### Tween On Complete

> 动画结束回调

```js
this.tweens.add({ targets: child, duration: time, y: targetY, onComplete: onCompleteHandler, onCompleteParams: [custom]});
```

---

## Animation Snippets

### Sprite sheet load

> 加载一个精灵表

```js
this.load.spritesheet('char', 'images/char.png', { frameWidth: 128, frameHeight: 128 });
```

### get frame names

> 获取精灵表的 frame 名称

```js
var frameNames = this.textures.get('char').getFrameNames();
```

### create an animation

> 创建一个全局动画

```js
this.anims.create({
    key: 'walk',
    frames:[
        { key: 'char', frame: 0 },
        { key: 'char', frame: 1 }
    ],
    frameRate: 8,
    repeat: -1
})
```

### Play an animation

> 在任何精灵上播放动画

```js
this.char.play('walk');
```

### get frame numbers

> 从精灵表生成帧信息，返回结果如
> { key: 'char',frame:1 }, { key: 'char',frame:2 }

```js
var frameNames = this.anims.generateFrameNumbers('chars');
```

### animation complete event

> 动画完成事件

```js
char.on('animationcomplete', animComplete, this);
```

### Generate a key frame sequence

> 从json文件中生成关键帧序列

```js
this.anims.generateFrameNames('key', { start: 0, end: 8, zeroPad: 3, prefix: 'animation_', suffix: '.png' });
```

## Physics Snippets

### Physic Object

> 配置入口，开启物理功能

```js
var config = {
    physics: {
        default: 'arcade',
        arcade: {
            debug: true
        }
    }
}
```

### Add physics sprite

> 添加一个精灵，赋予物理特性

```js
this.physics.add.sprite(400, 300, 'char');
```

### set velocity

> 设置精灵的速度

```js
sprite.setVelocity(100, 200);
```

### set bounce

> 设置精灵反弹系数

```js
sprite.setBounce(1, 1);
```

### collide with world bounds

> 设置为 true, 则与世界发生碰撞

```js
sprite.setCollideWorldBounds(true);
```

### set gravity

> 设置精灵的重力

```js
sprite.setGravityY(200)
```

### set collider

> 设置碰撞， 允许一个组和一个精灵相互碰撞

```js
this.physics.add.collider(sprite, group);
```

### set immovable

> 设置为固定不动的

```js
sprite.setImmovable();
```

### collision function

> 2个对象碰撞时调用一个函数
> Example:this.physics.world.collide(wall, char, this.hitTheWall);

```js
this.physics.world.collide(thing1, thing2, this.hitTheWall);

hitTheWall(thing1,thing2){}
```

### Move to

> 将对象移动到目标位置 
> Example:moveTo(gameObject, x, y [, speed] [, maxTime])

```js
this.physics.moveTo(player, x, y,60);
```

### Accelerate To

> 将对象加速到目标位置
> Example:accelerateTo(gameObject, x, y [, speed] [, xSpeedMax] [, ySpeedMax])

```js
this.physics.accelerateTo(player, x, y ,50)
```

### Convert Radians to Angles

> 弧度转成角度
> Example:angle * (180 / Math.PI);

```js
toDegrees(angle) {
    return angle * (180 / Math.PI);
}
```

### degrees to radians

> 角度转成弧度
> Example:radians=degrees*Math.PI/180;

```js
function getRadians(degrees) {
 return degrees*Math.PI/180;
}
```

### set camera size

> 设置摄像机大小
> Example:this.cameras.main.setBounds(0, 0, w, h);

```js
this.cameras.main.setBounds(0, 0, w, h);
```

### Camera follow

> 镜头跟随
> Example:this.cameras.main.startFollow(gameObject, true);

```js
this.cameras.main.startFollow(this.player, true);
```

### get x and y from angle

> 从角度上获取 x 和 y 的方向 
> Example: var rads = this.ship.angle*Math.PI/180; var tx = Math.cos(rads); var ty = Math.sin(rads);

```js
var rads = gameObj.angle*Math.PI/180;
var tx = Math.cos(rads);
var ty = Math.sin(rads);
```

### direction from angule

> 从角度获取方向
> Example:radians=degrees*Math.PI/180; var tx = Math.cos(radians); var ty = Math.sin(radians);

```js
function getDirFromAngle(angle) {
 var rads=angle*Math.PI/180;
 var tx = Math.cos(rads);
 var ty = Math.sin(rads);
 return {tx,ty}
}
```

### add a group of objects

> 添加一组物理对象
> Example:this.myGroup= this.physics.add.group({ key: 'key', frame: [0,1,2], frameQuantity: 20, bounceX: 1, bounceY: 1, angularVelocity: 1, collideWorldBounds: true });

```js
this.myGroup= this.physics.add.group({
    key: 'key',
    frame: [0,1,2],
    frameQuantity: 20,
    bounceX: 1,
    bounceY: 1,
    angularVelocity: 1,
    collideWorldBounds: true
});
```

## 参考

1. [phasergames.com](https://phasergames.com/)