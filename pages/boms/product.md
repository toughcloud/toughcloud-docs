# 资费套餐管理

系统支持以下4种资费策略：
 
- 包月资费：按月定价，按需购买，比如单月价30元，用户可一次性订购多个月，自由打包。

- 组合包月：即买断型的打包资费，比如包半年300元，包一年500元，将多个月打包成一个套餐，用户不能自由选择，但打包后价格可以更加优惠。

- 时长资费：按使用时长计价，打包固定的时长销售，比如10小时总价20元，当时长额度不足时，用户不能再继续上网。

- 流量资费：按使用流量计价，打包固定的流量销售，比如10G流量5元，当流量额度不足时，用户不能再继续上网。

> 免费授权模式：当用户订购资费过期，或余额，流量不足时，如果该资费允许到期免费授权，则用户可以继续认证接入，同时下发免费授权模式下的低速限速模式。

![创建资费](http://qnstatic.toughcloud.net/FotnzTjp0Ocqakd3ar8ZpqJh0DRn)

![资费套餐](http://qnstatic.toughcloud.net/FnLqYFyzfGnAWYwmVxlojbxNyJY7)

## 资费设置界面
---

![资费详情界面](http://qnstatic.toughcloud.net/FnTisqqPCIYyfmMD4VaA6YcNr0Xn)

#### 资费扩展 RADIUS 属性

有时候，可能会遇到需要支持一些特殊的 RADIUS 属性，比如更灵活的限速，地址池等，可以通过添加扩展 RADIUS 属性来实现。

![资费扩展 RADIUS 属性](http://qnstatic.toughcloud.net/FomzPZzwF5AOFV9jXBebyzxBfEpH)

系统提过了一些默认的参考，具体属性还需要参考设备厂商提供的协议文档。