# 快速搭建个人VPN科学上网教程

## 搭建自己的VPN
有时候我们需要通过 Google 查询官方文档或学术资料，但市面上的VPN工具往往不稳定且存在安全隐患。更好的选择是自己搭建一个VPN服务，这样可以完全掌控连接的安全性和稳定性。

但是纵然搭建自己的个人VPN确实很方便，但是对于没有开发经验的朋友，后期会遇到各种各样的问题，首先搭建整个环境就是一个很棘手的问题，因为毕竟要涉及到服务器的部署和运维等等，如果中途又遇到什么问题真的就是丈二的和尚摸不着头脑了。因此，对于没有开发经验，但是又需要**稳定和干净IP**的朋友，其实还有一条一劳永逸的路子，那就是使用可靠稳定的第三方的类似服务。

[Just My Socks](https://justmysocks.net/members/aff.php?aff=32405)就是一个很不错的选择，价格上比起自己搭建VPS服务差不多，而且不用自己去解决各种各样的疑难问题。[Just My Socks](https://justmysocks.net/members/aff.php?aff=32405)从2018年做到现在也是一个在圈子里很出名的产品，所以稳定可靠性都信得过，价格上面也丰俭由人，最便宜的只需要每个月5.88美金，也就是差不多30多块钱，所以还是很值得尝试的。

## 购买性价比超高的云服务器[vultr](https://www.vultr.com/?ref=9658005)
如果想要要快速搭建个人VPN进行科学上网，首先选择一个可靠的云服务器平台，如[Vultr](https://www.vultr.com/?ref=9658005)，并注册一个账户。[vultr](https://www.vultr.com/?ref=9658005)在国外的知名度和国内的阿里云接近，因此在产品力上还是很有保障。

值得一提的是，[Vultr](https://www.vultr.com/?ref=9658005) 对新用户的福利相当诱人。只需充值 10 美元，就可以获得 100 美元的赠送额度。你可以通过[专属链接注册](https://www.vultr.com/?ref=9658005)，抢先享受这个优惠。

![image](https://github.com/user-attachments/assets/debb38ad-51a2-411d-bc1a-d1a7a7a10350)

注册的流程不赘述，使用邮箱和密码就可以注册了。

进入后，你会看到一个页面，表明你已经成功通过 [Vultr的专属优惠链接](https://www.vultr.com/?ref=9658005)，获得了100美元的赠送额度，这个额度是有有效期的，也就是说需要在30天内免费使用这部分额度去体验产品，这么算下来能薅到的羊毛还是非常大的。现在你只需要选择支付宝充值或者其他方式充值10美元以上，就可以获得额外赠送的这100美元。

![image](https://github.com/user-attachments/assets/d319f546-8111-4002-bdf4-326309e3e608)

接下来你可以在该平台上选择云服务器。点击页面左侧菜单栏中的「Products」，进入服务器选择页面，进行购买操作。
服务器的类型选择 Cloud Compute

![image](https://github.com/user-attachments/assets/0c3f326d-aa04-4a7b-8312-5060ce857ceb)

Server Location 即服务器的位置，可以任意选择，或者根据自己的实际需要来进行选择，比如你的业务在北美，就选择美国的服务器

![image](https://github.com/user-attachments/assets/fb789152-5064-4b21-a1ac-92d5bc108450)

Server Type服务器系统的类型，选择CentOS 8 x64 系统或者你熟悉的系统

Server Size服务器的内存大小，对于一般的使用场景来说，10G完全够用，只需要3.5美金一个月，性价比是非常之高，注意不要选择IPv6 ONLY的

![image](https://github.com/user-attachments/assets/724ba914-4f76-482f-a812-add0f1259293)

然后点击右下角 Deploy Now，进行服务器的部署即可，部署成功之后，你就获得了一台自己的服务器主机，如下图：

<img width="1007" alt="111" src="https://github.com/user-attachments/assets/dc4143e6-6e84-40bd-b54b-288d0f4bc60e">

点击对应的服务器名称，即可进入到服务器对应的页面，可以查看到服务器对应的ip和密码，这个也是后面登陆到服务器上面安装VPN软件所必须的

<img width="1091" alt="WechatIMG639" src="https://github.com/user-attachments/assets/aeea7083-1477-40bf-890e-38dc237123d2">

## 登陆服务器来安装所需要的软件

### 如果你使用Windows系统的电脑

在这里我们使用[Putty](https://www.putty.org/)工具来进行服务器的登陆，打开之后选择 session，将你在 vultr 网上得到的服务器 ip 复制过来，端口号默认设置为22，连接类型选择SSH，然后点击“Open”打开连接。连接成功后，输入你的云服务器密码进行登录。

![image](https://github.com/user-attachments/assets/113018a2-580d-4197-be05-b24b1176dfa9)

### 如果你是Mac或者linux系统的电脑

则直接打开终端，输入如下命令即可, 星号部分就是你的ip地址，输入如下命令之后，继续输入 yes 后按回车，接着输入云服务器的密码，即可使用云服务器。

```
ssh root@xx.xx.xxx.xx
```

## 在服务器上安装软件，搭建VPN服务

接下来进入本教程关键的安装部分，没有经验的小伙伴只需要根据教程复制粘贴一步一步来即可。

书接上面，连接成功，成功登入到服务器上面之后，需要执行一系列的命令来安装我们所需要的vpn软件，按照步骤：

### 1.首先安装必要的库文件：

```
sudo yum -y install wget gcc gcc-c++ autoconf automake make
```

### 2.在线获取安装VPN所需要的脚本文件

```
wget –no-check-certificate -O ss.sh https://raw.githubusercontent.com/sucong426/VPN/main/ss.sh
```

### 3.执行脚本文件，进行VPN的安装

```
sh ss.sh
```

过程如下图

![image](https://github.com/user-attachments/assets/ae4bea5f-c909-4118-ad21-6fce08f34ba8)

根据提示，依次设置密码，输入端口

![image](https://github.com/user-attachments/assets/28206cdc-72a1-4abd-82ae-5c751548e5f3)

加密方式这里选择类型7，设置好了之后，回车即开始安装，输出了下面的提示则表明已经安装成功了

![image](https://github.com/user-attachments/assets/fabd0d3e-78af-417a-97e6-1910e4906038)

这里的信息切记记录下来，这里所代表的就是你专属VPN的IP地址、端口号、密码和加密方式。切记要记录下来！！将这些信息复制下来后，使用客户端进行设置，就可以通过代理连接到外面啦。
做完这一系列的操作之后，就可以放心关闭打开的窗口，VPN服务会一直稳稳运行在后面。

## 如何使用VPN

搭建好自己的VPN环境之后，接下来就是使用VPN。一般都会使用的工具是shadowsocks

电脑端的下载地址[shadowsocks](https://github.com/shadowsocks/shadowsocks-windows/releases/download/4.4.0.0/Shadowsocks-4.4.0.185.zip)，[客户端的使用教程](https://www.howru.cc/articles/414.html)网上挺多这里不赘述；

手机可以去应用市场下载shadowsocks软件，如果是ios可能需要海外的apple id账号来下载，然后在shadowsocks软件里面配置好上面安装所获得记录下来的云服务器 IP 地址，端口号，密码，加密方式，即可开始冲浪！




