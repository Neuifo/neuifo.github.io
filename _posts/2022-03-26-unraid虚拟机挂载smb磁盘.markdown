---
layout: post
title: "unraid虚拟机挂载smb磁盘"
date: 2022-03-26 16:26:23 +0800
categories: 2022-03
tags: unraid,smb,cifs
img: /assets/images/blog/2022-03/dai.jpg
describe: 解决aosp编译问题
---

## 0x01:需求
    
   通过虚拟机编译aosp源码
    
   目前环境：
    
   1.源码在unraid磁盘上，smb服务
    
   2.通过unraid安装的ubuntu虚拟机系统
    
## 0x02:安装xfce4/xrdp

   系统安装没什么，这里主要讨论安装xrdp，通过RDM远程连接
    
   ```shell
        sudo apt-get install xfce4
        sudo apt install xrdp
   ```
     [参考](https://www.cnblogs.com/zh-dream/p/13884260.html)
     
## 0x03:修复中文语言问题
    
   ```shell
      sudo apt-get install fonts-droid-fallback ttf-wqy-zenhei ttf-wqy-microhei fonts-arphic-ukai fonts-arphic-uming
   ```
    
   [参考](https://blog.csdn.net/weixin_39792252/article/details/80415550)
    
## 0x04:修复smb服务问题

   并不是没有安装smb服务，而是无法打开网路
    
   `Failed to open "/ on". Specified location is not supported.`
   ```shell
        sudo apt install gvfs-backends
   ```
    
   [参考](https://forums.debian.net/viewtopic.php?t=126176)
    
    
## 0x04:磁盘挂载
    
   ```shell
        sudo apt-get install cifs-utils
        sudo mkdir /mnt/neuifo/aosp7
        sudo mount -t cifs -o username=neuifo,password=1024,uid=1000,gid=100,dir_mode=0777,file_mode=0777 //192.168.50.83/aosp7 /mnt/aosp7
        //unmount /mnt/aosp7
   ```
   [参考](https://support.zadarastorage.com/hc/en-us/articles/213024986-How-to-Mount-a-SMB-Share-in-Ubuntu)
   
## 0x05:安装浏览器

   ```shell
        sudo apt-get install chromium-browser
   ```
   [参考](https://www.reddit.com/r/xfce/comments/p4giy7/how_to_install_a_web_browser_in_xfce/)
    
    