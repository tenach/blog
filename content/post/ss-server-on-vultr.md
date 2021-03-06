+++
title = "在 Vultr 上搭建 Shadowsocks 服务端"
date = "2017-06-03"
+++

<center>
<img src="vultr-logo.png" width="50%"/>

Vultr 云平台
</center>

本文介绍如何注册 Vultr 云平台账户、创建 PayPal 账户并绑定银行卡、下单购买 Vultr 主机
并部署 Shadowsocks 服务端。

配置过程步骤较多，如果不想麻烦，可联络我帮忙代购并配置 Vultr 主机，最后打赏一点手工费
就好啦。

依照本文教程进行 Shadowsocks server 配置时，需要具备一定 Linux 控制台使用基础，起码
需要了解 vi 等编辑器的使用和 ssh 的使用。

# 注册 Vultr 帐号
如果已有 Vultr 帐号，可忽略本节，跳到 “[配置支付方式](#setpay)” 。

打开 Vultr 网站 [www.vultr.com][1]。

<center>
<img src="ss-server-vultr-01.png" width="95%"/>

图 1. Vultr 主页
</center>

点击右上角 “Create Account” 创建帐号，填入邮箱和密码。

<center>
<img src="ss-server-vultr-02.png" width="95%"/>

图 2. 创建 Vultr 帐号
</center>

接着进入邮箱，查收确认邮件。

<center>
<img src="ss-server-vultr-03.png" width="95%"/>

图 3. 到邮箱确认注册
</center>

点击邮件中的确认按钮，通过验证并自动登录到 Vultr。

# <span id ="setpay"> 配置支付方式 </span>
在购买 VPS 之前，需要配置付款方式，才能进行支付。

支付方式有 3 种：

* 信用卡
* PayPal
* Bitcoin

如果没有信用卡或不想使用信用卡的话，可选择 PayPal。

Bitcoin 目前似乎还不支持，我也没有比特币，不作介绍。

下面以 PayPal 为例。

## 创建 PayPal 账户

如果已有绑定银行卡的 PayPal 账户，可忽略本节，跳到 “[充值到 Vultr](#pay2vultr)”。

PayPal 账户无需实名认证，可以使用银联的借记卡。

官网：https://www.paypal.com/

注册过程就不细说了，创建一个中国的帐号，姓名和地址不必真实。

## 绑定银行卡
注册 PayPal 后，在 “钱包” -> “信用卡和借记卡” 处选择 “关联卡” ，填入卡号和银行卡关联
的手机号。

<center>
<img src="ss-server-vultr-04.png" width="95%"/>

图 4. 绑定银行卡到 PayPal
</center>

接着会收到一条银联的验证短信，填入验证码，完成绑定。

绑定完成后不需要充值到 PayPal，等付款时会自动充值的。

PayPal 付完款后可以随时解除银行卡关联。如要解除绑定，点击 PayPal 关联的银行卡，然后
点击 “移除卡” 即可。

银联卡需要是下面类型之一的才能绑定成功。

* 中国工商银行、中国建设银行、中国农业银行 、中国银行、交通银行、华夏银行、平安银行、
兴业银行、宁波银行、潍坊银行、哈尔滨银行、珠海农信、尧都农信、武汉市商业银行、
晋城市商业银行、顺德农商银行发行的银联借记卡；
* 中国工商银行、中国银行、交通银行、中信银行、招商银行、广东发展银行、浦东发展银行
发行的银联信用卡。

使用银联卡付款前，请您先在银行开通该卡的网上支付功能。

银联卡只能用以进行在线购物。

# <span id ="pay2vultr"> 充值到 Vultr</span>
在创建 Vultr 主机前，需要先充值一定金额到 Vultr 帐号。这里充值 5 美元。

<center>
<img src="ss-server-vultr-05.png" width="95%"/>

图 5. 用 PayPal 充值到 Vultr 账户
</center>

在支付页面，同意并继续。

<center>
<img src="ss-server-vultr-06.png" width="95%"/>

图 6. 用 PayPal 支付
</center>

接着会再要求登入一次 PayPal 账户并填写验证码，完成付款。

# 创建 Vultr 主机
付款完成后，将自动进入购买主机页面。

<center>
<img src="ss-server-vultr-07.png" width="95%"/>

图 7. 创建主机
</center>

主机配置可参考下表。

<center>
表 1. 主机配置参考
</center>


| 项目 | 值 |
|:--|--:|
|Server Location|Asia / Singapore|
|Server Type|CentOS 7 x64|
|Server Size|25 GB SSD / 1 CPU / 1024MB Memory / 1000GB Bandwidth|
|Additional Features|-|
|Startup Script|-|
|SSH Keys|-|
|Server Hostname & Label|-|

检查配置无误后，点击 “Deploy Now”。

不出意外，将会有一台主机在部署。

<center>
<img src="ss-server-vultr-08.png" width="95%"/>

图 8. 创建中的主机
</center>


# 连接到主机

点击主机右侧 “...” 展开菜单，选择 “Server Details” 可以看到这台主机的一些信息。包括
这台主机的公网地址（IP Address）、登录用户名（Username）和密码（Password）。
记下这三项，后面所说的登录 VPS 要填写的用户名、密码，就是这一套。

<center>
<img src="ss-server-vultr-09.png" width="95%"/>

图 9. 主机详细信息
</center>

如果你用的电脑是 Linux 或 MacOS 系统。则可以直接用 SSH 连接过去。

```sh
ssh root@112.113.114.115
# 输入 yes 接受指纹
# 输入 VPS 主机的密码
```
> 将这里 112.113.114.115 替换为 VPS 主机的公网 IP。

如果你用的电脑是 Windows 系统，并且没有安装 Putty / XShell 这样的工具，那可以用 Vultr
提供的网页控制台。

<center>
<img src="ss-server-vultr-10.png" width="95%"/>

图 10. 打开 Vultr 控制台
</center>

在网页控制台，输入 VPS 的用户名和密码。

<center>
<img src="ss-server-vultr-11.png" width="95%"/>

图 11. Vultr 网页控制台
</center>


> 吐槽一下，这个网页控制台 5 毛水平，连粘贴都不支持。

登录后，会出现命令行界面，比如执行 `free -h` 能够显示内存占用情况。接下来将在这里执行
命令安装 Docker 并启动 Shadowsocks 服务端。

<center>
<img src="ss-server-vultr-12.png" width="95%"/>

图 12. Linux 中连接到 VPS
</center>

> 出于安全考虑，截图中 IP 等信息已被遮盖。

# 配置 Shadowsocks 服务端

和别的教程不一样的是，这里配置服务端，无需下载和运行脚本，也无需修改什么配置文件。只需要
下面两步，就能启动 Shadowsocks 服务端。

# 安装 Docker

[Docker][2] 是一种通用的用于打包、发布、运行应用程序的容器引擎，更多介绍可
查阅 《[What is Docker?][3]》。

在线下载 Docker 安装脚本并执行。
```sh
curl https://get.docker.com/ | sh
```

出现下面信息，说明已经安装完成。执行 `docker version` 可查看版本信息。

<center>
<img src="ss-server-vultr-13.png" width="95%"/>

图 13. 在 VPS 中安装 Docker
</center>

启用 Docker daemon 进程，并加入开机启动项。

```sh
systemctl start docker && systemctl enable docker
```


# 启动 ssserver
如果想要启动一个 ssserver（即 Shadowsocks server），可以直接运行下面命令。

```sh
docker run -d --restart=always \
    -p 8388:8388 fanach/ssserver -p 8388 -k abc123
```

这样，在后台将会有一个 ssserver 的容器在运行。执行 `docker ps` 查看。

<center>
<img src="ss-server-vultr-14.png" width="95%"/>

图 14. 启动 Shadowsocks 容器
</center>

接着，可以通过服务器地址、端口 `8388`、密码 `abc123` 以及默认加密方式 `aes-256-cfb`
去连接了，跳到 “[客户端连接与验证](#clientcfg)”。

> 这里端口、密码和加密方式可以自己设置。

## 命令解释

```sh
docker run -d --restart=always \
    -p 8388:8388 fanach/ssserver -p 8388 -k abc123
```

上面那条 `docker run` 命令执行后，将会做下面事情。

1. 下载 fanach/ssserver 这个镜像；
2. 根据给的端口、密码等参数，在后台运行一个 ssserver 容器。

这里 `-d` 是指在后台运行。

 `--restart=always` 是指在容器发生异常退出时自动重新启动。

`-p 8388:8388`， 前一个 8388 是称为主机端口，后一个 8388 是称为容器端口。

最后面还有个 `-p 8388` 是容器中 ssserver 程序的参数，即容器中 ssserver 监听的端口
为 8388。容器端口和 ssserver 监听端口必须相同。

`-k abc123` 为密码。

如果要设定加密方式，可用 `-m` 参数，如 `-m chacha20`。

所有支持的加密方式如下

* aes-128-cfb
* aes-192-cfb
* aes-256-cfb
* aes-128-ctr
* aes-192-ctr
* aes-256-ctr
* des-cfb
* bf-cfb
* cast5-cfb
* rc4-md5
* chacha20
* chacha20-ietf
* salsa20

各种加密方式的区别，需要自己查阅了。

如果需要再启动一个 ssserver ，换一个主机端口，如 `8399`，再运行一次命令即可。

```sh
docker run -d --restart=always \
    -p 8399:8388 fanach/ssserver -p 8388 -k abc456
```

> 如果对镜像 fanach/ssserver 有兴趣，可到点击 [这里][ssserver-image] 到 DockerHub 查看。
Dockerfile 开源于 [fanach/dockerfile-ssserver][ssserver-github]。

## 状态查询
### 基本信息
执行 `docker ps -a` 可查询所有容器（包括已退出的）的简要信息。第一列为容器 ID。

<center>
<img src="ss-server-vultr-15.png" width="95%"/>

图 15. Docker 容器
</center>

### 日志查询
执行 `docker logs -f` 并跟上容器 ID 查询服务端日志。
```sh
[root@vultr ~]# docker logs -f aaa89aea2169
2017/06/03 12:21:34 server listening port 8388 ...
2017/06/03 12:48:42 creating cipher for port: 8388
```

### 流量查询
执行 `docker stats` 并跟上容器 ID 查询容器资源使用情况。

<center>
<img src="ss-server-vultr-16.png" width="95%"/>

图 16. 查看容器资源用量
</center>

其中 `NET I/O` 分别为这个 ssserver 容器输入和输出的流量。

> 如果想要查看整个 VPS 流量使用情况，到 Vultr 主机详细信息页面查看。

# <span id ="clientcfg"> 客户端连接与验证 </span>

Android 用户见： 《[Android 上使用 Shadowsocks 教程][ss-android]》

iPhone / iPad 用户见： 《[iPhone/iPad 上使用 Shadowsocks 教程][ss-ios]》

Windows 用户见： 《[Windows 上使用 Shadowsocks 教程][ss-windows]》

MacBook 用户见： 《[Macbook 上使用 Shadowsocks 教程][ss-macos]》

Linux 用户见： 《[Linux 上使用 Shadowsocks 教程][ss-linux]》

# 其他一些过程记录（拓展部分）

## 修改密码
如果觉得 Vultr 自动生成的密码太长太复杂不好记。可以修改登录密码。

SSH 进入主机控制台，并运行命令：
```sh
$ passwd root
Changing password for root.
Current password: （输入原密码）
New password: （输入新密码）
Retype new password: （再次输入新密码）
```

> 修改后的密码自己要牢记，如果遗忘，Vultr 似乎没有办法重置，只能重装 VPS 系统了。

## 安全配置
尽管修改了密码，使用用户名、密码方式登录主机也并不安全。尤其是在修改密码后，设置了简单
的密码，那更危险了。我第二天登录时，发现有 4000 多次登录失败。假如密码被试对了，那骇客
就可以对这台主机做任何操作了。
```
Last failed login: Sun Jun  4 15:06:48 UTC 2017 from 61.177.172.56 on ssh:notty
There were 4728 failed login attempts since the last successful login.
```

一个好的方法是禁用密码登录，而是只使用密钥登录。这里密钥是指用
OpenSSL 工具生成的非对称密钥对。

** 为了安全，推荐禁止密码登录，只允许使用私钥登录。**

### 添加公钥
生成密钥对，添加公钥到受信任的密钥中，并保留私钥。
```sh
$ ssh-keygen
（一路回车，将在 ~/.ssh/ 下生成 id_rsa 和 id_rsa.pub 两个文件，分别为私钥和公钥。）

$ cat .ssh/id_rsa.pub >> .ssh/authorized_keys
```

复制私钥并妥善保存到自己的电脑上。

### 禁止通过密码登录
```sh
$ vi /etc/ssh/sshd_config
# 查找并修改下面两项
PasswordAuthentication no // 禁止使用基于口令认证的方式登陆
PubkeyAuthentication yes // 允许使用基于密钥认证的方式登陆
```

在执行下面命令之前，确保私钥已经保存到自己的电脑（自己的 Windows / Linux / MacOS 电脑，
而不是 VPS），否则重启 sshd 服务后，将无法通过密码再连接到 VPS，而只能用私钥连接。

```
$ systemctl restart sshd
# 重启 sshd 服务
```

假如保存下来的私钥文件名为 `id_rsa.vultr`，那后面要通过 SSH 连接 VPS 时，执行下面命令
即可。

```sh
$ ssh -i id_rsa.vultr root@112.113.114.115
```

> 将 `112.113.114.115` 替换为你的 VPS 公网 IP。

> Windows 用户可下载并学习 XShell 的使用，XShell 实现了 SSH 具有图形化配置界面。

## 创建 SWAP
为了防止内存溢出导致主机重启，可创建一个 2048M 的 SWAP 文件 /swapfile 。
```sh
$ dd if=/dev/zero of=/swapfile bs=1024k count=2048
$ chmod 600 /swapfile
$ mkswap /swapfile
$ swapon /swapfile
```

# Tips
* 如果不是用 root 用户，需要在部分命令之前加上 `sudo`。

# 修改历史
* 2017.08.05 使用 Vultr Affiliate 链接
* 2017.06.17 修复 go 版 ssserver 对安卓不兼容问题（默认镜像改为 fanach/ssserver ）。
* 2017.06.08 添加 swap 说明。
* 2017.06.04 添加拓展部分：安全配置。

[1]: http://www.vultr.com/?ref=7182454
[2]: https://www.docker.com
[3]: https://www.docker.com/what-docker
[ssserver-image]: https://hub.docker.com/r/fanach/ssserver/
[ssserver-github]: https://github.com/fanach/dockerfile-ssserver
[ss-android]: https://fanach.github.io/post/ss-android/
[ss-ios]: https://fanach.github.io/post/ss-ios/
[ss-windows]: https://fanach.github.io/post/ss-windows/
[ss-macos]: https://fanach.github.io/post/ss-macos/
[ss-linux]: https://fanach.github.io/post/ss-linux/
