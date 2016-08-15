# RouterOS 与硬派云对接实现无线热点认证

本文将一步一步指引你实现 RouterOS 与硬派云的对接，从而实现无线热点认证，让你的 WiFi 热点真正热起来。

在开始前，你应该已经完成了硬派云账号的注册，订购了免费的计费服务或收费服务，如果您还没有，请移步这里：[硬派云账号管理](http://www.jianshu.com/collection/39ae5e9979a8)

## 一. 在计费管理系统完成准备工作

登录[【硬派网络计费系统】](https://dashboard.toughcloud.net)管理控制台，接下来，我们需要完成一些基本的数据准备。

### 1. 设置运营区域和社区

进入区域管理界面，新建一个区域

![区域管理](http://qnstatic.toughcloud.net/FtLiJChYT7DbkaI6XP41Pf02_0nS)

![社区管理](http://qnstatic.toughcloud.net/Fq9ZYrb033ZH4omwuEPfN2lb-fb_)

### 2. 设置接入设备
- 接入设备地址：如果设备不是公网 ip，填写0.0.0.0。
- 接入设备标识：请设置 RouterOS 的设备 id 名，该标识在硬派云系统中全局唯一，可以手工填写，也可以采用系统辅助生成的。
- portal协议：选 RouterOS
- 接入设备类型：选 RouterOS
- AC 端口：RouterOS 设备无效
- 共享密钥：填写您在设备中配置的 Radius 密钥
- 授权端口：填写设备授权端口号，默认是3799，注意要在设备中开启。如果设备是内网 NAT 与云端对接，该端口将无效，后续我们会有相应的方案来解决这个问题。
- 免密码认证：根据实际情况设置。
- 记账间隔：从该设备接入的用户最小记账间隔，最低不能低于60秒，对于包月型用户：低于3600秒的值无效。
- 最大会话时长：用户上线后多长时间会断开。


![创建接入设备](http://qnstatic.toughcloud.net/FotMOj-jIN5ru4Z6WOAmc3pO5ZrU)


![接入设备列表](http://qnstatic.toughcloud.net/FgvVUN_AgLUjIhEwXjOHlCG-QRAR)

### 3. 设置无线认证域

一个认证域相当于一个群组，在这个域里面可以纳入 AP 节点的认证管理。每个域可以绑定一个 portal 模板，通过对模板的定制可以实现个性化的认证门户界面。

![创建无线认证域](http://qnstatic.toughcloud.net/FsRs7Y1sWlwuBzmrWsonI63GAr6I)

![认证域列表](http://qnstatic.toughcloud.net/Fl5GRSvqtnr0mndAkjPwX55gMMFQ)

进一步对认证域进行设置，每个域可以设置一组扩展属性，这些属性会因接入设备的不同而不同，其中包含一些预置的公共属性。对扩展属性的设置，我们将会额外提供更详细的文档说明。

每个域下可以加入不限数量的 AP 节点，每个 AP 节点会提供一个全局唯一标识 guid。

![认证域设置](http://qnstatic.toughcloud.net/Fj4aba3toKzlgjofPAk7uC5Fq-v9)

预览下效果

![模板预览](http://qnstatic.toughcloud.net/Fm1ZhdAEGZl18GdXXJPut9KnA4vi)

### 4. 设置无线认证资费

我们还需要为热点认证指定一个可自动提供短信验证的资费，如果不希望提供自动注册服务，则可以不用设置。

自动注册热点资费可以选择不同类型，根据你的运营需求进行设置，你可以设置固定流量的资费，固定时长的资费，包月时段类型的资费。

> 注意：对于热点自动注册的用户，包月时段类型只会提供一天的有效期，如果用户下次认证再次验证短信，微信等可以再次续费一天的有效期，即每个自动注册的用户可以免费上网一天。对于流量或时长，每次重新验证会重置流量和时长。

![热点自动注册资费](http://qnstatic.toughcloud.net/Fg0wSHcaGVsr76Rj11qOyQ52LhW3)

![资费列表](http://qnstatic.toughcloud.net/Fkdc54xytJJg_sYPyZ98XpwY6_9b)

在系统参数管理界面设置全局热点资费

![设置全局资费](http://qnstatic.toughcloud.net/Fj3VdrRr6M_LwwydbhHS7gBdJslz)

## 二. RouterOS 设备配置

### 1. 地址池设置
![IP 地址池设置](http://qnstatic.toughcloud.net/FstCGxv_zqfWabGmCkOOg6iBuQgM)

### 2. Hotspot 服务器设置
![Hotspot 服务器配置](http://qnstatic.toughcloud.net/FruzalByBwMMFQVS2L3U41YzESIs)


![Hotspot  Server profile 设置](http://qnstatic.toughcloud.net/FgAcZNSpqJkd4KpND--04NkBNJ-o)

### 3. 认证模板设置

你可能注意到了我们使用到了定制的模板

![定制模板](http://qnstatic.toughcloud.net/FkIy1ifDx6LBCGQ99me0CymEI8-9)

toughcloud 模板目录主要包含以下几个文件

> 注意: 模板里的 guid 值必须是无线认证域里存在的 AP guid

login.html 
rlogin.html

    <html>
    <title>...</title>
    <body>
    <form name="redirect" action="http://hotspot.toughcloud.net/routeros" method="post">
    <input type="hidden" name="guid" value="01010101010101010101010101010101">
    <input type="hidden" name="wlanusermac" value="$(mac)">
    <input type="hidden" name="wlanuserip" value="$(ip)">
    <input type="hidden" name="wlanusername" value="$(username)">
    <input type="hidden" name="link_login" value="$(link-login-only)">
    <input type="hidden" name="link_logout" value="$(link-logout)">
    <input type="hidden" name="link_orig" value="$(link-orig)">
    <input type="hidden" name="link_status" value="$(link-status)">
    <input type="hidden" name="error" value="$(error)">
    </form>
    <script language="JavaScript">
        document.redirect.submit();
    </script>
    </body>
    </html>


logout.html

    <html>
    <title>...</title>
    <body>
    <form name="redirect" action="http://hotspot.toughcloud.net/routeros/logout" method="post">
    <input type="hidden" name="guid" value="01010101010101010101010101010101">
    <input type="hidden" name="wlanusermac" value="$(mac)">
    <input type="hidden" name="wlanuserip" value="$(ip)">
    <input type="hidden" name="wlanusername" value="$(username)">
    <input type="hidden" name="link_login" value="$(link-login-only)">
    <input type="hidden" name="link_logout" value="$(link-logout)">
    <input type="hidden" name="link_orig" value="$(link-orig)">
    <input type="hidden" name="link_status" value="$(link-status)">
    <input type="hidden" name="error" value="$(error)">
    </form>
    <script language="JavaScript">
        document.redirect.submit();
    </script>
    </body>
    </html>

redirect.html

    $(if http-status == 302)Hotspot redirect$(endif)
    $(if http-header == "Location")$(link-redirect)$(endif)
    <html>
    <head>
    <title>...</title>
    <meta http-equiv="refresh" content="0; url=$(link-redirect)">
    <meta http-equiv="pragma" content="no-cache">
    <meta http-equiv="expires" content="-1">
    </head>
    <body>
    </body>
    </html>

status.html
rstatus.html

    <html>
    <title>...</title>
    <body>
    <form name="redirect" action="http://hotspot.toughcloud.net/routeros/status" method="get">
    <input type="hidden" name="guid" value="01010101010101010101010101010101">
    <input type="hidden" name="wlanusermac" value="$(mac)">
    <input type="hidden" name="wlanuserip" value="$(ip)">
    <input type="hidden" name="wlanusername" value="$(username)">
    <input type="hidden" name="link_login" value="$(link-login-only)">
    <input type="hidden" name="link_logout" value="$(link-logout)">
    <input type="hidden" name="link_orig" value="$(link-orig)">
    <input type="hidden" name="link_status" value="$(link-status)">
    <input type="hidden" name="uptime_secs" value="$(uptime-secs)">
    <input type="hidden" name="bytes_in" value="$(bytes-in)">
    <input type="hidden" name="bytes_out" value="$(bytes-out)">
    <input type="hidden" name="error" value="$(error)">
    </form>
    <script language="JavaScript">
        document.redirect.submit();
    </script>
    </body>
    </html>

将以上几个文件上传到 routeros 目录，统一放到新建的 toughcloud 目录下并配置使用。

### 4. Radius 服务设置

![Radius 列表](http://qnstatic.toughcloud.net/FseQ4YVut2-HwAkkk08xV298uexG)

![Radius 服务配置](http://qnstatic.toughcloud.net/FnYLxCpfwwPBU5Xw-a3kbwjpukg6)

![Radius 授权端口配置](http://qnstatic.toughcloud.net/FtWlDQUuxrUItJYpC8JPbbut6yIL)

### 5. 免认证列表

![管理地址免认证](http://qnstatic.toughcloud.net/FiGKulbqa4La9KgDF4jm82zdgMW1)

![免授权访问资源](http://qnstatic.toughcloud.net/Flr0hiexl0Yqeb87zP8egA6CYk5i)

## 三. 开始正式测试

完成以上两大步，我们就可以开始我们的认证测试了，当然记得把你的路由插上电源和网线，物理设施部署必须就位。

连上WiFi 试试吧

![连接 WiFi](http://qnstatic.toughcloud.net/Fq4-YOjTbYLmP71zlkGGOM3FOrXt?imageView2/2/w/480/interlace/0/q/100)

界面出来了，什么，还需要密码，让我短信验证试试看。

>友情提示，短信发送由硬派云网关统一提供，您需要根据使用量购买短信服务包，当然价格便宜的都不好意思说

![认证界面](http://qnstatic.toughcloud.net/FicmKHfrtp9Hpm_QcxHhaYGtp8ic?imageView2/2/w/480/interlace/0/q/100)

不是骗人的，密码发来了

![短信验证](http://qnstatic.toughcloud.net/FkERJE4cS21JOsOPkiIeCAEWm2B8?imageView2/2/w/480/interlace/0/q/100)

啊哈，连上网络啦

![认证成功](http://qnstatic.toughcloud.net/FvK5Cawb7yGaiIXlBwyFhWyDEB47?imageView2/2/w/480/interlace/0/q/100)

不说了，我要用着免费的 WiFi 看个剧先。