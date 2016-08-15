# 硬派云专线计费管理

## 概述
TOUGHPNS管理系统适用于VPN(虚拟专网)的接入运营与管理业务；支持PPTP，L2TP，OPENVPN；系统认证模式灵活可配置(支持基于IP的NAS认证，NAS标识认证，DDNS认证)，丰富的资费策略支持；系统采用云端集成部署，由硬派科技提供全程维护与技术支持，免除原始的本地服务器部署模式的烦恼，以便运营者更专注于用户的发展与服务提升。
本文希望能够帮助toughPNS用户快速地理解系统特性，各功能点流程和配置，迅速上手。

## 准备工作
在开始前，你需要注册硬派云服务账号，订购免费服务或收费服务，如果您还没有订购相关服务，请移步：[【硬派云官网】](https://toughcloud.net/customer) 注册相关信息，订购服务，按需求选择各个档次的VPN业务资费，订购完服务就可使用硬派云服务账号，密码登陆TOUGHPNS系统了。

## 系统功能介绍

### 1、登陆TOUGHPNS运营管理系统
登陆[【TOUGHPNS运营管理系统】](https://toughpns.toughcloud.net/login)，账号和密码为你在硬派云官网注册的账号和密码，此账号为你在ToughPNS系统的超级管理员账号。

![TOUGHPNS系统登陆页面](http://qnstatic.toughcloud.net/Fgw5ZDo02Pas-xNNIbLG9tEysuU6)

### 2、配置你的网络接入设备
登陆成功首页会显示你的基本信息和硬派云服务相关信息，同时列出可用的RADIUS引擎信息，你可以根据引擎信息配置你的网络接入设备上的RADIUS信息，如果你使用的是RouterOS参见[【RouterOS 与硬派云对接实现 PPPOE 计费】](../pages/example/routeros_pppoe_example.md)中第二步的RouterOS 设备配置。
![系统首页](http://qnstatic.toughcloud.net/Fs7hUTD8N0QIvc8aoOqpb27jSiuV)

###3、配置系统相关参数
此处可以设置自定义的系统名称，设置支付宝合作者相关参数，以及设置RADIUS记账间隔，RADIUS下发的最大会话时长，系统在用户详情页是否显示用户密码等。

![系统参数设置](http://qnstatic.toughcloud.net/FpdjkJKbtgQP5sihoaIGOOYc9Rnp)

### 4、修改当前登陆的操作员密码
如果修改系统当前操作员的密码，可以点击红色框选区域的连接修改密码即可，请记住修改后的密码。
![操作员修改密码](http://qnstatic.toughcloud.net/Ft6lAvadmMw7PzyAjvIXbzv6d1Wq)


### 5、NAS管理(接入设备管理)
点击下图红色框选位置按钮，注册你的接入设备信息：接入设备类型，接入设备IP地址，动态域名，NAS标识(接入设备IP地址和动态域名是可选填项，无固定IP地址的接入设备可使用NAS标识认证，不推荐使用动态域名认证)，共享秘钥，强制下线端口(COA DM)，认证模式等。

![NAS信息管理](http://qnstatic.toughcloud.net/FspDRRsmyndCZKP3p4rYtGrmd0da)
添加NAS设备
![添加NAS设备](http://qnstatic.toughcloud.net/Fv9Ucqb5MfrF-KTNKtv8JN74q0My)
其他NAS设备管理操作请自行尝试。

### 6、资费套餐管理
资费套餐支持买断包月，预付费包月，买断流量，买断时长等资费类型，你可以根据自身运营需求设置合理的资费套餐，添加完成后可点击资费名称查看资费心情和已绑定的NAS设备。

![添加资费](http://qnstatic.toughcloud.net/FqTIVCOVmeLUrljKn_I17jJq0z9O)

![资费套餐管理](http://qnstatic.toughcloud.net/FjwZyJLZaHgjcCgpbmGMosTdA3-Q)

![修改资费](http://qnstatic.toughcloud.net/FtKUcgm9_s-viCv9oum8DLNufNQZ)

### 7、操作员组管理
在添加操作员之前，需要先添加操作员权限组，操作员必须绑定一个权限组，权限就是操作员能够访问的菜单项集合。

![操作员组管理](http://qnstatic.toughcloud.net/FhlWpbi8r5W1vW8TmUXKvVKwEmuY)

添加操作员组

![添加操作员组](http://qnstatic.toughcloud.net/FgnVL9a0aa_w6NWp0f7o5shq9FqR)

### 8、操作员管理
现已经注册了操作员权限组，就可以添加二级操作员了，为操作员绑定特定的权限组，赋予资费套餐权限，下图操作员管理显示的ISP超级管理员就是你在硬派云注册的用户。

![操作员管理](http://qnstatic.toughcloud.net/FjMDC7qAh39_1Hhbq9VXerKddAMF)

添加二级操作员,修改二级操作员界面类似
![添加操作员](http://qnstatic.toughcloud.net/Fm-E17ngjqPMrt198ERFvx9lycUH)

### 8、系统操作日志
系统记录各操作员在系统中进行的各项操作供查询，以便于管理操作员规范操作，并使每项操作有据可查。
![操作日志查询](http://qnstatic.toughcloud.net/FnyG7DhnuuxI6oq0GUKM9A89B77X)

### 9、代理商管理
系统支持运营商发展代理商，可以给代理商赋予一定的资费套餐交由其发展用户，同时可以为代理商设置一定的折扣和费用减免优惠，参见代理商优惠规则。
在增加代理商之前，请先配置代理商优惠规则，参见10
![增加代理商](http://qnstatic.toughcloud.net/FnwN_1UAkXCjvnYSocwCvr60_D8Q)

代理商列表
![代理商管理](http://qnstatic.toughcloud.net/FsA5clsby-nRFrQLOar4uPw-UiBd)

添加完代理商，就可以在TOUGHPNS的代理商系统中登陆，营业了。链接地址：[【TOUGHPNS代理商系统】](http://toughpns.agency.toughcloud.net/)

### 10、代理商优惠规则
为代理商设定一定的优惠比例或者费用减免优惠，当然这个优惠是有时间限制的，过了过期时间就不能享有优惠减免了，当然你也可以继续修改过期时间，让优惠变为可用。
代理商优惠
![代理商优惠](http://qnstatic.toughcloud.net/FkQt2Dohb3K4g3WvaL3IIrViwLnc)
添加代理商优惠
![添加代理商优惠](http://qnstatic.toughcloud.net/FmGR121Pt5H6btxSM-5Z_cE9azpa)

### 11、快速开户
系统提供的快速开通用户的功能，用户名和上网账号都为同一个账号
![快速开户](http://qnstatic.toughcloud.net/Fh9kIUqQiiVdk6IejFW1EYYlqptc)

开户成功后可以使用会员账号和密码登陆自助服务平台[【TOUGHPNS自助服务平台】](http://toughpns.ssportal.toughcloud.net/)查询账号信息，修改密码等。
开户成功后用户详情页
![开户成功后用户详情页](http://qnstatic.toughcloud.net/FjM5hTRcOcGC4vEJcAPjqEXVzX51)

### 12、会员信息查询
查询系统中所有会员的基本信息，可按条件查出自发展会员，某个代理商发展的会员以及所有会员，同时也可以点击每条会员信息后的操作按钮为会员添加上网账号。

![会员信息查询](http://qnstatic.toughcloud.net/Ft-NPl9ggKvbpX6UC1MiWxcTiP0o)

会员开通上网账号
![会员开通上网账号](http://qnstatic.toughcloud.net/FnqcqlMMgZm141wrRAzRQIWXJ_jU)

### 13、上网账号查询
查询系统上网账号信息，每条上网后面的用户受理按钮可以对账号进行续费，停机，删除等操作。
![上网账号查询](http://qnstatic.toughcloud.net/FpvSaf9xCD-gfcWmGeBuuezHCgzg)

用户受理
![用户受理](http://qnstatic.toughcloud.net/FjM5hTRcOcGC4vEJcAPjqEXVzX51)

### 14、用户缴费查询
根据条件查询用户缴费信息
![用户缴费查询](http://qnstatic.toughcloud.net/FqYQx_lmoMz0xOncJGMXc3z7-E3P)

### 15、用户上网详情
查询用户上网详细情况
![用户上网详情](http://qnstatic.toughcloud.net/FubmSIJ0mgcLlZyUjizvKlU3kTj1)

### 16、在线用户查询
查询当前在线用户信息，可强制下线某用户，清理BAS在线用户是指删除这个BAS在系统中在线用户的信息，并不强制下线这些用户。
![在线用户查询](http://qnstatic.toughcloud.net/FnxxkCawdbpzbriULd1JH6xrPKNF)

### 17、代理商交易查询
一个简易的代理商交易查询功能，代理商的每笔交易记录都会记录下来，供对账和查询，但不提供统计。

![代理商交易查询](http://qnstatic.toughcloud.net/Fj2ouL7wUGmkhznydqbTEYxiq60C)