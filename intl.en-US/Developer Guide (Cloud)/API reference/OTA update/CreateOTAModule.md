# CreateOTAModule

Creates an OTA module for a product.

## Limits

The OTA modules are different upgradeable modules of the devices that belong to the same product. The default module represents the firmware for an entire device. You can call this operation to create a custom OTA module.

-   You can create a maximum of 10 custom OTA modules for each product.
-   After the OTA module is created, you cannot modify its name. You can call the [UpdateOTAModule](~~186061~~) operation to modify its alias and description.
-   Each Alibaba Cloud account can run a maximum of 10 queries per second \(QPS\).

**Note:** RAM users share the quota of the Alibaba Cloud account.


## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Iot&api=CreateOTAModule&type=RPC&version=2018-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateOTAModule|The operation that you want to perform. Set the value to CreateOTAModule. |
|ModuleName|String|Yes|barcodeScanner|The name of the OTA module. The name is unique in a product and cannot be modified. The name can contain letters, digits, periods \(.\), hyphens \(-\), and underscores \(\_\). It must be 1 to 64 characters in length. |
|ProductKey|String|Yes|a1Le6d0\*\*\*\*|The ProductKey of the product to which the OTA module belongs. |
|AliasName|String|No|Barcode\_scanner|The alias of the OTA module. The alias can contain letters, digits, periods \(.\), hyphens \(-\), and underscores \(\_\). It must be 1 to 64 characters in length. |
|IotInstanceId|String|No|iot-cn-0pp1n8t\*\*\*\*|The instance ID. This parameter is not required for the public instance but required for your purchased instances. |
|Desc|String|No|The firmware module of the barcode scanner.|The description of the OTA module. The description can be up to 100 characters in length. |

In addition to the preceding operation-specific request parameters, you must specify common request parameters when you call this API operation. For more information about common request parameters, see [Common request parameters](~~30561~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|String|iot.system.SystemException|The error code that is returned if the call fails. For more information, see [Error codes](~~87387~~). |
|ErrorMessage|String|A system exception has occurred.|The error message that is returned if the call fails. |
|RequestId|String|74C2BB8D-1D6F-41F5-AE68-6B2310883F63|The globally unique ID that Alibaba Cloud generated for the request. |
|Success|Boolean|true|Indicates whether the call was successful.

 -   **true**: The call was successful.
-   **false**: The call failed. |

## Examples

Sample requests

```
https://iot.cn-shanghai.aliyuncs.com/?Action=CreateOTAModule
&ModuleName=barcodeScanner
&ProductKey=a1Le6d0****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateOTAModuleResponse>
     <RequestId>29EC7245-0FA4-4BB6-B4F5-5F04818FDFB1</RequestId>
     <Success>true</Success>
</CreateOTAModuleResponse>
```

`JSON` format

```
{
  "RequestId": "9F41D14E-CB5F-4CCE-939C-057F39E688F5",
  "Success": true
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Iot).

