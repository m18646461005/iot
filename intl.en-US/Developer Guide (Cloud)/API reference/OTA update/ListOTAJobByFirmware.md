# ListOTAJobByFirmware

Queries the update batches of an update package.

## Limits

Each Alibaba Cloud account can run a maximum of 10 queries per second \(QPS\).

**Note:** RAM users of an Alibaba Cloud account share the quota of the account.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Iot&api=ListOTAJobByFirmware&type=RPC&version=2018-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListOTAJobByFirmware|The operation that you want to perform. Set the value to ListOTAJobByFirmware. |
|CurrentPage|Integer|Yes|1|The number of the page to return. Pages start from page 1. |
|FirmwareId|String|Yes|FJFx8JzpnhpIsKftRjjm03\*\*\*\*|The ID of the update package. The ID is the unique identifier for the update package.

 An update package ID is returned when you call the [CreateOTAFirmware](~~147311~~) operation to create the update pacakge.

 You can call the [ListOTAFirmware](~~147450~~) API operation to view the update package ID in the response. |
|PageSize|Integer|Yes|10|The number of entries to return on each page. Maximum value: 200. |
|IotInstanceId|String|No|iot-cn-0pp1n8t\*\*\*\*|The instance ID. This parameter is not required for public instances. However, the parameter is required for the instances that you have purchased. |

In addition to the preceding operation-specific request parameters, you must specify common request parameters when you call this API operation. For more information, see [Common request parameters](~~30561~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|String|iot.system.SystemException|The error code returned if the call fails. For more information about error codes, see [Error codes](~~87387~~). |
|CurrentPage|Integer|1|The page number of the returned page. |
|Data|Array of SimpleOTAJobInfo| |The update batch information returned when the call succeeds. For more information, see **SimpleOTATaskInfo**. |
|SimpleOTAJobInfo| | | |
|FirmwareId|String|UfuxnwygsuSkVE0VCN\*\*\*\*0100|The ID of the update package. |
|JobId|String|HvKuBpuk3rdk6E92CP\*\*\*\*0200|The ID of the update batch. The ID is the unique identifier of the update batch. |
|JobStatus|String|IN\_PROGRESS|The status of the update batch.

 -   **PLANNED**: The update batch is being planned. The update batch is created, but the scheduled time has not been reached. This parameter is returned only when you perform a static update.
-   **IN\_PROGRESS**: The update batch is in progress.
-   **COMPLETE**: The update batch is completed.
-   **CANCELED**: The update batch is canceled. |
|JobType|String|UPGRADE\_FIRMWARE|The type of the update batch. Valid values:

 -   **VERFIY\_FIRMWARE**: firmware verification.
-   **UPGRADE\_FIRMWARE**: batch update. |
|ProductKey|String|a19mzPZ\*\*\*\*|The key of the product to which the update package belongs. |
|SelectionType|String|STATIC|The update policy of the update batch. Valid value:

 -   **DYNAMIC**: dynamic update. This value is returned if you call the [CreateOTADynamicUpgradeJob](~~147887~~) API operation to create the update batch.
-   **STATIC**: static update. This value is returned if you call the [CreateOTAStaticUpgradeJob](~~147496~~) operation to create the update batch. |
|Tags|Array of OtaTagDTO| |The tags of the update batch. |
|OtaTagDTO| | | |
|Key|String|key1|The name of each tag. |
|Value|String|value1|The value of the tag. |
|TargetSelection|String|SPECIFIC|The scope of the update. Valid values:

 -   **ALL**: full update
-   **SPECIFIC**: specific update
-   **GRAY**: canary update

 **Note:** The value ALL is returned when you call the [CreateOTADynamicUpgradeJob](~~147887~~) API operation to create the update batch. |
|UtcCreate|String|2019-12-28T02:43:10.000Z|The time when the update batch was created. The time is in the UTC format. |
|UtcEndTime|String|2019-12-29T02:43:10.000Z|The end time of the update batch. The time is in the UTC format.

 This parameter is returned only if the update batch is completed. |
|UtcModified|String|2019-12-28T02:43:10.000Z|The last modification time of the update batch. The time is in the UTC format. |
|UtcStartTime|String|2019-12-28T02:43:10.000Z|The start time of the update batch. The time is in the UTC format. |
|ErrorMessage|String|A system exception occurred.|The error message returned if the call fails. |
|PageCount|Integer|1|The total number of pages returned. |
|PageSize|Integer|10|The number of entries returned per page. |
|RequestId|String|5D58AC86-D5BF-4B39-834E-913E7F2C985D|The globally unique ID that Alibaba Cloud generates for the request. |
|Success|Boolean|true|Indicates whether the call succeeded. **true** indicates that the call succeeded. **false** indicates that the call failed. |
|Total|Integer|1|The total number of update jobs returned. |

## Examples

Sample requests

```
https://iot.cn-shanghai.aliyuncs.com/?Action=ListOTAJobByFirmware
&FirmwareId=FJFx8JzpnhpIsKftRjjm03****
&PageSize=10
&CurrentPage=1
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListOTAJobByFirmwareResponse>
    <PageCount>1</PageCount>
    <Data>
        <SimpleOTAJobInfo>
            <SelectionType>STATIC</SelectionType>
            <TargetSelection>SPECIFIC</TargetSelection>
            <JobType>UPGRADE_FIRMWARE</JobType>
            <FirmwareId>yLYuCqfqQNQ1JOqkDa****0100</FirmwareId>
            <UtcStartTime>2019-12-28T02:43:10.000Z</UtcStartTime>
            <UtcEndTime>2019-12-29T02:43:10.000Z</UtcEndTime>
            <ProductKey>a19mzPZ****</ProductKey>
            <JobId>HvKuBpuk3rdk6E92CP****0200</JobId>
            <UtcModified>2019-12-28T02:43:10.000Z</UtcModified>
            <JobStatus>IN_PROGRESS</JobStatus>
            <UtcCreate>2019-12-28T02:43:10.000Z</UtcCreate>
        </SimpleOTAJobInfo>
    </Data>
    <PageSize>10</PageSize>
    <RequestId>5D58AC86-D5BF-4B39-834E-913E7F2C985D</RequestId>
    <CurrentPage>1</CurrentPage>
    <Success>true</Success>
    <Total>1</Total>
</ListOTAJobByFirmwareResponse>
```

`JSON` format

```
{
  "PageCount": 1,
  "Data": {
    "SimpleOTAJobInfo": [{
      "SelectionType": "STATIC",
      "TargetSelection": "SPECIFIC",
      "JobType": "UPGRADE_FIRMWARE",
      "FirmwareId": "UfuxnwygsuSkVE0VCN****0100",
      "UtcStartTime": "2019-12-28T02:43:10.000Z",
      "UtcEndTime": "2019-12-29T02:43:10.000Z",
      "ProductKey": "a19mzPZ****",
      "JobId": "HvKuBpuk3rdk6E92CP****0200",
      "UtcModified": "2019-12-28T02:43:10.000Z",
      "JobStatus": "IN_PROGRESS",
      "UtcCreate": "2019-12-28T02:43:10.000Z"
    }]
  },
  "PageSize": 10,
  "RequestId": "5D58AC86-D5BF-4B39-834E-913E7F2C985D",
  "CurrentPage": 1,
  "Success": true,
  "Total": 1
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Iot).

