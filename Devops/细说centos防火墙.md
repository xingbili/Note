## [细说firewalld和iptables](https://www.cnblogs.com/grimm/p/10345693.html)

在RHEL7里有几种防火墙共存：firewalld、iptables、ebtables，默认是使用firewalld来管理netfilter子系统，不过底层调用的命令仍然是iptables等。

##### firewalld跟iptables比起来至少有两大好处：

**1**、firewalld可以动态修改单条规则，而不需要像iptables那样，在修改了规则后必须得全部刷新才可以生效；

**2**、firewalld在使用上要比iptables人性化很多，即使不明白“五张表五条链”而且对TCP/IP协议也不理解也可以实现大部分功能。

 

firewalld跟iptables比起来，不好的地方是每个服务都需要去设置才能放行，因为默认是拒绝。而iptables里默认是每个服务是允许，需要拒绝的才去限制。

 

firewalld自身并不具备防火墙的功能，而是和iptables一样需要通过内核的netfilter来实现，也就是说firewalld和 iptables一样，他们的作用都是用于维护规则，而真正使用规则干活的是内核的netfilter，只不过firewalld和iptables的结构以及使用方法不一样罢了。

 

#### 一个重要的概念：区域管理

通过将网络划分成不同的区域，制定出不同区域之间的访问控制策略来控制不同程序区域间传送的数据流。例如，互联网是不可信任的区域，而内部网络是高度信任的区域。网络安全模型可以在安装，初次启动和首次建立网络连接时选择初始化。该模型描述了主机所连接的整个网络环境的可信级别，并定义了新连接的处理方式。有如下几种不同的初始化区域：

阻塞区域（block）：任何传入的网络数据包都将被阻止。

工作区域（work）：相信网络上的其他计算机，不会损害你的计算机。

家庭区域（home）：相信网络上的其他计算机，不会损害你的计算机。

公共区域（public）：不相信网络上的任何计算机，只有选择接受传入的网络连接。

隔离区域（DMZ）：隔离区域也称为非军事区域，内外网络之间增加的一层网络，起到缓冲作用。对于隔离区域，只有选择接受传入的网络连接。

信任区域（trusted）：所有的网络连接都可以接受。

丢弃区域（drop）：任何传入的网络连接都被拒绝。

内部区域（internal）：信任网络上的其他计算机，不会损害你的计算机。只有选择接受传入的网络连接。

外部区域（external）：不相信网络上的其他计算机，不会损害你的计算机。只有选择接受传入的网络连接。

注：FirewallD的默认区域是public。

firewalld默认提供了九个zone配置文件：block.xml、dmz.xml、drop.xml、external.xml、 home.xml、internal.xml、public.xml、trusted.xml、work.xml，他们都保存在“/usr/lib /firewalld/zones/”目录下。

 

## 配置方法

firewalld的配置方法主要有三种：firewall-config、firewall-cmd和直接编辑xml文件，其中 firewall-config是图形化工具，firewall-cmd是命令行工具，而对于linux来说大家应该更习惯使用命令行方式的操作，所以 firewall-config我们就不给大家介绍了。

### 安装配置：

 

1、安装firewalld

root执行 **# yum install firewalld firewall-config**

 

2、运行、停止、禁用firewalld

启动：**# systemctl start  firewalld**

查看状态：**# systemctl status firewalld** 或者 **firewall-cmd --state**

停止：**# systemctl disable firewalld**

禁用：**# systemctl stop firewalld**

**systemctl mask firewalld**

**systemctl unmask firewalld**

 

4、配置firewalld

查看版本：**$ firewall-cmd --version**

查看帮助：**$ firewall-cmd --help**

查看设置：

显示状态：**$ firewall-cmd --state**

查看区域信息: **$ firewall-cmd --get-active-zones**

查看指定接口所属区域：**$ firewall-cmd --get-zone-of-interface=eth0**

拒绝所有包：**# firewall-cmd --panic-on**

取消拒绝状态：**# firewall-cmd --panic-off**

查看是否拒绝：**$ firewall-cmd --query-panic**

 

更新防火墙规则：**# firewall-cmd --reload**

​     **# firewall-cmd --complete-reload**

  两者的区别就是第一个无需断开连接，就是firewalld特性之一动态添加规则，第二个需要断开连接，类似重启服务

 

将接口添加到区域，默认接口都在public

**# firewall-cmd --zone=public --add-interface=eth0**

永久生效再加上 **--permanent** 然后reload防火墙

 

设置默认接口区域

**# firewall-cmd --set-default-zone=public**

立即生效无需重启

 

打开端口（貌似这个才最常用）

查看所有打开的端口：

