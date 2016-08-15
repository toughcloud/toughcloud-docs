# RouterOS 与硬派云对接实现 PPPOE 计费

本文将一步一步指引你实现 RouterOS 与硬派云的对接，从而实现PPPOE 认证，为你的小区宽带事业添砖加瓦。

在开始前，你应该已经完成了硬派云账号的注册，订购了免费的计费服务或收费服务，如果您还没有，请移步这里：[硬派云账号管理](http://www.jianshu.com/collection/39ae5e9979a8)

## 一. 在计费管理系统完成准备工作

登录[【硬派网络计费系统】](https://dashboard.toughcloud.net)管理控制台，接下来，我们需要完成一些基本的数据准备。

### 1. 设置运营区域和社区

进入区域管理界面，新建一个区域

![区域管理](http://qnstatic.toughcloud.net/FtLiJChYT7DbkaI6XP41Pf02_0nS)

![社区管理](http://qnstatic.toughcloud.net/Fq9ZYrb033ZH4omwuEPfN2lb-fb_)

### 2. 设置接入设备
- 接入设备地址：目前云端暂时不需要以 IP 作为接入鉴别，填写0.0.0.0。
- 接入设备标识：请设置 RouterOS 的设备 id 名，该标识在硬派云系统中全局唯一，可以手工填写，也可以采用系统辅助生成的。
- portal协议：选 RouterOS(非必须)
- 接入设备类型：选 RouterOS（必选）
- AC 端口：RouterOS 设备无效
- 共享密钥：填写您在设备中配置的 Radius 密钥
- 授权端口：填写设备授权端口号，默认是3799，注意要在设备中开启。如果设备是内网 NAT 与云端对接，该端口将无效，后续我们会有相应的方案来解决这个问题。
- 免密码认证：根据实际情况设置。
- 记账间隔：从该设备接入的用户最小记账间隔，最低不能低于60秒，对于包月型用户：低于300秒的值会下发300秒。
- 最大会话时长：用户上线后多长时间会断开。


![创建接入设备](http://qnstatic.toughcloud.net/FotMOj-jIN5ru4Z6WOAmc3pO5ZrU)


![接入设备列表](http://qnstatic.toughcloud.net/FgvVUN_AgLUjIhEwXjOHlCG-QRAR)

### 3. 创建资费

系统支持以下4种资费策略：
 
- 包月资费：按月定价，按需购买，比如单月价30元，用户可一次性订购多个月，自由打包。

- 组合包月：即买断型的打包资费，比如包半年300元，包一年500元，将多个月打包成一个套餐，用户不能自由选择，但打包后价格可以更加优惠。

- 时长资费：按使用时长计价，打包固定的时长销售，比如10小时总价20元，当时长额度不足时，用户不能再继续上网。

- 流量资费：按使用流量计价，打包固定的流量销售，比如10G流量5元，当流量额度不足时，用户不能再继续上网。

> 免费授权模式：当用户订购资费过期，或余额，流量不足时，如果该资费允许到期免费授权，则用户可以继续认证接入，同时下发免费授权模式下的低速限速模式。

![创建资费](http://qnstatic.toughcloud.net/FotnzTjp0Ocqakd3ar8ZpqJh0DRn)

![资费套餐](http://qnstatic.toughcloud.net/FnLqYFyzfGnAWYwmVxlojbxNyJY7)

### 4. 创建认证用户

![创建认证用户](http://qnstatic.toughcloud.net/FgYhp952IqiduzESF-aAJHmggDAg)


![认证用户列表](http://qnstatic.toughcloud.net/FoCyqTvQ2OcLB-f049VdhL5jp5Ps)


## 二. RouterOS 设备配置

### 1. Radius 服务设置

![Radius 列表](http://qnstatic.toughcloud.net/FseQ4YVut2-HwAkkk08xV298uexG)

![Radius 服务配置](http://qnstatic.toughcloud.net/FnYLxCpfwwPBU5Xw-a3kbwjpukg6)


![Radius 授权端口配置](http://qnstatic.toughcloud.net/FtWlDQUuxrUItJYpC8JPbbut6yIL)



### 2. PPPOE 服务配置

>  注意：不选择 mschapv1，另外，你可能还需要进一步根据需要配置 RouterOS，比如地址池的分配等。

![PPPOE 服务配置](http://qnstatic.toughcloud.net/FqtSbgNwf0h5Y1Sd6Gl6XXDzpkKc)


![认证记账设置](http://qnstatic.toughcloud.net/Fvoi-TRvx4GF2rEIdl0xtdncAald)

> 与硬派云对接，无需设置 Interim Update 的间隔值，因为该值是通过硬派云 Radius 协议来控制的，根据接入设备的定义来控制用户间隔周期。

## 三. 测试 pppoe 认证

完成以上两大步，我们就可以开始我们的认证测试了，当然记得把你的路由插上电源和网线，物理设施部署必须就位。

![windows 拨号认证](http://qnstatic.toughcloud.net/Ft4U6mde0ILNUAbuGMIE3NITvP7L?imageView2/2/w/480/interlace/0/q/100)


![认证成功](http://qnstatic.toughcloud.net/Fp5CbC4_EPfPdRDhKxqeF2zrbDFv?imageView2/2/w/480/interlace/0/q/100)


