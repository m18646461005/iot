# QueryDeviceGroupByTags

调用该接口根据标签查询设备分组。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryDeviceGroupByTags&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryDeviceGroupByTags|系统规定参数。取值：QueryDeviceGroupByTags。 |
|Tag.N.TagKey|String|是|group|分组标签键（key）。 |
|Tag.N.TagValue|String|是|tag|分组标签值（value）。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|CurrentPage|Integer|否|1|指定显示查询结果的第几页。默认值是1。 |
|PageSize|Integer|否|10|指定每页显示的记录数。默认值是10。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Array of DeviceGroup| |调用成功时，返回分组信息。 |
|DeviceGroup| | | |
|GroupId|String|Z0ElGF5aqc0t\*\*\*\*|分组ID。 |
|GroupName|String|test11|分组名称。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|Page|Integer|1|当前页码。 |
|PageCount|Integer|1|总页数。 |
|PageSize|Integer|10|每页显示的记录数。 |
|RequestId|String|9599EE98-1642-4FCD-BFC4-039E458A4693|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |
|Total|Integer|1|总记录数。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryDeviceGroupByTags
&Tag.1.TagKey=group
&Tag.1.TagValue=tag
&CurrentPage=1
&PageSize=10
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryDeviceGroupByTagsResponse> 
    <PageCount>1</PageCount>  
    <Data> 
        <DeviceGroup> 
            <GroupName>test11</GroupName>  
            <GroupId>Z0ElGF5aqc0t****</GroupId> 
        </DeviceGroup> 
    </Data>  
    <Page>1</Page>  
    <PageSize>10</PageSize>  
    <RequestId>9599EE98-1642-4FCD-BFC4-039E458A4693</RequestId>  
    <Success>true</Success>  
    <Total>1</Total> 
</QueryDeviceGroupByTagsResponse>
```

`JSON` 格式

```
{
    "PageCount": 1, 
    "Data": {
        "DeviceGroup": [
            {
                "GroupName": "test11", 
                "GroupId": "Z0ElGF5aqc0t****"
            }
        ]
    }, 
    "Page": 1, 
    "PageSize": 10, 
    "RequestId": "9599EE98-1642-4FCD-BFC4-039E458A4693", 
    "Success": true, 
    "Total": 1
}
```

