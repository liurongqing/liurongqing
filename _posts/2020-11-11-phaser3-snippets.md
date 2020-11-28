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

```js
var game = new Phaser.Game(config);
```

### Blank Scene

```js
class SceneMain extends Phaser.Scene {
    constructor(){
        super('SceneMain');
    }
}
```

## Sprite Snippets

### Preload an Image

```js
this.load.image('face', 'images/face.png');
```

### Add An Image

```js
this.face = this.add.image(x, y, 'key');
```

### Add A Sprite

```js
this.face = this.add.sprite(x, y, 'key');
```

## Time Snippets

### Phaser Timer

```js
this.timeEventName = this.time.addEvent({ delay: secs, callback: myFunction, callbackScope: this, loop: true});
```

### Remove timed event

```js
this.timeEventName.remove();
```

## Tween Snippets

### Y Tween

```js
this.tweens.add({ targets: child, duration: time, y: targetY });
```

### Tween On Complete

```js
this.tweens.add({ targets: child, duration: time, y: targetY, onComplete: onCompleteHandler, onCompleteParams: [custom]});
```

## Animation Snippets

### Sprite sheet load

```js
this.load.spritesheet('char', 'images/char.png', { frameWidth: 128, frameHeight: 128 });
```

### get frame names

```js
var frameNames = this.textures.get('char').getFrameNames();
```

### create an animation

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

```js
this.char.play('walk');
```

### get frame numbers

```js
var frameNames = this.anims.generateFrameNumbers('chars');
```

### animation complete event

```js
char.on('animationcomplete', animComplete, this);
```

### Generate a key frame sequence

```js
this.anims.generateFrameNames('key', { start: 0, end: 8, zeroPad: 3, prefix: 'animation_', suffix: '.png' });
```

## Physics Snippets

### Physic Object

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

```js
this.physics.add.sprite(400, 300, 'char');
```


## 参考

1. [phasergames.com](https://phasergames.com/)