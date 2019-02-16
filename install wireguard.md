# 安装 wireguard 教程
Author: liming    Create: Thu Tue Jan 22 2019

> 参考资料：   
> 1. [wireguard官网](https://www.wireguard.com/)   
> 2. [安装 Google BBR 教程](https://www.vultr.com/docs/how-to-deploy-google-bbr-on-centos-7) (注：linux kernel>3.10 可忽略升级内核部分，直接安装 Google BBR)

1. 检查系统内核
```sh
$ uname -r
```
Linux kernel <= 3.10 时需要先升级内核。[参考文章](https://blog.csdn.net/kikajack/article/details/79396793)

**以下内容请在 `root` 用户下进行！**
--------------------------------------------------------------- 
2. 安装 wireguard
```sh
#  Ubuntu
$ sudo add-apt-repository ppa:wireguard/wireguard
$ sudo apt-get update
$ sudo apt-get install wireguard

# Red Hat Enterprise Linux / CentOS
$ sudo curl -Lo /etc/yum.repos.d/wireguard.repo https://copr.fedorainfracloud.org/coprs/jdoss/wireguard/repo/epel-7/jdoss-wireguard-epel-7.repo
$ sudo yum install epel-release
$ sudo yum install wireguard-dkms wireguard-tools
```

3. 在 `/etc` 目录下新建一个 `wireguard` 文件夹
```sh
$ sudo mkdir /etc/wireguard
```

4. 在 `/etc/wireguard` 文件夹内新建密钥和配置文件 `wg0.conf`
```sh
$ cd /etc/wireguard
$ umask 077

# 生成密钥
$ wg genkey | tee privatekey | wg pubkey > publickey

# 新建配置文件
$ touch wg0.conf
```

```sh
# 服务器端配置文件示例
[Interface]
# Address为该tunnel内分配给该节点的地址，用本地地址
Address = 192.168.11.1/24
# SaveConfig = true 表示 wg0 停止后，保存之前的流量数据
SaveConfig = true
# 该步特别注意 eth0,这是网卡的名字，要根据自己的实际情况填写，可用 ifconfig 命令查看本机的网络情况
PostUp = iptables -A FORWARD -i wg0 -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
PostDown = iptables -D FORWARD -i wg0 -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE
# ListenPort 为监听端口号，可随意设置
ListenPort = 51820
# PrivateKey 为私钥，在生产密钥是系统自动生成
PrivateKey = kAy9vEvWKePzd/muRwQ0RiYY2jTzOfSYVK8DW+5cLns=

# [Peer] 为一个节点，可多个
[Peer]
# PublicKey 为该 peer 的公钥
PublicKey = 7uwF0Xcft1+NYEHZqHBf4vsn4sYsiKFdXKgKEb7bVhs=
# AllowedIPs 为该 Peer 分配的IP，IPv4固定写 /32，表示一个唯一的IP
AllowedIPs = 192.168.12.1/32
```

```sh
# 客户端配置文件
[Interface]
# 客户端的私钥
PrivateKey = 2Nrxh43TqguAvvTaVyHaruBgUMEl570+P0A47WknQ1U=
# 设置DNS
DNS = 8.8.8.8 
# 该节点分配的tunnel内地址，
Address = 192.168.12.1/24

# 服务器端信息
[Peer]
# 服务器端的公钥
PublicKey = j49mp2kJUXWuYY5YjcfTAz+ncKcMD9joMSgXTXp96ks=
# 客户端全写 0.0.0.0/0
AllowedIPs = 0.0.0.0/0
# Endpoint 为服务器端的公网地址，可用写 IP，也可用域名
Endpoint = your ip address or domain:51820
# Send periodic keepalives to ensure connection stays up behind NAT
PersistentKeepalive = 25
```

5. 服务器端设置转发
```sh
$ vim /etc/sysctl.conf
net.ipv4.ip_forward=1

# 执行并生效
$ sysctl -p
```

6. 启动 wireguard
```sh
# 在 /etc/wireguard 内执行
$ wg-quick up wg0
```

7. 查看 wireguard 状态
```sh
$ wg
or
$ wg show
```

8. 关闭 wireguard
```sh
$ wg-quick down wg0
```

9. wireguard 客户端  
 Windows : [tunsafe](https://www.tunsafe.com)   
 Android : [wireguard](https://play.google.com/store/apps/details?id=com.wireguard.android)   
 ios : [wireguard](https://itunes.apple.com/us/app/wireguard/id1441195209?ls=1&mt=8)  
