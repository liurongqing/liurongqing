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

1. 通过 brew 命令来启动服务

    ```bash
    # 启动
    brew services start mongodb-community@4.4

    # 关闭
    brew services stop mongodb-community@4.4

    # 重启
    brew services restart mongodb-community@4.4
    ```

1. 通过 mongod 命令来启动服务

    ```bash
    # 不需要后台启动
    mongod --config /usr/local/etc/mongod.conf

    # 后台启动
    mongod --config /usr/local/etc/mongod.conf --fork

    # 后台启动的可以通过 mongo shell 控制台关闭
    db.adminCommand({"shutdown": 1})
    ```
1. kill 掉 mongod 进程 

    ```bash
    # 方式一
    lsof -i:27017
    kill -9 端口

    # 方式二
    pgrep mongod
    kill -9 端口

    # 方式三
    use admin
    db.shutdownServer()
    ```

## 验证 MongoDB 是否正在运行

```bash
ps aux | grep -v grep | grep mongod
```

## 关闭或开启权限验证
`vim /usr/local/etc/mongod.conf`

```bash
security:
  authorization: enabled # or disabled
```

## 快速上手

> 若提示权限问题，则看下面权限操作

```bash
mongo # 连接 mongo shell 实例

use db_test # 进入库，不存在则创建
# 插入（若集合不存在，则创建）
db.collection_name.insert({name: 'lisi', age: 20})

# 查询
db.collection_name.find({})
# { "_id" : ObjectId("5facaeed4c2525799d4c35fa"), "name" : "lisi", "age" : 20 }

# 更新
db.collection_name.update(
  { name: "lisi"},
  {
    $set: { "age": 30 }
  }
)
# { "_id" : ObjectId("5facaeed4c2525799d4c35fa"), "name" : "lisi", "age" : 30 }

# 删除
db.collection_name.remove( { name: "lisi" } )
```

## 添加用户

1. 创建管理员用户

    ```bash
    use admin # 进入 admin 库
    db.createUser({
        user: 'admin',
        pwd: 'admin',
        roles: [{
            role: 'root',
            db: 'admin'
        }]
    })
    db.auth('admin', 'admin') # 验证
    ```


1. 创建普通用户

    ```bash
    use game # 进入 game 库
    db.createUser({
        user: 'liurongqing',
        pwd: '123456',
        roles: ['readWrite', 'dbAdmin', 'userAdmin']
    })
    ```


## 角色权限

### 角色分类
角色 | 值
-- | --
数据库用户角色 | `read` `readWrite`
数据库管理角色 | `dbAdmin` `dbOwner` `userAdmin`
集群管理角色 | `clusterAdmin` `clusterManager` `clusterMonitor` `hostManager`
备份恢复角色 | ` backup` `restore`
所有数据库角色 | `readAnyDatabase` `readWriteAnyDatabase` `userAdminAnyDatabase` `dbAdminAnyDatabase`
超级用户角色 | `root` `dbOwner` `userAdmin` `userAdminAnyDatabase`
内部角色 | `system`

### 角色说明
角色 | 说明
-- | --
read |  允许用户读取指定数据库
readWrite | 允许用户读写指定数据库
dbAdmin | 允许用户在指定数据库中执行管理函数，如索引创建、删除，查看统计或访问 system.profile
userAdmin | 允许用户向system.users集合写入，可以找指定数据库里创建、删除和管理用户
clusterAdmin | 只在admin数据库中可用，赋予用户所有分片和复制集相关函数的管理权限
readAnyDatabase | 只在admin数据库中可用，赋予用户所有数据库的读权限
readWriteAnyDatabase |  只在admin数据库中可用，赋予用户所有数据库的读写权限
userAdminAnyDatabase | 只在admin数据库中可用，赋予用户所有数据库的userAdmin权限
dbAdminAnyDatabase | 只在admin数据库中可用，赋予用户所有数据库的dbAdmin权限
root | 只在admin数据库中可用。超级账号，超级权限

## mongodb 常用操作命令

### 用户操作

    命令 | 功能
    -- | -- 
    db.auth('admin', 'admin') | 授权验证
    db.system.users.find() | 查看用户列表
    show users | 查看用户列表
    db.createUser({user: '1', pwd: '1', roles: [{role: 'read', db: 'g'}]}) | 创建用户
    db.runCommand({usersInfo: 'liurongqing'}) | 查看指定用户信息
    db.runCommand({updateUser: 'x', pwd: '1'}) | 修改用户信息
    db.changeUserPassword('user', 'pwd') | 修改用户密码
    db.system.users.remove({user: 'username'}) | 删除用户

### db 库操作

    命令 | 功能
    -- | -- 
    show dbs | 查看所有库
    db.dropDatabase() | 删除数据库

### collection 集合操作(表)

    命令 | 功能
    -- | -- 
    show collections <br> show tables | 显示集合
    db.createCollection('user') | 创建集合
    db.COLLECTION_NAME.drop() | 删除集合

### 文档数据操作（行）

    命令 | 功能
    -- | -- 
    db.COLLECTION_NAME.insert({title: '123'}) | 插入文档
    db.COLLECTION_NAME.find() | 查询文档
    db.COLLECTION_NAME.update({id: 1}, {name: 'xxx'}, {multi: false}) | 更新文档
    db.COLLECTION_NAME.save({_id: 'xxxx', name: 'xxx'}) | 替换文档 
    db.COLLECTION_NAME.remove({id: 11}, 1) | 删除文档

### 索引

    命令 | 功能
    -- | --
    db.users.getIndexes() | 获取users表中的所有索引
    db.users.dropIndex('name_1') |  删除索引

### 其他

    命令 | 功能
    -- | --
    mongodb://${user}:${pwd}@${host}:${port}/${database} | 连接

## 文件路径

- 配置文件： `/usr/local/etc/mongod.conf`
- log 文件： `/usr/local/var/log/mongodb`
- data路径： `/usr/local/var/mongodb`

## 参考

https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/
