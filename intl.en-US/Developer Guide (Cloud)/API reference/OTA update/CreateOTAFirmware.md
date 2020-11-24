# CreateOTAFirmware

Creates firmware after firmware files are uploaded to Object Storage Service \(OSS\).

## Limits

-   An Alibaba Cloud account can upload a maximum of 500 firmware files.
-   A single Alibaba Cloud account can run a maximum of 10 queries per second \(QPS\). RAM users share the quota of the Alibaba Cloud account.
-   Before calling this operation to create firmware, you must call the [GenerateOTAUploadURL](~~147310~~) operation to generate the parameters that are required for uploading firmware files and then call the OSS [PostObject](~~31988~~) operation to upload firmware files.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Iot&api=CreateOTAFirmware&type=RPC&version=2018-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateOTAFirmware|The operation that you want to perform. Set the value to CreateOTAFirmware. |
|DestVersion|String|Yes|2.0.0|The current version of the firmware. The value can contain letters, digits, periods \(.\), hyphens \(-\), and underscores \(\_\). The value must be 1 to 64 characters in length. |
|FirmwareName|String|Yes|Firmware2|The name of the firmware. The name can contain letters, digits, and underscores \(\_\) and cannot start with an underscore \(\_\). The name must be 4 to 32 characters in length. |
|FirmwareUrl|String|Yes|https://iotx-ota.oss-cn-shanghai.aliyuncs.com/ota/bcd6142594d0183a16d825ad8225\*\*\*\*/A6B3400B70CA4D6D872160D1A91A\*\*\*\*.bin|The URL of the firmware. The URL indicates the storage location of the firmware file in OSS. This parameter is returned when you call the [GenerateOTAUploadURL](~~147310~~) operation to generate the parameters that are required for uploading firmware files. |
|IotInstanceId|String|No|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|The ID of the instance. This parameter is not required for public instances. However, the parameter is required for the instances that you have purchased. |
|FirmwareSign|String|No|93230c3bde425a9d7984a594ac55\*\*\*\*|The signature value of the firmware. The value is calculated by using the **SignMethod** algorithm to sign the firmware file.

 If you do not specify this parameter, the MD5 value of the firmware file in OSS is used as the firmware signature. |
|SignMethod|String|No|MD5|The signature method of the firmware. Valid value: **MD5**.

 Default value: **MD5**. |
|FirmwareSize|Integer|No|900|The size of the firmware. Unit: bytes.

 If you do not specify this parameter, the size of the firmware file in OSS is used as the firmware size. |
|ProductKey|String|No|aluctKe\*\*\*\*|The key of the product to which the firmware belongs. |
|FirmwareDesc|String|No|OTA function updated|The description of the firmware. You can specify a maximum of 100 characters in length. |
|Type|Integer|No|0|The type of the firmware update. Valid values:

 -   **0**: full update. The uploaded firmware file contains a complete firmware package. The system pushes the complete package to the device for update.
-   **1**: delta update. The uploaded firmware file contains only the changed portions between the target version and the current version. The system only pushes the changed portions to the device for update.

 Default value: **0**. |
|SrcVersion|String|No|1.0.0|The current version of the firmware to be updated.

 You can call the [QueryDeviceDetail](~~69594~~) operation to view the **FirmwareVersion** parameter.

 **Note:**

-   If the **Type** parameter is set to **1**, you must specify this parameter, and the value cannot be the same as the target firmware version that is indicated by the **DestVersion** parameter.
-   If the **Type** parameter is set to **0**, this parameter is optional. |
|ModuleName|String|No|WifiConfigModify|The name of the firmware module. The name can contain letters, digits, periods \(.\), hyphens \(-\), and underscores \(\_\). The name must be 1 to 64 characters in length.

 Firmware updates are based on firmware modules of a device. |

In addition to the preceding exclusive request parameters, you must specify common request parameters when calling this API operation. For more information about common request parameters, see [Common parameters](~~30561~~).

## Response parameters

|Element|Type|Example|Description|
|-------|----|-------|-----------|
|Code|String|iot.system.SystemException|The error code returned if the call failed. For more information about error codes, see [Error codes](~~87387~~). |
|Data|Struct| |The firmware information returned if the call was successful. For more information, see the following parameters in Data. |
|FirmwareId|String|s8SSHiKjpBfrM3BSN0z803\*\*\*\*|The ID of the firmware. |
|UtcCreate|String|2019-11-04T06:21:54.607Z|The time when the firmware was created. The time is in UTC. |
|ErrorMessage|String|A system exception occurred.|The error message returned if the call failed. |
|RequestId|String|291438BA-6E10-4C4C-B761-243B9A0D324F|The globally unique ID generated by Alibaba Cloud for the request. |
|Success|Boolean|true|Indicates whether the call was successful. **true** indicates that the call was successful. **false** indicates that the call failed. |

## Samples

Sample requests

```
https://iot.cn-shanghai.aliyuncs.com/?Action=CreateOTAFirmware
&ProductKey=aluctKe****
&FirmwareName=Firmware2
&DestVersion=2.0.0
&FirmwareUrl=https%3A%2F%2iotx-ota.oss-cn-shanghai.aliyuncs.com%2Fota%2F****%2F****.bin
&SignMethod=MD5
&FirmwareSign=93230c3bde425a9d7984a594ac55****
&FirmwareSize=900
&FirmwareDesc=OTA function updated
&Type=0
&ModuleName=WifiConfigModify
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateOTAFirmwareResponse>
    <Data>
        <FirmwareId>s8SSHiKjpBfrM3BSN0z803****</FirmwareId>
        <UtcCreate>2019-11-04T06:21:54.607Z</UtcCreate>
    </Data>
    <RequestId>E4BD5A12-7C1D-4712-A7D5-B2432331165E</RequestId>
    <Success>true</Success>
</CreateOTAFirmwareResponse>
```

`JSON` format

```
{  
  "Data": {
    "FirmwareId": "s8SSHiKjpBfrM3BSN0z803****",
    "UtcCreate": "2019-11-04T06:21:54.607Z"
  },
  "RequestId": "291438BA-6E10-4C4C-B761-243B9A0D324F",
  "Success": true
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Iot).

