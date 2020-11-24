# QueryOTAFirmware

Queries the details of a specified firmware.

## Limits

Each Alibaba Cloud account can run a maximum of 20 queries per second \(QPS\).

**Note:** RAM users share the quota of the Alibaba Cloud account.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Iot&api=QueryOTAFirmware&type=RPC&version=2018-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|QueryOTAFirmware|The operation that you want to perform. Set the value to QueryOTAFirmware. |
|FirmwareId|String|Yes|s8SSHiKjpBfrM3BSN0z803\*\*\*\*|The unique ID of the firmware.

 A firmware ID is returned when you call the [CreateOTAFirmware](~~147311~~) operation to create the firmware.

 You can call the [ListOTAFirmware](~~147450~~) operation and view the firmware ID in the response. |
|IotInstanceId|String|No|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|The instance ID. This parameter is not required for the public instances but required for your purchased instances. |

In addition to the preceding operation-specific request parameters, you must specify common request parameters when you call this API operation. For more information about common request parameters, see [Common request parameters](~~30561~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|String|iot.system.SystemException|The error code that is returned if the call failed. For more information, see [Error codes](~~87387~~). |
|ErrorMessage|String|A system exception has occurred.|The error message that is returned if the call failed. |
|FirmwareInfo|Struct| |The firmware information that is returned if the call was successful. For more information, see the following parameters. |
|DestVersion|String|4.0.0|The current version of the firmware. |
|FirmwareDesc|String|modified-WiFi-module|The description of the firmware. |
|FirmwareId|String|UfuxnwygsuSkVE0VCN\*\*\*\*0100|The unique ID of the firmware. |
|FirmwareName|String|t3q5rkNm|The name of the firmware. |
|FirmwareSign|String|3d04ab6462633508606e5f3daac8\*\*\*\*|The signature value of the firmware. |
|FirmwareSize|Integer|924|The size of the firmware. Unit: MB. |
|FirmwareUrl|String|https://ota-pre.iot-thing.cn-shanghai.aliyuncs.com/ota/572ef2fd12ca4791a5b21a9eb948\*\*\*\*/5E962CF83DB1495E8337E9C8A4D1\*\*\*\*.bin?Expires=1577587360&OSSAccessKeyId=cS8uRRy54Rsz\*\*\*\*&Signature=farzC8%2FVMN4HYdEtXvdiC2OevH\*\*\*\*|The firmware URL that is stored in OSS. |
|ModuleName|String|WifiConfigModify|The name of the firmware module.

 Firmware updates are based on the firmware modules of a device. |
|ProductKey|String|a19mzPZ\*\*\*\*|The ProductKey of the product to which the firmware belongs. |
|ProductName|String|MyProduct|The name of the product to which the firmware belongs. |
|SignMethod|String|MD5|The signature method of the firmware. |
|SrcVersion|String|1.0.0|The version of the firmware to be updated.

 **Note:** This parameter is returned only when you perform a delta update. |
|Status|Integer|2|The status of the firmware. Valid values:

 -   **0**: unverified
-   **1**: verified
-   **2**: verifying
-   **3**: failed to be verified |
|Type|Integer|0|The type of the firmware update. Valid values:

 -   **0**: full update
-   **1**: delta update |
|UtcCreate|String|2019-12-28T02:42:22.000Z|The time when the firmware was created. The time is in the UTC format. |
|UtcModified|String|2019-12-28T02:42:41.000Z|The time when the firmware was last modified. The time is in the UTC format. |
|VerifyProgress|Integer|0|The progress of the firmware verification. Valid values:

 -   **0**: unverified
-   **100**: verified
-   A value N between 0 and 100 indicates that the update task is N percent completed. You can check the **Status** response parameter to view the firmware verification status. |
|RequestId|String|A01829CE-75A1-4920-B775-921146A1AB79|The globally unique ID that Alibaba Cloud generated for the request. |
|Success|Boolean|true|Indicates whether the call was successful. **true** indicates that the call was successful. **false** indicates that the call failed. |

## Examples

Sample requests

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryOTAFirmware
&FirmwareId=s8SSHiKjpBfrM3BSN0z803****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<QueryOTAFirmwareResponse>
    <RequestId>A01829CE-75A1-4920-B775-921146A1AB79</RequestId>
    <FirmwareInfo>
        <SrcVersion></SrcVersion>
        <FirmwareSign>3d04ab6462633508606e5f3daac8****</FirmwareSign>
        <ProductKey>a19mzPZ****</ProductKey>
        <Type>0</Type>
        <UtcModified>2019-12-28T02:42:41.000Z</UtcModified>
        <SignMethod>MD5</SignMethod>
        <UtcCreate>2019-12-28T02:42:41.000Z</UtcCreate>
        <FirmwareSize>924</FirmwareSize>
        <Status>0</Status>
        <FirmwareId>yLYuCqfqQNQ1JOqkDa****0100</FirmwareId>
        <FirmwareDesc>modified-WiFi-module</FirmwareDesc>
        <FirmwareUrl><![ CDATA[https://ota-pre.iot-thing.cn-shanghai.aliyuncs.com/ota/572ef2fd12ca4791a5b21a9eb948****/5E962CF83DB1495E8337E9C8A4D1****.bin?Expires=1577587360&OSSAccessKeyId=cS8uRRy54Rsz****&Signature=farzC8%2FVMN4HYdEtXvdiC2OevH****]]></FirmwareUrl>
        <DestVersion>4.0.0</DestVersion>
        <ProductName>MyProduct</ProductName>
        <FirmwareName>t3q5rkNm</FirmwareName>
        <ModuleName>WifiConfigModify</ModuleName>
        <VerifyProgress>0</VerifyProgress>
    </FirmwareInfo>
    <Success>true</Success>
</QueryOTAFirmwareResponse>
```

`JSON` format

```
{
  "RequestId": "A01829CE-75A1-4920-B775-921146A1AB79",
  "FirmwareInfo": {
    "SrcVersion": "",
    "FirmwareSign": "3d04ab6462633508606e5f3daac8****",
    "ProductKey": "a19mzPZ****",
    "Type": 0,
    "UtcModified": "2019-12-28T02:42:41.000Z",
    "SignMethod": "MD5",
    "UtcCreate": "2019-12-28T02:42:22.000Z",
    "FirmwareSize": 924,
    "Status": 2,
    "FirmwareId": "UfuxnwygsuSkVE0VCN****0100",
    "FirmwareDesc": "modified-WiFi-module",
    "FirmwareUrl": "https://ota-pre.iot-thing.cn-shanghai.aliyuncs.com/ota/572ef2fd12ca4791a5b21a9eb948****/5E962CF83DB1495E8337E9C8A4D1****.bin?Expires=1577587360&OSSAccessKeyId=cS8uRRy54Rsz****&Signature=farzC8%2FVMN4HYdEtXvdiC2OevH****",
    "DestVersion": "4.0.0",
    "ProductName": "MyProduct",
    "FirmwareName": "t3q5rkNm",
    "ModuleName": "WifiConfigModify",
    "VerifyProgress": 0
  },
  "Success": true
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Iot).

