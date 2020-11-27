# QueryDeviceGroupTagList

调用该接口查询分组标签列表。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为500。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryDeviceGroupTagList&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryDeviceGroupTagList|系统规定参数。取值：QueryDeviceGroupTagList。 |
|GroupId|String|是|W16X8Tvdosec\*\*\*\*|分组ID，分组的全局唯一标识符。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Array of GroupTagInfo| |调用成功时，返回的标签信息。请参见以下**GroupTagInfo**。 |
|GroupTagInfo| | | |
|TagKey|String|room1|标签键。 |
|TagValue|String|bulb|标签值。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|214154FF-9D47-4E3F-AAAD-F4CE67F41060|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryDeviceGroupTagList
&GroupId=W16X8Tvdosec****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryDeviceGroupTagListResponse>
      <Data>
            <GroupTagInfo>
                  <TagValue>bulb</TagValue>
                  <TagKey>room1</TagKey>
            </GroupTagInfo>
      </Data>
      <RequestId>214154FF-9D47-4E3F-AAAD-F4CE67F41060</RequestId>
      <Success>true</Success>
</QueryDeviceGroupTagListResponse>
```

`JSON` 格式

```
{
    "Data":{
        "GroupTagInfo":[
            {
                "TagValue":"bulb",
                "TagKey":"room1"
            }
        ]
    },
    "RequestId":"214154FF-9D47-4E3F-AAAD-F4CE67F41060",
    "Success":true
}
```

