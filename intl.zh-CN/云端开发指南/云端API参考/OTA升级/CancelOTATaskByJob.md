# CancelOTATaskByJob

调用该接口取消指定批次下的设备升级作业。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=CancelOTATaskByJob&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CancelOTATaskByJob|系统规定参数。取值：CancelOTATaskByJob。 |
|JobId|String|是|7glPHmaDYLAYMD1HHutT02\*\*\*\*|升级批次ID。

 您调用[CreateOTAStaticUpgradeJob](~~147496~~)或[CreateOTADynamicUpgradeJob](~~147887~~)创建批次返回的**JobId**。您也可以在物联网平台控制台固件的**固件详情**页查看。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|CancelScheduledTask|Boolean|否|false|取消定时升级批次下的设备升级作业，即调用[CreateOTAStaticUpgradeJob](~~147496~~)时，传入了**ScheduleTime**参数创建的升级批次。取值：

 -   true：取消。
-   false：不取消。

 不传入此参数，则取默认值false。 |
|CancelQueuedTask|Boolean|否|false|取消批次下所有状态为待推送（**QUEUED**）的设备升级作业。取值：

 -   **true**：取消。
-   **false**：不取消。

 不传入此参数，则取默认值**false**。 |
|CancelInProgressTask|Boolean|否|false|取消批次下所有状态为升级中（**IN\_PROGRESS**）的设备升级作业。取值：

 -   **true**：取消。
-   **false**：不取消。

 不传入此参数，则取默认值**false**。 |
|CancelNotifiedTask|Boolean|否|false|取消批次下所有状态为已推送（**NOTIFIED**）的设备升级作业。取值：

 -   **true**：取消。
-   **false**：不取消。

 不传入此参数，则取默认值**false**。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|291438BA-6E10-4C4C-B761-243B9A0D324F|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=CancelOTATaskByJob
&JobId=7glPHmaDYLAYMD1HHutT02****
&CancelScheduledTask=false
&CancelQueuedTask=true
&CancelNotifiedTask=false
&CancelInProgressTask=false
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CancelOTATaskByJobResponse>
    <RequestId>A01829CE-75A1-4920-B775-921146A1AB79</RequestId>
    <Success>true</Success>
</CancelOTATaskByJobResponse>
```

`JSON` 格式

```
{
  "RequestId": "291438BA-6E10-4C4C-B761-243B9A0D324F",
  "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。

