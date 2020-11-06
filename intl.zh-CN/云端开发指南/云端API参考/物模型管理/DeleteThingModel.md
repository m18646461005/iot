# DeleteThingModel

调用该接口删除指定产品下物模型中的指定功能。

## 限制说明

-   请求参数中，**PropertyIdentifier.N**、**ServiceIdentifier.N**和**EventIdentifier.N**不能同时为空，且最多各传入10个标识符。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

**说明：** RAM账号共享该阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=DeleteThingModel&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteThingModel|系统规定参数。取值：DeleteThingModel。 |
|ProductKey|String|是|a1BwAGV\*\*\*\*|产品的ProductKey。 |
|IotInstanceId|String|否|iot-cn-0pp1n8t\*\*\*\*|实例ID。公共实例不传此参数；您购买的实例需传入。 |
|ResourceGroupId|String|否|rg-acfm4l5tcwd\*\*\*\*|资源组ID。

 **说明：** 目前不传入此参数。 |
|PropertyIdentifier.N|RepeatList|否|Temperature|需要删除的属性标识符列表。最多传入10个属性标识符。 |
|ServiceIdentifier.N|RepeatList|否|Set|需要删除的服务标识符列表。最多传入10个服务标识符。 |
|EventIdentifier.N|RepeatList|否|OfflineAlert|需要删除的事件标识符列表。最多传入10个事件标识符。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。更多信息，请参见 [公共参数文档](~~30561~~)。

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
https://iot.cn-shanghai.aliyuncs.com/?Action=DeleteThingModel
&ProductKeySource=a1rYuVF****
&PropertyIdentifier.1=speed
&ServiceIdentifier.1=SetSpeed
&EventIdentifier.1=SpeedAlarm
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DeleteThingModelResponse>
  <RequestId>9E76053E-26ED-4AB4-AE58-8AFC3F1E7E8E</RequestId>
  <Success>true</Success>
</DeleteThingModelResponse>
```

`JSON` 格式

```
{
  "RequestId": "9E76053E-26ED-4AB4-AE58-8AFC3F1E7E8E",
  "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。

