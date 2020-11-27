# CancelOTATaskByDevice

调用该接口取消指定固件下状态为待升级的设备升级作业。

## 限制说明

-   该接口只能取消待升级状态的设备升级。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=CancelOTATaskByDevice&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CancelOTATaskByDevice|系统规定参数。取值：CancelOTATaskByDevice。 |
|DeviceName.N|RepeatList|是|device1|要取消升级的设备名称。

 设备名称不能重复。

 最多可传入200个设备名称。 |
|FirmwareId|String|是|T0F5b5tpFnHQrgfk\*\*\*\*030100|固件ID，固件的唯一标识符。

 固件ID是调用[CreateOTAFirmware](~~147311~~)创建固件时，返回的参数之一。

 可以调用[ListOTAFirmware](~~147450~~)，从返回参数中查看。 |
|ProductKey|String|是|a1V4kde\*\*\*\*|要取消升级的设备所属产品的ProductKey。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|JobId|String|否|wahVIzGkCMuAUE2gDERM02\*\*\*\*|升级批次ID。传入此参数则只删除指定批次下的设备升级任务。

 批次ID是您调用[CreateOTAVerifyJob](~~147480~~)、[CreateOTAStaticUpgradeJob](~~147496~~)或[CreateOTADynamicUpgradeJob](~~147887~~)创建升级任务后返回的**JobId**。您也可以在物联网平台控制台上固件的**固件详情**页查看。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|A01829CE-75A1-4920-B775-921146A1AB79|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=CancelOTATaskByDevice
&FirmwareId=T0F5b5tpFnHQrgfk****030100
&ProductKey=a1V4kde****
&DeviceName.1=deviceName1
&DeviceName.2=deviceName2
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CancelOTATaskByDeviceResponse>
    <RequestId>A01829CE-75A1-4920-B775-921146A1AB79</RequestId>
    <Success>true</Success>
</CancelOTATaskByDeviceResponse>
```

`JSON` 格式

```
{
  "RequestId": "A01829CE-75A1-4920-B775-921146A1AB79",
  "Success": true
}
```

