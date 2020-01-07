---
title: Linux升级SSH
categories: Linux
---
>由于在工作中项目涉及服务器SSH版本过低，无法通过安全漏洞扫描，需要升级SSH版本至7.4以上；但因涉及到卸载SSH服务等操作，在网上参考一些教程，依然踩了一些坑。现在将详细的升级过程记录下来，供各位技术人员参考。

#### 查看现版本信息
> 环境：Centos7.2
SSH版本：openSSH 6.6
##### 查看SSH版本 
```vim
#ssh -V
```

##### 查看SSL版本 
```vim
#openssl version
```

##### 查看zlib版本
```vim
#rpm -qa|grep zlib
```

> 需要openSSL在1.01以上以及zlib在1.2.5以上才能升级SSH

##### 升级openSSL&&zlib
openSSL升级为1.01以上以及zlib升级为1.2.5以上。升级过程略。

<!--more-->
##### 下载openssh-7.4
在openssh官网下载openssh-7.4p1.tar.gz包放置到服务器的usr/src目录下

<a href="https://cloudflare.cdn.openbsd.org/pub/OpenBSD/OpenSSH/portable/">官网下载地址</a>

#### 安装并开启telnet服务
openssh升级过程中需要卸载旧版本openssh，为了保证主机不失联，需要开启telnet连接通道。
##### 查看telnet服务
```vim
#rpm -q telnet-server 
```
查看telnet-server是否已安装，若没有安装则进行如下操作。
```vim
# yum install telnet-server 安装telnet的服务器
# yum list|grep xinetd 安装xinetd服务
# yum install xinetd.x86_64 将xinetd 服务安装到系统中
#rpm -qa | grep telnet  安装后的检查
#rpm -qa | grep xinetd
```
##### 关闭防火墙
防止telnet可能无法连接。
```vim
# service iptables stop
# chkconfig iptables off
```
##### 启动telnet服务
telnet服务之后,默认是不开启服务,修改文件/etc/xinetd.d/telnet。
```vim
# vim /etc/xinetd.d/telnet
```
下面内容复制进去
```vim
## # unencrypted username/password pairs for authentication.
## service telnet
service telnet
{
flags = REUSE
socket_type = stream
wait = no
user = root
server =/usr/sbin/in.telnetd
log_on_failure += USERID
disable = no
}
disable值变更： （yes ----> no）

修改完成之后点击Esc键即可进入命令提示行开始进行保存操作，最下面的INSERT消失之后就可以输入：wq进行保存操作了
```
##### 启动telnet服务
```vim
# systemctl enable xinetd.service //开机启动
# systemctl enable telnet.socket //开机启动
# systemctl start xinetd.service
# systemctl start telnet.socket
```
##### 查看启动
```vim
#ps -ef | grep xinetd
```
##### telnet登录验证
```vim
# telnet 127.0.0.1
```
#### 停止SSH服务
```vim
#systemctl stop sshd.service
```
#### 卸载老版本的SSH
##### 查询老版本的SSH
```vim
# rpm -qa |grep openssh
# openssh-server-6.6.1p1-22.el7.x86_64
# openssh-clients-6.6.1p1-22.el7.x86_64
# openssh-6.6.1p1-22.el7.x86_64
```
##### 卸载老版本的SSH
```vim
# yum remove eopenssh-server-6.6.1p1-22.el7.x86_64
# yum remove eopenssh-clients-6.6.1p1-22.el7.x86_64
# yum remove openssh-6.6.1p1-22.el7.x86_64
```
#### 安装新版本的openSSH
##### 备份原有SSH目录
```vim
# mv /etc/ssh/ /etc/ssh.bak/
```
##### 编译openSSH
```vim
# cd /usr/src
# tar -xvzf openssh-7.4p1.tar.gz
# cd openssh-7.4p1/
#./configure --prefix=/usr/local --sysconfdir=/etc/ssh
```
遇到问题 lib.h missing  
```vim
#yum install zlib-devel
```
继续运行
```vim
#./configure --prefix=/usr/local --sysconfdir=/etc/ssh
```
遇到问题 openssl header missing
```vim
#yum install openSSl-devel
```
继续运行
```vim
#./configure --prefix=/usr/local --sysconfdir=/etc/ssh
```
运行
```vim
# make
# make install
```
##### 配置sshd服务
复制启动文件到/etc/init.d/下并命名为sshd：
```vim
# cp contrib/redhat/sshd.init /etc/init.d/sshd
#sed -i 's/\/usr\/sbin\/sshd/\/usr\/local\/sbin\/sshd/g' /etc/init.d/sshd
#/etc/init.d/sshd restart
#mv /usr/bin/ssh /usr/bin/ssh_bak
#mv /usr/local/bin/ssh /usr/bin/ssh
```
##### 设置root账户权限
openssh7.4默认root用户是不能用ssh远程登录的，需要修改配置文件
```vim
# vi /etc/ssh/sshd_config
```
输入I为insert模式 找到#PermitRootLogin prohibit-password项，去掉注释并把prohibit-password改为yes
PermitRootLogin yes

##### 启动openSSH
```vim
#/bin/systemctl restart sshd.service
# service sshd restart
```
遇到如下问题
```vim
Restarting sshd (via systemctl): Job for sshd.service failed because the contro
l process exited with error code. See "systemctl status sshd.service" and "journ
alctl -xe" for details.
FAILED]
```
```vim
修改sshd配置文件：
vim /etc/init.d/sshd
SSHD=/usr/sbin/sshd 为 SSHD=/usr/local/sbin/sshd
```
##### 验证openSSH版本
```vim
# ssh -V
```
#### 卸载telnet
##### SSH登录
使用root用户，通过SSH协议登录服务器

##### 停止telnet服务
```vim
# systemctl stop telnet.socket
# systemctl stop xinetd
```
##### 卸载telnet
```vim
# rpm -e telnet-server.x86_64
# rpm -e telnet.x86_64
# rpm -e xinetd.x86_64
```
