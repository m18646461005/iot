# SetDeviceProperty

调用该接口为指定设备设置属性值。

## 返回结果说明

因为云端下发属性设置命令和设备收到并执行该命令是异步的，所以调用该接口时，返回的成功结果只表示云端下发属性设置的请求成功，不能保证设备端收到并执行了该请求。需设备端SDK成功响应云端设置设备属性值的请求，设备属性值才能真正设置成功。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为500。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=SetDeviceProperty&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SetDeviceProperty|系统规定参数。取值：SetDeviceProperty。 |
|Items|String|是|\{"Switch":1,"Color":"blue"\}|要设置的属性信息，数据格式为 JSON String。属性组成为**属性标识符key:属性值value**，多个属性用英文逗号隔开。

 例如，设置智能灯的如下两个属性：

 -   标识符为**Switch**的开关属性，数据类型为**Bool**，设置值为**1**（开）；
-   标识符为**Color**的灯颜色属性，数据类型为**String**，设置值为**blue**。

 那么，**Items=\{"Switch":1,"Color":"blue"\}**。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|IotId|String|否|Q7uOhVRdZRRlDnTLv\*\*\*\*00100|设备ID。物联网平台为该设备颁发的ID，设备的唯一标识符。

 **说明：** 如果传入该参数，则无需传入**ProductKey**和**DeviceName**。**IotId**作为设备唯一标识符，和**ProductKey**与**DeviceName**组合是一一对应的关系。如果您同时传入**IotId**和**ProductKey**与**DeviceName**组合，则以**IotId**为准。 |
|DeviceName|String|否|light|设备名称。

 **说明：** 如果传入该参数，需同时传入**ProductKey**。 |
|ProductKey|String|否|a1BwAGV\*\*\*\*|设备所隶属的产品ProductKey。

 **说明：** 如果传入该参数，需同时传入**DeviceName**。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Struct| |调用成功时，返回的数据。 |
|MessageId|String|abcabc123|云端给设备下发属性设置的消息ID。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=SetDeviceProperty
&ProductKey=a1BwAGV****
&DeviceName=device1
&Items=%7B%22LightAdjustLevel%22%3A1%7D
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<SetDevicePropertyResponse>
  <RequestId>57b144cf-09fc-4916-a272-a62902d5b207</RequestId>
  <Success>true</Success>
  <Data>
        <MessageId>abcabc123</MessageId>
  </Data>
</SetDevicePropertyResponse>
```

`JSON` 格式

```
{ 
  "RequestId":"57b144cf-09fc-4916-a272-a62902d5b207", 
  "Success": true, 
  "Data": {
     "MessageId":"abcabc123"
   } 
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。

