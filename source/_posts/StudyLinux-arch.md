---
title: StudyLinux----arch
date: 2018-09-23 17:21:03
tags: [linux]
description: ["Arch 作为'最难'安装的linux系统  通过它可以更好的了解linux"]
toc: true
---

# Arch 踩坑笔记

> 记录一下从0开始玩linux的经历
>
> 其实之前已经有了一点ubuntu的使用经验 但是很浅
>
>Arch 作为'最难'安装的linux系统  通过它可以更好的了解linux
>
> 这里是VMware安装的Arch虚拟机

## 安装:

这里参考

> [这是最全面的安装指南](https://www.viseator.com/2017/05/17/arch_install/)

## 命令行

> linux 强大的命令行操作,使效率倍增,所以配置好命令行,并安装实用命令行软件是必要的

#### zsh[^1]

[^1]: [终端环境之Zsh＆oh-my-zsh](https://mtaoist.xyz/2018/03/14/oh-my-zsh/)

```shell
sudo pacman -S zsh zsh-completions

# 将zsh设为默认shell
chsh -s /bin/zsh
#其他发行版可先用chsh -l 查看zsh安装位置
```

##### oh-my-zsh

- curl 和 git 应该已被安装(若没有Arch 用sudo pacman -S curl git 安装，其他发行版类似。)

- [Oh-my-zsh](http://ohmyz.sh/)是一个傻瓜化的zsh配置管理框架，提供了大量实用的功能，主题等。做到开箱即用，现在基本成为了Zsh的标配。

- 安装

  ```
  sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
  ```

- 配置文件位置： ~/.zshrc

- 主题
  `oh-my-zsh`自带大量[Themes](https://github.com/robbyrussell/oh-my-zsh/wiki/Themes)，默认为`robbyrussell`。你也可以选择`random`，即每次打开终端随机选一个主题。

  > ZSH_THEME=”你喜欢的主题名”
  > ![themes](https://mtaoist.xyz/img/zsh_theme.png)

- 常用插件

  - git: 提供大量git的Aliases，[详情](https://github.com/robbyrussell/oh-my-zsh/wiki/Plugin:git)

  - archlinux： 提供一些pacman包管理器的Aliases，[详情](https://github.com/robbyrussell/oh-my-zsh/wiki/Plugins#archlinux)

  - z：经常使用cd 切换路径，积累一定数据后可用z快速跳转到指定位置

  - sudo：按两次[Esc]自动在前面加sudo

  - pip： 补全pip 命令

  - zsh-autosuggestions: 根据历史记录进行智能提示(按 ctrl+E 是正确姿势)。非oh-my-zsh自带，用git下载安装

    ```
    git clone https://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
    ```

  - zsh-syntax-highlighting：命令高亮，正确显示绿色，错误为红色。非oh-my-zsh自带，用git下载安装

    ```
    git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
    ```

    > plugins=( 你想启用的插件，空格分隔 )
    > ![plugins](https://mtaoist.xyz/img/zsh_plugins.png)

  - 重新加载配置文件，立刻生效。

    > source ~/.zshrc

- 其他插件请参见官方[wiki](https://github.com/robbyrussell/oh-my-zsh/wiki/Plugins-Overview)

- 少即是多，启用大量插件会严重拖慢zsh启动速度

---

我这里是在root下安装的,在`zsh`与`oh-my-zsh`的使用中,发现切换用户会出现错误

```shell
Last login: Sun Sep 16 14:21:35 2018 from 192.168.174.1
/home/tabris/.zshrc:source:71: permission denied: /root/.oh-my-zsh/oh-my-zsh.sh
```

原因是

#### tmux



#### neovim

> neovim属于vim的加强版  功能更加强大

注意的是  启动neovim的命令式`nvim`而不是`neovim`



##### spacevim

一个定制化的vim配置,支持`vim,neovim`

[官网]()



#### *Xshell下256/真色支持

检查当前是否为256/真色[参考本篇文章](https://gaomf.cn/2017/01/16/Terminal_Color/)

为了使`TERM=tmux-256color` 将 `export TERM=tmux-256color`加入到每个用户的`.zshrc`中 解决此问题(我这里加到`.zshrc`文件的顶部了) 

**真色的支持还没有**



#### TERM

Xshell远程连接 使用

本地采用``



## 桌面环境

> [参考](https://blog.csdn.net/kingolie/article/details/76723448)

#### **1、安装显卡驱动**

```
# lspci | grep VGA    # 确定显卡型号
# pacman -S <驱动包>
#
# # 官方仓库提供的驱动包：
# # +----------------------+--------------------+--------------+
# # |                      |        开源        |     私有     |
# # +----------------------+--------------------+--------------+
# # |         通用         |   xf86-video-vesa  |              |
# # +----------------------+--------------------+--------------+
# # |         Intel        |  xf86-video-intel  |              |
# # +--------+-------------+--------------------+--------------+
# # |        | GeForce 9+  |                    |    nvidia    |
# # +        +-------------+                    +--------------+
# # | nVidia | GeForce 8/9 | xf86-video-nouveau | nvidia-340xx |
# # +        +-------------+                    +--------------+
# # |        | GeForce 6/7 |                    | nvidia-304xx |
# # +--------+-------------+--------------------+--------------+
# # |        AMD/ATI       |   xf86-video-ati   |              |
# # +----------------------+--------------------+--------------+12345678910111213141516171819
```

#### **2、安装桌面环境**

所有桌面环境都需要依赖xorg。所以先要安装xorg组。

```shell
pacman -S xorg1
```

输入命令之后首先会询问要安装xorg组下的哪些包，选择全部。然后对于libgl包有个四个不同的实现，选择mesa-libgl。 
然后再安装xorg-xinit和xterm：

```shell
pacman -S xorg-xinit xterm1
```

安装完成之后就可以使用startx命令启动xorg的简易界面了。进入成功的话会显示出几个简陋的窗口。然后按Ctrl+D就可以退出了。

#### **3、安装xfce4桌面**

安装xfce4桌面和附带的软件包：

```shell
pacman -S xfce4 xfce4-goodies1
```

#### **4、安装LightDM登录管理器(显示管理器)**

详细安装和配置看arch-wiki-lighdm 
我没有通过startx的方式启动桌面环境，而是使用了登录管理器lightdm 
安装：

```zsh
pacman -S lightdm lightdm-gtk-greeter1
```

其配置文件为：
/etc/lightdm/lightdm.conf 
安装好之后测试启动：

```shell
systemctl start lightdm.service1
```

如果正常就会看到熟悉的登录界面了，不过不要登录，现在只是测试lightdm是否可以正常启动 
点击画面上的关机小图标，弹出关机对话，选择注销! 
注销之后就回到之前的tty命令行模式了，可以看到相关的启动信息 
一切正常，所以设置lightdm为开机自动启动，这样以后开机就不会出现tty命令行界面了，而是直接进入登录界面：

```shell
systemctl enable lightdm.service1
```

之后你可以重启进入xfce4图形界面，然后在图形界面中使用终端来继续以下配置步骤，也可以不重启，直接继续

进入xfce4图形界面的命令为`startxfce4`



#### 桌面美化



[^1]: 
