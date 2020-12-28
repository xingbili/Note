# Ubuntu 20.04 虚拟机安装

```sehll
软件：Vmware 15.0

​           ubuntu 20.04 server Iso 文件

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

```



