> 阿里云 地址：https://developer.aliyun.com/mirror/
>
> ​                       https://mirrors.tuna.tsinghua.edu.cn/
>
> ubuntu 修改虚拟机ip sudo /etc/network/interfaces  

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

设置root 用户登录
1、修改root 用户密码
sudo passwd root
2、修改ssh配置文件允许root登录
sudo vim /etc/ssh/sshd_config
#permitRootLogin without-password 注释掉这行，新增下面一行
permitRootLogin yes
3、重启 ssh 服务
sudo /etc/init.d/ssh restart
```



# jenkins 虚拟机安装

##     安装JDK

```shell
step1 下载jdk linux.tar.gz 版本
step2 tar -zxvf  linux.tar.gz 解压缩
step3 递归创建目录  mkdir -p  /usr/local/java/
step4 mv jdk  /usr/local/java
step5 设置所有者 chown -R root:root /usr/local/java/     //-R 递归

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

## 安装Jenkins

> 参考官网：https://www.jenkins.io/doc/book/installing/linux

### ubuntu安装jenkins

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


修改相关配置（修改端口）
/etc/init.d/jenkins
/etc/default/jenkins  

修改jenkins 插件源  插件管理-》升级
https://mirrors.tuna.tsinghua.edu.cn/jenkins/updates/update-center.json

```

### centos 安装jenkins

```shell
1）安装JDK
Jenkins需要依赖JDK，所以先安装JDK1.8
yum install java-1.8.0-openjdk* -y
安装目录为：/usr/lib/jvm
2）获取jenkins安装包
下载页面：https://jenkins.io/zh/download/
安装文件：jenkins-2.190.3-1.1.noarch.rpm
3）把安装包上传到192.168.66.101服务器，进行安装
rpm -ivh jenkins-2.190.3-1.1.noarch.rpm
4）修改Jenkins配置
vi /etc/syscofig/jenkins
修改内容如下：
JENKINS_USER="root"
JENKINS_PORT="8888"
5）启动Jenkins
systemctl start jenkins
6）打开浏览器访问
http://192.168.66.101:8888
7）获取并输入admin账户密码
cat /var/lib/jenkins/secrets/initialAdminPassword 8）跳过插件安装
因为Jenkins插件需要连接默认官网下载，速度非常慢，而且经过会失败，所以我们暂时先跳过插件安
装
```

## start Jenkins

```shell
1、安装插件（git,maven,角色，等等）
2、添加角色、添加用户、给用户赋予角色
3、添加项目
```

# gitLab 安装

## centos 安装gitLab

> 参考官网：https://about.gitlab.com/install/#centos-7/

```shell
安装基础依赖包
 yum install curl policycoreutils openssh-server openssh-clients
 开启sshd服务
 systemctl enable sshd 
 systemctl start sshd
 开放GitLab Web 的端口
 firewall-cmd --permanent --add-port=80/tcp
 新建yum源
 vim /etc/yum.repos.d/gitlab-ce.repo
 
[gitlab-ce]
name=Gitlab CE Repository
baseurl=https://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/yum/el$releasever/
gpgcheck=0
enabled=1

执行安装
 yum makecache
 yum install gitlab-ce
 
 启动并初始化安装
gitlab-ctl start
gitlab-ctl reconfigure

```

## ubuntu 安装gitlab

> 官网：

```shell
下载指定安装包
https://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/ubuntu/pool/bionic/main/g/gitlab-ce/
解压安装
dpkg  -i  gitlab-ce_8.17.4-ce.0_amd64.deb
修改设置
vim /etc/gitlab/gitlab.rb 主要以下配置

external_url 'http://192.168.10.123:80'
......
gitlab_rails['time_zone'] = 'Asia/Shanghai'
gitlab_rails['gitlab_email_from'] = 'xxxxxx@163.com'
......
gitlab_rails['smtp_enable'] = true
gitlab_rails['smtp_address'] = "smtp.163.com"
gitlab_rails['smtp_port'] = 25
gitlab_rails['smtp_user_name'] = "xxxxxx@163.com"
gitlab_rails['smtp_password'] = "111111" # 客户端授权密码
gitlab_rails['smtp_domain'] = "163.com"
gitlab_rails['smtp_authentication'] = "login"
gitlab_rails['smtp_enable_starttls_auto'] = true
......
user["git_user_email"] = "xxxxxx@163.com"

修改配置文件需要gitlab-ctl reconfigure

默认用户密码  root  5iveL!fe


.测试配置是否成功：
执行 gitlab-rails console进入控制台。 然后在控制台提示符后输入下面的命令 发送一封测试邮件：Notify.test_email('收件人邮箱', '邮件标题', '邮件正文').deliver_now

```

## gitlab 常用命令

| 常用命令                                    | 说明                                                      |
| ------------------------------------------- | --------------------------------------------------------- |
| sudo gitlab-ctl reconfigure                 | 重新加载配置，每次修改`/etc/gitlab/gitlab.rb`文件之后执行 |
| sudo gitlab-ctl status                      | 查看 GitLab 状态                                          |
| sudo gitlab-ctl start                       | 启动 GitLab                                               |
| sudo gitlab-ctl stop                        | 停止 GitLab                                               |
| sudo gitlab-ctl restart                     | 重启 GitLab                                               |
| sudo gitlab-ctl tail                        | 查看所有日志                                              |
| sudo gitlab-ctl tail nginx/gitlab_acces.log | 查看 nginx 访问日志                                       |
| sudo gitlab-ctl tail postgresql             | 查看 postgresql 日志                                      |



# 安装docker

```shell
参考官方文档
```

##



# 问题







