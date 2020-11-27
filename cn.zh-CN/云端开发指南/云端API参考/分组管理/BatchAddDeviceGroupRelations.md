# BatchAddDeviceGroupRelations

调用该接口添加设备到某一分组（可批量添加设备）。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为500。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=BatchAddDeviceGroupRelations&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|BatchAddDeviceGroupRelations|系统规定参数。取值：BatchAddDeviceGroupRelations。 |
|Device.N.DeviceName|String|是|ZHuPo6sZzv7pOzYh\*\*\*\*|要添加到分组的设备名称。 |
|Device.N.ProductKey|String|是|a1kORrK\*\*\*\*|要添加到分组的设备所属的产品Key。 |
|GroupId|String|是|6VfhebLg5iUe\*\*\*\*|分组ID，分组的全局唯一标识符。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|AlreadyRelatedGroupDeviceCount|Integer|0|原已经添加到此分组的设备数量。 |
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|ExceedTenGroupDeviceCount|Integer|0|请求参数中，已经添加到10个或者10个以上分组的设备数量（一个设备最多添加到10个分组）。 |
|RequestId|String|671D0F8F-FDC7-4B12-93FA-336C079C965A|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |
|SuccessAddedDeviceCount|Integer|2|成功添加到分组的设备数量。 |
|ValidDeviceCount|Integer|2|请求参数中合法的设备数量。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=BatchAddDeviceGroupRelations
&Device.1.DeviceName=ZHuPo6sZzv7pOzYh****
&Device.1.ProductKey=a1kORrK****
&Device.2.DeviceName=rB4V9PDW2FCPmwuf****
&Device.2.ProductKey=a1kORrK****
&GroupId=6VfhebLg5iUe****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<BatchAddDeviceGroupRelationsResponse>
      <SuccessAddedDeviceCount>2</SuccessAddedDeviceCount>
      <ExceedTenGroupDeviceCount>0</ExceedTenGroupDeviceCount>
      <ErrorMessage>2 devices have been added, and 0 devices failed to be added.</ErrorMessage>
      <ValidDeviceCount>2</ValidDeviceCount>
      <AlreadyRelatedGroupDeviceCount>0</AlreadyRelatedGroupDeviceCount>
      <RequestId>671D0F8F-FDC7-4B12-93FA-336C079C965A</RequestId>
      <Success>true</Success>
</BatchAddDeviceGroupRelationsResponse>
```

`JSON` 格式

```
{
    "SuccessAddedDeviceCount":2,
    "ExceedTenGroupDeviceCount":0,
    "ErrorMessage":"2 devices have been added, and 0 devices failed to be added.",
    "ValidDeviceCount":2,
    "AlreadyRelatedGroupDeviceCount":0,
    "RequestId":"671D0F8F-FDC7-4B12-93FA-336C079C965A",
    "Success":true   
}
```

