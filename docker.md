

### docker 概述

docker  2010

```shell
文档地址：https://docs.docker.com
仓库地址：https://hub.docker.com/
```

docker 能干吗：

```shell
容器化技术：容器内的应用直接运行再宿主机的内容，容器没有自己的内核，也没有虚拟我们的硬件，
每个容器间互相隔离，互不影响
```

> DevOps(开发运维)

**应用更快速的交付和部署**

传统：一堆文档，安装程序

Docker：打包镜像发布测试，一键运行

**更便捷的升级和扩容**

使用docker 之后，我们部署应用就和搭积木一样 

项目打包为一个镜像，扩展 服务器A！服务器B

**更简单的系统运维**

在容器化之后，我们的开发， 测试环境都是高度一致的

**更高效的计算资源利用**

Docker 是内核级别的虚拟化，可以在一个物理机上运行很多的容器实例

![Docker架构图](http://gz.bcebos.com/liminjun-blog/2017/04/26/Docker_Architecture.png)

**镜像（image）：**

docker 镜像就好比是一个模板，可以通过这个模板来创建容器服务，tomcat 镜像====>run====> tomcat01容器

通过这个镜像可以创建多个容器（最终服务运行或者项目运行就是在容器中）

**容器（container）：**

Docker 利用容器技术，独立运行一个或者一组应用，通过镜像来创建

启动，停止，删除，基本命令

目前就可以把这个容器理解为就是体格建议的linux系统

**仓库（repository）：**

仓库就是存放镜像的地方

仓库分为私有和共有

### docker 安装

#### 1、 卸载旧 的

   ```shell
  sudo yum remove docker \              
  docker-client \                 
  docker-client-latest \                
  docker-common \                 
  docker-latest \                
  docker-latest-logrotate \               
  docker-logrotate \                
  docker-engine
   ```

#### 2、需要的安装包

 ```shell
sudo yum install -y yum-utils
 ```

#### 3、设置仓库镜像

```shell
sudo yum-config-manager \    --add-repo \    https://download.docker.com/linux/centos/docker-ce.repo
sudo yum-config-manager \    --add-repo \    [**http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo**](http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo)
```

#### **4、 安装docker 相关资源， docker-ce 社区版   ee 企业版**

```shell
sudo yum install docker-ce docker-ce-cli containerd.io
```

#### 5、启动 docker

```shell
sudo systemctl start docker
```

#### 6 、验证是否安装成功

```shell
docker -version or  sudo docker run hello-world
```

#### 7 卸载

```shell
$ sudo yum remove docker-ce docker-ce-cli containerd.io
$ sudo rm -rf /var/lib/docker
```

### 配置阿里云

![image-20200924224625291](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200924224625291.png)

![image-20200924224848719](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200924224848719.png)





Docker 是一个Client-server 结构的系统，Docker 的守护进程运行

```shell
sudo mkdir -p /etc/docker sudo tee /etc/docker/daemon.json <<-'EOF' {  "registry-mirrors": ["https://fuf9gr5l.mirror.aliyuncs.com"] } EOF sudo systemctl daemon-reload sudo systemctl restart docker
回顾helloworld 流程
docker 怎么工作
docker 是一个 Client-Server 结构的系统，Docker 的守护进行运行在主机上，通过Socket 从客户端访问
```

### docker命令：

#### **帮助命令**

```shell
docker version
docker info
docker 命令 --help
```



#### 镜像命令

**docker images **

```shell
docker images -a -q
-a # 列出所有镜像
-q # 只列出 id
```

##### **docker search  搜索镜像**

```shell
# 可选项
--filter = stars =3000   # stars >3000 的
```

##### **docker pull 下载镜像**

```shell
# docker pull mysql:<版本 >
```

![image-20200925213738619](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200925213738619.png)

##### **dockers rmi  删除镜像**

```shell
-f (强制删除) <镜像名或者id>
docker rmi -f $(docker images -aq) #删除全部的容器
```

#### 容器命令

，**有了镜像才可以创建容器，Linux下载一个centos镜像来测试学习**

```shell
docker pull centos
```

#####  **新建容器并启动**

```shell
docker run [可选参数] image
#参数说明
-a stdin: 指定标准输入输出内容类型，可选 STDIN/STDOUT/STDERR 三项；
-d: 后台运行容器，并返回容器ID；
-i: 以交互模式运行容器，通常与 -t 同时使用；
-P: 随机端口映射，容器内部端口随机映射到主机的高端口
-p: 指定端口映射，格式为：主机(宿主)端口:容器端口
-t: 为容器重新分配一个伪输入终端，通常与 -i 同时使用；
--name="nginx-lb": 为容器指定一个名称；
--dns 8.8.8.8: 指定容器使用的DNS服务器，默认和宿主一致；
--dns-search example.com: 指定容器DNS搜索域名，默认和宿主一致；
-h "mars": 指定容器的hostname；
-e username="ritchie": 设置环境变量；
--env-file=[]: 从指定文件读入环境变量；
--cpuset="0-2" or --cpuset="0,1,2": 绑定容器到指定CPU运行；
-m :设置容器使用内存最大值；
--net="bridge": 指定容器的网络连接类型，支持 bridge/host/none/container: 四种类型；
--link=[]: 添加链接到另一个容器；
--expose=[]: 开放一个端口或一组端口；
--volume , -v:    绑定一个卷
# 测试启动进入容器
#实例：
使用docker镜像nginx:latest以后台模式启动一个容器,并将容器命名为mynginx。
docker run --name mynginx -d nginx:latest
使用镜像nginx:latest以后台模式启动一个容器,并将容器的80端口映射到主机随机端口。
docker run -P -d nginx:latest
使用镜像 nginx:latest，以后台模式启动一个容器,将容器的 80 端口映射到主机的 80 端口,主机的目录 /data 映射到容器的 /data。
docker run -p 80:80 -v /data:/data -d nginx:latest
绑定容器的 8080 端口，并将其映射到本地主机 127.0.0.1 的 80 端口上。
docker run -p 127.0.0.1:80:8080/tcp ubuntu bash
使用镜像nginx:latest以交互模式启动一个容器,在容器内执行/bin/bash命令。
docker run -it nginx:latest /bin/bash

# 从容器中退回主机
exit

```

##### **列出所有的运行的容器**

```shell
# docker ps 命令
   #列出当前正在运行的容器
-a #列出当前正在运行的容器+带出历史运行过的容器
-n=? #显示最近创建的容器
-q #只显示容器的编号

[root@VM_0_3_centos usr]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
[root@VM_0_3_centos usr]# docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                     PORTS               NAMES
eed6d4efb463        centos              "/bin/bash"         7 minutes ago       Exited (0) 2 minutes ago                       friendly_hawking
8588687cde58        bf756fb1ae65        "/hello"            8 days ago          Exited (0) 8 days ago                          affectionate_visvesvaraya



```

##### ***退出容器***

```shell
exit #直接退出并停止容器
Ctrl+P+Q #容器退出不停止

```

##### **删除容器**

```shell
docker rm 容器id   #删除指定的容器，不能删除正在运行的容器,要强制删除 加 -f
docker rm -f $(docker ps -aq)
docker ps -a -q|xargs docker rm #删除所有的容器
```

##### **启动和停止容器的操作**

```shell
docker start 容器 id   #启动容器
docker restart 容器 id # 重启容器
docker stop 容器 id # 停止当前正在运行的容器
docker kill 容器 id # 强制停止当前容器
```



#### **常用的其它命令**

##### **后台启动容器**

```shell
# 命令 docker run -d 镜像名
# 问题 docker ps 发现centos 停止了

# dockers 容器使用后台运行，就必须要有一个前台进程，dockers发现没有应用，就自动停止

```

##### **查看日志命令**

```shell
docker logs [oprtions] continer name
-f -t #显示时间
docker logs -f -t --tail 10  查看最近的10 条日志

#自己写一段shell 脚本
"while true; do echo xhl;sleep 2;done"
[root@VM_0_3_centos ~]# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
10a3589103ca        centos              "/bin/sh -c 'while t…"   39 seconds ago      Up 38 seconds                           inspiring_boyd
1b7fa0951dbd        centos              "/bin/bash"              6 minutes ago       Up 6 minutes                            xenodochial_mendel
[root@VM_0_3_centos ~]# docker logs -tf --tail 10 10a3589103ca
```

##### **查看容器中进程信息**

```shell
#命令 docker top 容器 id

```

##### **查看镜像元数据**

```shell
# docker  inspect 容器 ID

测试：
[root@VM_0_3_centos ~]# docker inspect 10a3589103ca
[
    {
        "Id": "10a3589103ca6e0acd78c855aae92d467281227d7ad2f4a66f7fbc64595b08fb",
        "Created": "2020-09-26T04:38:31.263331123Z",
        "Path": "/bin/sh",
        "Args": [
            "-c",
            "while true; do echo xhl;sleep 2;done"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 18326,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2020-09-26T04:38:31.592147992Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:0d120b6ccaa8c5e149176798b3501d4dd1885f961922497cd0abef155c869566",
        "ResolvConfPath": "/var/lib/docker/containers/10a3589103ca6e0acd78c855aae92d467281227d7ad2f4a66f7fbc64595b08fb/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/10a3589103ca6e0acd78c855aae92d467281227d7ad2f4a66f7fbc64595b08fb/hostname",
        "HostsPath": "/var/lib/docker/containers/10a3589103ca6e0acd78c855aae92d467281227d7ad2f4a66f7fbc64595b08fb/hosts",
        "LogPath": "/var/lib/docker/containers/10a3589103ca6e0acd78c855aae92d467281227d7ad2f4a66f7fbc64595b08fb/10a3589103ca6e0acd78c855aae92d467281227d7ad2f4a66f7fbc64595b08fb-json.log",
        "Name": "/inspiring_boyd",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {},
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "CapAdd": null,
            "CapDrop": null,
            "Capabilities": null,
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "ConsoleSize": [
                0,
                0
            ],
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "KernelMemory": 0,
            "KernelMemoryTCP": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/3d054e95d4ea8cc918a14b4ff8789be99221e3b0f40dcecedbc299327fbf2c13-init/diff:/var/lib/docker/overlay2/7877dcab536ed88af728ffed1e5efa5b730ed0590bcc181cbcbe1324825762e9/diff",
                "MergedDir": "/var/lib/docker/overlay2/3d054e95d4ea8cc918a14b4ff8789be99221e3b0f40dcecedbc299327fbf2c13/merged",
                "UpperDir": "/var/lib/docker/overlay2/3d054e95d4ea8cc918a14b4ff8789be99221e3b0f40dcecedbc299327fbf2c13/diff",
                "WorkDir": "/var/lib/docker/overlay2/3d054e95d4ea8cc918a14b4ff8789be99221e3b0f40dcecedbc299327fbf2c13/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "10a3589103ca",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/bin/sh",
                "-c",
                "while true; do echo xhl;sleep 2;done"
            ],
            "Image": "centos",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {
                "org.label-schema.build-date": "20200809",
                "org.label-schema.license": "GPLv2",
                "org.label-schema.name": "CentOS Base Image",
                "org.label-schema.schema-version": "1.0",
                "org.label-schema.vendor": "CentOS"
            }
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "3c8a7b3044094833f3b1338d2a64756dbc5cbdca98037da14e1a50a9b9634847",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {},
            "SandboxKey": "/var/run/docker/netns/3c8a7b304409",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "7db5e819e617d1228d79def185dce396679738d07d4b39df3cbd1b95583bb28d",
            "Gateway": "172.18.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.18.0.3",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:12:00:03",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "ee14b283c2e25d9515c0fed44109f4a0647cb9278b5c916c5751a08747193dbb",
                    "EndpointID": "7db5e819e617d1228d79def185dce396679738d07d4b39df3cbd1b95583bb28d",
                    "Gateway": "172.18.0.1",
                    "IPAddress": "172.18.0.3",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:12:00:03",
                    "DriverOpts": null
                }
            }
        }
    }
]

```

##### **进入当前正在运行的容器**

```shell
# 方式 一 
docker exec -it(交互模式) 容器 id  + 目录 
进入容器后开启新的终端，可以在里面操作（常用）

# 方式 二
docker attach 容器  进入的是正在执行的终端，不会启动新的进程

```

##### **从容器内拷贝文件到主机上**

```shell
docker cp 容器 id: 容器内路径  目标主机路径

#举例

[root@VM_0_3_centos /]# docker cp cc271beb7e87:/txt /root
[root@VM_0_3_centos /]# ls

```

#### 小结

![image-20200926183111462](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200926183111462.png)

```shell
Commands:
  attach      Attach localto a running container  			 #当前shell下的attach 连接指定运行镜像
  build       Build an image from a Dockerfile    			 #通过Dockerfile 定制镜像
  commit      Create a new image from a container's changes	 # 提交当前容器未新的镜像
  cp          Copy files/folders between a container and the local filesystem 
  create      Create a new container                         # 创建容器但不启动
  diff        Inspect changes to files or directories on a container's filesystem
  events      Get real time events from the server            #从docker 服务获取容器实时事件
  exec        Run a command in a running container			 # 进入容器执行命令
  export      Export a container's filesystem as a tar archive #导出容器的内容流作为一个tar归档文件
  history     Show the history of an image
  images      List images
  import      Import the contents from a tarball to create a filesystem image
  info        Display system-wide information
  inspect     Return low-level information on Docker objects
  kill        Kill one or more running containers
  load        Load an image from a tar archive or STDIN
  login       Log in to a Docker registry
  logout      Log out from a Docker registry
  logs        Fetch the logs of a container
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  ps          List containers
  pull        Pull an image or a repository from a registry
  push        Push an image or a repository to a registry
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  rmi         Remove one or more images
  run         Run a command in a new container
  save        Save one or more images to a tar archive (streamed to STDOUT by default)
  search      Search the Docker Hub for images
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  version     Show the Docker version information
  wait        Block until one or more containers stop, then print their exit codes

```



##### 练习

> Docker 安装Nginx

```shell
#1、搜索镜像 search 建议大家去docker 送偶所，可以看帮助文档
#2、下载镜像 pull 
#3、运行测试
[root@VM_0_3_centos ~]# docker pull nginx
[root@VM_0_3_centos ~]# docker run -d --name nginx01 -P 3344:80 nginx
[root@VM_0_3_centos ~]# docker ps

# -d 后台运行
# --name 取的容器名称
# -p 宿主机端口：容器内部端口
[root@VM_0_3_centos ~]# curl localhost:3344
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>

# 进入容器
[root@VM_0_3_centos ~]# docker exec -it nginx01 /bin/bash
root@747faee4bf56:/# ls
bin  boot  dev	docker-entrypoint.d  docker-entrypoint.sh  etc	home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@747faee4bf56:/# where nginx
bash: where: command not found
root@747faee4bf56:/# whereis nginx
nginx: /usr/sbin/nginx /usr/lib/nginx /etc/nginx /usr/share/nginx
root@747faee4bf56:/# cd /etc/nginx
root@747faee4bf56:/etc/nginx# ls
conf.d	fastcgi_params	koi-utf  koi-win  mime.types  modules  nginx.conf  scgi_params	uwsgi_params  win-utf
root@747faee4bf56:/etc/nginx# vi conf.d

```

> 作业2 docker来安装一个tomcat

```shell
#官方使用
docker run -it --rm tomcat:9.0  ###用完就删

# 先下载 docker pull tomcat
# 启动运行 docker run -d -p 3355:8080 --name tomcat01 tomcat
```

> 练习3 docker 安装elasticsearch  并通过 -e 配置容器环境

```shell
docker run -d --name elasticsearch01 -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" -e ES_JAVA_OPTS="-Xms64m -Xms512m" elasticsearch:7.6.2

# docker stats + docker id  查看容器状态
```



#### 什么是portainer？

Docker 图形化管理工具！提供一个后台面板供我们操作

```shell
docker run -d -p 8088:9000 \
--restart=always -v /var/run/docker.sock:/var/run/docker.sock --privileged=true portainer/portainer
#界面如下
```

![image-20200928161103341](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200928161103341.png)



### Docker镜像讲解

> 镜像是什么

镜像是一种轻量级、可执行的独立软件包，用来打包软件运行环境和基于运行环境开发的软件，它包含运行某个软件所需的所有内容，包括代码运行时和库环境变量和配置文件

所有应用，直接打包docker 镜像，就可以直接跑起来

> 如何得到镜像

* 从远程仓库下载
* 从某些地方copy
* 自己制作一个DockerFile 



### Docker 镜像加载原理

> UnionFS（联合文件系统）

UnionFS :是一种分层、轻量级并且高性能的文件系统，它支持对文件系统的修改，作为一次提交来一层层的叠加，同时可以将不同目录挂载到同一个虚拟文件系统下，Union 文件系统时Docker 镜像的基础，镜像可以通过分层来进行继承，基于基础镜像，可以制作各种具体的应用镜像

特性：一次同时加载多个文件系统，但从外面看来，智能看到一个文件系统，联合加载会把各层文件系统叠加起来，这样最终的文件系统会包含所有底层的文件和目录

> docker 镜像加载原理

docker 镜像实际是由一层一层的文件系统组成，这种层级文件系统UnionFS

![img](https://cdn.zsite.com/data/upload/d/docker/202009/f_3b5473a75c425ebf3c7e8ab3a78f2260.png)

### docker 镜像

### 容器数据卷

### dockerFile

### docker 网络原理

刚接触Docker的时候，你是否好奇容器之间是怎么通信的呢？今天我们就一起来认识一下Docker的网络吧~

Docker的网络模块是可插拔式的，默认有五种网络模式可以选择。



通过docker network ls这个命令来查看本机中所有的网络模式。



```js
[root@VM_0_14_centos ~]# docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
c79756cf9cde        bridge              bridge              local
204025a5abbc        host                host                local
9b9024f5ac40        macvlan             macvlan             local
6478888548d8        none                null                local
p2e02u1zhn8x        overlay             overlay             swarm
```


下面就让我们来动手实践一下这五种模式吧！

#### Bridge

Bridge模式是Docker的默认网络模式，此模式会为每一个容器设置Network Namespace、IP地址等，在Docker启动时候，就会在主机上创建一个名为docker0的虚拟网桥，在该主机上启动的Docker容器都会连接到这个虚拟网桥上，这样就可以和同一宿主机上桥接模式的其它容器进行通信啦。



```js
#运行一个名为box1的busybox容器，网络模式是bridge
[root@VM_0_14_centos ~]# docker run -itd --name box1 busybox
24d88c0b3af9df06c367e9991c7628a2eaeb54e4f40a5326585fcf1274ea2f8f
[root@VM_0_14_centos ~]# docker exec -it box1 sh
/ # ip addr show eth0
68: eth0@if69: <BROADCAST,MULTICAST,UP,LOWER_UP,M-DOWN> mtu 1500 qdisc noqueue
    link/ether 02:42:ac:12:00:02 brd ff:ff:ff:ff:ff:ff
    inet 172.18.0.2/16 brd 172.18.255.255 scope global eth0
       valid_lft forever preferred_lft forever
#运行一个名为box2的busybox容器，网络模式是bridge       
[root@VM_0_14_centos ~]# docker run -itd --name box2 busybox
f3980be667731ae36aa567910f4a7e80fcc877c33dec59b70f7dc6e49f8fe3f2
[root@VM_0_14_centos ~]# docker exec -it box2 sh
/ # ping 172.18.0.2
PING 172.18.0.2 (172.18.0.2): 56 data bytes
64 bytes from 172.18.0.2: seq=0 ttl=64 time=0.146 ms
64 bytes from 172.18.0.2: seq=1 ttl=64 time=0.120 ms
...
```


从上面的示例可以看出，同一节点下的容器默认都是可以彼此交流哒~

![img](https://www.docker.org.cn/file.php?f=202009/f_0dbf9b2279ae879ce1f5e61a5a295624&t=png&o=&s=&v=1598890808)

#### Host

Host模式下，容器不会设置自己的Network Namespace、IP等，而是和宿主机共用，通过--network host可以将容器直接绑定在Docker主机的网络，没有网络隔离，但是其它方面，比如文件系统、进程列表还是与宿主机隔离的。外界也可以直接访问容器。



```js
#运行一个名为box3的busybox容器，网络模式是host
[root@VM_0_14_centos ~]# docker run -itd --network host --name box3 busybox
```

#### BusyBox

接下来我们来比较一下宿主机和容器box3的网络，不用怀疑，肯定是一样的啦。





```js
[root@VM_0_14_centos ~]# ip addr show eth0
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 52:54:00:26:bb:53 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.14/20 brd 172.17.15.255 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::5054:ff:fe26:bb53/64 scope link
       valid_lft forever preferred_lft forever
[root@VM_0_14_centos ~]# docker exec -it box3 sh
/ # ip addr show eth0
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast qlen 1000
    link/ether 52:54:00:26:bb:53 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.14/20 brd 172.17.15.255 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::5054:ff:fe26:bb53/64 scope link
       valid_lft forever preferred_lft forever
```



#### Macvlan

对于某一些应用程序，比如需要监视网络流量，期望直接连接到物理网络，这种情况下，可以使用Macvlan的网络模式，Docker会为容器的虚拟网络接口分配MAC地址。



创建一个Macvlan网络：



```js
$ docker network create -d macvlan --subnet=172.16.86.0/24 --gateway=172.16.86.1 -o parent=eth0 macvlann
```



启动一个BusyBox容器，网络模式是Macvlan：



```js
[root@VM_0_14_centos ~]# docker run -itd --network macvlan --name box busybox
77436b9c2c1638c498396ff765c27ffec885ff62d892c2064f41497460037156
[root@VM_0_14_centos ~]# docker exec box ip addr show eth0
67: eth0@if2: <BROADCAST,MULTICAST,UP,LOWER_UP,M-DOWN> mtu 1500 qdisc noqueue
    link/ether 02:42:ac:10:56:03 brd ff:ff:ff:ff:ff:ff
    inet 172.16.86.3/24 brd 172.16.86.255 scope global eth0
       valid_lft forever preferred_lft forever
[root@VM_0_14_centos ~]# docker exec box ip route
default via 172.16.86.1 dev eth0
172.16.86.0/24 dev eth0 scope link  src 172.16.86.3
```

#### Overlay

Overlay网络是使用在Swarm集群中，用于连接不同主机上的Docker容器，允许不同宿主机上的容器相互通信。



```js
#通过此命令我们可以创建集群中的manager,在输出信息中会包含一个token
[root@VM_0_14_centos ~]# docker swarm init
```



然后执行以下命令将工作节点加入集群。



```js
$ docker swarm join --token <token> <manager_host>:2377
```



新建一个Overlay网络：



```js
[root@VM_0_14_centos ~]# docker network create --driver=overlay --attachable overlay
#列出docker swarm中所有节点，其中VM_0_14_centos这个节点是leader，其它两个节点是工作节点
[root@VM_0_14_centos ~]# docker node ls
ID                            HOSTNAME                  STATUS              AVAILABILITY        MANAGER STATUS      ENGINE VERSION
sa3m7r6m1lg4iz6dcfvyggr6s *   VM_0_14_centos             Ready               Active              Leader              19.03.11
azpq5fgozz5rd9y4lm11u69wq     VM_0_15_centos             Ready               Active                                  19.03.11
5mbf4l9k0y8zg69il7pk5ztxw     VM_0_16_centos             Ready               Active                                  19.03.7
```



分别在manager节点和work节点上启动一个BusyBox容器，并连接到Overlay网络。



```js
$ docker run -it --network overlay --name box4 sh
```


然后我们在同一个Overlay网络下的容器中互相去ping对方，是可以连接哒~



我们也可以利用Overlay网络去创建一个集群服务，使用Docker Swarm去管理我们的集群服务。现在创建一个五副本的连接到Overlay网络的Nginx服务，暴露端口为80。



```js
$ docker service create --name my-nginx --publish target=80,published=80 --replicas=5 --network overlay nginx
```



利用docker ps命令我们可以发现工作节点上也启动了Nginx应用，这个就是通过Overlay来实现不同主机中容器之间的通信。细心的小伙伴还会发现在任一节点结束一个副本，集群服务就会重启一个新的副本，会一直保持节点内的Nginx副本数量为五个，有木有觉得还蛮有意思的！



```js
[root@VM_0_15_centos ~]# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
1bf24ed438cf        nginx:latest        "/docker-entrypoint.…"   16 minutes ago      Up 16 minutes       80/tcp                 my-nginx.3.lcrhn4eelu1d5z4ln1ss9dczq
```


Overlay网络模型在Docker集群节点间的加入了一层虚拟网络，它有独立的虚拟网段，因此Docker容器发送的内容，会先发送到虚拟子网，再由虚拟子网包装为宿主机的真实网址进行发送。

![img](https://www.docker.org.cn/file.php?f=202009/f_fb0e50b6c320debbf7ee9ccd1dcd63dd&t=png&o=&s=&v=1599032920)

#### None

使用的None模式后，这个容器就是封闭的，不会去参与网络通信，这样就能够保证容器的安全性。



```js
#启动一个名为box3的busybox容器，网络模式是none
[root@VM_0_14_centos ~]# docker run -itd --network none --name box3 busybox
f431bffbd88712f940aee745d7a1e6795f3ef545f79bb2151628f9198c9b1c1e
[root@VM_0_14_centos ~]# docker exec -it box3 sh
/ # ifconfig
lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
```

#### 总结

Docker网络就介绍到这啦，通过上面的实践我们不难发现：

1. 在需要多个Docker容器在同一个宿主机上进行通信，最好就直接使用默认的Bridge模式；
2. 当多个应用程序需要组成集群提供高可用服务时候，Overlay肯定是最佳的选择；
3. Host模式对于优化性能以及在容器需要处理大量端口的情况下很有用，因为它不需要NAT，并且也不会为每个端口创建“ userland-proxy”。当想要容器对网络传输效率有较高要求，就可以选择Host模式，但是要注意端口占用的问题哦~

### Idea 整合docker

### Docker Compose

### Docker Swarm

### CI\CD Jenkins

