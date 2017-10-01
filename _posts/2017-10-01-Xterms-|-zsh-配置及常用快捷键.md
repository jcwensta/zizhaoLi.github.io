---
layout:     post
title:      iTerm2 | zsh 配置及常用快捷键
date:       2017-10-01
author:     xiaozi
header-img: img/post-bg-2017-02.jpg
catalog: true
tags:
    - terminal
    - iTerm2
    - zsh
    - mac 
---

本来想给mac的终端加点颜色看起来不那么费劲，但是无意中发现了[iTerm2](https://www.iterm2.com/)这个终端的替代器，下面介绍一下iTerm2的配置和终端中常用的快捷键。

# iTerm2 配置
## 下载和安装
在[官网](https://www.iterm2.com/downloads.html)上下载，然后解压，将 iTerm 拖拽进入 Application 文件夹中。然后在 Launchpad 中启动 iTerm。
## 基础设置
在下拉菜单选择`iTerm2 - Preference`或者用快捷键`command + ,`打开设置界面，可以根据自己的使用习惯进行设置。但还可以更炫酷！
### 配色方案
iTerm2 自带了一些配色方案，其中有很出名的[Solarized](http://ethanschoonover.com/solarized)（支持很多软件和编辑器），可以在`Preference - Profiles - Colors - Color Presets`直接选择使用，但是[iTerm2-Color-Schemes](https://github.com/mbadolato/iTerm2-Color-Schemes)提供了更多基于iTerm2的配色方案，在`Preference - Profiles - Colors - Color Presets`中import存储在`iTerm2-Color-Schemes/schemes`中后缀为`itermcolors`中的主题，然后再选择使用即可。

如果设置了配色方案但终端显示无变化，在shell的配置文件中（对于bash来说是`~/.bash_profile`）添加：

```
export CLICOLOR=1
# sets up thecolor scheme for list export
export LSCOLORS=gxfxcxdxbxegedabagacad
# sets up theprompt color (currently a green similar to linux terminal)
export PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;36m\]\w\[\033[00m\]\$ '
# enables colorfor iTerm
export TERM=xterm-color
```

到这里为止，基本就完成了对iTerm2的配色方案的配置，可以使用了。但是如果想要如下图的加箭头的界面，还需要借助`zsh`进行配置。

![](https://gist.githubusercontent.com/agnoster/3712874/raw/screenshot.png)


# zsh和oh-my-zsh

zsh (Z Shell)是一个强大的shell脚本命令解释器，但是配置过于繁琐，所以有人开发了[oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)并开源在了GitHub上。要实现上图中的箭头效果，需要应用一个oh-my-zsh中的主题。

## oh-my-zsh 安装
首先用命令`cat /etc/shells`查看系统中是否有zsh，一般mac都会自带zsh，如果没有，用命令`brew install zsh`安装zsh。然后用
`curl -L http://install.ohmyz.sh | sh`或者`wget --no-check-certificate http://install.ohmyz.sh -O - | sh`安装`oh-my-zsh`。 一般安装完成后系统会自动切换到zsh，如果没有，用命令`chsh -s bin/zsh`切换到zsh，同理，如果想切到别的Shell，用命令`chsh -s bin/YOUR-SHELL`。

## oh-my-zsh 配置
zsh的配置文件是`~/.zshrc`，如果想要达到上图的效果，要把主题改为[**agnoster**](https://github.com/agnoster/agnoster-zsh-theme)。

```
ZSH_THEME="agnoster"
```

当然，[这里](https://github.com/robbyrussell/oh-my-zsh/wiki/Themes)还提供了oh-my-zsh的所有主题的截图。

修改好主题如果之后发现并不能显示完整，那是因为**agnoster**这个主题是依赖[PowerLine](https://github.com/powerline/fonts)这个项目中的字体的。可以直接下载字体包，然后用下面的命令安装。

```
# clone
git clone https://github.com/powerline/fonts.git --depth=1
# install
cd fonts
./install.sh
# clean-up a bit
cd ..
rm -rf fonts
```

然后在iTerm2中设置字体和Non-ASCII字体都是Powerline的，这里我用的是`Meslo LG L Regular for Powerline`。
设置完成后打开一个新的终端或者在终端执行`source ~/.zshrc`，就可以看到设置好的界面了。

# iTerm 常用快捷键
* 双击选中，三击选中整行，四击智能选中，选中即复制
* 按下`command`，点击url，可以打开该网址，点击文件（夹），可以打开该文件（夹）
* `command + d` 垂直分割视窗
* `command + shift + d` 水平分割视窗
* `command + t` 打开新视窗
* `command + w` 关闭当前视窗
* `command + shift + s` 保存当前的视窗排列
* `command + shift + r` 打开默认的视窗排列
* `alt(⌥) + Space ` 显示/隐藏iTerm界面
* `command + /` 高亮光标
* `command + ;` 显示历史命令
* `command + shift + h` 显示历史记录
* `command + enter` 全屏
* `command + alt(⌥) + e` 展示并搜索所有的TAB
* `command + f` 查找，支持正则表达式

还发现了一个黑科技~

* 隐藏在Dock上的图标

```
/usr/libexec/PlistBuddy -c "Add :LSUIElement bool true" /Applications/iTerm.app/Contents/Info.plist
```
* 重新显示

```
/usr/libexec/PlistBuddy -c "Delete :LSUIElement" /Applications/iTerm.app/Contents/Info.plist
```

对于别的应用同样适用。

当然还有别的很强大的功能，要靠自己去发掘了~

# Terminal常用快捷键
* `ctrl + a` 移动光标到句首
* `ctrl + e` 移动光标到句尾
* `ctrl + d` del
* `ctrl + k` 删除光标后面的所有内容
* `ctrl + l` 清屏


在iTerm中设置左`Alt(⌥) `为`Esc+`，如下图

![](https://ws2.sinaimg.cn/large/006tNc79gy1fk38222oe5j31k80vggta.jpg)

* `Alt(⌥) + f` 光标向前移动一个词
* `Alt(⌥) + b` 光标向后移动一个词

PS : 强烈建议`alias` Visual Studio Code这个应用，然后就可以作为应用打开各种文件。

```
alias code='/Applications/Visual\ Studio\ Code.app/Contents/Resources/app/bin/code'
```

PPS: `zsh`还提供很多`plugins`，这里推荐一个[zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)。如果输入的命令不正确，则会红色高亮显示。安装方法如下：

```
cd ~/.oh-my-zsh/custom/plugins
git clone git://github.com/zsh-users/zsh-syntax-highlighting.git
```

然后在`~/.zshrc`中修改`plugins=([plugins] zsh-syntax-highlighting)`。 当然`zsh`中还有很多自带的好用的`plugins`，比如`extract`，`z`等，但需要注意的是添加过多plugins会影响打开速度。



> ### 参考文章
* [配置iTerm2](https://laoshuterry.gitbooks.io/mac_os_setup_guide/content/4_ZshConfig.html)
* [Mac OSX 新手入門](https://mac-osx-for-newbie-book.kejyun.com/software/SoftwareTooliTerm.html)
* [iterm2有什么酷功能？](https://www.zhihu.com/question/27447370)
* [我常用的 oh-my-zsh 插件](http://blog.yxjxx.com/2016/01/22/Most-useful-oh-my-zsh-plugins.html)


—— 小紫 于 2017.10.01