# BatchPub

调用该接口通过自定义Topic，向指定产品下的多个设备，批量发送消息。

## 使用说明

-   该接口目前仅支持白名单用户使用，如需使用请先提交工单反馈。
-   单批次最多向同一产品下的100个设备发送消息。
-   不支持使用BatchPub接口下发设置属性和调用服务的指令。设置属性，请使用接口[SetDeviceProperty](~~69579~~)或[SetDevicesProperty](~~96243~~)；调用服务，请使用接口[InvokeThingService](~~69584~~)或[InvokeThingsService](~~96242~~)。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为50。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=BatchPub&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|BatchPub|系统规定参数。取值：BatchPub。 |
|DeviceName.N|RepeatList|是|newdevice1|要接收消息的设备名称。

 **说明：**

-   与**ProductKey**结合使用，传入设备必须属于同一产品。
-   单次调用，最多传入100个设备名称。 |
|MessageContent|String|是|aGVsbG8gd29ybGQ%3D|要发送的消息主体。最大报文256 KB。

 您需要将消息原文转换成二进制数据，并进行Base64编码，从而生成消息主体。 |
|ProductKey|String|是|a1BwAGV\*\*\*\*|要发送消息的产品**ProductKey**。 |
|TopicShortName|String|是|get|自定义Topic的后缀。

 自定义Topic的格式为`/${productKey}/${deviceName}/user/${TopicShortName}`，传入后缀$\{TopicShortName\}。

 **说明：** 指定Topic的操作权限须为订阅，或发布和订阅，且所有设备已订阅该Topic。

 您可通过以下途径查看自定义Topic：

 -   在产品详情页的**Topic类列表**页签下，查看产品下的自定义Topic。
-   在设备详情页的**Topic列表**页签下，查看设备已订阅的自定义Topic。
-   调用[QueryProductTopic](~~69647~~)接口查询产品下的自定义Topic。 |
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
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=BatchPub
&DeviceName.1=newdevice1
&MessageContent=aGVsbG8gd29ybGQ%3D
&ProductKey=a1BwAGV****
&TopicShortName=get
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<BatchPubResponse>
  <RequestId>9E76053E-26ED-4AB4-AE58-8AFC3F1E7E8E</RequestId>
  <Success>true</Success>
</BatchPubResponse>
```

`JSON` 格式

```
{
  "RequestId": "9E76053E-26ED-4AB4-AE58-8AFC3F1E7E8E",
  "Success": true
}
```

