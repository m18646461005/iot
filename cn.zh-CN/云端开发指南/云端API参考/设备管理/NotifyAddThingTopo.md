# NotifyAddThingTopo

调用该接口通知网关设备增加拓扑关系。

## 使用说明

返回的成功结果只表示添加拓扑关系的指令成功下发给网关，但并不表示网关成功添加拓扑关系。

开发网关设备端时，需订阅通知添加拓扑关系消息的Topic。具体Topic和消息格式，请参见[管理拓扑关系](~~89299~~)。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为500。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=NotifyAddThingTopo&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|NotifyAddThingTopo|系统规定参数。取值：NotifyAddThingTopo。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|DeviceListStr|String|否|\[\{"productKey":"a1BwAGV\*\*\*\*","deviceName":"device1"\},\{"IotId":"Q7uOhVRdZRRlDnTLv\*\*\*\*00100"\}\]|要挂载在目标网关设备上的子设备数组，为JSON字符串形式的子设备标识信息，可使用**ProductKey**和**DeviceName**或**IotId**指代设备，例如**\[\{"productKey":"a1BwAGV1234","deviceName":"device1"\},\{"IotId":"Q7uOhVRdZRRlDnTLv123400100"\}\]**。 |
|GwIotId|String|否|vWxNur6BUApsqjv\*\*\*\*4000100|网关设备ID。物联网平台为该设备颁发的ID，设备的唯一标识符。

 **说明：** 如果传入该参数，则无需传入**ProductKey**和**DeviceName**。**IotId**作为设备唯一标识符，和**ProductKey**与**DeviceName**组合是一一对应的关系。如果您同时传入**IotId**和**ProductKey**与**DeviceName**组合，则以**IotId**为准。 |
|GwProductKey|String|否|a1T27vz\*\*\*\*|网关设备所隶属的产品ProductKey。

 **说明：** 如果传入该参数，需同时传入**DeviceName**。 |
|GwDeviceName|String|否|gateway|网关设备名称。

 **说明：** 如果传入该参数，需同时传入**ProductKey**。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Struct| |调用成功时，返回的数据。 |
|MessageId|String|5443123|云端向网关设备下发增加拓扑关系的消息ID。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=NotifyAddThingTopo
&GwProductKey=aldnfald7a
&GwDeviceName=gateway
&DeviceListStr=[{"productKey":"alabcabcab","deviceName":"device1"},{"IotId":"edAjkIeBSsdfadjjllja***"}]
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<NotifyAddThingTopoResponse>
  <RequestId>419A3FC1-B517-4958-9414-5546765FA51F</RequestId>
  <Success>true</Success>
  <Data>
        <MessageId>2345123</MessageId>
  </Data>
</NotifyAddThingTopoResponse>
```

`JSON` 格式

```
{
  "RequestId":"419A3FC1-B517-4958-9414-5546765FA51F",
  "Success": true,
  "Data": {
     "MessageId": "2345123"
  }
}
```

