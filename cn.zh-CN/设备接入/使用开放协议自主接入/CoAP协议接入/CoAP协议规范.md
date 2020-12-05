---
keyword: [CoAP, RFC 7252, 物联网, DTLS v1.2, UDP协议, IoT, 物联网平台, 设备连接]
---

# CoAP协议规范

本文介绍物联网平台支持的CoAP协议规范。

## 协议版本

支持 RFC 7252 Constrained Application Protocol协议，更多信息，请参见[RFC 7252](http://tools.ietf.org/html/rfc7252)。

## 通道安全

使用 DTLS v1.2保证通道安全，更多信息，请参见[DTLS v1.2](https://tools.ietf.org/html/rfc6347)。

## 开源客户端

[coap technology](https://coap.technology/impls.html)。

**说明：** 若使用第三方代码，阿里云不提供技术支持。

## 限制

-   仅华东2（上海）、华北2（北京）、华南1（深圳）地域支持CoAP通信。
-   暂时不支持资源发现。
-   仅支持UDP协议，目前支持DTLS和对称加密两种安全模式。

## 说明

-   URI规范，CoAP的URI资源和MQTT Topic保持一致，请参见[MQTT协议规范](/cn.zh-CN/设备接入/使用开放协议自主接入/MQTT协议接入/MQTT协议规范.md)。
-   Topic规范和MQTT Topic一致，CoAP协议内 `coap://host:port/topic/${topic}`接口对于所有`${topic}`和MQTT Topic可以复用。
-   客户端缓存认证返回的token是请求的令牌。
-   传输的数据大小依赖于MTU的大小，建议在1 KB以内。
-   如设备在10分钟内使用CoAP协议上报过数据，则设备在物联网平台控制台显示为在线状态。

