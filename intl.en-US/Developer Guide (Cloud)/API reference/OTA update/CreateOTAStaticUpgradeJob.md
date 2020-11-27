# CreateOTAStaticUpgradeJob

Creates a static update batch.

## Limits

-   When you call the [CreateOTAFirmware](~~147311~~) API operation to create an update package, no verification is required for the update package. However, before you call the CreateOTAStaticUpgradeJob API operation to create an update batch, make sure that the update package is verified. For more information, see [CreateOTAVerifyJob](~~147480~~).
-   You can initiate update tasks for a maximum of 200 devices in each call. If you use a device list file, you can initiate update tasks for a maximum of 10,000 devices. However, you must call the [GenerateDeviceNameListURL](~~186062~~) API operation to generate the URL for the device list file in advance. Then, you can perform the operations as prompted to upload the device list file.
-   Each device of a batch can be only in the pending or updating state. If you initiate another update task for a device that is in the pending or updating state, the update task fails.
-   You can initiate multiple static update batches for a single update package.
-   Each Alibaba Cloud account can run a maximum of 20 queries per second \(QPS\).

**Note:** RAM users of an Alibaba Cloud account share the quota of the account.


## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Iot&api=CreateOTAStaticUpgradeJob&type=RPC&version=2018-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateOTAStaticUpgradeJob|The operation that you want to perform. Set the value to CreateOTAStaticUpgradeJob. |
|FirmwareId|String|Yes|nx3xxVvFdwvn6dim50PY03\*\*\*\*|The ID of the update package. The ID is the unique identifier for the update package.

An update package ID is returned when you call the [CreateOTAFirmware](~~147311~~) operation to create the update package.

You can call the [ListOTAFirmware](~~147450~~) API operation to view the update package ID in the response. |
|ProductKey|String|Yes|a1Le6d0\*\*\*\*|The key of the product to which the update package belongs. |
|Tag.N.Key|String|Yes|key1|The key of each update batch tag. The key can contain letters, digits, and periods \(.\). The key must 1 to 30 characters in length. An update batch tag is sent to devices when IoT Platform pushes an update notification to these devices.

**Note:** Update batch tags are optional. If you specify update batch tags, you must specify a **value**and **key** for each update batch tag. |
|Tag.N.Value|String|Yes|value1|The value of the update batch tag. The value must be 1 to 128 characters in length.

**Note:** Update batch tags are optional. If you specify update batch tags, you must specify a **value** and **key** for each update batch tag. |
|TargetSelection|String|Yes|ALL|The scope of the update batch. Valid values:

-   **ALL**: full update
-   **SPECIFIC**: specific update
-   **GRAY**: canary update |
|IotInstanceId|String|No|iot-cn-0pp1n8t\*\*\*\*|The instance ID. This parameter is not required for public instances. However, the parameter is required for the instances that you have purchased. |
|SrcVersion.N|RepeatList|No|V1.0.1|The list of firmware versions to be updated.

**Note:**

-   If you set the TargetSelection parameter to `ALL` or set the TargetSelection parameter to `GRAY`, you can specify this parameter.
-   When you use a differential update package to perform full update or canary update tasks, the value of this parameter must be the same as the value of the **SrcVersion** parameter.
-   If you set the TargetSelection parameter to `SPECIFIC`, you cannot specify this parameter.
-   You can call the [QueryDeviceDetail](~~69594~~) API operation to view the **FirmwareVersion** parameter in the response.
-   The list cannot contain duplicate versions.
-   A maximum of 10 versions can be specified. |
|ScheduleTime|Long|No|1577808000000|The time to start the OTA update.

The scheduled time ranges from 5 minutes later than the current time to 7 days. The value must be a 13-bit timestamp.

If you do not specify this parameter, the update starts immediately. |
|RetryInterval|Integer|No|60|The automatic retry interval after a device fails to be updated. Unit: minutes. Valid values:

-   **0**: An automatic retry is immediately performed.
-   **10**: An automatic retry is performed after 10 minutes.
-   **30**: An automatic retry is performed after 30 minutes.
-   **60**: An automatic retry is performed after 60 minutes \(1 hour\).
-   **1440**: An automatic retry is performed after 1,440 minutes \(24 hours\).

If you do not specify this parameter, no retry is performed. |
|RetryCount|Integer|No|1|The number of automatic retries.

You must specify this parameter if you specify the **RetryInterval** parameter.

Valid values:

-   **1**: retries once
-   **2**: retries twice
-   **5**: retries five times |
|TimeoutInMinutes|Integer|No|1440|The timeout period for a device update. Unit: minutes. Valid values: 1 to 1440.

If an update is not completed after the specified timeout period, the update fails.

