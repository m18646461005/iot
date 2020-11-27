# InvokeThingService

调用该接口在一个设备上调用指定服务。

## 限制说明

-   如果同步调用服务，最大超时时间为5秒。若5秒内服务器未收到回复，则返回超时错误；如果异步调用服务，则无最大超时时间限制。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为500。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=InvokeThingService&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|InvokeThingService|系统规定参数。取值：InvokeThingService。 |
|Args|String|是|\{"param1":1\}|要启用服务的入参信息，数据格式为JSON String，例如**Args=\{"param1":1\}**。

 若此参数为空时，需传入 **Args=\{\}** 。 |
|Identifier|String|是|Set|服务的标识符。设备的服务Identifier，可在控制台中，设备所属的产品的**功能定义**中查看；或调用[QueryThingModel](~~150321~~)，从返回的物模型信息中查看。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|IotId|String|否|Q7uOhVRdZRRlDnTLv\*\*\*\*00100|要调用服务的设备ID。物联网平台为该设备颁发的ID，设备的唯一标识符。

 **说明：** 如果传入该参数，则无需传入**ProductKey**和**DeviceName**。**IotId**作为设备唯一标识符，和**ProductKey**与**DeviceName**组合是一一对应的关系。

 如果您同时传入**IotId**和**ProductKey**与**DeviceName**组合，则以**IotId**为准。 |
|ProductKey|String|否|a1BwAGV\*\*\*\*|要调用服务的设备所隶属的产品ProductKey。

 **说明：** 如果传入该参数，需同时传入**DeviceName**。 |
|DeviceName|String|否|light|要调用服务的设备所隶属的产品DeviceName。

 **说明：** 如果传入该参数，需同时传入**ProductKey**。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Struct| |调用成功时，返回的数据。 |
|MessageId|String|abcabcabc1234\*\*\*\*|云端向设备下发服务调用的消息ID。 |
|Result|String|\{"param1":1\}|同步调用服务，返回的调用结果。

 异步调用服务，不返回此参数。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=InvokeThingService
&ProductKey=a1BwAGV****
&DeviceName=device1
&Identifier=service1
&Args=%7B%22param1%22%3A1%7D
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<InvokeThingServiceResponse>
  <Data>
        <Result>{"code":200,"data":{},"id":"100686","message":"success","version":"1.0"}</Result>
        <MessageId>abcabc123</MessageId>
  </Data>
  <RequestId>A44C818E-FA7F-4765-B1E7-01D14AE01C6A</RequestId>
  <Success>true</Success>
</InvokeThingServiceResponse>
```

`JSON` 格式

```
{
  "Data": {
    "Result": "{\"code\":200,\"data\":{},\"id\":\"100686\",\"message\":\"success\",\"version\":\"1.0\"}", 
    "MessageId": "abcabc123"
  }, 
  "RequestId": "A44C818E-FA7F-4765-B1E7-01D14AE01C6A", 
  "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。

