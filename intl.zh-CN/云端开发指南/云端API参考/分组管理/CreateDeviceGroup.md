# CreateDeviceGroup

调用该接口新建分组。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为500。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=CreateDeviceGroup&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateDeviceGroup|系统规定参数。取值：CreateDeviceGroup。 |
|GroupName|String|是|grouptest|分组名称。名称可包含中文汉字、英文字母、数字和下划线（\_）。

 长度范围为4~30个字符（一个中文汉字占二个字符）。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|SuperGroupId|String|否|SuperGroupId1|父组ID。

 若要创建的是一级分组，则不传入此参数。 |
|GroupDesc|String|否|Group test|分组描述。长度限制为100字符（一个中文汉字占一个字符）。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Struct| |调用成功时，返回的分组信息。 |
|GroupDesc|String|Group test|分组描述。 |
|GroupId|String|HtMLECKbdJQL\*\*\*\*|分组ID，系统为分组生成的全局唯一标识符。 |
|GroupName|String|grouptest|分组名称。 |
|UtcCreate|String|2018-10-17T11:19:31.000Z|创建时间。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|4D6D7F71-1C94-4160-8511-EFF4B8F0634D|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=CreateDeviceGroup
&GroupDesc=Group test
&GroupName=grouptest
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CreateDeviceGroupResponse>
      <Data>
            <GroupDesc>Group test</GroupDesc>
            <GroupName>grouptest</GroupName>
            <UtcCreate>2018-10-17T11:19:31.000Z</UtcCreate>
            <GroupId>HtMLECKbdJQL****</GroupId>
      </Data>
      <RequestId>4D6D7F71-1C94-4160-8511-EFF4B8F0634D</RequestId>
      <Success>true</Success>
</CreateDeviceGroupResponse>
```

`JSON` 格式

```
{
    "Data":{
        "GroupDesc":"Group test",
        "GroupName":"grouptest",
        "UtcCreate":"2018-10-17T11:19:31.000Z",
        "GroupId":"HtMLECKbdJQL****"
    },
    "RequestId":"4D6D7F71-1C94-4160-8511-EFF4B8F0634D",
    "Success":true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。

