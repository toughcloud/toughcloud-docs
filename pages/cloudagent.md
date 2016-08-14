# 使用硬派云代理对接本地路由设备

当我们一谈到本地路由对接云端计费，很多问题就来了：

- 本地路由是内网，云端怎么识别 IP，如果采用网关动态映射，用 DDNS仍然麻烦，DDNS 不稳定怎么办。
- 用路由设备标识代理 IP，但是失去 IP 鉴权的优势了。
- 云端计费怎么像本地路由器发送强制下线请求，DMZ 好麻烦，还不安全。
- 本地路由与云端计费通信，中间消息可以被截获，被暴力破解怎么办。
- 云端计费发布的公开 IP 和端口被 DDOS，服务停摆，客户怎么办。

这仅是其中一部分问题而已，对接云端带来的一些列问题给用户带来各种困扰。

那么我们的解决方案是什么？

那就是云代理，如下图：

![硬派云代理](http://qnstatic.toughcloud.net/FgGWKF_g--SQHQvU0h0GfYr01kU6?imageView2/2/w/720/interlace/0/q/100)

> 云代理与云端服务采用基于 SSL 的加密隧道通信，在客户内网提供所有云端的服务代理，不管是 UDP 的认证计费，还是 HTTP 协议的 web 服务，同时除了基本的代理通信，还提供所有服务的负载均衡；本地设备与云代理对接实现计费服务，热点认证。客户几乎感知不到云的存在。

> 而在云端，会有成百上千个服务节点存在，也许在阿里云，也许在腾讯云，也许在北京，也许在上海或者香港，根据DNS 智能匹配，客户端云代理可以连接最快的服务节点。

> 云端不再需要向所有用户提供公开的服务地址，而是通过云代理的算法去自动获取服务。

> 我们前面担心的哪些问题，一下悄然化解。


### 如何使用硬派云代理

硬派云代理是一个 linux 下的应用程序，可以下载直接运行，在本地运行代理需要在硬派云申请一个授权接入码。

![申请授权码](http://qnstatic.toughcloud.net/FoMZs7pcCVYK46fZN32P2pG2mGkj)

> sid 可以在运行代理的时候看到

下载 [硬派云代理](https://www.toughstruct.com/download/cloudagent)，上传到你的 linux 服务器，比如目录  /usr/local/bin/cloudagent，修改可执行权限

    wget http://www.toughstruct.net/download/cloudagent -O /usr/local/bin/cloudagent

    chmod +x /usr/local/bin/cloudagent

运行代理

    /usr/local/bin/cloudagent --auth-port 1812 --acct-port 1813 --boms-port 9080 --wlan-port 9081

> 首次运行，由于没有云端授权，会报错退出，控制台显示如下，拷贝其中的 SID 值申请授权码，申请成功后，再次运行代理即可成功运行。
2016-08-13 21:58:06+0800 [-] Log opened.
2016-08-13 21:58:06+0800 [-] ToughAgent(SID=8221d670775cfa8efef35389a8122218): authport=1812,acctport=0,portalport=0, cloudport=0, bomsport=0, wlanport=0
2016-08-13 21:58:14+0800 [-] u'fetch endpoints failure, Unauthorized License'

以上代理启动了四个服务，本地的 radius 认证记账代理，本地的计费管理代理和无线认证门户代理：

1812/udp  Radius 认证
1813/udp  Radius 记账
9080/http  计费管理
9081/http  无线认证门户

对于管理员来说，所有服务就如同运行在本地内网一样。