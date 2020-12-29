

# Ubuntu 20.04 虚拟机安装

```sehll
软件：Vmware 15.0
​ ubuntu 20.04 server Iso 文件
网络模式选择 Nat
磁盘扩容选 lvm
安装ssh 

设置镜像源：cd /etc/apt/sources.list
apt-get update 更新源
apt-get install 
apt-get remove 卸载
apt-get autoclean 自动清理
apt-get autoremove
```

# jenkins 虚拟机安装

##     安装JDK 

```shell
step1 下载jdk linux.tar.gz 版本
step2 tar -zxvf  linux.tar.gz 解压缩
step3 递归创建目录  mkdir -p  /usr/local/java/
step4 mv jdk  /usr/local/java
step5 设置所有者 chown -R root:root /usr/local/java/  -R 递归
配置环境变量
etc/environment

PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games"
export JAVA_HOME=/usr/local/java/jdk1.8.0_201
export JRE_HOME=/usr/local/java/jdk1.8.0_201/jre
export CLASSPATH=$CLASSPATH:$JAVA_HOME/lib:$JAVA_HOME/jre/lib

配置用户环境变量
/etc/profile
export JAVA_HOME=/usr/local/java/jdk1.8.0_201
export JRE_HOME=/usr/local/java/jdk1.8.0_201/jre
export CLASSPATH=$CLASSPATH:$JAVA_HOME/lib:$JAVA_HOME/jre/lib
export PATH=$JAVA_HOME/bin:$JAVA_HOME/jre/bin:$PATH:$HOME/bin

让修改立即生效
.  /etc/profile
或
source  /etc/profile


```

## 安装docker

```shell
参照官网
```

## 安装Jenkins

```shell
在Ubuntu上安装Jenkins相对简单。我们将启用Jenkins APT存储库，导入存储库GPG密钥，并安装Jenkins软件包。

使用以下wget命令导入Jenkins存储库的GPG密钥：
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
使用以下命令将Jenkins存储库添加到系统中：
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
更新apt软件包列表
sudo apt update
sudo apt install jenkins
如果因为No Java executable found in current PATH
确认安装配置了jdk
.建立软连接：ln -s /usr/java/jdk1.8/bin/java /usr/bin/java（换成你自己的路径）
service jenkins restart  
```

## start Jenkins

###  jenkins pipeline



