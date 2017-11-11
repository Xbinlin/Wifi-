# 考勤机的树莓派设置

用树莓派做可以WiFi考勤与指纹识别的考勤机

## 树莓派的基础设置

### 烧录系统

1.准备硬件：树莓派3代、电脑、网线、电源线、tf卡及读卡器
2.TF卡安装操作系统（img镜像文件刻录）：从树莓派官网http://www.raspberrypi.org/downloads上下载树莓派的linux的操作系统的zip文件；下载第三方工具Image Write for Windows (Win32 Disk Imager)http://sourceforge.net/projects/win32diskimager/将TF卡插入读卡器，把读卡器插入电脑的USB接口，打开Win32DiskImager文件夹，运行其中的Win32DiskImager程序，选择Raspbian文件夹中的img文件，点击write，然后选择yes，等到程序运行完毕即可，取出TF卡。
3.将tf卡插入树莓派，将网线插入树莓派、电脑，插入电源

### ssh连接树莓派

4.控制面板共享网络，将tcp/ipv4属性中的ip地址改为192.168.137.1
5.在电脑上用命令行win10（arp -a）找到树莓派ip地址，打开SecureCRT选择ssh连接树莓派

### 系统初次配置

6.输入用户名Pi、密码raspberry，回车，输入初始配置的命令：sudo raspi-config进入树莓派的配置界面
7.运行Expand_Filesystem（将整张SD卡存储空间分配给操作系统使用）
8.进入Internationalisation Options按照顺序进行重要设置：I1是区域配置，设置系统界面语言，所属国家区域的特别属性，设置中文界面的方法：区域应先选择en_GB.UTF-8和zh_CN.UTF-8（分别移动到上述2个项目，按空格键出现“*”号表示已选择，再按一次“*”取消选择），然后在确认界面缺省显示语言，en_GB.UTF-8显示英文；zn_CN.UTF-8显示中文：I2是设置时区，应该选择Asia – Shanghai；配置结束以后,选择最下面的<finish >，一般树莓派会重新启动。以后有需求的话，可以手动重新运行：sudo raspi-config

## 设置数据库

### 安装MySQL
9.获取管理员权限，输入命令sudo passwd，输入密码；安装MySQL，$ sudo apt-get install mysql-server python-mysqldb，安装过程中输入root管理员的密码；重启，使用sudo apt-get update 更新软件；输入命令进入mysql mysql -u root -p，发现Mysql已经安装完毕；修改Mysql配置文件，优化树莓派上的Mysql，nano /etc/mysql/my.cnf，同样在尾部追加
[mysqld]
character-set-server=utf8
key_buffer = 16k
max_allowed_packet = 1M
thread_stack = 64K
thread_cache_size = 4
query_cache_limit = 1M
default-storage-engine = MYISAM
loose-skip-innodb
给root用户设置外部访问权限，这样局域网就可以通过ip地址统一访问，登入 Mysql，输入grant all privileges on *.* to root@'ip地址' identified by 'root密码' with grant option;
登录Mysql，输入SHOW DATABASES; 

### 数据库设计

### 数据库开发

## Wifi AP热点功能设置

### 选择网卡

### 安装软件

### 配置DHCP功能

### 配置参数

### 配置NAT(IP转发)

### 基本验证

## 指纹识别模块设置





