# DeleteDeviceProp

调用该接口删除设备下的指定标签。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为500。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=DeleteDeviceProp&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteDeviceProp|系统规定参数。取值：DeleteDeviceProp。 |
|PropKey|String|是|room|要删除的设备标签键值（Key）。

 **说明：** 物联网平台在目标设备的标签中检索您提供的Key值，并删除与之对应的标签。如果目标设备的标签中没有与您提供的Key值对应的记录，则不执行任何操作。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|IotId|String|否|Q7uOhVRdZRRlDnTLv\*\*\*\*00100|标签所属设备的ID

 **说明：** 如果传入该参数，则无需传入**ProductKey**和**DeviceName**。**IotId**作为设备唯一标识符，和**ProductKey**与**DeviceName**组合是一一对应的关系。如果您同时传入**IotId**和**ProductKey**与**DeviceName**组合，则以**IotId**为准。 |
|DeviceName|String|否|light|标签所属设备的名称。

 **说明：** 如果传入该参数，需同时传入**ProductKey**。 |
|ProductKey|String|否|a1BwAGV\*\*\*\*|标签所属设备隶属的产品ProductKey。

 **说明：** 如果传入该参数，需同时传入**DeviceName**。 |

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
https://iot.cn-shanghai.aliyuncs.com/?Action=DeleteDeviceProp
&ProductKey=aladIwW****
&DeviceName=device1
&PropKey=temperature
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DeleteDevicePropResponse>
  <RequestId>57b144cf-09fc-4916-a272-a62902d5b207</RequestId>
  <Success>true</Success>
</DeleteDevicePropResponse>
```

`JSON` 格式

```
{
    "RequestId":"57b144cf-09fc-4916-a272-a62902d5b207",
    "Success": true
}
```

