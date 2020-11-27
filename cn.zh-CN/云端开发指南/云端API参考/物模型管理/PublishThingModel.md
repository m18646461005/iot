# PublishThingModel

调用该接口发布指定产品的物模型。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=PublishThingModel&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|PublishThingModel|系统规定参数。取值：PublishThingModel。 |
|ProductKey|String|是|a1BwAGV\*\*\*\*|产品的ProductKey。

 可以在物联网平台控制台产品页查看，或调用[QueryProductList](~~69271~~)查看ProductKey的取值。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|ResourceGroupId|String|否|rg-acfm4l5tcwd\*\*\*\*|资源组ID。

 **说明：** 目前不传入此参数。 |
|ModelVersion|String|否|v1.0.0|设置物模型的版本号。

 版本号支持英文大、小字母、数字和点号（.），长度范围：1个～16个字符。 |
|Description|String|否|第二版|物模型版本的描述。 |

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
https://iot.cn-shanghai.aliyuncs.com/?Action=PublishThingModel
&ProductKeySource=a1rYuVF****
&ModelVersion=V1.0.0
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<PublishThingModelResponse>
  <RequestId>5252CC6E-9E4B-4DB1-B1D8-7EEA190A5B3E</RequestId>
  <Success>true</Success>
</PublishThingModelResponse>
```

`JSON` 格式

```
{
  "RequestId": "5252CC6E-9E4B-4DB1-B1D8-7EEA190A5B3E",
  "Success": true
}
```

