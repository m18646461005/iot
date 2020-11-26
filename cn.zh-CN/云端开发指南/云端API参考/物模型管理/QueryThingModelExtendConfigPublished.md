# QueryThingModelExtendConfigPublished

调用该接口获取已发布物模型的扩展描述配置。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为20。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryThingModelExtendConfigPublished&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryThingModelExtendConfigPublished|系统规定参数。取值：QueryThingModelExtendConfigPublished。 |
|ProductKey|String|是|a1BwAGV\*\*\*\*|产品的**ProductKey**。

 可以在物联网平台控制台产品页查看，或调用[QueryProductList](~~69271~~)查看ProductKey的取值。 |
|IotInstanceId|String|否|iot-cn-0pp1n8t\*\*\*\*|实例ID。公共实例不传此参数；您购买的企业实例需传入此参数。 |
|ModelVersion|String|否|v1.0.0|要获取的物模型版本号。不传入此参数，则返回已发布的最新版本。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Struct| |调用成功时，返回的数据。 |
|Configuration|String|\{\\"profile\\":\{\\"productKey\\":\\"a114x\*\*\*\*\*\*\\"\},\\"properties\\":\[\{\\"originalDataType\\":\{\\"specs\\":\{\\"registerCount\\":1,\\"reverseRegister\\":0,\\"swap16\\":0\},\\"type\\":\\"bool\\"\},\\"identifier\\":\\"WakeUpData\\",\\"registerAddress\\":\\"0x04\\",\\"scaling\\":1,\\"writeFunctionCode\\":0,\\"operateType\\":\\"inputStatus\\",\\"pollingTime\\":1000,\\"trigger\\":1\}\]\}|物模型扩展描述配置。参数含义请参见[CreateThingModel](~~150323~~)的extendConfig说明。

 更多信息，请参见[ThingModelJson数据说明](~~150457~~)。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=QueryThingModelExtendConfigPublished
&ProductKey=a1BwAGV****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryThingModelExtendConfigPublishedResponse>
  <Data>
        <Configuration>{"profile":{"productKey":"a114x******"},"properties":[{"originalDataType":{"specs":{"registerCount":1,"reverseRegister":0,"swap16":0},"type":"bool"},"identifier":"WakeUpData","registerAddress":"0x04","scaling":1,"writeFunctionCode":0,"operateType":"inputStatus","pollingTime":1000,"trigger":1}]}</Configuration>
  </Data>
  <RequestId>6DDF9D04-24C3-40D8-B490-2A528E59EA67</RequestId>
  <Success>true</Success>
</QueryThingModelExtendConfigPublishedResponse>
```

`JSON` 格式

```
{
   "Data": {
      "Configuration": "{\"profile\":{\"productKey\":\"a114x******\"},\"properties\":[{\"originalDataType\":{\"specs\":{\"registerCount\":1,\"reverseRegister\":0,\"swap16\":0},\"type\":\"bool\"},\"identifier\":\"WakeUpData\",\"registerAddress\":\"0x04\",\"scaling\":1,\"writeFunctionCode\":0,\"operateType\":\"inputStatus\",\"pollingTime\":1000,\"trigger\":1}]}"
   },
   "RequestId": "6DDF9D04-24C3-40D8-B490-2A528E59EA67",
   "Success": true
}
```

