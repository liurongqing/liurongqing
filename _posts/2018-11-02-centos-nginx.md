---
title: CentOS 7 上通过 yum 安装配置 Nginx
author: liurongqing
date: 2018-11-02 11:33:00 +0800
categories: [Linux]
tags: [centos, nginx]
---

## 环境说明

查看 CentOS 版本

```bash
cat /etc/redhat-release # CentOS Linux release 7.8.2003 (Core)
```

## 安装 EPEL 

1. 通过 EPEL 软件包来安装 Nginx
1. 需在 root 权限下操作

```bash
yum install epel-release
```

## 安装 Nginx

```bash
yum install nginx
```

## 配置 Nginx

启动服务
```bash
systemctl start nginx
```

重启服务
```bash
systemctl restart nginx
```

重载服务
```bash
systemctl reload nginx
```

设置开机启动
```bash
systemctl enable nginx
```

查看状态
```bash
systemctl status nginx
```

查看版本
```bash
nginx -v
```

## 简单配置文件

`vim /etc/nginx/conf.d/www.xx.com.conf`

```bash
server { 
    listen       80;
    server_name  xx.com www.xx.com;
    root /Users/username/www;
    index index.html index.htm index.php;
}
```


## 配置文件

1. 所有配置文件目录 `/etc/nginx`
1. 主配置文件 `/etc/nginx/nginx.conf`
1. 独立配置文件目录 `/etc/nginx/conf.d`
1. 日志文件目录 `/var/log/nginx/`
1. 建议代码目录
    1. `/home/user_name/site_name`
    1. `/var/www/site_name`
    1. `/var/www/html/site_name`