# ListOTAModuleByProduct

Queries all OTA modules of a product.

Each Alibaba Cloud account can run a maximum of 10 queries per second \(QPS\).

**Note:** RAM users share the quota of the Alibaba Cloud account.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Iot&api=ListOTAModuleByProduct&type=RPC&version=2018-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListOTAModuleByProduct|The operation that you want to perform. Set the value to ListOTAModuleByProduct. |
|ProductKey|String|Yes|a1uctKe\*\*\*\*|The ProductKey of the product. |
|IotInstanceId|String|No|iot-cn-0pp1n8t\*\*\*\*|The instance ID. This parameter is not required for the public instance but required for your purchased instances. |

In addition to the preceding operation-specific request parameters, you must specify common request parameters when you call this API operation. For more information, see [Common request parameters](~~30561~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|String|iot.system.SystemException|The error code that is returned if the call fails. For more information, see[Error codes](~~87387~~). |
|Data|Array of OtaModuleDTO| |The list of OTA modules that is returned if the call is successful. |
|AliasName|String|Barcode\_scanner|The alias of the OTA module. |
|Desc|String|This module represents the firmware of the barcode scanner.|The description of the OTA module. |
|GmtCreate|String|Wed, 20-Feb-2019 02:16:09 GMT|The time when the OTA module was created. The time is in the GMT format. |
|GmtModified|String|Wed, 20-Feb-2019 02:16:09 GMT|The last time when the OTA module was updated. The time is in the GMT format. |
|ModuleName|String|barcodeScanner|The name of the OTA module. |
|ProductKey|String|aluctKe\*\*\*\*|The ProductKeyof the product. |
|ErrorMessage|String|A system exception has occurred.|The error message that is returned if the call fails. |
|RequestId|String|74C2BB8D-1D6F-41F5-AE68-6B2310883F63|The globally unique ID that Alibaba Cloud generated for the request. |
|Success|Boolean|true|Indicates whether the call was successful.

-   **true**: The call was successful.
-   **false**: The call failed. |

## Examples

Sample requests

```
https://iot.cn-shanghai.aliyuncs.com/?Action=ListOTAModuleByProduct
&ProductKey=a1uctKe****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListOTAModuleByProductResponse>
      <RequestId>74C2BB8D-1D6F-41F5-AE68-6B2310883F63</RequestId>
      <Data>
            <Desc>This module represents the firmware of the barcode scanner.</Desc>
            <GmtCreate>Wed, 20-Feb-2019 02:16:09 GMT</GmtCreate>
            <ModuleName>barcodeScanner</ModuleName>
            <AliasName>Barcode_scanner</AliasName>
            <GmtModified>Wed, 20-Feb-2019 02:16:09 GMT</GmtModified>
            <ProductKey>a1uctKe****</ProductKey>
      </Data>
      <Success>true</Success>
</ListOTAModuleByProductResponse>
```

`JSON` format

```
{
    "Data": {
        "Desc": "This module represents the firmware of the barcode scanner.",
        "GmtCreate": "Wed, 20-Feb-2019 02:16:09 GMT",
        "ModuleName": "barcodeScanner",
        "AliasName": "Barcode_scanner",
        "GmtModified": "Wed, 20-Feb-2019 02:16:09 GMT",
        "ProductKey": "a1uctKe****"
    },
    "RequestId": "74C2BB8D-1D6F-41F5-AE68-6B2310883F63",
    "Success": true
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Iot).

