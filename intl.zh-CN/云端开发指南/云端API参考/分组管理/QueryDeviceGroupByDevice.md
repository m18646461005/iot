# QueryDeviceGroupByDevice

调用该接口查询某一设备所在的分组列表。

## 限制说明

-   一个设备最多能被添加到10个分组中 。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为50。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryDeviceGroupByDevice&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryDeviceGroupByDevice|系统规定参数。取值：QueryDeviceGroupByDevice。 |
|DeviceName|String|是|test456|设备名称。 |
|ProductKey|String|是|a1SKk9K\*\*\*\*|设备所属产品的ProductKey。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|GroupInfos|Array of GroupInfo| |调用成功时，返回的分组信息。详情请参见以下GroupInfo。 |
|GroupInfo| | | |
|GroupDesc|String|father desc|分组描述。 |
|GroupId|String|6a3FF2XE2BKa\*\*\*\*|分组ID。 |
|GroupName|String|father1543152336554|分组名称。 |
|UtcCreate|String|2018-11-25T13:25:37.000Z|分组的创建时间。 |
|RequestId|String|7941C8CD-7764-4A94-8CD9-E2762D4A73AC|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryDeviceGroupByDevice
&DeviceName=test456
&ProductKey=a1SKk9K****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryDeviceGroupByDeviceResponse>
      <RequestId>7941C8CD-7764-4A94-8CD9-E2762D4A73AC</RequestId>
      <GroupInfos>
            <GroupInfo>
                  <GroupDesc>father desc</GroupDesc>
                  <GroupName>father1543152336554</GroupName>
                  <UtcCreate>2018-11-25T13:25:37.000Z</UtcCreate>
                  <GroupId>6a3FF2XE2BKayWsM</GroupId>
            </GroupInfo>
      </GroupInfos>
      <Success>true</Success>
</QueryDeviceGroupByDeviceResponse>
```

`JSON` 格式

```
{
  "RequestId": "7941C8CD-7764-4A94-8CD9-E2762D4A73AC",
  "GroupInfos": {
    "GroupInfo": [
      {
        "GroupDesc": "father desc",
        "GroupName": "father1543152336554",
        "UtcCreate": "2018-11-25T13:25:37.000Z",
        "GroupId": "6a3FF2XE2BKa****"
      }
    ]
  },
  "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。

