# ImportThingModelTsl

调用该接口为指定产品导入物模型。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=ImportThingModelTsl&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ImportThingModelTsl|系统规定参数。取值：ImportThingModelTsl。 |
|ProductKey|String|是|a1BwAGV\*\*\*\*|产品的ProductKey。

 可以在物联网平台控制台产品页查看，或调用[QueryProductList](~~69271~~)查看ProductKey的取值。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|ResourceGroupId|String|否|rg-acfm4l5tcwd\*\*\*\*|资源组ID。

 **说明：** 目前不传入此参数。 |
|TslStr|String|否|\{"schema":"https://iotx-tsl.oss-ap-southeast-1.aliyuncs.com/schema.json","profile":\{"productKey":"a14TeW\*\*\*\*"\},"properties":\[\]\}|您编辑的物模型（TSL）。JSON格式的字符串。产品的物模型（TSL）包含属性、服务和事件的定义。

 **TslStr**格式需为标准的物模型数据格式，请参见[物模型格式](~~73727~~)。

 **说明：** 目前该参数为必填参数，只能通过**TslStr**导入物模型。 |
|TslUrl|String|否|https://iotx-pop-dsl.oss-cn-shanghai.aliyuncs.com/thing/a14TeWI\*\*\*\*/model.json?Expires=1581947119...|物模型数据在对象存储（OSS）上的存储地址URI。

 **说明：** 目前该参数暂时无效，请传入**TslStr**导入物模型。 |

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
https://iot.cn-shanghai.aliyuncs.com/?Action=ImportThingModelTsl
&ProductKey=a1lWSUw****
&TslStr={\"profile\":{\"productKey\": \"a1bPo9p****\"},\"services\":[],\"properties\":[],\"events\":[]}
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ImportThingModelTslResponse>
  <RequestId>9E76053E-26ED-4AB4-AE58-8AFC3F1E7E8E</RequestId>
  <Success>true</Success>
</ImportThingModelTslResponse>
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

