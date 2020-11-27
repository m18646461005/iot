# QueryConsumerGroupList

使用AMQP服务端订阅时，可以调用该接口查询用户所有消费组列表，或按消费组名称进行模糊查询。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryConsumerGroupList&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryConsumerGroupList|系统规定参数。取值：QueryConsumerGroupList。 |
|CurrentPage|Integer|是|1|指定显示返回结果中的第几页，最小值为1。 |
|PageSize|Integer|是|2|指定返回结果中每页显示的消费组数量，最小值为1，最大值为1000。 |
|IotInstanceId|String|否|iot-cn-0pp1n8t\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|Fuzzy|Boolean|否|false|是否使用模糊查询。可选值：

 -   **true**：使用模糊查询，需指定**GroupName**参数。
-   **false**：查询该用户的所有消费组。

 默认为**false**。 |
|GroupName|String|否|A类消费组|模糊查询时要查询的消费组名称，当**Fuzzy**取值为**true**时传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|CurrentPage|Integer|1|当前页码。 |
|Data|Array of ConsumerGroupDTO| |调用成功时，返回的消费组详情，请参见ConsumerGroupDTO。 |
|ConsumerGroupDTO| | | |
|CreateTime|String|2020-05-20T00:05:20.000Z|消费组创建时间。为UTC时间，以毫秒计，格式为“yyyy-MM-dd'T'HH:mm:ss.SSSZ”。 |
|GroupId|String|nJRaJPn5U1JITGf\*\*\*\*\*\*|消费组ID。 |
|GroupName|String|XX消费组1|消费组名称。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|PageCount|Integer|4|返回结果总页数。 |
|PageSize|Integer|2|每页显示的消费组数。 |
|RequestId|String|73B9DF43-7780-47DE-8BED-077729D28BD2|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |
|Total|Integer|8|查询到的消费组总数。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryConsumerGroupList
&CurrentPage=1
&PageSize=2
&Fuzzy=true
&GroupName=A类消费组
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryConsumerGroupListResponse>
    <PageSize>2</PageSize>
    <PageCount>4</PageCount>
    <CurrentPage>1</CurrentPage>
    <Total>8</Total>
    <Data>
        <ConsumerGroupDTO>
            <GroupId>nJRaJPn5U1JITGf******</GroupId>
            <GroupName>A类消费组1</GroupName>
            <CreateTime>2020-05-29T03:37:56.000Z</CreateTime>
        </ConsumerGroupDTO>
        <ConsumerGroupDTO>
            <GroupId>qJRaJPndeefwgef******</GroupId>
            <GroupName>A类消费组2</GroupName>
            <CreateTime>2020-01-17T07:27:01.000Z</CreateTime>
        </ConsumerGroupDTO>
    </Data>
    <RequestId>73B9DF43-7780-47DE-8BED-077729D28BD2</RequestId>
    <Success>true</Success>
</QueryConsumerGroupListResponse>
```

`JSON` 格式

```
{
    "PageSize": 2,
    "PageCount": 4,
    "CurrentPage": 1,
    "Total": 8,
    "Data": {
        "ConsumerGroupDTO": [
            {
                "GroupId": "nJRaJPn5U1JITGf******",
                "GroupName": "A类消费组1",
                "CreateTime": "2020-05-29T03:37:56.000Z"
            },
            {
                "GroupId": "qJRaJPndeefwgef******",
                "GroupName": "A类消费组2",
                "CreateTime": "2020-01-17T07:27:01.000Z"
            }
        ]
    },
  "RequestId": "73B9DF43-7780-47DE-8BED-077729D28BD2",
  "Success": true
}
```