**Note:**

-   The timeout period starts from the time when the specified device submits the update progress for the first time.
-   If an update fails due to a timeout issue, no retry is triggered. |
|MaximumPerMinute|Integer|No|1000|The maximum number of devices to which the download URL of the update package is pushed per minute. Valid values: 0 to 1000.

If you do not specify this parameter, the default value 1000 is used. |
|GrayPercent|String|No|33.33|The update percentage of the canary update. The value is a percentage in the string format. The value can have a maximum of three decimal places. The calculated number of devices is rounded down to the nearest integer. You must specify a minimum of one device for a canary update.

For example, if you set the canary update percentage to 33.33 for 100 devices, the number of devices to be updated is 33.

You must specify this parameter if you set the TargetSelection parameter to `GRAY`. |
|TargetDeviceName.N|RepeatList|No|deviceName1|The name of each device.

**Note:**

-   If you set the TargetSelection parameter to `SPECIFIC`, you must specify this parameter or the **DnListFileUrl** parameter. You cannot specify the two parameters at the same time.
-   When you use a differential update package to perform a specific update, the OTA module version of the device to be updated must be the same as the value of the **SrcVersion** parameter.
-   You can call the [QueryDeviceDetail](~~69594~~) API operation to view the **FirmwareVersion** parameter in the response.
-   The devices in the list must belong to the same product as the update package.
-   The list cannot contain duplicate device names.
-   A maximum of 100,000 devices name can be specified. |
|ScheduleFinishTime|Long|No|1577909000000|The time to end the update.

The end time must be 1 hour to 30 days later than the start time that is specified by the **ScheduleTime** parameter. The value must be a 13-bit timestamp.

If you do not specify this parameter, the update does not end. |
|OverwriteMode|Integer|No|1|Specifies whether to overwrite the previous update task. Valid values:

-   1: do not overwrite. If a device already has an update task, the previous update task is implemented.
-   2: overwrite. Only the current update task is implemented.

If you do not specify this parameter, the previous update task is not overwritten by default.

**Note:** The update task that is in progress is not overwritten. |
|DnListFileUrl|String|No|https://iotx-ota.oss-cn-shanghai.aliyuncs.com/ota/65dfcda0473be29836dfde585472\*\*\*\*/ck2nfzljo00023g7kysg0\*\*\*\*.bin|The URL of the device list file that is used to perform a specific update.

**Note:**

-   If you set the TargetSelection parameter to `SPECIFIC`, you must specify this parameter or the **TargetDeviceName.N** parameter. You cannot specify the two parameters at the same time.
-   You can call the [GenerateDeviceNameListURL](~~186062~~) API operation to generate the URL. Then, you can perform the operations as prompted to upload the device list file. |

In addition to the preceding operation-specific request parameters, you must specify common request parameters when you call this API operation. For more information about common request parameters, see [Common request parameters](~~30561~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|String|MissingFirmwareId|The error code returned if the call fails. For more information about error codes, see [Error codes](~~87387~~). |
|Data|Struct| |The update batch information is returned if the call succeeds. For more information, see the following table. |
|JobId|String|wahVIzGkCMuAUE2gDERM02\*\*\*\*|The ID of the update batch. The ID is the unique identifier for the update batch. |
|UtcCreate|String|2019-11-04T06:22:19.566Z|The time when the update batch was created. The time is in the UTC format. |
|ErrorMessage|String|FirmwareId is mandatory for this action.|The error message returned if the call fails. |
|RequestId|String|29EC7245-0FA4-4BB6-B4F5-5F04818FDFB1|The globally unique ID that Alibaba Cloud generates for the request. |
|Success|Boolean|true|Indicates whether the call succeeded.**true**indicates that the call succeeded and **false**indicates that the call failed. |

## Examples

Sample requests

```
https://iot.cn-shanghai.aliyuncs.com/?Action=CreateOTAStaticUpgradeJob
&FirmwareId=nx3xxVvFdwvn6dim50PY03****
&MaximumPerMinute=1000
&ProductKey=a1Le6d0****
&RetryCount=1
&RetryInterval=60
&TargetSelection=ALL
&TimeoutInMinutes=1440
&SrcVersion.1=V1.0.1
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateOTAStaticUpgradeJobResponse>
   <Data>
       <JobId>wahVIzGkCMuAUE2gDERM02****</JobId>
       <UtcCreate>2019-11-04T06:22:19.566Z</UtcCreate>
   </Data>
   <RequestId>29EC7245-0FA4-4BB6-B4F5-5F04818FDFB1</RequestId>
   <Success>true</Success>
</CreateOTAStaticUpgradeJobResponse>
```

`JSON` format

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

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Iot).

