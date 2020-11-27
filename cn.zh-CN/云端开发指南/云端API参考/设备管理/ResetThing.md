# ResetThing

调用该接口重置指定设备，重置直连设备一型一密状态，同时删除当前设备的拓扑关系。

## 使用说明

如果直连设备通过动态注册获取设备证书信息（ProductKey、DeviceName和DeviceSecret）并激活后，无法再通过动态注册获取设备证书信息，可以通过ResetThing接口重置设备，然后再次通过动态注册获取设备证书信息。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为500。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=ResetThing&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ResetThing|系统规定参数。取值：ResetThing。 |
|IotInstanceId|String|否|iot-cn-0pp1n8t\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|ProductKey|String|否|a1KiV\*\*\*\*\*\*|要重置的设备所隶属的产品ProductKey。

 **说明：** 如果传入该参数，需同时传入**DeviceName**。 |
|DeviceName|String|否|device1|指定重置的设备的名称。

 **说明：** 如果传入该参数，需同时传入**ProductKey**。 |
|IotId|String|否|SR8FiTu1R9tlUR2V1bmi0010a5\*\*\*\*|要重置的设备ID。

 **说明：** 如果传入该参数，则无需传入**ProductKey**和**DeviceName**。**IotId**作为设备唯一标识符，与**ProductKey**和**DeviceName**组合是一一对应的关系。如果您同时传入**IotId**和**ProductKey**与**DeviceName**组合，则以**IotId**为准。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|57b144cf-09fc-4916-a272-a62902d5b207|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。**true**表示调用成功，**false**表示调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=ResetThing
&IotId=MpEKNuEUJzIORNANAWJX0010929900*****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ResetThingResponse>
      <RequestId>57b144cf-09fc-4916-a272-a62902d5b207</RequestId>
      <Success>true</Success>
</ResetThingResponse>
```

`JSON` 格式

```
{
  "RequestId":"57b144cf-09fc-4916-a272-a62902d5b207",
  "Success": true
}
```

