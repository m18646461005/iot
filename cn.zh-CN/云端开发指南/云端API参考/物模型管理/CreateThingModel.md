# CreateThingModel

调用该接口为指定产品的物模型新增功能，支持同时新增物模型扩展描述。

## 限制说明

-   单次调用最多可新增10个功能，即新增属性、服务和事件的数量总计不超过10。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=CreateThingModel&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateThingModel|系统规定参数。取值：CreateThingModel。 |
|ProductKey|String|是|a1BwAGV\*\*\*\*|产品的**ProductKey**。

 可以在物联网平台控制台产品页查看，或调用[QueryProductList](~~69271~~)查看ProductKey的取值。 |
|ThingModelJson|String|是|\{ "properties":\[ \{ "identifier": "SimCardType", "extendConfig":"\{...\}", "dataSpecs": \{ "max": "1", "dataType": "INT", "unit": "mmHg", "min": "0", "step": "1" \}, "std": false, "custom": true, "dataType": "INT", "rwFlag": "READ\_ONLY", "productKey": "a1bPo9p\*\*\*\*", "required": false, "customFlag": true, "name": "sim卡类型" \} \]， "services":\[...\], "events":\[...\] \}|新增的功能定义详情。

 **说明：** 最多能包含10个功能的定义信息。

 在**ThingModelJson**每个**property**结构中，可以使用**extendConfig**来描述扩展物模型的数据。更多信息，请参见[ThingModelJson数据说明](~~150457~~)。 |
|IotInstanceId|String|否|iot-cn-0pp1n8t\*\*\*\*|实例ID。公共实例不传此参数，企业版企业实例需传入。 |

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
https://iot.cn-shanghai.aliyuncs.com/?Action=CreateThingModel
&ProductKey=a1bPo9p****
&ThingModelJson={"properties":[{"identifier": "SimCardType","dataSpecs": {"max": "1", "dataType": "INT","unit": "mmHg","min": "0","step": "1"},"std": false,"custom": true,"dataType": "INT","rwFlag": "READ_ONLY","productKey": "a1bPo9p****","required": false,"customFlag": true, "name": "sim卡类型"}]}
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CreateThingModelResponse>
  <RequestId>9E76053E-26ED-4AB4-AE58-8AFC3F1E7E8E</RequestId>
  <Success>true</Success>
</CreateThingModelResponse>
```

`JSON` 格式

```
{
  "RequestId": "9E76053E-26ED-4AB4-AE58-8AFC3F1E7E8E",
  "Success": true
}
```

