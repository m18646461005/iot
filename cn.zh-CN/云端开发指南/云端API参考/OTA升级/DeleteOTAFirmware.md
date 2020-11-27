# DeleteOTAFirmware

调用该接口删除指定固件。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=DeleteOTAFirmware&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteOTAFirmware|系统规定参数。取值：DeleteOTAFirmware。 |
|FirmwareId|String|是|s8SSHiKjpBfrM3BSN0z803\*\*\*\*|固件ID，固件的唯一标识符。

 固件ID是调用[CreateOTAFirmware](~~147311~~)创建固件时，返回的参数之一。

 可以调用[ListOTAFirmware](~~147450~~)，从返回参数中查看。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|9B7BF858-7686-496E-B8B0-BF9E5D7F86CE|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=DeleteOTAFirmware
&FirmwareId=s8SSHiKjpBfrM3BSN0z803****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DeleteOTAFirmwareResponse>
    <RequestId>9B7BF858-7686-496E-B8B0-BF9E5D7F86CE</RequestId>
    <Success>true</Success>
</DeleteOTAFirmwareResponse>
```

`JSON` 格式

```
{
  "RequestId": "9B7BF858-7686-496E-B8B0-BF9E5D7F86CE",
  "Success": true
}
```

