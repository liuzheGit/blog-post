---
title: windows下改键AutoHotKey
date: 2018-12-24 21:15:58
tags: windows
categories: Tools
---

## Win下效率神器: AutoHotKey

**AutoHotkey**是一个windows下的开源、免费、自动化软件工具。它由最初旨在提供键盘快捷键的脚本语言驱动(称为：**热键**)，随着时间的推移演变成一个完整的脚本语言。但你不需要把它想得太深，你只需要知道它可以简化你的重复性工作，一键自动化启动或运行程序等等；以此提高我们的**工作效率**，改善**生活品质**；通过按键映射，鼠标模拟，定义宏等。

## 为什么使用AutoHotKey

**caps键**是一个有着天然优势的按键,但是却是一个被设计的最没用的按键(系统默认下), 只是为了切换大小写. (我输入大写字母不会按shift吗?)



## 下载安装 AutoHotKey

进入官网 [AutoHokey](http://www.autohotkey.com/) 点击download  , 之后一路下一步



## 脚本

这里简单说明下脚本中常用符号代表的含义：

> **#** 号代表 **Win** 键；
> **!** 号代表 **Alt** 键；
> **^** 号代表 **Ctrl** 键；
> **+** 号代表 **shift** 键；
> **::** 号(两个英文冒号)起分隔作用；
> **run**，非常常用 的 AHK 命令之一;
> **;** 号代表 注释后面一行内容；

 **run**它的后面是要运行的程序完整路径





## win 下的系统默认 win 快捷键

Win + E：打开资源管理器；
Win + D：显示桌面；
Win + F：打开查找对话框；
Win + R：打开运行对话框；
Win + L：锁定电脑；
Win + PauseBreak：打开系统属性对话框;
Win + Q: 本地文件/网页等搜索;
Win + U: 打开控制面板－轻松使用设置中心;

## 我的配置

1. 主要为了 把 caps 改为 ctrl 

   ```
   ;;changeCaps.ahk
   
   +Capslock::Capslock
   Capslock::Ctrl
   ```

   把`caps键`, 改为 `ctrl 键`,  原来切换 大小写的 改为 `shift + capslock`

2. 颜色拾取

   ```
   ^#z::
   MouseGetPos, mouseX, mouseY
   ; 获得鼠标所在坐标，把鼠标的 X 坐标赋值给变量 mouseX ，同理 mouseY
   PixelGetColor, color, %mouseX%, %mouseY%, RGB
   ; 调用 PixelGetColor 函数，获得鼠标所在坐标的 RGB 值，并赋值给 color
   StringRight color,color,6
   ; 截取 color（第二个 color）右边的6个字符，因为获得的值是这样的：#RRGGBB，一般我们只需要 RRGGBB 部分。把截取到的值再赋给 color（第一个 color）。
   clipboard = %color%
   ; 把 color 的值发送到剪贴板
   return
   ```

   用 `ctrl + win + z` 快速拾取 鼠标位置的 16进制的颜色值.



## 未完

- [AHK中文指南](https://ahkcn.github.io/docs/Tutorial.htm#Create)
- [晚晴幽草轩](https://www.jeffjade.com/2016/03/11/2016-03-11-autohotkey/)

