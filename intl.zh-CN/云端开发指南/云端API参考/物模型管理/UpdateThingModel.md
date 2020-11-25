# UpdateThingModel

调用接口更新指定产品物模型中的单个功能，支持同步更新物模型的扩展描述。

## 限制说明

-   单次调用最多可更新1个功能，即更新1个属性、服务或事件的定义信息。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=UpdateThingModel&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UpdateThingModel|系统规定参数。取值：UpdateThingModel。 |
|Identifier|String|是|Temperature|功能的标识符。

 更新某个功能，需传入该功能原有的标识符。可调用[GetThingModelTsl](~~150319~~)，从返回参数TslStr中查看具体功能的identifier。 |
|ProductKey|String|是|a1BwAGV\*\*\*\*|产品的**ProductKey**。

 可以在物联网平台控制台产品页查看，或调用[QueryProductList](~~69271~~)查看ProductKey的取值。 |
|ThingModelJson|String|是|\{ "properties":\[ \{ "identifier": "SimCardType", "extendConfig":"\{...\}", "dataSpecs": \{ "max": "1", "dataType": "INT", "unit": "mmHg", "min": "0", "step": "1" \}, "std": false, "custom": true, "dataType": "INT", "rwFlag": "READ\_ONLY", "productKey": "a1Jw4i\*\*\*\*", "required": false, "customFlag": true, "name": "sim卡类型" \} \] \}|新的功能定义详情。

 **说明：** 最多能包含1个功能的定义信息。

 ThingModelJson的编写指导，请参见[ThingModelJson数据说明](~~150457~~)。 |
|IotInstanceId|String|否|iot-cn-0pp1n8t\*\*\*\*|实例ID。公共实例不传此参数；您购买的企业实例需传入此参数。 |

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
https://iot.cn-shanghai.aliyuncs.com/?Action=UpdateThingModel
&ProductKey=a1Jw4id****
&ThingModelJson={"properties":[{"identifier": "SimCardType","dataSpecs": {"max": "1", "dataType": "INT","unit": "mmHg","min": "0","step": "1"},"std": false,"custom": true,"dataType": "INT","rwFlag": "READ_ONLY","productKey": "a1Jw4id****","required": false,"customFlag": true, "name": "sim卡类型"}]}
&Identifier=SimCardType
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<UpdateThingModelResponse>
  <RequestId>5573D217-8E3E-47AD-9331-2083B88E64B2</RequestId>
  <Success>true</Success>
</UpdateThingModelResponse>
```

`JSON` 格式

```
{
  "RequestId": "5573D217-8E3E-47AD-9331-2083B88E64B2",
  "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。

