# QueryThingModelExtendConfig

调用接口导出指定产品的物模型扩展描述配置。

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为20。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryThingModelExtendConfig&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryThingModelExtendConfig|系统规定参数。取值：QueryThingModelExtendConfig。 |
|ProductKey|String|是|a1T27vz\*\*\*\*|产品的ProductKey。 |
|IotInstanceId|String|否|iot-cn-0pp1n8t\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|ResourceGroupId|String|否|rg-acfm4l5tcwd\*\*\*\*|资源组ID。

 **说明：** 目前不传入此参数。 |
|ModelVersion|String|否|v1.0.0|物模型版本号。

 可调用[ListThingModelVersion](~~150318~~)查看产品下的物模型版本号。

 为空时返回已发布的最新版本。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|Data|Struct| |调用成功时，返回的数据。 |
|Configuration|String|\{\\"profile\\":\{\\"productKey\\":\\"a114x\*\*\*\*\*\*\\"\},\\"properties\\":\[\{\\"originalDataType\\":\{\\"specs\\":\{\\"registerCount\\":1,\\"reverseRegister\\":0,\\"swap16\\":0\},\\"type\\":\\"bool\\"\},\\"identifier\\":\\"WakeUpData\\",\\"registerAddress\\":\\"0x04\\",\\"scaling\\":1,\\"writeFunctionCode\\":0,\\"operateType\\":\\"inputStatus\\",\\"pollingTime\\":1000,\\"trigger\\":1\}\]\}|物模型扩展描述配置。参数含义请参见[CreateThingModel](~~150323~~)的extendConfig说明。 |
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryThingModelExtendConfig
&ProductKey=a1T27vz****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryThingModelExtendConfigResponse>
    <Data>
        <Configuration>{"profile":{"productKey":"a114x******"},"properties":[{"originalDataType":{"specs":{"registerCount":1,"reverseRegister":0,"swap16":0},"type":"bool"},"identifier":"WakeUpData","registerAddress":"0x04","scaling":1,"writeFunctionCode":0,"operateType":"inputStatus","pollingTime":1000,"trigger":1}]}</Configuration>
    </Data>
    <RequestId>6DDF9D04-24C3-40D8-B490-2A528E59EA67</RequestId>
    <Success>true</Success>
</QueryThingModelExtendConfigResponse>
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

