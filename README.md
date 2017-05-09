
**i3wm配置**
---

![](arch-i3.png)

# 安装
- 安装i3wm，一般其包名叫做i3，包含i3-wm，i3lock和i3status。
- 下载本配置文件并解压，将i3和i3status放于~/.config/目录，将Pictures（包含几张示例壁纸）放于当前用户家目录下（即~/下）。
- 需要的软件
  - dmenu	程序启动器
  - feh   设置壁纸
  - 适合的终端（参照下文配置-终端）
  - mate-power-manager或其他电源管理软件（可选，主要用于笔记本调节亮度和方便电源管理）
  - xcompmgr     终端透明（可选）
  - scrot     截屏（可选，本配置使用的截屏快捷键调用此工具）
  - alsa-utils    声音管理（可选）
  - networkmanager、nm-connection-editor和nm-applet    联网管理和相应托盘图标 （可选）
# 配置说明
关于本配置的一些重要说明。
## 快捷键
以下列出此配置文件的自定义快捷键的说明，未作更改的其他i3wm的默认快捷键请参阅i3wm相关文档或查看config文件。

快捷键在默认配置上稍作修改，参照了windows下的常用快捷键和vim操作习惯。

$mod key使用的默认的Mod4，**一般指的是**windows键或super键或meta键。


- 截图：`$mod+PrtSc`（配置里绑定的是scrot截屏工具，**需要安装scrot**，PrtSc即PrintScreen键，参考的windwos下的截屏快捷键）。

- 文件管理器：`$mod+e`（配置里使用的lxde桌面pcmanfm文件管理器，小巧依赖少功能齐全，须安装pcmanfm，参考windows的文件管理器快捷键，e-explore）。

- 关闭窗口：`Alt+F4`（Alt一般是mod1键，参考windows的关闭窗口快捷键）。

- 隐藏和再现窗口：`$mod+minus`和`mod+plus`（minus即是减号所在键，plus即是加号所在键）。

- 调整窗口边框风格：
  - `$mod+n`有边框（就是一般的风格，有边框有顶部栏，n-normal）。
  - `$mod+u`无边框（本配置默认风格，打开新窗口也不会有边框，可自行设置，u-unnormal）。
  - `$mod+o`1像素边框（o-one pixel）。
  - `$mod+b`可在上面三种风格来回切换（b-border style）。

- 视窗焦点切换：
  `$mod+h/j/k/l`或者`$mod+上下左右箭头`（可以切换当前焦点，模仿vim）。

- 移动当前窗口：
  `$mod+Shift+h/j/k/l`或者`$mod+上下左右箭头`（可以将当前的浮动或平铺窗口向指定方向移动，模仿vim）。

- 分隔窗口：
  - `$mod+v`上下分割（v-vertical）。
  - `$mod+Shift+h`左右分割（左右分割，默认风格，h-horizon）。

- 窗口布局风格：
  平铺时有效
  - `$mod+s`堆叠式（s-stacking）。
  - `$mod+t`标签式（t-tab）。
  - `$mod+c`平铺式（默认风格），反复按下此快捷键可在上下分割平铺和左右分割平铺之间来回切换（c-change）。

- 相邻工作区切换:`$mod+tab`（后一个）或`alt+tab`（前一个）。

- 亮度和音量（笔记本）：
  `Fn+音量加减键或静音`调整音量。（荧幕不会出现提示，可参看bar，也可以用终端的`alsamixer`调整）

  `Fn+亮度加减键`调整亮度。（需要一个电源管理软件，推荐**mate-power-manager**）

  注：也可能不需要按下fn键，这和其BIOS中是否设置了需要fn辅助按键有关。

## 壁纸和锁屏
壁纸图片路径是～/Pictures/wallpaper/wallpaper.jpg，不过本配置文件默认使用下文所述的随机壁纸切换。

锁屏图片路径是~/Pictures/wallpaper/lock/lock.jpg。

*建议用一个固定的路径设置壁纸或锁屏，需要更换壁纸的时候将新图片命名位wallpaper放进去覆盖即可，这样比较方便（当然要注意后缀名是否一致）。*

### 随机壁纸
本配置默认使用一个wallpaper.sh的脚本随机更换壁纸。
将图片放置到~/Pictures/wallpaper/目录下即可（如需更换壁纸路径，请在i3/config文件中根据注释说明更改）。

