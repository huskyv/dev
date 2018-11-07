---
description: Windows下安装启动Zookeeper
---

# Zookeeper

## 1.解压  zookeeper-3.3.6.tar.gz 至你电脑安装目录

![](../.gitbook/assets/image%20%286%29.png)

## 2.备份 conf/zoo\_sample.cfg 文件, 重命名为 zoo.cfg



![](../.gitbook/assets/image%20%285%29.png)

## 3.双击 bin/zkServer.cmd 启动zk

![](../.gitbook/assets/image%20%2813%29.png)

##  4.出现以下日志代表启动成功 默认端口 2181 

![](../.gitbook/assets/image%20%283%29.png)

## 5.如出现端口冲突,需修改端口,修改 conf/zoo.cfg 文件中 clientPort 项 

![](../.gitbook/assets/image%20%289%29.png)



