Aria2 + AriaNg

English | [简体中文](https://github.com/huangzulin/aria2-ariang-docker-pi/blob/master/README.md)

[![](https://images.microbadger.com/badges/image/huangzulin/aria2-ui-pi.svg)](https://microbadger.com/images/huangzulin/aria2-ui-pi "Get your own image badge on microbadger.com")

<!-- TOC -->

- [Features](#features)
- [How to run](#how-to-run)
  - [Simple Usage](#simple-usage)
  - [Full Usage](#full-usage)
  - [Supported Environment Variables](#supported-environment-variables)
  - [Supported Volumes](#supported-volumes)
- [Docker Hub](#docker-hub)
- [Usage it in Docker compose](#usage-it-in-docker-compose)

<!-- /TOC -->
Aria2
![Screenshot](https://github.com/wahyd4/aria2-ariang-x-docker-compose/raw/master/images/ariang.png)

File Manager
![Filemanager](https://github.com/huangzulin/aria2-ariang-docker-pi/raw/master/filemanager.png)
## Features

  * Aria2 (SSL support)
  * AriaNg
  * Auto HTTPS （Let's Encrypt）
  * Basic Auth
  * File indexing and video playing ([File Manager](https://henriquedias.com/filemanager/))

## How to run

### Simple Usage

```shell
  docker run -d --name aria2-ui-pi -p 80:80 -p 6800:6800 huangzulin/aria2-ui-pi
```

* Aria2: <http://yourip>
* FileManger: <http://yourip/files>
* Please use admin/admin as username and password to login

### Full Usage
```shell
  docker run -d --name ariang -p 80:80 -p 6800:6800 -p 443:443 -e ENABLE_AUTH=true -e RPC_SECRET=Hello -e DOMAIN=example.com -e ARIA2_USER=user -e ARIA2_PWD=pwd -v /yourdata:/data -v /yoursslkeys/:/root/conf/key -v /<to your aria2.conf>:/root/conf/aria2.conf huangzulin/aria2-ui-pi
```

### Supported Environment Variables

  * ENABLE_AUTH enable Basic auth
  * ARIA2_USER Basic Auth username
  * ARIA2_PWD Basic Auth
  * RPC_SECRET The Aria2 RPC secret token
  * DOMAIN The domain you'd like to bind


### Supported Volumes
  * `/data` The folder of all Aria2 downloaded files.
  * `/root/conf/key` The folder which stored Aria2 SSL `certificate` and `key` file. `Notice`: The certificate file should be named `aria2.crt` and the key file should be named `aria2.key`
  * `/root/conf/aria2.conf` The Aria2 configuration file.


## Docker Hub

  <https://hub.docker.com/r/huangzulin/aria2-ui-pi/>
