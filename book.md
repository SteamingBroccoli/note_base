# Linux

集合基础知识以及实操经验总结Linux的使用手册

- Linux系统文件结构以及存储方式
- 指令
  - 基础
  - 常用（重点掌握）

- 实操
  - 部署
  - 调试
  - 测试

## 基础知识

=.= 

### Linux系统文件结构



### 软件管理

两个方向

1. yum源：可理解为在线源
2. rpm管理：本地安装源码包

#### yum

```
#查询
yum list installed

#下载
yum -y xxxx（安装的名字）

#卸载
yum remove xxxx
```

#### rpm

```
#查询所有 -》查询单个用管道加grep
rpm -qa

#安装
rpm 

#卸载
rpm -e -nood 


```



### 指令























## 架构部署



#### LAMP架构（Web经典架构）

步骤：

##### 初始化系统生产环境

```
#新机器的检查
从端口与进程
netstat -tnpl | grep xx

#清空linux下的软件进行初始化
yum clean all

rm -rf /var/cache/yum
```

```
###基础软件库安装

linux很多软件的运行，依赖于操作系统本身的一些软件支持
yum groupinstall "Development tools" -y

桌面开发工具包（图形化相关包）
yum groupinstall "Desktop Platform Development" -y 

底层编译库的安装
yum install cmake make pcre-devel ncurses-devel openssl-devel libcurl-devel -y
```

```
# 安装如下基础软件，就可以解决你后面编译脚本的，绝大多数错误问题了
# 安装如下基础软件，就可以解决你后面编译脚本的，绝大多数错误问题了

yum install gcc patch libffi-devel python-devel zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel net-tools vim -y

yum install libxml2-devel  libjpeg-devel libpng-devel freetype-devel  libcurl-devel wget -y
```

##### 更改yum源（阿里云、清华等）

```
#安装wget
yum -y install wget

#配置yum源
wget -O /etc/yum.repos.d/CentOS-Base.repo https://mirrors.aliyun.com/repo/Centos-7.repo

#清空yum缓存
yum clean all

rm -rf /var/cache/yum

##!!!!!!!注意！！！！！！！！！ 关闭selinux以及firewalld （可能会导致目录数据无法写入）

#关闭selinux
grep -i 'selinux' /etc/selinux/config
# SELINUX= can take one of these three values:
SELINUX=disabled

#关闭防火墙
systemctl stop firewalld
systemctl disable firewalld
```



##### 依次安装版本适配的apache、mysql、php

```
mysql安装

1. 创建mysql用户，用于给mysql的数据，进程，设置相关的user属主
2. cd /usr/local ; mkdir software-mysql;cd software-mysql
wget -c https://repo.huaweicloud.com/mysql/Downloads/MySQL-5.6/mysql-5.6.50.tar.gz

```



```
apache安装

```





## 磁盘管理	

重要掌握，环境初始化以及增减配常用



#### 环境状态检查

##### df 命令



##### lsblk 命令











#### 分区

- GPT类型
- mbr类型

##### GPT类型（大于2TB）



##### mbr类型（小与2TB）

实践

任务：将sdb硬盘分区（20G）

- 1个主分区  (2G)
- 1个扩展分区 （剩下的全给他） 18G
- 2个逻辑分区
  - 逻辑分区1，10G
  - 逻辑分区2，剩下的都给他  8G



#### 格式化

使用mkfs命令可以进行分区，文件系统格式化。

```

1.把机器上的/dev/sdc硬盘，重新分区一个单个分区，是20G
fdisk /dev/sdc

2.给这个分区，分别格式化xfs文件系统
[yuchao-linux01 root ~]$mkfs.xfs /dev/sdc1
meta-data=/dev/sdc1              isize=512    agcount=4, agsize=1310656 blks
         =                       sectsz=512   attr=2, projid32bit=1
         =                       crc=1        finobt=0, sparse=0
data     =                       bsize=4096   blocks=5242624, imaxpct=25
         =                       sunit=0      swidth=0 blks
naming   =version 2              bsize=4096   ascii-ci=0 ftype=1
log      =internal log           bsize=4096   blocks=2560, version=2
         =                       sectsz=512   sunit=0 blks, lazy-count=1
realtime =none                   extsz=4096   blocks=0, rtextents=0


3.挂载一个目录，到这个分区，即可使用该分区，存储数据了
[yuchao-linux01 root ~]$mount /dev/sdc1 /opt/my_sdc/
[yuchao-linux01 root ~]$
[yuchao-linux01 root ~]$
[yuchao-linux01 root ~]$mount -l |grep sdc1
/dev/sdc1 on /opt/my_sdc type xfs (rw,relatime,attr2,inode64,noquota)
[yuchao-linux01 root ~]$


4.查看挂载情况
mount -l


5.设置永久挂载
上述的mount挂载命令是临时生效，需要开机就让系统自动挂载，方可实现，永久生效
编辑 /etc/fstab文件即可
[yuchao-linux01 root /opt]$tail -1 /etc/fstab 
/dev/sdc1 /opt/my_sdc xfs defaults 0 0 


6.重启机器，查看是否开机就能自动挂载，读取到/dev/sdc1磁盘的数据
再次使用mount -l |grep sdc 查看磁盘的挂载情况

以及去访问挂载点，是否能读到分区的数据即可

[yuchao-linux01 root ~]$mount -l |grep sdc
/dev/sdc1 on /opt/my_sdc type xfs (rw,relatime,attr2,inode64,noquota)
[yuchao-linux01 root ~]$
[yuchao-linux01 root ~]$
[yuchao-linux01 root ~]$
[yuchao-linux01 root ~]$ls /opt/my_sdc/


```











# 分布式版本控制系统

- git

- svn

  

## Git

 Git 是一个分布式版本控制系统，它允许开发者在本地仓库中工作，并可以将更改推送到远程仓库。

### 基础知识



### 指令

#### 连接

ssh：

#### 本地仓库的创建以及推送

```
1. cd到需要提交的文件夹

2. git init：初始化一个新的 Git 仓库。

3. git add：将文件添加到暂存区。如果使用 `.` 作为参数，则添加当前目录中的所有文件。
   #git add .

#SSH连接方式
4. git remote add origin git@github.com:SteamingBroccoli/note_base.git
5. git push -u origin master

```

#### 

#### 更新推送

```
#先保存
1. git add .  
2. git commit -m “更新内容”
2. git push origin “分支名字”
```



 

#### 查询类指令

```
git commit：提交暂存区的更改到本地仓库。可以使用 `-m` 参数来添加提交信息。
#例如：git commit -m “测试”


git reset：重置工作目录或暂存区的文件到某个历史提交。
git branch：查看和操作本地分支。
git checkout：切换到某个分支或查看某个提交的状态。

git push：将本地分支的更改推送到远程仓库。

Git 命令的组合使用可以实现更复杂的操作，例如：
git stash：保存当前工作目录的更改，以便稍后恢复。
git stash apply：应用保存的更改。
git stash drop：删除保存的更改。
git stash clear：删除所有保存的更改。
```



#### 拉取

git merge：将指定的分支合并到当前分支。
git pull：从远程仓库获取并合并分支









# 数据库



# 服务器

Nginx高性能HTTP/Pr0xy服务器



# 自动化运维



# 运维监控





# 容器虚拟化技术







# 中间件









# 堡垒机



