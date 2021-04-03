> 阿里云 地址：https://developer.aliyun.com/mirror/
>
> ​                       https://mirrors.tuna.tsinghua.edu.cn/
>
> ubuntu 修改虚拟机ip sudo/etc/network/interfaces  

# Ubuntu 20.04 虚拟机安装

```i
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
sudo vim /etc/ssh/sshd_config菜单
#permitRootLogin without-password 注释掉这行，新增下面一行
permitRootLogin yes
3、重启 ssh 服务sucd
sudo /etc/init.d/ssh restart
配置ip
sudo vi /etc/netplan/00-installer-config.yaml

network:
  ethernets:
    ens33:     #配置的网卡的名称
      addresses: [192.168.31.215/24]    #配置的静态ip地址和掩码
      dhcp4: no    #关闭DHCP，如果需要打开DHCP则写yes
      optional: true
      gateway4: 192.168.31.1    #网关地址
      nameservers:
         addresses: [192.168.31.1,114.114.114.114]    #DNS服务器地址，多个DNS服务器地址需要用英文逗号分隔开
  version: 2
  renderer: networkd    #指定后端采用systemd-networkd或者Network Manager，可不填写则默认使用systemd-workd
  
netplan apply 后生效
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

## docker 安装jenkins

```shell
1)docker pull jenkinsci/blueocean  下载最新版本的jenkins 镜像


docker run \
  -u root \
  --rm \  
  -d \ 
  -p 8080:8080 \ 
  -p 50000:50000 \ 
  -v jenkins-data:/var/jenkins_home \ 
  -v /var/run/docker.sock:/var/run/docker.sock \ 
  jenkinsci/blueocean 
（可选） jenkinsci/blueocean 关闭时自动删除Docker容器（下图为实例）。如果您需要退出Jenkins，这可以保持整洁。
（可选）jenkinsci/blueocean 在后台运行容器（即“分离”模式）并输出容器ID。如果您不指定此选项， 则在终端窗口中输出正在运行的此容器的Docker日志。
映射（例如“发布”）jenkinsci/blueocean 容器的端口8080到主机上的端口8080。 第一个数字代表主机上的端口，而最后一个代表容器的端口。因此，如果您为此选项指定 -p 49000:8080 ，您将通过端口49000访问主机上的Jenkins。
（可选）将 jenkinsci/blueocean 容器的端口50000 映射到主机上的端口50000。 如果您在其他机器上设置了一个或多个基于JNLP的Jenkins代理程序，而这些代理程序又与 jenkinsci/blueocean 容器交互（充当“主”Jenkins服务器，或者简称为“Jenkins主”）， 则这是必需的。默认情况下，基于JNLP的Jenkins代理通过TCP端口50000与Jenkins主站进行通信。 您可以通过“ 配置全局安全性” 页面更改Jenkins主服务器上的端口号。如果您要将您的Jenkins主机的JNLP代理端口的TCP端口 值更改为51000（例如），那么您需要重新运行Jenkins（通过此 docker run …​命令）并指定此“发布”选项 -p 52000:51000，其中最后一个值与Jenkins master上的这个更改值相匹配，第一个值是Jenkins主机的主机上的端口号， 通过它，基于JNLP的Jenkins代理与Jenkins主机进行通信 - 例如52000。
（可选，但强烈建议）映射在容器中的`/var/jenkins_home` 目录到具有名字 jenkins-data 的volume。 如果这个卷不存在，那么这个 docker run 命令会自动为你创建卷。 如果您希望每次重新启动Jenkins（通过此 docker run ... 命令）时保持Jenkins状态，则此选项是必需的 。 如果你没有指定这个选项，那么在每次重新启动后，Jenkins将有效地重置为新的实例。
注意: 所述的 jenkins-data 卷也可以 docker volume create命令创建： docker volume create jenkins-data 代替映射 /var/jenkins_home 目录转换为Docker卷，还 可以将此目录映射到计算机本地文件系统上的目录。 例如，指定该选项 -v $HOME/jenkins:/var/jenkins_home 会将容器的 /var/jenkins_home 目录映射 到 本地计算机上目录中的 jenkins 子目录， 该$HOME目录通常是 /Users/<your-username>/jenkins 或`/home/<your-username>/jenkins` 。
（可选 /var/run/docker.sock 表示Docker守护程序通过其监听的基于Unix的套接字。 该映射允许 jenkinsci/blueocean 容器与Docker守护进程通信， 如果 jenkinsci/blueocean 容器需要实例化其他Docker容器，则该守护进程是必需的。 如果运行声明式管道，其语法包含agent部分用 docker
例如， agent { docker { ... } } 此选项是必需的。 在Pipeline Syntax 页面上阅读更多关于这个的信息 。

