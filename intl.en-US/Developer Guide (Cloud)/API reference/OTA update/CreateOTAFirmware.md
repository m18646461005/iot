# CreateOTAFirmware

Creates an update package after the update package file is uploaded to OSS.

## Limits

-   An Alibaba Cloud account can upload a maximum of 500 update packages.
-   Before calling this operation to create update packages, you must call the [GenerateOTAUploadURL](~~147310~~) operation to generate the parameters that are required for uploading the update packages and then call the OSS [PostObject](~~31988~~) operation to upload update package files.
-   Each Alibaba Cloud account can run a maximum of 10 queries per second \(QPS\).

**Note:** RAM users of an Alibaba Cloud account share the quota of the account.


## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Iot&api=CreateOTAFirmware&type=RPC&version=2018-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateOTAFirmware|The operation that you want to perform. Set the value to CreateOTAFirmware. |
|DestVersion|String|Yes|2.0.0|The version number of the update package. The version can contain letters, digits, periods \(.\), hyphens \(-\), and underscores \(\_\). The version name must be 1 to 64 characters in length. |
|FirmwareName|String|Yes|Firmware2|The name of the update package. The name must be 1 to 40 characters in length. The name can contain letters, digits, hyphens \(-\), underscores \(\_\), and parentheses \(\). |
|FirmwareUrl|String|Yes|https://iotx-ota.oss-cn-shanghai.aliyuncs.com/ota/bcd6142594d0183a16d825ad8225\*\*\*\*/A6B3400B70CA4D6D872160D1A91A\*\*\*\*.bin|The URL of the update package. This parameter specifies the storage location of the update package in OSS. This parameter is returned when you call the [GenerateOTAUploadURL](~~147310~~) operation to generate the parameters that are required for uploading update packages. |
|IotInstanceId|String|No|iot-cn-0pp1n8t\*\*\*\*|The instance ID. This parameter is not required for public instances. However, the parameter is required for the instances that you have purchased. |
|FirmwareSign|String|No|93230c3bde425a9d7984a594ac55\*\*\*\*|The signature of the update package. The value is calculated by using the specified **signature method** to sign the update package.

 If you do not specify this parameter, the MD5 value of the update package in OSS is used as the update package signature. |
|SignMethod|String|No|MD5|The signature method of the update package. Valid value: **MD5**.

 Default value: **MD5**. |
|FirmwareSize|Integer|No|900|The size of the update package. Unit: bytes.

 If you do not specify this parameter, the size of the update package file in OSS is used as the update package size. |
|ProductKey|String|No|a1uctKe\*\*\*\*|The key of the product to which the udpate package belongs. |
|FirmwareDesc|String|No|OTA function updated|The description of the update package. The description must be 1 to 100 characters in length. |
|Type|Integer|No|0|The type of the update package. Valid values:

 -   **0**: full. The uploaded update package file contains a full update package. The system pushes a full update package to a device for update.
-   **1**: differential. The uploaded update package file contains only the differences between the latest update package and previous update package. The system only pushes the differences to a device for update.

 Default value: **0**. |
|SrcVersion|String|No|1.0.0|The version number of the OTA module for a device to be updated.

 You can call the [QueryDeviceDetail](~~69594~~) operation to view the **FirmwareVersion** parameter in the response.

 **Note:**

-   If the **Type** parameter is set to **1**, you must specify this parameter, and the value cannot be the same as the update package version that is indicated by the **DestVersion** parameter.
-   If the **Type** parameter is set to **0**, this parameter is optional. |
|ModuleName|String|No|WifiConfigModify|The name of the OTA module. The OTA modules are different upgradeable modules of the devices that belong to the same product.

 **Note:**

-   If you do not specify this parameter, the default OTA module is used. The default module represents the firmware for an entire device.
-   You can call the [CreateOTAModule](~~186066~~) API operation to create a custom OTA moduele. You can call the [ListOTAModuleByProduct](~~186532~~) API operation to query the existing OTA modules of a product. |
|NeedToVerify|Boolean|No|true|Specifies whether the update package must be verified before you create a batch update task.

 -   true: required.
-   false: not required.

 Default value: true. |

In addition to the preceding operation-specific request parameters, you must specify common request parameters when you call this API operation. For more information, see [Common request parameters](~~30561~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|String|iot.system.SystemException|The error code returned if the call fails. For more information about error codes, see [Error codes](~~87387~~). |
|Data|Struct| |The update package information returned if the call succeeds. For more information, see the following Data parameter. |
|FirmwareId|String|s8SSHiKjpBfrM3BSN0z803\*\*\*\*|The ID of the update package. The ID is the unique identifier that is generated by IoT Platform for the update package. |
|UtcCreate|String|2019-11-04T06:21:54.607Z|The time when the update package was created. The time is displayed in UTC. |
|ErrorMessage|String|A system exception occurred.|The error message returned if the call fails. |
|RequestId|String|291438BA-6E10-4C4C-B761-243B9A0D324F|The globally unique ID that Alibaba Cloud generates for the request. |
|Success|Boolean|true|Indicates whether the call succeeds. **true** indicates that the call succeeded. **false** indicates that the call failed. |

## Examples

Sample requests

```
https://iot.cn-shanghai.aliyuncs.com/?Action=CreateOTAFirmware
&ProductKey=a1uctKe****
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

