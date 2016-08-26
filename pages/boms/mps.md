# 对接微信公众号实现自助服务

计费管理系统提供了微信公众号的接口，在本章中我们将引导你一步一步实现微信公众号的对接，实现用户自助服务。

## 准备工作

首先你需要申请微信公众号，订阅号服务号均可，具体申请什么类型的公众号你需要确定好，比如你需要自定义微信公众号菜单，那么最好就是申请服务号了，如果你是用于运营最好是以公司名义申请并认证，个人微信订阅号无法认证也无法具有自定义菜单的功能。

## 参数配置

登录你的微信公众号管理，同时登录你的计费管理系统，将微信公众号管理开发栏目－基础配置的参数填写到计费管理系统的微信公众号参数配置里，同时将微信公众号接口地址设置到微信公众号管理配置里，以及设置Token。

![wechatconfig](http://qnstatic.toughcloud.net/Fv7LeGMGWRXObhdIruvCsnWcCCXh)

![wechatconfig](http://qnstatic.toughcloud.net/Fu-AeBf0dRj2Mqfh0eJSZNiCH7tm)

![wechatconfig](http://qnstatic.toughcloud.net/Fh3PXR18gIawDwQgey3fGXsdd8AC)

- 微信公众号接口地址：由计费管理系统提供，格式如 https://mp.toughcloud.net/mps/{isp_code}, 将改地址填入微信配置。
- 微信公众号令牌(Token)：该参数在计费管理系统先填写，再配置到微信公众号管理配置里。
- 微信公众号应用ID：从微信公众号配置里拷贝过来。
- 微信公众号应用密钥：从微信公众号配置里拷贝过来。
- 微信公众号消息加解密密钥：在微信公众号配置里生成并拷贝过来，如果不启用安全模式则不需要。
- 微信公众号消息加解密模式：和微信公众号配置一致。
- 公众号欢迎信息：用户关注微信后推出的消息。

## 关键字回复

系统默认提供了 service 呼出用户自助服务的关键字，可以在欢迎信息中说明。

## 自定义菜单

计费管理系统内置了微信公众号自定义菜单的设置，配置好菜单后，同步即可。

![菜单配置](http://qnstatic.toughcloud.net/FtWFaN0_3rfh95wpnqK1gNqn3O1J)

### 系统提供的菜单链接列表

在配置时，注意 {isp_code} 需要替换成您自己的服务商编码

- 常见问题

https://mp.toughcloud.net/mps/{isp_code}/faqs

页面为静态内容，您可以自己链接到自定义的链接去。

- 资费套餐

https://mp.toughcloud.net/mps/{isp_code}/products

显示系统中对外发布的服务资费列表，在支持微信支付的条件下可实现在线订购。

- 账号绑定(查询)

https://mp.toughcloud.net/mps/{isp_code}/userbind

提供用户上网帐号绑定功能，如果已经绑定则直接打开用户帐号信息页面，在支持微信支付的条件下可实现在线续费。

- 交易查询(需要完成绑定)

https://mp.toughcloud.net/mps/{isp_code}/userorder

提供用户订购纪录查询，含缴费信息数据。

- 密码修改(需要完成绑定)

https://mp.toughcloud.net/mps/{isp_code}/useruppw

提供用户密码修改功能







