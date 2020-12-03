---
keyword: [IoT, 物联网平台, AMQP, 服务端订阅设备消息, Rhea, Node.js]
---

# Node.js SDK接入示例

本文介绍使用Node.js语言的AMQP SDK接入阿里云物联网平台，接收服务端订阅消息的示例。

## 开发环境

本示例所使用的开发环境为Node.js 8.0.0及以上版本。

## 下载SDK

Node.js版本AMQP SDK，推荐使用rhea。请访问[rhea](https://github.com/amqp/rhea)下载库和查看使用说明。

## 添加依赖

在package.json中添加以下依赖。

```
"dependencies": {
    "rhea": "^1.0.12"
 }
```

## 代码示例

以下Demo中涉及的参数说明，请参见[AMQP客户端接入说明](/cn.zh-CN/消息通信/服务端订阅/使用AMQP服务端订阅/AMQP客户端接入说明.md)。

```
const container = require('rhea');
const crypto = require('crypto');

//创建Connection。
var connection = container.connect({
    //接入域名，请参见AMQP客户端接入说明文档。
    'host': '${YourHost}',
    'port': 5671,
    'transport':'tls',
    'reconnect':true,
    'idle_time_out':60000,
    //userName组装方法，请参见AMQP客户端接入说明文档。其中的iotInstanceId，企业版实例请填写实例ID，公共实例直接删除${YourIotInstanceId}。
    'username':'${YourClientId}|authMode=aksign,signMethod=hmacsha1,timestamp=1573489088171,authId=${YourAccessKeyId},iotInstanceId=${YourIotInstanceId},consumerGroupId=${YourConsumerGroupId}|', 
    //计算签名，password组装方法，请参见AMQP客户端接入说明文档。
    'password': hmacSha1('${YourAccessKeySecret}', 'authId=${YourAccessKeyId}&timestamp=1573489088171'),
});

//创建Receiver Link。
var receiver = connection.open_receiver();

//接收云端推送消息的回调函数。
container.on('message', function (context) {
    var msg = context.message;
    var messageId = msg.message_id;
    var topic = msg.application_properties.topic;
    var content = Buffer.from(msg.body.content).toString();

    // 输出内容。
    console.log(content);

    //发送ACK，注意不要在回调函数有耗时逻辑。
    context.delivery.accept();
});

//计算password签名。
function hmacSha1(key, context) {
    return Buffer.from(crypto.createHmac('sha1', key).update(context).digest())
        .toString('base64');
}
```

