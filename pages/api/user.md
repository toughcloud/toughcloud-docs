### 用户数据同步

同步 Radius 用户数据至硬派云认证计费引擎


- API 接口地址

    https://www.toughcloud.net/api/v1/engine/user/add

例子：

    GET https://www.toughcloud.net/api/v1/user/engine/add?isp_code=1234567&up_rate=10&down_rate=10&auth_limit=1&domain=ddd&time_length=0&bill_type=timestep&bind_vlan=0&bind_mac_num=&bind_nas_addr=&password=888888&flow_length=0&ip_pool=&ip_address=&username=test01&vlan_id2=0&vlan_id1=0&status=0&expire_date=2017-07-03&update_time=2016-07-03%2014%3A20%3A32&sign=1117257C5F2A472A249BAC4435079EE3&timestamp=1467629822&apikey=LpWE9AtfDPQ3ufXBS6gJ37WW8TnSF920&radius_attr_Framed_Pool=vippool 

#### 参数说明

    username: 用户认证账号，必选参数，长度4-32位
    realname: 用户姓名，必选参数，长度1-32位
    password: 用户认证密码，可选 RSA 加密
    pwd_encrypt: 用户密码加密方式，默认 none 不加密，可选 RSA 加密，使用平台提供公钥加密密码
    bill_type: 资费类型: 时段(timestep)  时长(timelen)  流量(flowlen)
    status: 用户状态 0-未激活 1-正常 2-停机
    time_length: 用户剩余时长，秒，默认0
    flow_length: 用户剩余流量，kb，默认0
    fixd_flows: 用户流量包，kb，默认0
    expire_date: 用户过期时间, yyyy-mm-dd,必选参数 
    session_limit: 用户会话限制数，默认1，最小为1
    bind_nas_id: 用户绑定接入设备标识码，可选参数
    bind_mac: 用户是否绑定 mac，0-不绑定 1-绑定 默认0
    mac_addr: 用户绑定 mac，可选参数
    bind_vlan: 用户是否绑定 vlan，0-不绑定 1-绑定
    vlan_id1: 用户绑定内层vlanid，默认0
    vlan_id2: 用户绑定外层vlanid，默认0
    ip_address： 用户固定 IP 地址，可选参数
    ip_pool: 用户地址池,可选参数
    up_rate: 用户上行速率 Mbps，可选参数, 默认0
    down_rate: 用户下行速率 Mbps，可选参数，默认0
    free_auth: 是否到期免费授权 0-否 1-是
    free_up_rate: 免费授权最大上行速率
    free_down_rate: 免费授权最大下行速率
    domain: 用户域，可选参数
    update_time: 用户创建时间，可选参数，默认服务器端生成
    apikey: 服务商 apikey，接口调用时传递，必选属性
    timestamp: 消息时间戳，必选参数
    sign: 使用与 apikey 对应的 apisecret 签名生成，必选参数

#### Radius 扩展参数

同步用户时可以携带多个 Radius 参数，必须是 硬派云认证计费引擎 Radius 协议字典里有的属性。

参数以 radius_attr_ 开头，后面跟上 属性名，- 用 _ 代替，如：

    radius_attr_Framed_Pool  //表示标准Radius地址池属性
 
#### 响应

    {
      "msg": "处理成功",
      "nonce": "1467629824",
      "code": 0,
      "sign": "B337ECE11028519BFFCDB903962A5602"
    }

### 查询用户信息

查询单个或多个用户

- API 接口地址

    https://www.toughcloud.net/api/v1/engine/user/get 

例子:

    GET https://www.toughcloud.net/api/v1/user/engine/get?sign=F12E1CDAB1C1553460DF80849F4167DD&timestamp=1467613841&apikey=LpWE9AtfDPQ3ufXBS6gJ37WW8TnSF920

#### 参数说明

    username: 用户认证账号，可选参数，长度4-32位
    apikey: 服务商 apikey，接口调用时传递，必选属性
    timestamp: 消息时间戳，必选参数
    sign: 使用与 apikey 对应的 apisecret 签名生成，必选参数

#### 响应

    {
      "nonce": "1467647808",
      "code": 0,
      "page_size": 20,
      "sign": "A8FADB150E12D7B1B35CBAF5A4041D8A",
      "msg": "ok",
      "total": 1,
      "data": [
        {
          "down_rate": "10",
          "username": "test01",
          "domain": "ddd",
          "time_length": "0",
          "radius_attrs": {
            "Framed_Pool": "xxx"
          },
          "update_time": "2016-07-03 14:20:32",
          "flow_length": "0",
          "session_limit": "1",
          "vlan_id2": "0",
          "vlan_id1": "0",
          "expire_date": "2017-07-03",
          "status": "0",
          "bind_mac": 0,
          "isp_code": "1234567890123",
          "bill_type": "timestep",
          "bind_vlan": "0",
          "pwd_encrypt": "none",
          "bind_nas_addr": "",
          "password": "666666",
          "ip_address": "",
          "ip_pool": "",
          "up_rate": "10",
          "mac_addr": "",
          "_id": "577a7c19a9fc284d4d2dcbef"
        }
      ],
      "page": 1
    }

### 更新用户信息

- API 接口地址

    https://www.toughcloud.net/api/v1/user/engine/update 

例子:

    GET https://www.toughcloud.net/api/v1/user/update?sign=C9D898DA496482A70A8545A3051D03DC&timestamp=1467638117&apikey=LpWE9AtfDPQ3ufXBS6gJ37WW8TnSF920&username=test01&password=666666&radius_attr_Framed_Pool=xxx

#### 参数说明

    username: 用户认证账号，必选参数，长度4-32位

其他参数参考用户注册参数说明

#### 响应

    {
        "msg": "处理成功",
        "nonce": "1467638117",
        "code": 0,
        "sign": "45F23FBA87629451622798C361CDC1DC"
    }

### 删除用户信息

- API 接口地址

    https://www.toughcloud.net/api/v1/user/engine/delete 

例子:

    GET https://www.toughcloud.net/api/v1/user/engine/delete?sign=CBA60DA2951E62DD9845B4EE44342C48&timestamp=1467638267&apikey=LpWE9AtfDPQ3ufXBS6gJ37WW8TnSF920&username=test01

#### 参数说明

    username: 用户认证账号，必选参数，长度4-32位
    apikey: 服务商 apikey，接口调用时传递，必选属性
    timestamp: 消息时间戳，必选参数
    sign: 使用与 apikey 对应的 apisecret 签名生成，必选参数

#### 响应

    {
      "msg": "处理成功",
      "nonce": "1467638268",
      "code": 0,
      "sign": "12F7DA05AED49E9686BA0B3B9D934DCB"
    }