jenkinsci/blueocean Docker镜像本身。如果此镜像尚未下载，则此 docker run 命令 将自动为您下载镜像。此外，如果自上次运行此命令后发布了此镜像的任何更新， 则再次运行此命令将自动为您下载这些已发布的镜像更新。 注意：这个Docker镜像也可以使用以下 docker pull命令独立下载（或更新） ： docker pull jenkinsci/blueocean 注意: 如果复制并粘贴上面的命令片段不起作用，请尝试在此处复制并粘贴此无注释版本：
docker run \
  -u root \
  --rm \
  -d \
  -p 8080:8080 \
  -p 50000:50000 \
  -v jenkins-data:/var/jenkins_home \
  -v /var/run/docker.sock:/var/run/docker.sock \
  jenkinsci/blueocean
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
gitlab_rails['smtp_address'] = "smtp.qq.com"
gitlab_rails['smtp_port'] = 465
gitlab_rails['smtp_user_name'] = "65645976@qq.com"
gitlab_rails['smtp_password'] = "vpuuabrigznwbhfd" //客户端授权码
gitlab_rails['smtp_domain'] = "smtp.qq.com"
gitlab_rails['smtp_authentication'] = "login"
gitlab_rails['smtp_enable_starttls_auto'] = true
gitlab_rails['smtp_tls'] = true
gitlab_rails['gitlab_email_from']='65645976@qq.com'

......
user["git_user_email"] = "xxxxxx@163.com"

修改配置文件需要gitlab-ctl reconfigure

默认用户密码  root  5iveL!fe


.测试配置是否成功：
执行 gitlab-rails console进入控制台。 然后在控制台提示符后输入下面的命令 发送一封测试邮件：Notify.test_email('收件人邮箱', '邮件标题', '邮件正文').deliver_now

```

### gitlab ubuntu 在线安装

```shell
步骤
sudo apt update
sudo apt install ca-certificates curl openssh-server postfix
cd /tmp
curl -LO https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh
sudo bash /tmp/script.deb.sh
sudo apt install gitlab-ce
备注：如果使用国内镜像：首先
信任公钥
curl https://packages.gitlab.com/gpg.key 2> /dev/null | sudo apt-key add - &>/dev/null

注意：根据系统不同版本更新 源
vim /etc/apt/sources.list.d/gitlab_gitlab-ce.list
deb https://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/ubuntu focal main
deb-src https://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/ubuntu focal main

gitlab 配置之前 使用ufw 防火墙规则
ufw enable 激活

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

### gitlab 忘记root密码

```shell
1、gitlab-rails console -e production
2、user = User.where(username:"root").first
3、user.password = "test"(最少8位)
4、user.save!
```

### gitlab 密钥管理



# docker 安装gitlab

```shell
参考官方文档
 docker pull gitlab/gitlab-ce
$ docker run -d  -p 443:443 -p 80:80 -p 222:22 --name gitlab --restart always -v /home/gitlab/config:/etc/gitlab -v /home/gitlab/logs:/var/log/gitlab -v /home/gitlab/data:/var/opt/gitlab gitlab/gitlab-ce
# -d：后台运行
# -p：将容器内部端口向外映射
# --name：命名容器名称
# -v：将容器内数据文件夹或者日志、配置等文件夹挂载到宿主机指定目录
```

## docker 安装zookeeper

```shell
docker pull zookeeper
docker run --privileged=true -d --name zookeeper --publish 2181:2181  -d zookeeper:latest
```



# 问题







