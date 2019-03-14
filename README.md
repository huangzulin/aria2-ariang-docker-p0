Aria2 + AriaNg

[English](https://github.com/huangzulin/aria2-ariang-docker-p0/blob/master/README.EN.md) | 简体中文

[![](https://images.microbadger.com/badges/image/huangzulin/aria2-ui-p0.svg)](https://microbadger.com/images/huangzulin/aria2-ui-p0 "Get your own image badge on microbadger.com")
[![Docker Pulls](https://img.shields.io/docker/pulls/huangzulin/aria2-ui-p0.svg)](https://hub.docker.com/r/huangzulin/aria2-ui-p0/)

本镜像包含 Aria2、AriaNg 和File Manager，主要方便那些用户期望只运行一个镜像就能实现图形化下载文件和在线播放文件。（类似离线下载的功能），只使用一个 Docker 镜像也方便用户在群晖NAS 中运行本程序。

<!-- TOC -->

- [功能特性](#功能特性)
- [安装于运行](#安装于运行)
  - [快速运行](#快速运行)
  - [开启所有功能](#开启所有功能)
  - [支持的 Docker 环境变量](#支持的-docker-环境变量)
  - [支持的 Docker volume 属性](#支持的-docker-volume-属性)
- [自行构建镜像](#自行构建镜像)
- [Docker Hub](#docker-hub)
- [使用 Docker compose 来运行](#使用-docker-compose-来运行)

<!-- /TOC -->
## 功能特性

  * Aria2 (SSL 支持)
  * AriaNg 通过 UI 来操作，下载文件
  * 自动 HTTPS （Let's Encrypt）
  * Basic Auth 用户认证
  * 文件管理和视频播放 ([File Manager](https://henriquedias.com/filemanager/)，注意默认情况下，只能访问和管理 `/data` 目录下的文件)

## 安装于运行

### 快速运行

```shell
  docker run -d --restart=always --name aria2-ui-p0 -p 80:80 -p 6800:6800 -v /data:/data huangzulin/aria2-ui-p0
```

* Aria2: <http://yourip>
* FileManger: <http://yourip/files>
* 请使用 admin/admin 进行登录
### 开启所有功能
```shell
  docker run -d --name ariang -p 80:80 -p 6800:6800 -p 443:443 -e ENABLE_AUTH=true -e RPC_SECRET=Hello -e DOMAIN=example.com -e ARIA2_USER=user -e ARIA2_PWD=pwd -v /yourdata:/data -v /yoursslkeys/:/root/conf/key -v <to your aria2.conf>:/root/conf/aria2.conf huangzulin/aria2-ui-p0
```

### 支持的 Docker 环境变量

  * ENABLE_AUTH 启用 Basic auth 用户认证
  * ARIA2_USER Basic Auth 用户认证用户名
  * ARIA2_PWD Basic Auth 密码
  * RPC_SECRET Aria2 RPC 加密 token
  * DOMAIN 绑定的域名


### 支持的 Docker volume 属性
  * `/data` 用来放置所有下载的文件的目录
  * `/root/conf/key` 用户来放置 Aria2 SSL `certificate`证书和 `key` 文件. `注意`: 证书的名字必须是 `aria2.crt`， Key 文件的名字必须是 `aria2.key`
  * `/root/conf/aria2.conf` 为 aria2 的配置文件，你可以映射自己的配置文件。

## 自行构建镜像

```
cd caddy
docker build -t aria2-ui-p0 .
```

## Docker Hub

  <https://hub.docker.com/r/huangzulin/aria2-ui-p0/>