**# firewall-cmd --zone=dmz --list-ports**

加入一个端口到区域：

**# firewall-cmd --zone=dmz --add-port=8080/tcp**

若要永久生效方法同上

 

打开一个服务，类似于将端口可视化，服务需要在配置文件中添加，/etc/firewalld 目录下有services文件夹，这个不详细说了，详情参考文档

**# firewall-cmd --zone=work --add-service=smtp**

 

移除服务

**# firewall-cmd --zone=work --remove-service=smtp**

 

还有端口转发功能、自定义复杂规则功能、lockdown

 

 

iptables 是与最新的 3.5 版本 Linux 内核集成的 IP 信息包过滤系统。如果 Linux 系统连接到因特网或 LAN、服务器或连接 LAN 和因特网的代理服务器， 则该系统有利于在 Linux 系统上更好地控制 IP 信息包过滤和防火墙配置。

 

iptables 基本命令使用举例

一、链及NAT的基本操作
1、清除所有的规则。
1）清除预设表filter中所有规则链中的规则。
\# iptables -F
2）清除预设表filter中使用者自定链中的规则。
\#iptables -X

\#iptables -Z

3)清楚NAT表规则

\#iptables -F -t nat

4)NAT表的显示

\#iptables -t nat -nL

 

2、设置链的默认策略。一般有两种方法。
1）首先允许所有的包，然后再禁止有危险的包通过放火墙。
\#iptables -P INPUT ACCEPT
\#iptables -P OUTPUT ACCEPT
\#iptables -P FORWARD ACCEPT
2）首先禁止所有的包，然后根据需要的服务允许特定的包通过防火墙。
\#iptables -P INPUT DROP
\#iptables -P OUTPUT DROP
\#iptables -P FORWARD DROP
3、列出表/链中的所有规则。默认只列出filter表。
\#iptables -L
4、向链中添加规则。下面的语句用于开放网络接口：
\#iptables -A INPUT -i lo -j ACCEPT
\#iptables -A OUTPUT -o lo -j ACCEPT
\#iptables -A INPUT -i eth0 -j ACEPT
\#iptables -A OUTPUT -o eth1 -j ACCEPT
\#iptables -A FORWARD -i eth1 -j ACCEPT
\#iptables -A FORWARD -0 eth1 -j ACCEPT
注意:由于本地进程不会经过FORWARD链，因此回环接口lo只在INPUT和OUTPUT两个链上作用。
5、使用者自定义链。
\#iptables -N custom
\#iptables -A custom -s 0/0 -d 0/0 -p icmp -j DROP
\#iptables -A INPUT -s 0/0 -d 0/0 -j DROP
二、设置基本的规则匹配
1、指定协议匹配。
1）匹配指定协议。
\#iptables -A INPUT -p tcp
2）匹配指定协议之外的所有协议。
\#iptables -A INPUT -p !tcp
2、指定地址匹配。
1）指定匹配的主机。
\#iptables -A INPUT -s 192.168.0.18
2）指定匹配的网络。
\#iptables -A INPUT -s 192.168.2.0/24
3）匹配指定主机之外的地址。
\#iptables -A FORWARD -s !192.168.0.19
4）匹配指定网络之外的网络。
\#iptables -A FORWARD -s ! 192.168.3.0/24
3、指定网络接口匹配。
1）指定单一的网络接口匹配。
\#iptables -A INPUT -i eth0
\#iptables -A FORWARD -o eth0
2）指定同类型的网络接口匹配。
\#iptables -A FORWARD -o ppp+
4、指定端口匹配。
1）指定单一端口匹配。
\#iptables -A INPUT -p tcp --sport www
\#iptables -A INPUT -p udp –dport 53
2）匹配指定端口之外的端口。
\#iptables -A INPUT -p tcp –dport !22
3）匹配端口范围。
\#iptables -A INPUT -p tcp –sport 22:80
4）匹配ICMP端口和ICMP类型。
\#iptables -A INOUT -p icmp –icimp-type 8
5）指定ip碎片。
每
个网络接口都有一个MTU（最大传输单元），这个参数定义了可以通过的数据包的最大尺寸。如果一个数据包大于这个参数值时，系统会将其划分成更小的数据包
（称为ip碎片）来传输，而接受方则对这些ip碎片再进行重组以还原整个包。这样会导致一个问题：当系统将大数据包划分成ip碎片传输时，第一个碎片含有
完整的包头信息（IP+TCP、UDP和ICMP），但是后续的碎片只有包头的部分信息（如源地址、目的地址）。因此，检查后面的ip碎片的头部（象有
TCP、UDP和ICMP一样）是不可能的。假如有这样的一条规则：
\#iptables -A FORWARD -p tcp -s 192.168.1.0/24 -d 192.168.2.100 –dport 80 -j ACCEPT
并且这时的FORWARD的policy为DROP时，系统只会让第一个ip碎片通过，而余下的碎片因为包头信息不完整而无法通过。可以通过—fragment/-f 选项来指定第二个及以后的ip碎片解决上述问题。
\#iptables -A FORWARD -f -s 192.168.1.0/24 -d 192.168.2.100 -j ACCEPT
注意现在有许多进行ip碎片攻击的实例，如DoS攻击，因此允许ip碎片通过是有安全隐患的，对于这一点可以采用iptables的匹配扩展来进行限制。
三、设置扩展的规则匹配（举例已忽略目标动作）
1、多端口匹配。
1）匹配多个源端口。
\#iptables -A INPUT -p tcp -m multiport –sport 22,53,80,110
2）匹配多个目的端口。
\#iptables -A INPUT -p tcp -m multiport –dpoort 22,53,80
3）匹配多端口(无论是源端口还是目的端口）
\#iptables -A INPUT -p tcp -m multiport –port 22,53,80,110
2、指定TCP匹配扩展
使用 –tcp-flags 选项可以根据tcp包的标志位进行过滤。
\#iptables -A INPUT -p tcp –tcp-flags SYN,FIN,ACK SYN
\#iptables -A FROWARD -p tcp –tcp-flags ALL SYN,ACK
上实例中第一个表示SYN、ACK、FIN的标志都检查，但是只有SYN匹配。第二个表示ALL（SYN，ACK，FIN，RST，URG，PSH）的标志都检查，但是只有设置了SYN和ACK的匹配。
\#iptables -A FORWARD -p tcp --syn
选项—syn相当于”--tcp-flags SYN,RST,ACK SYN”的简写。
3、limit速率匹配扩展。
1）指定单位时间内允许通过的数据包个数，单位时间可以是/second、/minute、/hour、/day或使用第一个子母。
\#iptables -A INPUT -m limit --limit 300/hour
2 )指定触发事件的阀值。
\#iptables -A INPUT -m limit –limit-burst 10 
用来比对一次同时涌入的封包是否超过10个，超过此上限的包将直接丢弃。
3）同时指定速率限制和触发阀值。
\#iptables -A INPUT -p icmp -m limit –-limit 3/m –limit-burst 3
表示每分钟允许的最大包数量为限制速率（本例为3）加上当前的触发阀值burst数。任何情况下，都可保证3个数据包通过，触发阀值burst相当于允许额外的包数量。 
4）基于状态的匹配扩展（连接跟踪）
每个网络连接包括以下信息：源地址、目标地址、源端口、目的端口，称为套接字对（socket pairs）；协议类型、连接状态（TCP协议）
和超时时间等。防火墙把这些信息称为状态（stateful）。状态包过滤防火墙能在内存中维护一个跟踪状态的表，比简单包过滤防火墙具有更大的安全性，命令格式如下： 
iptables -m state –-state [!]state [,state,state,state]
其中，state表是一个逗号分割的列表，用来指定连接状态，4种：
\>NEW: 该包想要开始一个新的连接（重新连接或连接重定向）
\>RELATED:该包是属于某个已经建立的连接所建立的新连接。举例：
FTP的数据传输连接和控制连接之间就是RELATED关系。
\>ESTABLISHED：该包属于某个已经建立的连接。
\>INVALID:该包不匹配于任何连接，通常这些包被DROP。
例如：
（1）在INPUT链添加一条规则，匹配已经建立的连接或由已经建立的连接所建立的新连接。即匹配所有的TCP回应包。
\#iptables -A INPUT -m state –state RELATED,ESTABLISHED
（2）在INPUT链链添加一条规则，匹配所有从非eth0接口来的连接请求包。
\#iptables -A INPUT -m state -–state NEW -i !eth0
又如，对于ftp连接可以使用下面的连接跟踪：
（1）被动（Passive）ftp连接模式。
\#iptables -A INPUT -p tcp --sport 1024: --dport 1024: -m state –-state ESTABLISHED -j ACCEPT
\#iptables -A OUTPUT -p tcp --sport 1024: --dport 1024: -m 
state -–state ESTABLISHED,RELATED -j ACCEPT
（2）主动（Active）ftp连接模式
\#iptables -A INNPUT -p tcp --sport 20 -m state –-state ESTABLISHED,RELATED -j ACCEPT
\#iptables -A OUTPUT -p tcp –OUTPUT -p tcp –dport 20 -m state --state ESTABLISHED -j ACCEPT