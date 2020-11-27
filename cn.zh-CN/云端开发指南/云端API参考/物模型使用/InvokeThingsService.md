# InvokeThingsService

调用该接口批量调用设备服务。

## 使用限制

-   目前只支持异步调用该接口。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享该阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=InvokeThingsService&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|InvokeThingsService|系统规定参数。取值：InvokeThingsService。 |
|Args|String|是|\{"param1":1\}|要启用服务的入参信息，数据格式为JSON String，例如**Args=\{"param1":1\}**。

 若此参数为空时，需传入**Args=\{\}**。 |
|DeviceName.N|RepeatList|是|device1|要调用服务的设备的名称列表。最多支持传入100个设备名称。 |
|Identifier|String|是|Set|服务的标识符。

 设备的服务Identifier，可在控制台中，设备所属产品的**功能定义**中查看；或调用[QueryThingModel](~~150321~~)，从返回的物模型信息中查看。 |
|ProductKey|String|是|a1BwAGV\*\*\*\*|要调用服务的设备所隶属的产品**ProductKey**。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

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
https://iot.cn-shanghai.aliyuncs.com/?Action=InvokeThingsService
&Args=%7B%20%20%20%20%20%22walk%22%3A%22a~z%22%2C%20%20%20%20%20%22city%22%3A%22shanghai%22%20%7D
&DeviceName.1=1102andriod02
&DeviceName.2=1102android01
&Identifier=TimeReset
&ProductKey=a1hWjHD****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<InvokeThingsServiceResponse>
  <RequestId>059C3274-6197-4BEC-95E4-49A076330E57</RequestId>
  <Success>true</Success>
</InvokeThingsServiceResponse>
```

`JSON` 格式

```
{
  "RequestId": "059C3274-6197-4BEC-95E4-49A076330E57",
  "Success": true
}
```

