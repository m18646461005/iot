# CopyThingModel

调用该接口复制指定产品的物模型到目标产品。

## 限制说明

-   目标产品和物模型源产品的品类（**CategoryKey**）必须相同。调用[QueryProduct](~~69272~~)，从返回结果中可查看产品的**CategoryKey**。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=CopyThingModel&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CopyThingModel|系统规定参数。取值：CopyThingModel。 |
|SourceProductKey|String|是|a1BwAGV\*\*\*\*|要复制的物模型所属产品的ProductKey。

 可以在物联网平台控制台产品页查看，或调用[QueryProductList](~~69271~~)查看ProductKey的取值。 |
|TargetProductKey|String|是|a1BwwG0\*\*\*\*|目标产品的ProductKey。

 可以在物联网平台控制台产品页查看，或调用[QueryProductList](~~69271~~)查看ProductKey的取值。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|ResourceGroupId|String|否|rg-acfm4l5tcwd\*\*\*\*|资源组ID。

 **说明：** 目前不传入此参数。 |
|SourceModelVersion|String|否|V1.0.0|要复制的物模型版本号。

 可以调用[ListThingModelVersion](~~150318~~)，查看源物模型的版本号。 |

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
https://iot.cn-shanghai.aliyuncs.com/?Action=CopyThingModel
&ProductKeySource=a1rYuVF****
&ProductKeyTarget=a1bPo9p****
&SourceModelVersion=v1.0.0
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CopyThingModelResponse>
  <RequestId>9E76053E-26ED-4AB4-AE58-8AFC3F1E7E8E</RequestId>
  <Success>true</Success>
</CopyThingModelResponse>
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

