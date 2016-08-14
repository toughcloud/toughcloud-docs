该接口提供服务商同步接入设备信息时用，服务商必须已经注册才能使用。

服务商接入设备主要包括，路由器，VPN 服务器，无线控制器 AC 等具备 ppp接入协议或Portal 协议的设备。

### 接入设备注册

新增一个接入设备

- API 接口地址

    https://www.toughcloud.net/api/v1/engine/nas/add

例子：

    GET https://www.toughcloud.net/api/v1/engine/nas/add?isp_code=1234567&sign=15E3120587123D47C9B8D483F9E678DE&dns_name=&ip_addr=127.0.0.2&vendor_id=0&nas_id=rosnas0011&nas_name=ros1&nas_secret=secret&coa_port=3799&apikey=LpWE9AtfDPQ3ufXBS6gJ37WW8TnSF920&timestamp=1467625569 


#### 参数说明

    dns_name: 接入设备域名，可选参数，最大长度128
    vendor_id: 接入设备厂商标识码，0标识标准设备
    portal_vendor: Portal 协议类型，支持 ros,wifidog,cmccv1,cmccv2,huaweiv1,huaweiv2
    ip_addr: 接入设备 ip 地址，可选参数
    nas_id: 接入设备标识码，接入设备唯一标识
    nas_name: 接入设备名称，可选参数
    nas_secret: 接入设备 Radius 共享密钥，必选参数
    coa_port: 接入设备授权端口，可用于强制下线，默认3799
    bypass: 接入设备认证模式 0-免密码认证 1-强制密码认证
    interim_intelval: 记账间隔，默认600秒，不能低于60秒
    session_timeout: 下发最大会话时长，默认86400秒(一天)
    apikey: 服务商 apikey，接口调用时传递，必选属性
    timestamp: 消息时间戳，必选参数
    sign: 使用与 apikey 对应的 apisecret 签名生成，必选参数

#### 响应

    {
      "msg": "处理成功",
      "nonce": "1467625569",
      "code": 0,
      "sign": "E4E5233946E6114DC7EE897F20C345D4"
    }  

### 更新接入设备

查询单个或多个接入设备

    https://www.toughcloud.net/api/v1/engine/nas/update

例子：

    GET https://www.toughcloud.net/api/v1/engine/nas/update?sign=758624EA6742A2AD09C91A6968AB09A4&apikey=LpWE9AtfDPQ3ufXBS6gJ37WW8TnSF920&timestamp=1467648006&nas_name=test11&nas_id=rosnas0011

#### 参数说明

    nas_id: 接入设备标识码，接入设备唯一标识，必选参数
    apikey: 服务商 apikey，接口调用时传递，必选属性
    timestamp: 消息时间戳，必选参数
    sign: 使用与 apikey 对应的 apisecret 签名生成，必选参数

其他更新参数参考增加接入设备参数说明

#### 响应

    {
      "msg": "处理成功",
      "nonce": "1467648007",
      "code": 0,
      "sign": "E60EDCF75DD12DD3F64CBB9AB39FFE5D"
    }


### 查询接入设备

查询单个或多个接入设备

- API 接口地址

    https://www.toughcloud.net/api/v1/nas/get 

例子：

    https://www.toughcloud.net/api/v1/nas/get?isp_code=1234567&sign=80CDB4E41C087A05F54667F4386779FA&apikey=LpWE9AtfDPQ3ufXBS6gJ37WW8TnSF920&timestamp=1467613866

#### 参数说明

    ip_addr: 接入设备 ip 地址，可选参数
    nas_id: 接入设备标识码，接入设备唯一标识，可选参数
    apikey: 服务商 apikey，接口调用时传递，必选属性
    timestamp: 消息时间戳，必选参数
    sign: 使用与 apikey 对应的 apisecret 签名生成，必选参数

#### 响应

    {
    "msg": "ok",
    "nonce": "1467647729",
    "code": 0,
    "data": [
      {
        "isp_code": "1234567890123",
        "coa_port": "3799",
        "nas_name": "test11",
        "dns_name": "",
        "vendor_id": "0",
        "portal_vendor": "ros",
        "nas_secret": "secret",
        "nas_id": "rosnas0011",
        "bypass": 0,
        "interim_intelval": 600,
        "session_timeout": 86400,
        "ip_addr": "127.0.0.2",
        "_id": "577a7e6ba9fc284df395e40d"
      }
    ],
    "sign": "B1D1C96A288F3AAB0A2392ABC99DDFDE"
    }

### 删除接入设备

删除一个接入设备

- API 接口地址

    https://www.toughcloud.net/api/v1/engine/nas/delete

例子：

    GET https://www.toughcloud.net/api/v1/engine/nas/delete?nas_id=rosnas0011&sign=BBC40ED4D4050C03C8058AB2199C54DB&apikey=LpWE9AtfDPQ3ufXBS6gJ37WW8TnSF920&timestamp=1467637888

#### 参数说明

    nas_id: 接入设备标识码，接入设备唯一标识，可选参数
    apikey: 服务商 apikey，接口调用时传递，必选属性
    timestamp: 消息时间戳，必选参数
    sign: 使用与 apikey 对应的 apisecret 签名生成，必选参数

#### 响应

    {
      "msg": "处理成功",
      "nonce": "1467637888",
      "code": 0,
      "sign": "A0973E3FBEDA42FAE73B853EC8D40130"
    }