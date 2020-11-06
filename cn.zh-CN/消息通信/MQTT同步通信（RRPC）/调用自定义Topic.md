---
keyword: [物联网, 物联网平台, IoT, 同步调用, RRPC, 同步获取响应结果, 自定义Topic]
---

# 调用自定义Topic

RRPC支持调用自定义Topic与云端通信，且相关Topic中包含了您自定义的完整的Topic。

支持使用以下Link SDK开发的设备通过自定义Topic与云端通信：

-   [C SDK](https://help.aliyun.com/document_detail/96623.html)
-   [Android SDK](https://help.aliyun.com/document_detail/96607.html)
-   [Node.js SDK](https://help.aliyun.com/document_detail/96618.html)
-   [Python SDK](https://help.aliyun.com/document_detail/98292.html)

## 自定义Topic

RRPC调用自定义Topic的格式如下：

-   RRPC请求消息Topic：`/ext/rrpc/${messageId}/${topic}`
-   RRPC响应消息Topic：`/ext/rrpc/${messageId}/${topic}`
-   RRPC订阅Topic：`/ext/rrpc/+/${topic}`

其中$\{messageId\}是云端生成的唯一的RRPC消息ID，$\{topic\}是您的自定义Topic。

## RRPC接入

1.  云端发送RRPC消息。

    服务端调用云端API的RRpc接口向设备发送消息。更多信息，请参见[RRpc](/cn.zh-CN/云端开发指南/云端API参考/消息通信/RRpc.md)。

    以使用Java SDK为例。

    使用自定义Topic格式时，您需要确保您的云端Java SDK（aliyun-java-sdk-iot）为6.0.0及以上版本。

    ```
    <dependency>
        <groupId>com.aliyun</groupId>
        <artifactId>aliyun-java-sdk-iot</artifactId>
        <version>6.0.0</version>
    </dependency>
    ```

    调用RRpc接口的示例：

    ```
    RRpcRequest request = new RRpcRequest();
    request.setProductKey("testProductKey");
    request.setDeviceName("testDeviceName");
    request.setRequestBase64Byte(Base64.getEncoder().encodeToString("hello world"));
    request.setTopic("/testProductKey/testDeviceName/user/get");//如果是自定义Topic调用方式，在这里传递自定义Topic。
    request.setTimeout(3000);
    RRpcResponse response = client.getAcsResponse(request);
    ```

    **说明：** 请登录 [OpenAPI Explorer](https://api.aliyun.com/)，在线调用RRpc接口，便可查看多种语言云端SDK调用示例。

2.  设备端接入。

    -   对于使用Node.js SDK的设备，需要在开发设备前，将SDK下载到本地，修改src文件夹中的model.js文件，在genConnectPrarms函数中的clientId中添加`ext=1`，再使用该SDK进行设备开发。

        原clientId为：

        ```
        clientId:`${this.clientId}|securemode=${this.securemode },signmethod=hmac${this.signAlgorithm},timestamp=${this.timestamp},${extra}`,
        ```

        添加`ext=1`后，clientId为：

        ```
        clientId:`${this.clientId}|securemode=${this.securemode },signmethod=hmac${this.signAlgorithm},timestamp=${this.timestamp},${extra},ext=1`,
        ```

    -   对于使用C SDK、Android SDk、Python SDK的设备，无需做任何特殊操作。
3.  设备端返回RRPC响应的Topic。

    RRPC请求Topic和响应Topic格式一样，直接将请求Topic作为响应Topic即可。

    **说明：** 目前，仅支持设备端返回QoS=0的RRPC响应消息。

    关于如何通过Python语言设备端SDK响应RRPC调用，请参见[RRPC能力](https://help.aliyun.com/document_detail/108172.html)。


