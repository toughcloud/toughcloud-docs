# 硬派云 API 接口

本文档描述了硬派云计费系统的接口规范，提供第三方开发者开发参考。第三方系统按此接口规范实现响应功能，完成与硬派云计费系统的对接。

- 硬派云计费系统

硬派云端认证计费引擎，实现了标准的Radius协议，以及支持Radius协议扩展，部署与硬派云端，提供标准 Radius 协议接口，以及 http 数据管理接口。

- 第三方计费系统 

无需实现Radius协议，只需要实现硬派云认证计费引擎接口规范就可以实现AAA功能，可以通过对企业现有ERP，CRM以及其他用户管理系统进行扩展改造，实现对认证计费授权的支持。

## 协议规范

- 协议采用基于http restfull风格的接口调用方式。
- 消息发起方：第三方用户管理系统。
- 消息接受方：硬派云计费系统。
- 接口调用地址：硬派云认证计费引擎平台提供。
- 接口请求方法：HTTP GET/POST，支持标准 HTTP 1.1 协议。
- 消息报文编码：UTF-8
- 接口鉴权：MD5签名，md5(共享密钥+排序的参数值+随机字符串), 签名校验是双向的，消息接收方对请求消息进行签名验证，同时需对结果进行签名返回，消息发起方对响应结果的签名进行验证。


## 签名代码参考

### Python


    from hashlib import md5
    def make_sign(api_secret, params=[]):
        """
            >>> make_sign("testsecret",params={'name':'test','attrname':'attrvalue'}.values())
            '8C3CD49F386485E3C34307E29ABC6877'
        """
        _params = [unicode(p,'utf-8') for p in params if p is not None]
        _params.sort()
        _params.insert(0, api_secret)
        strs = ''.join(_params)
        mds = md5(strs.encode('utf-8')).hexdigest()
        return mds.upper()

    if __name__ == '__main__':
        import doctest
        doctest.testmod()