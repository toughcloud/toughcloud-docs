### 在线用户查询

- API 接口地址

    https://www.toughcloud.net/api/v1/engine/online/get

例子：

    GET https://www.toughcloud.net/api/v1/engine/online/get/api/v1/engine/online/get?sign=8BE865FB4E90C0F86CAE170A60C446D8&timestamp=1469093478&apikey=L1AiKT7KrOGPOJLDK

#### 参数说明

    username: 用户认证账号，可选参数
    nas_addr: 接入设备地址，可选参数
    acct_session_id: 用户会话 ID，与接入设备会话 ID 对应，可选参数
    framed_ipaddr: 用户 IP 地址，可选参数
    mac_addr: 用户 MAC 地址，可选参数
    nas_id: 接入设备标识码，接入设备唯一标识，可选参数
    apikey: 服务商 apikey，接口调用时传递，必选属性
    timestamp: 消息时间戳，必选参数
    page: 分页查询的第几页
    page_size: 分页大小，默认15
    sign: 使用与 apikey 对应的 apisecret 签名生成，必选参数

#### 响应

    total: 总记录条数

    {
    "nonce": "1469093478",
    "code": 0,
    "page_size": 20,
    "sign": "4079E56AF7546064A11D79164568A8BE",
    "msg": "ok",
    "total": 1,
    "data": [
      {
        "username": "test01",
        "acct_input_total": 0,
        "mac_addr": "54:26:96:D1:B7:F7",
        "framed_ipaddr": "172.16.79.99",
        "isp_code": "1234567890123456",
        "nas_class": "",
        "acct_output_packets": 0,
        "nas_addr": "192.168.88.1",
        "nas_port_id": "bridge-local",
        "nas_port_type": 15,
        "session_timeout": 0,
        "acct_output_total": 0,
        "acct_session_id": "81700000",
        "nas_port": 15728640,
        "acct_terminate_cause": 0,
        "acct_start_time": "2016-07-21 17:31:05",
        "nas_id": "toughac",
        "acct_input_packets": 0,
        "_id": "5790965942e0f20001cbe5ae",
        "acct_session_time": 0,
        "framed_netmask": ""
      }
    ],
    "page": 1
    }