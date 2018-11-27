---
title: StudyLinux----arch
date: 2018-09-23 17:21:03
tags: [linux]
description: ["Arch 作为'最难'安装的linux系统  通过它可以更好的了解linux"]
toc: true
---

> manjaro 真好用 arch 再见!
> 桌面环境真的是个大坑啊   

# Arch 踩坑笔记

> 记录一下从0开始玩linux的经历
>
> 其实之前已经有了一点ubuntu的使用经验 但是很浅
>
>Arch 作为'最难'安装的linux系统  通过它可以更好的了解linux
>
> 这里是VMware安装的Arch虚拟机
> [配置和美化Arch Linux](https://blog.csdn.net/u011054333/article/details/50631599)
## 安装:

这里参考

> [这是最全面的安装指南](https://www.viseator.com/2017/05/17/arch_install/)

## 基础设置:

#### 创建新用户
```
# useradd -m -G wheel username （请自行替换username为你的用户名）
# passwd username （请自行替换username为你的用户名）
```
#### 开机自动联网

```shell
# systemctl enable dhcpcd
```

#### 网络工具

```shell
# pacman -Syy net-tools
```

#### 时间

装完archlinux，时间总是比实际快了8个小时，找了各种办法，最终使用了openNTPD的方法

设置时区：`sudo ln sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime`

安装openNTPD：`sudo pacman -S openntpd`

重启openNTPD：`systemctl restart openntpd`

设置开机启动：`systemctl enable openntpd`


#### ssh
安装ssh
```
# pacman -Syy openssh
```
启动服务
```
# systemctl start sshd
```
开机启动
```
# systemctl enable sshd.service
```


#### aur助手
[yay](https://github.com/Jguer/yay) 是下一个最好的 AUR 助手。它使用 Go 语言写成，宗旨是提供最少化用户输入的 `pacman` 界面、yaourt 式的搜索，而几乎没有任何依赖软件。

yay 的特性：

- `yay` 提供 AUR 表格补全，并且从 ABS 或 AUR 下载 PKGBUILD
- 支持收窄搜索，并且不需要引用 PKGBUILD 源
- `yay` 的二进制文件除了 `pacman` 以外别无依赖
- 提供先进的包依赖解决方案，以及在编译安装之后移除编译时的依赖
- 当在 `/etc/pacman.conf` 文件配置中启用了色彩时支持色彩输出
- `yay` 可被配置成只支持 AUR 或者 repo 里的软件包

安装 yay：

你可以从 `git` 克隆并编译安装。

```
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```

使用 yay：

搜索：

```
yay -Ss <package-name>
```

安装：

```
yay -S <package-name>
```


#### powerline
Powerline 是 vim、zsh、bash、tmux、IPython、Awesome、bar、fish、lemonbar、pdb、rc、shell、tcsh、wm、i3 和 Qtil 中的一个状态栏插件。它给程序提供了状态栏，并使程序更好看。它用 Python 写成。

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

---

我这里采用的是`agnoster`主题
为在使用tmux时不重复显示`whoami@whereami`做两处修改
- 在`/etc/profile`中添加环境变量
  ```
  DEFAULT_USER=$USER
  ```
- 在`agnoster`主题文件91行中做如下修改
  ```git
  - if [[ "$USER" != "$DEFAULT_USER" || -n "$SSH_CLIENT"]]; then
  + if [[ "$USER" != "$DEFAULT_USER" || (( -n "$SSH_CLIENT" && -z "$TMUX" )) ]]; then
  ```
这样在本地初始打开一个terminal时不会显示,ssh远程连接是时显示
进入tmux时不会显示


原因是
[Archlinux下安装和配置zsh](https://blog.csdn.net/kingolie/article/details/53066679)
#### tmux

安装tmux
 
```shell
sudo pacman -S tmux
```

在这里配置tmux
https://github.com/search?utf8=%E2%9C%93&q=tmux&type=
https://github.com/samoshkin/tmux-config  <--推荐这个配置

[为 vim + tmux 开启真彩色(true color)](http://lotabout.me/2018/true-color-for-tmux-and-vim/)

[tmux进阶之tmuxinator](https://blog.csdn.net/u014717036/article/details/60139776)

#### neovim

> neovim属于vim的加强版  功能更加强大

注意的是启动neovim的命令式`nvim`而不是`neovim`

同时安装 [nerd-fonts](https://gitee.com/hustlion-dev/nerd-fonts#option-3-install-script)


##### spacevim

一个定制化的vim配置,支持`vim,neovim`

[官网](https://spacevim.org/)



#### *Xshell下256/真色支持

检查当前是否为256/真色[参考本篇文章](https://gaomf.cn/2017/01/16/Terminal_Color/)


我这里的xshell只能支持256色

这时xshell中只有在tmux下spacevim才能显示256色,不支持真色

在.zshrc文件头添加
```
sh /${.zshrc的目录}/.change_term.sh
```
.change_term.sh文件内容如下
```shell
echo "before: $TERM"
if [ "$TERM" = "linux" ]
then
  echo "export TERM=xterm-256color"
  export TERM=xterm-256color
elif [ "$TERM" = "xterm" ]
then
  echo "export TERM=tmux-direct"
  export TERM=tmux-direct
elif [ "$TERM" = "xterm-256color" ]
then
  echo "export TERM=xterm-direct"
  export TERM=xterm-direct
else
  echo "export TERM=tmux-256color"
  export TERM=tmux-256color
fi
echo "now: $TERM"
# 如果是ssh自动启用tmux
if [ -n "$SSH_CLIENT" ]
then
  tmux
fi

clear 
```

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
pacman -S xorg
```

输入命令之后首先会询问要安装xorg组下的哪些包，选择全部。然后对于libgl包有个四个不同的实现，选择mesa-libgl。 
然后再安装xorg-xinit和xterm：

```shell
pacman -S xorg-xinit xterm
```

安装完成之后就可以使用startx命令启动xorg的简易界面了。进入成功的话会显示出几个简陋的窗口。然后按Ctrl+D就可以退出了。

#### **3、安装xfce4桌面**

安装xfce4桌面和附带的软件包：

```shell
pacman -S xfce4 xfce4-goodies
```

#### **4、安装LightDM登录管理器(显示管理器)**

详细安装和配置看arch-wiki-lighdm 
我没有通过startx的方式启动桌面环境，而是使用了登录管理器lightdm 
安装：

```zsh
pacman -S lightdm lightdm-gtk-greeter
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
systemctl enable lightdm.service
```

之后你可以重启进入xfce4图形界面，然后在图形界面中使用终端来继续以下配置步骤，也可以不重启，直接继续

进入xfce4图形界面的命令为`startxfce4`



#### 桌面美化



[^1]: 