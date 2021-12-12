# 安装Centos7,出现无法联网的问题-----解决办法

我安装的是centos7的版本s

在我照着[centos7安装教程-CentOS-PHP中文网](https://www.php.cn/centos/472898.html)这个教程安装完后

我发现我的centOS无法联网,在看过网上的各种办法后,都没有一种适合自己这种的

后来无意间 我发现了解决这个问题的解决办法

## 解决办法

1. 点击添加一个网络适配器

   ![image-20210914230206047](https://gitee.com/IU_czx/images/raw/master/img/centos%E8%81%94%E7%BD%91.png)

2. 点击添加后,选择网络适配器,添加就行

3. 网络连接模式继续选择`桥接模式`,重新开机,就能发现系统就能连上网了