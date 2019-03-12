---
title: vim使用心得
date: 2019-03-11 15:33:11
categories:  
tags: [editor] #文章标签，可空，多标签请用格式，注意:后面有个空格
description: tabris的vim使用心得
toc: true
---



# vim

Vim是从 vi 发展出来的一个文本编辑器。代码补完、编译及错误跳转等方便编程的功能特别丰富，在程序员中被广泛使用。

所有的 Unix Like 系统都会内建 vi 文书编辑器，其他的文书编辑器则不一定会存在。

但是目前我们使用比较多的是 vim 编辑器。

vim 具有程序编辑的能力，可以主动的以字体颜色辨别语法的正确性，方便程序设计。

vim主要有以下几个优点.

- 可以不使用鼠标，完全用键盘操作。
- 系统资源占用小，打开大文件毫无压力。
- 键盘命令变成肌肉记忆以后，操作速度极快。

同时现今很多开源软件采用的快捷键都与vim类似.学习vim变得很有必要.

但我这里采用的是`neovim`

[NeoVim](https://neovim.io/) 旨在成为Vim的升级版，有不少对它的介绍，我就不赘述了。NeoVim官网强调了它的四大特点：Powerful plugins（强大的插件）、Better out-of-the-box（更好的开箱即用）、First-class embedding（高度支持嵌入模式）、Drop-in replacement for Vim（直接替换Vim）。

## vim插件管理器

> 参考 https://www.jianshu.com/p/0c83e6aed270

### 安装

现在流行的有这几种插件管理器,`VBunle`,`NeoBunle`,`vim-plug`, 我这里采用的是`vim-plug`.

neovim下安装命令

```shell
curl -fLo ~/.config/nvim/autoload/plug.vim --create-dirs \ https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

vim下安装命令

```shell
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \ https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

### 用法

#### 安装插件

要安装插件，你必须如下所示首先在 Vim 配置文件中声明它们。一般 Vim 的配置文件是 `~/.vimrc`，Neovim 的配置文件是 `~/.config/nvim/init.vim`。请记住，当你在配置文件中声明插件时，列表应该以 `call plug#begin(PLUGIN_DIRECTORY)` 开始，并以 `plug#end()` 结束。

例如，我们安装 “lightline.vim” 插件。为此，请在 `~/.vimrc` 的顶部添加以下行。

```typescript
call plug#begin('~/.vim/plugged')
Plug 'itchyny/lightline.vim'
call plug#end()
```

在 vim 配置文件中添加上面的行后，通过输入以下命令重新加载：
 `:source ~/.vimrc`
 或者，只需重新加载 Vim 编辑器。

 现在，打开 vim 编辑器：
 `$ vim`
 使用以下命令检查状态：
 `:PlugStatus`
 然后输入下面的命令，然后按回车键安装之前在配置文件中声明的插件。
 `:PlugInstall`

#### 更新插件

要更新插件，请运行：

```
:PlugUpdate
```

更新插件后，按下 `d` 查看更改。或者，你可以之后输入 `:PlugDiff`。

#### 审查插件

有时，更新的插件可能有新的 bug 或无法正常工作。要解决这个问题，你可以简单地回滚有问题的插件。输入 `:PlugDiff` 命令，然后按回车键查看上次 `:PlugUpdate`的更改，并在每个段落上按 `X` 将每个插件回滚到更新前的前一个状态。

#### 删除插件

删除一个插件删除或注释掉你以前在你的 vim 配置文件中添加的 `plug` 命令。然后，运行 `:source ~/.vimrc` 或重启 Vim 编辑器。最后，运行以下命令卸载插件：
 `:PlugClean`

该命令将删除 vim 配置文件中所有未声明的插件。

#### 升级 Vim-plug

要升级vim-plug本身，请输入：
 `:PlugUpgrade`

如你所见，使用 Vim-plug 管理插件并不难。它简化了插件管理。现在去找出你最喜欢的插件并使用 Vim-plug 来安装它们。

## 安装插件

### 安装[vim中文手册](https://github.com/yianwillis/vimcdoc)

`Plug 'yianwillis/vimcdoc'`

### 安装状态栏插件

状态栏能显示当前的状态，还是有不少用处的，好看的状态栏就是为了美观，毕竟谁也不喜欢对着个难看的东西吧。
 　　这里使用的是 [airline ](https://link.jianshu.com?t=https%3A%2F%2Fgithub.com%2Fvim-airline%2Fvim-airline)：

```
Plug 'vim-airline/vim-airline'
Plug 'vim-airline/vim-airline-themes'
```

### 安装主题

### 安装自动补全工具

vim要有python支持,如果没有需要输入`pip install neovim`命令安装neovim的python支持模块.

`Plug 'Valloric/YouCompleteMe'`
