# CreateOTAVerifyJob

调用该接口创建固件验证任务。

## 限制说明

-   将固件推送给设备批量升级前，必须完成固件验证。只有已验证的固件才可用于批量设备升级。您可以调用[QueryOTAFirmware](~~147461~~)查看固件验证状态。
-   不能对验证进行中或验证已成功的固件重复发起验证任务。
-   最多只能传入10个设备用于固件验证。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=CreateOTAVerifyJob&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateOTAVerifyJob|系统规定参数。取值：CreateOTAVerifyJob。 |
|FirmwareId|String|是|nx3xxVvFdwvn6dim50PY03\*\*\*\*|固件ID，固件的唯一标识符。

 固件ID是调用[CreateOTAFirmware](~~147311~~)创建固件时，返回的参数之一。

 可以调用[ListOTAFirmware](~~147450~~)，从返回参数中查看。 |
|ProductKey|String|是|a1VJwBw\*\*\*\*|固件所属产品的ProductKey。 |
|TargetDeviceName.N|RepeatList|是|testdevice|待验证的设备。

 **说明：**

-   设备所属产品必须与固件所属产品一致。
-   设备名称不能重复。
-   最多可传入10个设备名称。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|TimeoutInMinutes|Integer|否|1440|设置设备升级超时时间，单位分钟。范围1~1,440。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Struct| |调用成功时，返回的验证批次信息。详情见以下参数。 |
|JobId|String|wahVIzGkCMuAUE2gDERM02\*\*\*\*|固件验证任务ID，即用于验证固件的设备升级批次ID。 |
|UtcCreate|String|2019-11-04T06:22:19.566Z|固件验证任务的创建时间，UTC格式。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|29EC7245-0FA4-4BB6-B4F5-5F04818FDFB1|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=CreateOTAVerifyJob
&FirmwareId=nx3xxVvFdwvn6dim50PY03****
&ProductKey=a1VJwBw****
&TargetDeviceNames.1=testdevice
&TimeoutInMinutes=1440
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CreateOTAVerifyJobResponse>
   <Data>
       <JobId>wahVIzGkCMuAUE2gDERM02****</JobId>
       <UtcCreate>2019-11-04T06:22:19.566Z</UtcCreate>
   </Data>
   <RequestId>29EC7245-0FA4-4BB6-B4F5-5F04818FDFB1</RequestId>
   <Success>true</Success>
</CreateOTAVerifyJobResponse>
```

`JSON` 格式

```
{
  "Data": {
    "JobId": "wahVIzGkCMuAUE2gDERM02****",
    "UtcCreate": "2019-11-04T06:22:19.566Z"
  },
  "RequestId": "29EC7245-0FA4-4BB6-B4F5-5F04818FDFB1",
  "Success": true
}
```

