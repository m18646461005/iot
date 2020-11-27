# QueryOTAJob

Queries the details of an update batch.

## Limits

Each Alibaba Cloud account can run a maximum of 10 queries per second \(QPS\).

**Note:** RAM users of an Alibaba Cloud account share the quota of the account.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Iot&api=QueryOTAJob&type=RPC&version=2018-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|QueryOTAJob|The operation that you want to perform. Set the value to QueryOTAJob. |
|JobId|String|Yes|wahVIzGkCMuAUE2gDERM02\*\*\*\*|The ID of the update batch.

After you call the [CreateOTAVerifyJob](~~147480~~), [CreateOTAStaticUpgradeJob](~~147496~~), or [CreateOTADynamicUpgradeJob](~~147887~~) API operation to create the update batch, you can obtain the **JobId** parameter. You can also view the batch ID on the **Firmware Details** page of the IoT Platform console. |
|IotInstanceId|String|No|iot-cn-0pp1n8t\*\*\*\*|The instance ID. This parameter is not required for public instances. However, the parameter is required for the instances that you have purchased. |

In addition to the preceding operation-specific request parameters, you must specify common request parameters when you call this API operation. For more information, see [Common request parameters](~~30561~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|String|iot.system.SystemException|The error code returned if the call fails. For more information about error codes, see [Error codes](~~87387~~). |
|Data|Struct| |The update batch information is returned if the call succeeds. A data struct contains the following parameters. |
|DestVersion|String|1.0.1|The destination firmware version of the update. |
|DynamicMode|Integer|1|The mode of dynamic update. Valid values:

-   **1**: constantly updates the devices that meet the conditions.
-   **2**: updates only the devices that subsequently submit the latest firmware versions.

This parameter is returned only when you perform a dynamic update. |
|FirmwareId|String|UfuxnwygsuSkVE0VCN\*\*\*\*0100|The ID of the update package. |
|GrayPercent|String|50.00|The update percentage of the canary update.

This parameter is returned only if the update is a canary update. |
|JobDesc|String|batch upgrade|The description of the update batch. |
|JobId|String|HvKuBpuk3rdk6E92CP\*\*\*\*0200|The ID of the update batch. The ID is the unique identifier of the update batch. |
|JobStatus|String|IN\_PROGRESS|The status of the update batch.

-   **PLANNED**: The update batch is being planned. The update batch is created, but the scheduled time has not been reached. This parameter is returned only when you perform a static update.
-   **IN\_PROGRESS**: The update batch is in progress.
-   **COMPLETE**: The update batch is completed.
-   **CANCELED**: The update batch is canceled. |
|JobType|String|UPGRADE\_FIRMWARE|The type of the update batch. Valid values:

-   **VERFIY\_FIRMWARE**: firmware verification.
-   **UPGRADE\_FIRMWARE**: batch update. |
|MaximumPerMinute|Integer|1000|The maximum number of devices to which the download URL of the update package is pushed per minute. |
|Name|String|Firmware2|The name of the update package. |
|OverwriteMode|Integer|1|Indicates whether the previous update task is overwritten. Valid values:

-   **1**: The previous update task is not overwritten. If a device already has an update task, the previous update task is implemented.
-   **2**: The previous update task is overwritten. Only the current update task is implemented.

The update task that is in progress is not overwritten. |
|ProductKey|String|a19mzPZ\*\*\*\*|The key of the product to which the update package belongs. |
|RetryCount|Integer|1|The number of automatic retries after a device fails to be updated.

This parameter is returned if a retry policy is set when you create the update batch. |
|RetryInterval|Integer|60|The automatic retry interval after a device fails to be updated. Unit: minutes.

This parameter is returned if a retry policy is set when you create the update batch. |
|SelectionType|String|STATIC|The update policy of the update batch. Valid values:

-   **DYNAMIC**: dynamic update. This value is returned if you call the[CreateOTADynamicUpgradeJob](~~147887~~) API operation to create the update batch.
-   **STATIC**: static update. This value is returned if you call the [CreateOTAStaticUpgradeJob](~~147496~~) API operation to create the update batch. |
|SrcVersions|List|\{"SrcVersion": \["1.0.0"\]\}|The list of firmware versions to be updated. |
|Tags|Array of OtaTagDTO| |The tags of the update batch. |
|OtaTagDTO| | | |
|Key|String|key1|The key of each tag. |
|Value|String|value1|The value of the tag. |
|TargetSelection|String|SPECIFIC|The scope of the update batch. Valid values:

-   **ALL**: full update
-   **SPECIFIC**: specific update
-   **GRAY**: canary update

**Note:** The value ALL is returned if you call the [CreateOTADynamicUpgradeJob](~~147887~~) API operation to create the update batch. |
|TimeoutInMinutes|Integer|5|The timeout period for a device update. Unit: minutes.

This parameter is returned if the timeout period is set when you create the update batch. |
|UtcCreate|String|2019-12-28T02:43:10.000Z|The time when the update batch was created. The time is in the UTC format. |
|UtcEndTime|String|2019-12-29T02:43:10.000Z|The end time of the update job. The time is in the UTC format.

This parameter is returned only after the update batch is completed. |
|UtcModified|String|2019-12-28T02:43:10.000Z|The last modification time of the update batch. The time is in the UTC format. |
|UtcScheduleFinishTime|String|2019-12-30T02:43:10.000Z|The end time of the scheduled update task. This parameter is returned only if the update task is scheduled and the end time of the scheduled update is specified. |
|UtcScheduleTime|String|2019-12-29T02:43:10.000Z|The start time of the scheduled update task. This parameter is returned only after the update task is scheduled. |
|UtcStartTime|String|2019-12-28T02:43:10.000Z|The start time of the update task. The time is in the UTC format. |
|ErrorMessage|String|A system exception occurred.|The error message returned if the call fails. |
|RequestId|String|30F1BB8D-EDBF-44FD-BBC0-BE97DEA73991|The globally unique ID that Alibaba Cloud generates for the request. |
|Success|Boolean|true|Indicates whether the call succeeds.**true**indicates that the call succeeded.**false**indicates that the call failed. |

## Examples

Sample requests

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryOTAJob
&JobId=wahVIzGkCMuAUE2gDERM02****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<QueryOTAJobResponse>
  <Data>
        <TimeoutInMinutes>5</TimeoutInMinutes>
        <JobDesc>batch upgrade</JobDesc>
        <UtcStartTime>2019-12-28T02:43:10.000Z</UtcStartTime>
        <UtcEndTime>2019-12-29T02:43:10.000Z</UtcEndTime>
        <ProductKey>a19mzPZ****</ProductKey>
        <UtcModified>2019-12-28T02:43:10.000Z</UtcModified>
        <JobStatus>IN_PROGRESS</JobStatus>
        <UtcCreate>2019-12-28T02:43:10.000Z</UtcCreate>
        <SelectionType>STATIC</SelectionType>
        <TargetSelection>SPECIFIC</TargetSelection>
        <JobType>UPGRADE_FIRMWARE</JobType>
        <RetryInterval>60</RetryInterval>
        <RetryCount>1</RetryCount>
        <OverwriteMode>1</OverwriteMode>
        <MaximumPerMinute>1000</MaximumPerMinute>
        <SrcVersions>
              <SrcVersion>1.0.0</SrcVersion>
        </SrcVersions>
        <Name>firmware2</Name>
        <FirmwareId>UfuxnwygsuSkVE0VCN****0100</FirmwareId>
        <JobId>HvKuBpuk3rdk6E92CP****0200</JobId>
        <DestVersion>1.0.1</DestVersion>
  </Data>
  <RequestId>30F1BB8D-EDBF-44FD-BBC0-BE97DEA73991</RequestId>
  <Success>true</Success>
</QueryOTAJobResponse>
```

`JSON` format

```
{
  "Data": {
    "TimeoutInMinutes": 5,
    "JobDesc": "batch upgrade",
    "UtcStartTime": "2019-12-28T02:43:10.000Z",
    "UtcEndTime": "2019-12-29T02:43:10.000Z",
    "ProductKey": "a19mzPZ****",
    "UtcModified": "2019-12-28T02:43:10.000Z",
    "JobStatus": "IN_PROGRESS",
    "UtcCreate": "2019-12-28T02:43:10.000Z",
    "SelectionType": "STATIC",
    "TargetSelection": "SPECIFIC",
    "JobType": "UPGRADE_FIRMWARE",
    "RetryInterval":60,
    "RetryCount":1,
    "OverwriteMode":1,
    "MaximumPerMinute":1000,
    "SrcVersions": {
      "SrcVersion": ["1.0.0"]
    },
    "Name":"firmware2",
    "FirmwareId": "UfuxnwygsuSkVE0VCN****0100",
    "JobId": "HvKuBpuk3rdk6E92CP****0200",
    "DestVersion": "1.0.1"
  },
  "RequestId": "30F1BB8D-EDBF-44FD-BBC0-BE97DEA73991",
  "Success": true
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Iot).

