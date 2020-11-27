# Pub

调用该接口通过自定义Topic向指定设备发布消息。

## 限制说明

-   不支持使用Pub接口下发设置属性和调用服务的指令。设置属性，请使用[SetDeviceProperty](~~69579~~)或[SetDevicesProperty](~~96243~~)；调用服务，请使用[InvokeThingService](~~69584~~)或[InvokeThingsService](~~96242~~)。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为1600。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=Pub&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|Pub|系统规定参数。取值：Pub。 |
|MessageContent|String|是|aGVsbG8gd29ybGQ%3D|要发送的消息主体。

 您需要将消息原文转换成二进制数据，并进行Base64编码，从而生成消息主体。 |
|ProductKey|String|是|a1Q5XoY\*\*\*\*|要接收消息的产品**ProductKey**。 |
|TopicFullName|String|是|/a1Q5XoY\*\*\*\*/device1/user/get|要接收消息的设备的自定义Topic。自定义Topic的格式为`/${productKey}/${deviceName}/user/${TopicShortName}`。

 **说明：** 指定Topic的操作权限须为订阅，或发布和订阅，且设备已订阅该Topic。

 您可以在产品详情页的**Topic类列表**页签下，或调用[QueryProductTopic](~~69647~~)接口查询产品下的自定义Topic，或在设备详情页的**Topic列表**页签下查看设备已订阅的自定义Topic。 |
|IotInstanceId|String|否|iot-cn-0pp1n8t\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|Qos|Integer|否|0|指定消息的发送方式。取值：

 -   **0**：最多发送一次。
-   **1**：最少发送一次。

 如果不传入此参数，则使用默认值**0**。

 **说明：** QoS=1的消息在物联网平台中最多可以保存7天。物联网平台不保存QoS=0的消息。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|MessageId|String|889455942124347329|成功发送消息后，云端生成的消息ID，用于标识该消息。 |
|RequestId|String|BB71E443-4447-4024-A000-EDE09922891E|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=Pub
&ProductKey=a1Q5XoY****
&TopicFullName=/a1Q5XoY****/device1/user/get
&MessageContent=aGVsbG8gd29ybGQ%3D
&Qos=0
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<PubResponse>
    <RequestId>BB71E443-4447-4024-A000-EDE09922891E</RequestId>
    <Success>true</Success>
    <MessageId>889455942124347329</MessageId>
</PubResponse>
```

`JSON` 格式

```
{
      "RequestId":"BB71E443-4447-4024-A000-EDE09922891E",
      "Success":true,
      "MessageId":889455942124347329
  }
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。

