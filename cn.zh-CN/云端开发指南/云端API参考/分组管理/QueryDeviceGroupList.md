# QueryDeviceGroupList

调用该接口分页查询分组列表。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为100。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryDeviceGroupList&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryDeviceGroupList|系统规定参数。取值：QueryDeviceGroupList。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|SuperGroupId|String|否|8vDubXr4nUvZkNgk9mle010200|父组ID。查询某父组下的子分组列表时，需传入此参数。 |
|GroupName|String|否|GroupName1|分组名称。

 -   传入分组名称，则根据名称进行查询。支持分组名称模糊查询。
-   若不传入此参数，则进行全量分组查询。 |
|CurrentPage|Integer|否|1|指定从返回结果中的第几页开始显示。默认值为1。 |
|PageSize|Integer|否|10|每页记录数。最大值是200。默认值是10。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|CurrentPage|Integer|1|当前页号。 |
|Data|Array of GroupInfo| |调用成功时，返回的分组信息。请参见GroupInfo。

 **说明：** 返回的分组信息按照分组创建时间倒序排列。 |
|GroupInfo| | | |
|GroupDesc|String|usefulGroup|分组描述。 |
|GroupId|String|Kzt9FD8wje8o\*\*\*\*|分组ID。 |
|GroupName|String|test1|分组名称。 |
|UtcCreate|String|2018-10-09T02:58:34.000Z|分组创建时间。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|PageCount|Integer|3|总页数。 |
|PageSize|Integer|10|每页记录数。 |
|RequestId|String|BEFCA316-D6C7-470C-81ED-1FF4FFD4AA0D|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |
|Total|Integer|24|总记录数。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryDeviceGroupList
&PageSize=10
&CurrentPage=1
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryDeviceGroupListResponse>
      <PageCount>3</PageCount>
      <Data>
            <GroupInfo>
                  <GroupName>test1</GroupName>
                  <UtcCreate>2018-10-09T02:58:34.000Z</UtcCreate>
                  <GroupId>Kzt9FD8wje8o****</GroupId>
            </GroupInfo>
            <GroupInfo>
                  <GroupName>test2</GroupName>
                  <UtcCreate>2018-10-09T02:56:40.000Z</UtcCreate>
                  <GroupId>0ayrSQ3DSd7u****</GroupId>
            </GroupInfo>
            <GroupInfo>
                  <GroupDesc>Test</GroupDesc>
                  <GroupName>test3</GroupName>
                  <UtcCreate>2018-09-16T05:38:27.000Z</UtcCreate>
                  <GroupId>oWXlIQeFZtzC****</GroupId>
            </GroupInfo>
            <GroupInfo>
                  <GroupName>ylv0915</GroupName>
                  <UtcCreate>2018-09-15T04:51:56.000Z</UtcCreate>
                  <GroupId>SfEiVapLPUjBVvSq</GroupId>
            </GroupInfo>
            <GroupInfo>
                  <GroupName>ydlv</GroupName>
                  <UtcCreate>2018-09-14T14:35:51.000Z</UtcCreate>
                  <GroupId>z2S2h9NsDTZm****</GroupId>
            </GroupInfo>
            <GroupInfo>
                  <GroupName>ldh_group_3</GroupName>
                  <UtcCreate>2018-09-14T12:26:20.000Z</UtcCreate>
                  <GroupId>chn5fkjinXGc****</GroupId>
            </GroupInfo>
            <GroupInfo>
                  <GroupDesc>ddd</GroupDesc>
                  <GroupName>ylvgisbim</GroupName>
                  <UtcCreate>2018-09-14T11:41:20.000Z</UtcCreate>
                  <GroupId>ncUZ8DjWYaB9****</GroupId>
            </GroupInfo>
            <GroupInfo>
                  <GroupName>abc</GroupName>
                  <UtcCreate>2018-09-14T09:14:30.000Z</UtcCreate>
                  <GroupId>zpdvwxzBdt4F****</GroupId>
            </GroupInfo>
            <GroupInfo>
                  <GroupName>test11</GroupName>
                  <UtcCreate>2018-09-14T07:22:39.000Z</UtcCreate>
                  <GroupId>BTaudF16X2xK****</GroupId>
            </GroupInfo>
            <GroupInfo>
                  <GroupName>testy</GroupName>
                  <UtcCreate>2018-09-14T01:58:06.000Z</UtcCreate>
                  <GroupId>PrTm3VOeggPw****</GroupId>
            </GroupInfo>
      </Data>
      <PageSize>10</PageSize>
      <RequestId>BEFCA316-D6C7-470C-81ED-1FF4FFD4AA0D</RequestId>
      <CurrentPage>1</CurrentPage>
      <Success>true</Success>
      <Total>24</Total>
</QueryDeviceGroupListResponse>
```

`JSON` 格式

```
{
    "PageCount":3,
    "Data":{
        "GroupInfo":[
            {
                "GroupName":"test1",
                "UtcCreate":"2018-10-09T02:58:34.000Z",
                "GroupId":"Kzt9FD8wje8o****"
            },
            {
                "GroupName":"test2",
                "UtcCreate":"2018-10-09T02:56:40.000Z",
                "GroupId":"0ayrSQ3DSd7uXXXC"
            },
            {
                "GroupDesc":"Test",
                "GroupName":"test3",
                "UtcCreate":"2018-09-16T05:38:27.000Z",
                "GroupId":"oWXlIQeFZtzC****"
            },
            {
                "GroupName":"ylv0915",
                "UtcCreate":"2018-09-15T04:51:56.000Z",
                "GroupId":"SfEiVapLPUjB****"
            },
            {
                "GroupName":"ydlv",
                "UtcCreate":"2018-09-14T14:35:51.000Z",
                "GroupId":"z2S2h9NsDTZm****"
            },
            {
                "GroupName":"ldh_group_3",
                "UtcCreate":"2018-09-14T12:26:20.000Z",
                "GroupId":"chn5fkjinXGc7pGl"
            },
            {
                "GroupDesc":"ddd",
                "GroupName":"ylvgisbim",
                "UtcCreate":"2018-09-14T11:41:20.000Z",
                "GroupId":"ncUZ8DjWYaB9****"
            },
            {
                "GroupName":"abc",
                "UtcCreate":"2018-09-14T09:14:30.000Z",
                "GroupId":"zpdvwxzBdt4F****"
            },
            {
                "GroupName":"test11",
                "UtcCreate":"2018-09-14T07:22:39.000Z",
                "GroupId":"BTaudF16X2xK****"
            },
            {
                "GroupName":"testy",
                "UtcCreate":"2018-09-14T01:58:06.000Z",
                "GroupId":"PrTm3VOeggPw****"
            }
        ]
    },
    "PageSize":10,
    "RequestId":"BEFCA316-D6C7-470C-81ED-1FF4FFD4AA0D",
    "CurrentPage":1,
    "Success":true,
    "Total":24
}
```