如需要使用单张固定壁纸，在i3/config中取消设定壁纸图片的命令的注释，并注释掉自动更换壁纸的命令。

**注意**
**～/.config/i3/wallpaper.sh文件需要可执行权限**，如壁纸加载出问题，执行：
`chmod +x ～/.config/i3/wallpaper.sh`
给予执行权限。


`$mod+alt+l`锁屏，按下后再按回车即锁屏，按Esc取消。

锁屏后输入当前用户密码再按回车即解锁。

可参考[archwiki-feh](https://wiki.archlinux.org/index.php/Feh_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87))


## 电源管理
参看配置中exec --no-startup-id xset dpms一行。

`exec --no-startup-id xset dpms 300 1800 8888`

分别代表灭屏时间、系统暂停时间和关机时间。（单位：秒）

锁屏/关机/重启/退出：按下`mod+Shift+q`或会提示选择，接下来----

按下L锁屏（lock）、e退出（exit）、r重启（reboot）和p关机（poweroff）。

（注意：mod+Shift+q本来是i3wm的默认关闭窗口键）

## 终端

配置中使用了xcompmgr这个工具来配合终端设置透明，需要安装xcompmgr。

最好使用下面的终端之一。
>因为按下 $mod+Return, 便会启动 i3-sensible-terminal, 即执行虚拟终端的脚本。它会试图按以下顺序一一执行，直到成功启动某虚拟终端： 
>- urxvt
>- rxvt
>- terminator
>- Eterm
>- aterm
>- xterm
>- gnome-terminal
>- roxterm
>- xfce4-terminal

参考自[archlinux-wiki:i3wm-虚拟终端](https://wiki.archlinux.org/index.php/I3_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E8.99.9A.E6.8B.9F.E7.BB.88.E7.AB.AF)

推荐选择可以较为方便设置透明度的终端如roxterm、xfce-terminal和terminator。

## 托盘图标
bar上某些要显示托盘图标（tray icon），须执行xrandr--output，在i3wm配置文件添加类似语句：

`exec --no-startup-id xrandr --output eDP1 --primary`

其中eDP1是我的计算机的显示设备的名字。查看计算机显示设备名称的命令：

`xrandr`

例如我的显示内容有：

`
xrandr
Screen 0: minimum 8 x 8, current 1920 x 1080, maximum 32767 x 32767
eDP1 connected 1920x1080+0+0 (normal left inverted right x axis y axis) 310mm x 170mm
`

其中的eDP1便是我的显示设备名称。

---

注意：
更改了配置文件需要重新加载或重新启动i3方能生效（按下$Mod+Shift+s或者$Mod+Shift+r，分别为restart和reload）

---

其余参考config内注释和i3wm相关文档说明。

i3wm使用参考：

[i3wm官方文档](http://i3wm.org/docs/)

[ArchLinux-wiki:i3wm（简体中文）](https://wiki.archlinux.org/index.php/I3_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87))

[DeepinLinux-wiki:i3](https://wiki.deepin.org/?title=I3)

# 其他
- pcmanfm的垃圾桶功能需安装gvfs
- 挂载mtp设备安装gvfs-mtp或libmtp(参考[MTP](https://wiki.archlinux.org/index.php/MTP_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.AE.89.E8.A3.85)
- 更改主题可使用lxappearance
- 高分辨显示器缩放问题（参考[HIDPI](https://wiki.archlinux.org/index.php/HiDPI#X_Resources)

在用户目录下编辑（如果没有则新建）~/.Xresources，添加以下内容：
>Xft.dpi: 144
>Xft.autohint: 0
>Xft.lcdfilter:  lcddefault
>Xft.hintstyle:  hintfull
>Xft.hinting: 1
>Xft.antialias: 1
>Xft.rgba: rgb

其中第一行的Xft.dpi: 144就是dpi，根据实际情况调整大小。 保存该文件，然后在~/.xinitrc写入。

>xrdb -merge ~/.Xresources

当然高分屏下文字过小，也可以适当调整字体大小（可以使用lxappearance）。

- 关闭警告声（alarm sound/beep/蜂鸣）
参考[PC speaker](https://wiki.archlinux.org/index.php/PC_speaker),方法多样,如：
`echo "blacklist pcspkr" > /etc/modprobe.d/nobeep.conf`
或
`amixer set channel 0% mute`(安装alsa-utils)
或
`echo xset -b >> /etc/xprofile`
