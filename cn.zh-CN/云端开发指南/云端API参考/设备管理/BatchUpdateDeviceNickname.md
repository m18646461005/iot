# BatchUpdateDeviceNickname

调用该接口批量修改设备备注名称。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=BatchUpdateDeviceNickname&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|BatchUpdateDeviceNickname|系统规定参数。取值：BatchUpdateDeviceNickname。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|DeviceNicknameInfo.N.ProductKey|String|否|a1BwAGV\*\*\*\*|要修改备注名称的设备所隶属的产品ProductKey。

 **说明：** 如果传入该参数，需同时传入**DeviceName**。 |
|DeviceNicknameInfo.N.DeviceName|String|否|light|要修改备注名称的设备名称。

 **说明：** 如果传入该参数，需同时传入**ProductKey**。 |
|DeviceNicknameInfo.N.Nickname|String|否|AliyunDataCenter|新的设备备注名称。备注名称长度为4-32个字符，可包含中文汉字、英文字母、数字和下划线（\_）。一个中文汉字算2字符。

 **说明：** 若不传入该参数，则删除该设备原有的备注名称。 |
|DeviceNicknameInfo.N.IotId|String|否|Q7uOhVRdZRRlDnTLv\*\*\*\*00100|要修改备注名称的设备ID。

 **说明：** 如果传入该参数，则无需传入**ProductKey**和**DeviceName**。**IotId**作为设备唯一标识符，和**ProductKey**与**DeviceName**组合是一一对应的关系。如果您同时传入**IotId**和**ProductKey**与**DeviceName**组合，则以**IotId**为准。 |

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
https://iot.cn-shanghai.aliyuncs.com/?Action=BatchUpdateDeviceNickname
&DeviceNicknameInfo.1.ProductKey=a1rYuVF****
&DeviceNicknameInfo.1.DeviceName=SR8FiTu1R9tlUR2V1bmi
&DeviceNicknameInfo.1.Nickname=airconditioning_type1
&DeviceNicknameInfo.2.ProductKey=a1yrZMH****
&DeviceNicknameInfo.2.DeviceName=RkQ8CFtNpDok4BEunymt
&DeviceNicknameInfo.2.Nickname=airconditioning_type2
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<BatchUpdateDeviceNicknameResponse>
  <RequestId>57b144cf-09fc-4916-a272-a62902d5b207</RequestId>
  <Success>true</Success>
</BatchUpdateDeviceNicknameResponse>
```

`JSON` 格式

```
{
  "RequestId":"57b144cf-09fc-4916-a272-a62902d5b207",
  "Success": true
}
```

