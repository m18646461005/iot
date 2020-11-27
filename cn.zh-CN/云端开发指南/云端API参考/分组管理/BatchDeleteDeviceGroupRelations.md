# BatchDeleteDeviceGroupRelations

调用该接口批量删除指定分组中的设备。（只删除设备与分组的关联关系，不会删除设备本身。）

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为50。

**说明：** 子RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=BatchDeleteDeviceGroupRelations&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|BatchDeleteDeviceGroupRelations|系统规定参数。取值：BatchDeleteDeviceGroupRelations。 |
|Device.N.DeviceName|String|是|ZHuPo6sZzv7pOzYh\*\*\*\*|要从分组中删除的设备名称。 |
|Device.N.ProductKey|String|是|a1kORrK\*\*\*\*|要从分组中删除的设备所属产品的ProductKey。 |
|GroupId|String|是|W16X8Tvdosec\*\*\*\*|分组ID，分组的全局唯一标识符。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|AlreadyRelatedGroupDeviceCount|Integer|2|删除前，已添加到此分组的设备数量。 |
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|8739385E-143F-4389-B900-B7DF9174CE0D|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |
|SuccessDeviceCount|Integer|2|成功从分组中删除的设备数量。 |
|ValidDeviceCount|Integer|2|请求参数中要删除的设备中，有效的设备数量（即可删除的设备数量）。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=BatchDeleteDeviceGroupRelations
&Device.1.DeviceName=ZHuPo6sZzv7pOzYh****
&Device.1.ProductKey=a1kORrK****
&Device.2.DeviceName=rB4V9PDW2FCPmwuf****
&Device.2.ProductKey=a1kORrK****
&GroupId=W16X8Tvdosec****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<BatchDeleteDeviceGroupRelationsResponse>
      <SuccessDeviceCount>2</SuccessDeviceCount>
      <ValidDeviceCount>2</ValidDeviceCount>
      <AlreadyRelatedGroupDeviceCount>2</AlreadyRelatedGroupDeviceCount>
      <RequestId>8739385E-143F-4389-B900-B7DF9174CE0D</RequestId>
      <Success>true</Success>
</BatchDeleteDeviceGroupRelationsResponse>
```

`JSON` 格式

```
{
    "SuccessDeviceCount":2,
    "ValidDeviceCount":2,
    "AlreadyRelatedGroupDeviceCount":2,
    "RequestId":"8739385E-143F-4389-B900-B7DF9174CE0D",
    "Success":true    
}
```

