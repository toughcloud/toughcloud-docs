# RouterOS 对接常见问题

## 如何设置 RouterOS 的 标识(NAS_ID),以便于与硬派云对接？

在 RouterOS 管理菜单 system 下的 Identity 下设置。

![routeros id](http://qnstatic.toughcloud.net/FidLSolX63yg13_ApbmxOIsEc1aT)


## 对接硬派云 Radius 引擎后，认证失败， RouterOS 日志出現 radius timeout 是什么原因？

通常可能的原因是：

- RouterOS 设备与硬派云引擎网络连接不通导致，请检查您的网络。
- 在硬派云计费管理系统中未正确配置接入设备信息，导致设备发送的认证消息被丢弃，无响应，请检查您的接入配置是否正确。
- 如果确认不是以上原因，可以联系硬派云技术支持人员辅助定位。
