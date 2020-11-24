# CreateOTAVerifyJob

Creates a firmware verification job.

## Limits

-   You must verify a firmware before you push the firmware to devices for a batch update. Only verified firmware can be used to update devices in batches. You can call the [QueryOTAFirmware](~~147461~~) operation to view the status of the firmware verification.
-   You cannot initiate a verification job for a firmware that is being verified or has been verified.
-   You can specify a maximum of 10 devices for a firmware verification job.
-   Each Alibaba Cloud account can run a maximum of 10 queries per second \(QPS\).

**Note:** RAM users share the quota of the Alibaba Cloud account.


## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Iot&api=CreateOTAVerifyJob&type=RPC&version=2018-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateOTAVerifyJob|The operation that you want to perform. Set the value to CreateOTAVerifyJob. |
|FirmwareId|String|Yes|nx3xxVvFdwvn6dim50PY03\*\*\*\*|The unique ID of the firmware.

 A firmware ID is returned when you call the [CreateOTAFirmware](~~147311~~) operation to create the firmware.

 You can call the [ListOTAFirmware](~~147450~~) operation and view the firmware ID in the response. |
|ProductKey|String|Yes|a1VJwBw\*\*\*\*|The ProductKey of the product to which the firmware belongs. |
|TargetDeviceName.N|RepeatList|Yes|testdevice|The list of devices to be verified.

 **Note:**

-   The devices in the list must belong to the same product as the firmware.
-   The list cannot contain duplicate device names.
-   You can specify a maximum of 10 devices. |
|IotInstanceId|String|No|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|The instance ID. This parameter is not required for the public instance but required for your purchased instances. |
|TimeoutInMinutes|Integer|No|1440|The timeout period for a device to update the firmware. Unit: minutes. Valid values: 1 to 1,440. |

In addition to the preceding API operation-specific request parameters, you must specify common request parameters when you call this API operation. For more information about common request parameters, see [Common request parameters](~~30561~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|String|iot.system.SystemException|The error code that is returned if the call failed. For more information, see [Error codes](~~87387~~). |
|Data|Struct| |The job information that is returned if the call was successful. For more information, see the following parameters. |
|JobId|String|wahVIzGkCMuAUE2gDERM02\*\*\*\*|The ID of the firmware verification job. |
|UtcCreate|String|2019-11-04T06:22:19.566Z|The time when the firmware verification job was created. The time is in the UTC format. |
|ErrorMessage|String|A system exception has occurred.|The error message that is returned if the call failed. |
|RequestId|String|29EC7245-0FA4-4BB6-B4F5-5F04818FDFB1|The globally unique ID that Alibaba Cloud generated for the request. |
|Success|Boolean|true|Indicates whether the call was successful. **true** indicates that the call was successful. **false** indicates that the call failed. |

## Examples

Sample requests

```
https://iot.cn-shanghai.aliyuncs.com/?Action=CreateOTAVerifyJob
&FirmwareId=nx3xxVvFdwvn6dim50PY03****
&ProductKey=a1VJwBw****
&TargetDeviceNames.1=testdevice
&TimeoutInMinutes=1440
&<Common request parameters>
```

Sample success responses

`XML` format

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

