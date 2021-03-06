# QueryThingModelPublished

调用该接口查看指定产品的已发布物模型中的功能定义详情。

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryThingModelPublished&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryThingModelPublished|系统规定参数。取值：QueryThingModelPublished。 |
|ProductKey|String|是|a1BwAGV\*\*\*\*|产品的ProductKey。 |
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
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Struct| |返回数据。 |
|ThingModelJson|String|\{\\"\_ppk\\":\{\\"version\\":\\"1594253010934\\"\},\\"events\\":\[\],\\"productKey\\":\\"a1BwAGV\*\*\*\*\\",\\"properties\\":\[\{\\"configCode\\":\\"8C03F0EEC63D4897BF2637F89AE36B011594227294067\\",\\"custom\\":true,\\"customFlag\\":true,\\"dataSpecs\\":\{\\"custom\\":true,\\"dataType\\":\\"INT\\",\\"max\\":\\"1\\",\\"min\\":\\"0\\",\\"step\\":\\"1\\",\\"unit\\":\\"ppb\\"\},\\"dataType\\":\\"INT\\",\\"description\\":\\"1\\",\\"extendConfig\\":\\"\{\\\\\\"originalDataType\\\\\\":\{\\\\\\"specs\\\\\\":\{\\\\\\"registerCount\\\\\\":1,\\\\\\"reverseRegister\\\\\\":0,\\\\\\"swap16\\\\\\":0\},\\\\\\"type\\\\\\":\\\\\\"bool\\\\\\"\},\\\\\\"identifier\\\\\\":\\\\\\"WakeUpData\\\\\\",\\\\\\"registerAddress\\\\\\":\\\\\\"0x04\\\\\\",\\\\\\"scaling\\\\\\":1,\\\\\\"writeFunctionCode\\\\\\":0,\\\\\\"operateType\\\\\\":\\\\\\"inputStatus\\\\\\",\\\\\\"pollingTime\\\\\\":1000,\\\\\\"trigger\\\\\\":1\}\\",\\"identifier\\":\\"WakeUpData\\",\\"name\\":\\"唤醒数据\\",\\"productKey\\":\\"a114xeJGj2p\\",\\"required\\":false,\\"rwFlag\\":\\"READ\_ONLY\\",\\"std\\":false\}\],\\"services\\":\[\]\}|物模型的功能定义。ThingModelJson取值的数据格式说明，请参见[ThingModelJson数据说明](~~150457~~)。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|ProductKey|String|a1BwAGV\*\*\*\*|产品的ProductKey。 |
|RequestId|String|E4C0FF92-2A86-41DB-92D3-73B60310D25E|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryThingModelPublished
&ProductKey=a1BwAGV****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryThingModelPublishedResponse>
    <RequestId>1F9041A2-ED5B-4A5A-9C44-598E28C0B434</RequestId>
    <Data>
        <ThingModelJson>{"_ppk":{"version":"1594253010934"},"events":[],"productKey":"a1BwAGV****","properties":[{"configCode":"8C03F0EEC63D4897BF2637F89AE36B011594227294067","custom":true,"customFlag":true,"dataSpecs":{"custom":true,"dataType":"INT","max":"1","min":"0","step":"1","unit":"ppb"},"dataType":"INT","description":"1","extendConfig":"{\"originalDataType\":{\"specs\":{\"registerCount\":1,\"reverseRegister\":0,\"swap16\":0},\"type\":\"bool\"},\"identifier\":\"WakeUpData\",\"registerAddress\":\"0x04\",\"scaling\":1,\"writeFunctionCode\":0,\"operateType\":\"inputStatus\",\"pollingTime\":1000,\"trigger\":1}","identifier":"WakeUpData","name":"唤醒数据","productKey":"a114xeJ****","required":false,"rwFlag":"READ_ONLY","std":false}],"services":[]}</ThingModelJson>
    </Data>
    <Success>true</Success>
</QueryThingModelPublishedResponse>
```

`JSON` 格式

```
{
   "RequestId": "1F9041A2-ED5B-4A5A-9C44-598E28C0B434",
   "Data": {
      "ThingModelJson": "{\"_ppk\":{\"version\":\"1594253010934\"},\"events\":[],\"productKey\":\"a1BwAGV****\",\"properties\":[{\"configCode\":\"8C03F0EEC63D4897BF2637F89AE36B011594227294067\",\"custom\":true,\"customFlag\":true,\"dataSpecs\":{\"custom\":true,\"dataType\":\"INT\",\"max\":\"1\",\"min\":\"0\",\"step\":\"1\",\"unit\":\"ppb\"},\"dataType\":\"INT\",\"description\":\"1\",\"extendConfig\":\"{\\\"originalDataType\\\":{\\\"specs\\\":{\\\"registerCount\\\":1,\\\"reverseRegister\\\":0,\\\"swap16\\\":0},\\\"type\\\":\\\"bool\\\"},\\\"identifier\\\":\\\"WakeUpData\\\",\\\"registerAddress\\\":\\\"0x04\\\",\\\"scaling\\\":1,\\\"writeFunctionCode\\\":0,\\\"operateType\\\":\\\"inputStatus\\\",\\\"pollingTime\\\":1000,\\\"trigger\\\":1}\",\"identifier\":\"WakeUpData\",\"name\":\"唤醒数据\",\"productKey\":\"a114xeJGj2p\",\"required\":false,\"rwFlag\":\"READ_ONLY\",\"std\":false}],\"services\":[]}"
   },
   "Success": true
}
```

