---
title: VSCode 断点调试
author: liurongqing
date: 2021-02-01 10:00:00 +0800
categories: [VSCode]
tags: [vscode, 'debug']
---

## 前提条件

1. Mac 系统
1. VSCode 编辑器

## 有二种方式 `Launch` 与 `Attach`
- Launch (不喜欢，麻烦)
  > VSCode 会新打开一个浏览器窗口，关闭调试，浏览器也关闭

- Attach（推荐，后面说的都是这个）
  > 监听当前运行的项目，需要浏览器允许监听(后面会讲如何配置)

## VSCode 配置

1. 进入调试选项  `cmd` + `shift` + `d`
1. 生成配置 点击运行和调试，选择 `Chrome` 生成 `launch.json` 文件
1. 清空 `configurations` 数组
  ```js
  {
    "version": "0.2.0",
    "configurations": []
  }
  ```
1. 新加配置 `Chrome Attach`, 然后尽量都不要改动(我就喜欢用默认的)
  ```js
  {
    "version": "0.2.0",
    "configurations": [
      {
        "name": "Attach to Chrome",
        "port": 9222,
        "request": "attach",
        "type": "pwa-chrome",
        "webRoot": "${workspaceFolder}"
      }
    ]
  }
  ```

## Mac 下 Google Chrome 浏览器配置

1. 临时打开浏览器

    ```bash
    /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --remote-debugging-port=9222
    ```

1. 通过 `Alfred` 和 `Automator` 配置打开可调试 `Chrome` 浏览器

    1. 通过 `Alfred` 打开 `Automator`，或去应用程序里查找
    1. 选择 `应用程序`
    1. 搜索选择双击 `运行 Shell 脚本`
    1. 将内容放进去
      ```bash
      /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --remote-debugging-port=9222
      ```
    1. 点击上面中间的未命名，起个名字
    1. 保存到应用程序中

1. 通过 `Alfred` 搜索刚才起的名字的应用


## 测试

1. 运行项目
1. 打开浏览器，进入项目
1. `VSCode` 打开调试，打断点
1. 进入浏览器中打断点的页面
1. 会自动 跳转到 `VSCode` 指定断点处，就可以在 `VSCode` 中打断点调试了



