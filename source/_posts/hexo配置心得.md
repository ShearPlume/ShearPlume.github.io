---
title: hexo配置心得
date: 2022-09-22 13:32:59
tags:
---

 ![](../images/1.jpg)

1.由于config.yml配置文件里的git仓库是master，所以每次hexo g hexo d后 public文件夹会被git到master的branch里，所以域名指向master是没问题的，而hexo仓库是用来多设备之间git整个大文件夹的，所以没必要把域名指向它（万一寄了至少域名指向的网页还正常）
