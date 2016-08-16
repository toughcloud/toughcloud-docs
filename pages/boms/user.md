# 用户信息管理

## 用户规范定义
---

#### 用户授权有效期

- 用户授权有效期因资费而不同。
- 包月资费由过期时间来控制用户账号的使用有效期。
- 时长和流量资费靠用户剩余时长与剩余流量来控制用户账号的使用权限。

#### 用户交易订单

当用户受理产生相关缴费退费费用时，比如开户，销户，续费，充值操作，营业系统会为该操作生成订单，订单记录了用户名，上网账号，资费，费用，支付状态，受理渠道，受理时间信息。

## 用户查询列表
---
对所有用户信息的条件查询，以及用户受理入口，支持导出用户信息数据为Excel格式。

![用户查询](http://qnstatic.toughcloud.net/FkBswq0fFTZ-WQuLsdy3STSvbYSJ)

## 用户业务受理
---
在用户信息列表点击用户受理即可进入用户详情界面，提供了所有用户受理的链接按钮。

![用户业务受理](http://qnstatic.toughcloud.net/FrMNA02_1CVe4KwcO79R6kEcHsSa)

对于二级操作员，只能看到被分配了权限的操作按钮。

#### 基本资料修改
---
![基本资料修改](http://qnstatic.toughcloud.net/FrcM5YAhryYpBkH4scRa7kJfALMz)

#### 修改授权策略
---

![修改授权策略](http://qnstatic.toughcloud.net/FkBhaHJOI7cYpIg89kObcDHP8vAz)

#### 修改用户认证密码
---

![修改用户认证密码](http://qnstatic.toughcloud.net/FnKzooJ4nkVdAczavB9vZTbHXLwS)

#### 释放绑定
---
释放绑定操作会清除用户已经绑定的 MAC 地址和 VLANID，如果用户迁移了地址，如果绑定了 VLAN 信息的必须释放。

#### 变更用户资费
---

![变更用户资费](http://qnstatic.toughcloud.net/FgBJY-xTmZ5tfCO9QocbHoT61bsJ)

#### 用户续费
---

![用户续费](http://qnstatic.toughcloud.net/FgVPzBI0ty5pIPpTVHh2_IPOTn9E)


#### 用户停机
---
停机后，用户暂停接入认证，记录停机时间，当下次复机时，到期时间自动顺延。


#### 用户销户
---
处理用户退订服务，用户不再使用服务，并要求退款，退款金额由操作员根据用户使用情况调整金额。
用户销户不会删除账号资料，用户已经产生的交易，日志会保留备查。如果确信不再保留该账号，可以删除用户资料。

![用户销户](http://qnstatic.toughcloud.net/Fh7fV3KSMbG9YPRXFRO3ZU_vtjZa)

#### 删除用户
---
删除用户会删除用户相关的所有信息，此操作不可撤销，删除操作只能由高权限的操作管理员执行，避免不必要的误操作。

