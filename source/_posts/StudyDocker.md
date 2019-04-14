---
title: StudyDocker
date: 2019-1-10 17:21:03
tags: [linux,docker,虚拟化]
description: ["Docker 轻量级虚拟化"]
toc: true
---



操作环境: Arch & manjaro 

docker命令行管理工具使用的`dockly` 但仍然有缺陷,以后再找找 有没有其他更好用的命令行工具.

教程先看了一遍 [B站的尚硅谷教程](https://www.bilibili.com/video/av27122140) 有些av号的顺序不对.  看这个就行了.

tabris's 阿里云镜像加速器: https://oj7znbfj.mirror.aliyuncs.com



# 安装篇

命令安装`docker`本体

```shell
sudo pacman -S docker
```



> 同时建议安装`dockly`作为docker的命令行管理软件.
>
> https://www.npmjs.com/package/dockly

非root用户运行docker是执行如下命令

```shell
sudo usermod -aG docker $USER #your usrname
```

执行如下命令启动docker服务

```shell
#systemctl enable docker  
systenctl start docker
```

## 镜像加速

鉴于国内网络问题，后续拉取 Docker 镜像十分缓慢，我们可以需要配置加速器来解决，我使用的是阿里云的镜像加速器: https://oj7znbfj.mirror.aliyuncs.com

新版的 `Docker` 使用 `/etc/docker/daemon.json（Linux）` 或者 `%programdata%\docker\config\daemon.json（Windows）` 来配置 `Daemon`。

请在该配置文件中加入（没有该文件的话，请先建一个）：

```json
{
    "registry-mirrors": ["https://oj7znbfj.mirror.aliyuncs.com"]
}
```

