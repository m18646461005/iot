# RemoveThingTopo

调用该接口移除网关与子设备的拓扑关系。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为500。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=RemoveThingTopo&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|RemoveThingTopo|系统规定参数。取值：RemoveThingTopo。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|IotId|String|否|Q7uOhVRdZRRlDnTLv\*\*\*\*00100|要删除拓扑关系的设备ID。物联网平台为该设备颁发的ID，设备的唯一标识符。

 **说明：** 如果传入该参数，则无需传入**ProductKey**和**DeviceName**。**IotId**作为设备唯一标识符，和**ProductKey**与**DeviceName**组合是一一对应的关系。如果您同时传入**IotId**和**ProductKey**与**DeviceName**组合，则以**IotId**为准。 |
|ProductKey|String|否|a1BwAGV\*\*\*\*|要删除拓扑关系的设备所隶属的产品ProductKey。

 **说明：** 如果传入该参数，需同时传入**DeviceName**。 |
|DeviceName|String|否|light|要删除拓扑关系的设备名称。

 **说明：** 如果传入该参数，需同时传入**ProductKey**。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Boolean|true|删除拓扑关系的结果。

 -   **true**：删除成功。
-   **false**：删除失败。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=RemoveThingTopo
&ProductKey=a1bPo9p****
&DeviceName=device1
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<RemoveThingTopoResponse>
  <Data>true</Data>
  <RequestId>098BEEF4-58F4-4181-A891-5D37DB6C4C3B</RequestId>
  <Success>true</Success>
</RemoveThingTopoResponse>
```

`JSON` 格式

```
{
    "Data": true,
    "RequestId": "098BEEF4-58F4-4181-A891-5D37DB6C4C3B",
    "Success": true
}
```

