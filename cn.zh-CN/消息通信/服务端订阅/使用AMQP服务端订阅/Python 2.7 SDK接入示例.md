---
keyword: [IoT, 物联网平台, AMQP, 服务端订阅设备消息, Apache qpid-proton, Python SDK]
---

# Python 2.7 SDK接入示例

本文介绍使用Python 2.7 SDK接入阿里云物联网平台，接收服务端订阅消息的示例。

## 开发环境

本示例所使用的开发环境为Python 2.7版。

## 下载SDK

Python语言的AMQP SDK，推荐使用Apache Qpid Proton 0.29.0。该库中已封装了Python API。请访问[Qpid Proton 0.29.0](https://qpid.apache.org/releases/qpid-proton-0.29.0/index.html)下载库和查看使用说明。

安装Proton。安装操作指导，请参见[Installing Qpid Proton](https://github.com/apache/qpid-proton/blob/master/INSTALL.md)。

安装完成后，通过以下Python命令查看SSL库是否安装成功。

```
import proton;print('%s' % 'SSL present' if proton.SSL.present() else 'SSL NOT AVAILABLE')
```

## 代码示例

以下Demo中涉及的参数说明，请参见[AMQP客户端接入说明](/cn.zh-CN/消息通信/服务端订阅/使用AMQP服务端订阅/AMQP客户端接入说明.md)。

```
# encoding=utf-8
import sys
import logging
import time
from proton.handlers import MessagingHandler
from proton.reactor import Container
import hashlib
import hmac
import base64

reload(sys)
sys.setdefaultencoding('utf-8')
logging.basicConfig(level=logging.INFO, format='%(asctime)s - %(name)s - %(levelname)s - %(message)s')
logger = logging.getLogger(__name__)
console_handler = logging.StreamHandler(sys.stdout)


def current_time_millis():
    return str(int(round(time.time() * 1000)))


def do_sign(secret, sign_content):
    m = hmac.new(secret, sign_content, digestmod=hashlib.sha1)
    return base64.b64encode(m.digest())


class AmqpClient(MessagingHandler):
    def __init__(self):
        super(AmqpClient, self).__init__()

    def on_start(self, event):
        # 接入域名，请参见AMQP客户端接入说明文档。
        url = "amqps://${YourHost}:5671"
        accessKey = "${YourAccessKeyID}"
        accessSecret = "${YourAccessKeySecret}"
        consumerGroupId = "${YourConsumerGroupId}"
        clientId = "${YourClientId}"
        # iotInstanceId：企业版实例请填写实例ID，公共实例请填空字符串""。
        iotInstanceId = "${YourIotInstanceId}"
        # 签名方法：支持hmacmd5，hmacsha1和hmacsha256。
        signMethod = "hmacsha1"
        timestamp = current_time_millis()
        # userName组装方法，请参见AMQP客户端接入说明文档。
        userName = clientId + "|authMode=aksign" + ",signMethod=" + signMethod \
                        + ",timestamp=" + timestamp + ",authId=" + accessKey \
                        + ",iotInstanceId=" + iotInstanceId + ",consumerGroupId=" + consumerGroupId + "|"
        signContent = "authId=" + accessKey + "&timestamp=" + timestamp
        # 计算签名，password组装方法，请参见AMQP客户端接入说明文档。
        passWord = do_sign(accessSecret.encode("utf-8"), signContent.encode("utf-8"))
        conn = event.container.connect(url, user=userName, password=passWord, heartbeat=60)
        self.receiver = event.container.create_receiver(conn)

    # 当连接成功建立时被调用。
    def on_connection_opened(self, event):
        logger.info("Connection established, remoteUrl: %s", event.connection.hostname)

    # 当连接关闭时被调用。
    def on_connection_closed(self, event):
        logger.info("Connection closed: %s", self)

    # 当远端因错误而关闭连接时被调用。
    def on_connection_error(self, event):
        logger.info("Connection error")

    # 当建立AMQP连接错误时被调用，包括身份验证错误和套接字错误。
    def on_transport_error(self, event):
        if event.transport.condition:
            if event.transport.condition.info:
                logger.error("%s: %s: %s" % (
                    event.transport.condition.name, event.transport.condition.description,
                    event.transport.condition.info))
            else:
                logger.error("%s: %s" % (event.transport.condition.name, event.transport.condition.description))
        else:
            logging.error("Unspecified transport error")

    # 当收到消息时被调用。
    def on_message(self, event):
        message = event.message
        content = message.body.decode('utf-8')
        topic = message.properties.get("topic")
        message_id = message.properties.get("messageId")
        print("receive message: message_id=%s, topic=%s, content=%s" % (message_id, topic, content))
        event.receiver.flow(1)


Container(AmqpClient()).run()
```

