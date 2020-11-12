---
title: macOS 系统通过 brew 安装 MongoDB 4.4 社区版
author: liurongqing
date: 2020-02-02 10:00:00 +0800
categories: [MongoDB]
tags: [MongoDB, db]
---

## 平台支持

MongoDB 4.4 社区版支持 macOS 10.13或更高版本

## 安装

```bash
brew tap mongodb/brew
brew install mongodb-community@4.4
```

## 运行 MongoDB

1. 通过 mongod 命令来启动服务

    ```bash
    # 不需要后台启动
    mongod --config /usr/local/etc/mongod.conf

    # 后台启动
    mongod --config /usr/local/etc/mongod.conf --fork

    # 后台启动的可以通过 mongo shell 控制台关闭
    db.adminCommand({"shutdown": 1})
    ```
2. 通过 brew 命令来启动服务

    ```bash
    # 启动
    brew services start mongodb-community@4.4

    # 关闭
    brew services stop mongodb-community@4.4

    # 重启
    brew services restart mongodb-community@4.4
    ```

## 验证 MongoDB 是否正在运行

```bash
ps aux | grep -v grep | grep mongod
```

## 快速上手

> 若提示权限问题，则看下面权限操作

```bash
mongo # 连接 mongo shell 实例
# 插入（若集合不存在，则创建）
db.collection.insertOne({item: "canvas", qty: 100, tags: ["cotton"]})

# 查询
db.inventory.find({})

# 更新
db.inventory.updateOne(
  { item: "canvas"},
  {
    $set: { "qty": 200 }
  }
)

# 删除
db.inventory.deleteOne( { item: "canvas" } )

```

## 权限

## 文件路径

- 配置文件： `/usr/local/etc/mongod.conf`
- log 文件： `/usr/local/var/log/mongodb`
- data路径： `/usr/local/var/mongodb`

## 参考

[docs.mongodb.com](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/)
