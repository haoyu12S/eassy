---
title: Problems with installing NVIDIA driver
date: 2018-06-03 19:07:23
tags: NVIDIA
categories: Linux
---

安装Nvidia显卡驱动出现了一大堆问题，特此在这里总结，以备日后参考

以上是文章摘要
<!--more-->
以下是余下全文

# 驱动下载 #
到官网[http://www.nvidia.cn/Download/index.aspx?lang=cn](http://www.nvidia.cn/Download/index.aspx?lang=cn "Nvidia驱动下载")下载自己系统和显卡的版本，这里主要针对的是Linux系统下的问题。

# 驱动安装 #
## 1-删除旧驱动 ##

*如果是apt-get模式安装的旧驱动用以下方法* 

    sudo apt-get remove –purge nvidia*
	sudo autoremove

*如果是NVIDIA-\*.run模式安装的旧驱动用以下方法*

	sudo NVIDIA-*run --uninstall

## 2-禁用自带驱动nouveau ##
打开编辑配置文件 

	sudo gedit /etc/modprobe.d/blacklist.conf

末尾一行添加 blacklist nouveau 之后执行 

	sudo update-initramfs -u

重启电脑，检查是否禁用nouveau

	lsmod | grep nouveau

如果没有任何输出则表示禁用成功

## 3-安装驱动 ##
进入命令行界面

	Ctrl-Alt+F1

登陆账户，并且禁用图形界面（X-server）

	sudo service lightdm stop

进入下载驱动的文件夹，赋予驱动安装文件执行的权限

	sudo chmod a+x NVIDIA-*.run

安装

	sudo ./NVIDIA-*.run –no-opengl-files

- no-opengl-files 只安装驱动文件，不安装OpenGL文件。这个参数最重要
- no-x-check 安装驱动时不检查X服务
- no-nouveau-check 安装驱动时不检查nouveau 
- 后面两个参数可不加。

## 4-检测是否安装成功 ##
	nvidia -smi
	nvidia -settings
如果有返回，说明安装成功


----------

# <font color=red> 出现了循环登陆的问题  </font> #

## 1-最简单无脑方法，卸载全部驱动，重新再次安装，确保添加参数 –no-opengl-files ##
## 2-重新启动，在Grub界面选Ubuntu系统那一行然后按E键进入编辑模式！ ##
![](https://i.imgur.com/8WTfElY.jpg)
![](https://i.imgur.com/11tkddr.jpg)

在上图那个位置，我们会看到 "quiet splash nomodeset",主要看是否有nomodeset，有的话删除它（可能有人是queit splash= nomodeset,删除'= nomodeset'即可！）
然后在原来那个位置加 acpi_osi=linux（代码之间用空格隔开！），然后按F10启动，就可以进入界面了。

进入系统后查看grub文件

	sudo vi /etc/default/grub 或 sudo gedit /etc/default/grub
	#打开文件后将nomodest删除替换为 acpi_osi=linux
	#然后更新grub
	sudo update-grub
## 3-查看报错文件 ##
出现循环登录问题的时候，可以按照上面说的方法进入shell，在home目录下找到.xsession-errors文件 

	cd ~
	ls -a
	vi(gedit) .xsession-errors
接着你就可以看到里面的日志信息，按照日志里面的信息去google，也许可以解决驱动安装的办法。 

## 4-下载最近的驱动 ##
出现这个问题最大的可能原因是安装的Nvidia驱动和系统或者硬件有不兼容，下载最新的驱动一般可以解决问题。