# 基于IPv6的MQTT连接通信

物联网平台支持设备端使用基于IPv6协议的MQTT通道接入物联网平台。

-   目前，仅华东2（上海）地域支持基于IPv6协议的MQTT通道。
-   环境验证测试时，请使用以下域名和端口，通过MQTT直连方式接入物联网平台。

    测试环境使用域名：`ipv6.itls.cn-shanghai.aliyuncs.com`

    端口：1883

    传输加密：TLSv1.2

    **说明：** 请勿将测试域名用于正式使用场景。


## 设备端接入物联网平台

正式环境中，设备端必须通过产品对应的正式MQTT连接域名接入物联网平台。

1.  登录[工单系统](https://selfservice.console.aliyun.com/ticket/createIndex)，提交工单，申请开通产品对应的正式MQTT连接域名的AAAA记录。

    产品对应的正式MQTT连接域名：`${YourProductKey}.iot-as-mqtt.cn-shanghai.aliyuncs.com`。请将$\{YourProductKey\}替换为您的产品的PorductKey。

2.  下载用于TLS加密的[根证书](http://aliyun-iot.oss-cn-hangzhou.aliyuncs.com/cert_pub/root.crt)。

3.  开发设备端，配置MQTT连接。

    建议您使用阿里云提供的设备端SDK接入物联网平台。如果您自行开发设备端，签名时，请参见[MQTT连接签名示例](/cn.zh-CN/设备接入/使用开放协议自主接入/MQTT协议接入/MQTT连接签名示例.md)。

    需配置的信息如下表。

    |字段|具体信息|
    |--|----|
    |连接域名和端口|`${YourProductKey}.iot-as-mqtt.cn-shanghai.aliyuncs.com:1883`请将$\{YourProductKey\}替换为您的产品的PorductKey。 |
    |可变报头（variable header）：Keep Alive|CONNECT指令中需包含Keep Alive（保活时间）。保活心跳时间取值范围为30至1200秒。如果心跳时间不在此区间内，物联网平台会拒绝连接。建议取值300秒以上。如果网络不稳定，将心跳时间设置高一些。|
    |MQTT的CONNECT报文参数|    ```
mqttClientId: clientId+"|securemode=3,signmethod=hmacsha1,timestamp=132323232|"
mqttUsername: deviceName+"&"+productKey
mqttPassword: sign_hmac(deviceSecret,content)
    ```

mqttPassword：sign签名需把提交给服务器的参数按字典排序后，根据signmethod加签。

content的值为提交给服务器的参数（ProductKey、DeviceName、timestamp和clientId），按照字母顺序排序， 然后将参数值依次拼接。

    -   clientId：表示客户端ID，建议使用设备的MAC地址或SN码，64字符内。
    -   timestamp：表示当前时间毫秒值，可以不传递。
    -   mqttClientId：格式中`||`内为扩展参数。
    -   signmethod：表示签名算法类型。支持hmacmd5，hmacsha1和hmacsha256，默认为hmacmd5。
    -   securemode：表示目前安全模式，可选值有2 （TLS直连模式）和3（TCP直连模式）。
示例：

假设`clientId = 12345，deviceName = device， productKey = pk， timestamp = 789，signmethod=hmacsha1，deviceSecret=secret`，那么使用TCP方式提交给MQTT的参数如下：

    ```
mqttclientId=12345|securemode=3,signmethod=hmacsha1,timestamp=789|
mqttUsername=device&pk
mqttPassword=hmacsha1("secret","clientId12345deviceNamedeviceproductKeypktimestamp789").toHexString(); 
    ```

加密后的Password为二进制转16制字符串，示例结果为：

    ```
FAFD82A3D602B37FB0FA8B7892F24A477F85****
    ``` |


更多关于MQTT-TCP连接信息，请参见[MQTT-TCP连接通信](/cn.zh-CN/设备接入/使用开放协议自主接入/MQTT协议接入/MQTT-TCP连接通信.md)。

