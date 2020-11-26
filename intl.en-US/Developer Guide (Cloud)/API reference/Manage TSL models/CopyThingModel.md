---
keyword: [IoT, Internet of Things, CopyThingModel]
---

# CopyThingModel

Copies the Thing Specification Language \(TSL\) of a specified product to a target product.

## Limits

The category keys of the source product and target product must be the same.

## Request parameters

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set the value to CopyThingModel.|
|SourceProductKey|String|Yes|The key of the source product. You can go to the Product page of the IoT Platform console to view the product key. You can also call the [QueryProductList](/intl.en-US/Developer Guide (Cloud)/API reference/Manage products/QueryProductList.md) operation to retrieve the value of the ProductKey parameter. |
|TargetProductKey|String|Yes|The key of the target product. You can go to the Product page of the IoT Platform console to view the product key. You can also call the [QueryProductList](/intl.en-US/Developer Guide (Cloud)/API reference/Manage products/QueryProductList.md) operation to retrieve the value of the ProductKey parameter. |
|SourceModelVersion|String|Yes|The version of the TSL to be copied. You can call the [ListThingModelVersion](/intl.en-US/Developer Guide (Cloud)/API reference/Manage TSL models/ListThingModelVersion.md) operation to view the TSL version. |
|IotInstanceId|String|No|The ID of the instance. This parameter is not required for public instances. However, the parameter is required for the instances that you have purchased.|
|Common request parameters|-|Yes|For more information, see [Common parameters](/intl.en-US/Developer Guide (Cloud)/API reference/Common parameters.md).|

## Response parameters

|Parameter|Type|Description|
|:--------|:---|:----------|
|RequestId|String|The ID of the request.|
|Success|Boolean|Indicates whether the call was successful. true indicates that the call was successful. false indicates that the call failed.|
|ErrorMessage|String|The error message returned if the call failed.|
|Code|String|The error code returned if the call failed. For information about error codes, see [Error codes](/intl.en-US/Developer Guide (Cloud)/API reference/Error codes.md).|

## Examples

Sample requests

```
https://iot.cn-shanghai.aliyuncs.com/?Action=CopyThingModel
&ProductKeySource=a1rYuVF****
&ProductKeyTarget=a1bPo9p****
&SourceModelVersion=v1.0.0
&<Common request parameters>
```

Sample responses

-   JSON format

    ```
    {
      "RequestId": "9E76053E-26ED-4AB4-AE58-8AFC3F1E7E8E",
      "Success": true
    }
    ```

-   XML format

    ```
    <CopyThingModelResponse>
      <RequestId>9E76053E-26ED-4AB4-AE58-8AFC3F1E7E8E</RequestId>
      <Success>true</Success>
    </CopyThingModelResponse>
    ```


