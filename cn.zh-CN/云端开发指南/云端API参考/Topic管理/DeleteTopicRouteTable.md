# DeleteTopicRouteTable

调用该接口删除指定自定义Topic的路由关系。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为50。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=DeleteTopicRouteTable&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteTopicRouteTable|系统规定参数。取值：DeleteTopicRouteTable。 |
|DstTopic.N|RepeatList|是|/x7aWKW94bb8/deviceNameTest1/user/add|目标Topic，即从**SrcTopic**订阅消息的Topic。如，`DstTopic.1=/x7aWKW9****/deviceNameTest1/user/add`，`DstTopic.2=/x7aWKW9****/deviceNameTest2/user/delete`。 |
|SrcTopic|String|是|/x7aWKW94bb8/testDataToDataHub/user/update|源Topic，即被订阅的Topic。如，`SrcTopic.1=/x7aWKW9****/testDataToDataHub/user/update`。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|FailureTopics|List|\["/x7aWKW94bb8/deviceNameTest2/user/delete"\]|未能成功删除路由关系的Topic列表。 |
|IsAllSucceed|Boolean|true|指定的Topic路由关系是否全部成功删除。

 -   **true**表示全部成功删除。
-   **false**表示未全部成功删除。 |
|RequestId|String|FCC27691-9151-4B93-9622-9C90F30542EC|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=DeleteTopicRouteTable
&SrcTopic=%2Fx7aWKW94bb8%2FtestDataToDataHub%2Fuser%2Fupdate
&DstTopic.1=%2Fx7aWKW94bb8%2FdeviceNameTest1%2Fuser%2Fadd
&DstTopic.2=%2Fx7aWKW94bb8%2FdeviceNameTest2%2Fuser%2Fdelete
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DeleteTopicRouteTableResponse>
  <RequestId>9DEBEF66-2B75-4CB2-BF19-1488802F4381</RequestId>
  <FailureTopics></FailureTopics>
  <Success>true</Success>
</DeleteTopicRouteTableResponse>
```

`JSON` 格式

```
{
	"RequestId": "9DEBEF66-2B75-4CB2-BF19-1488802F4381",
	"FailureTopics": {
		"Topic": []
	},
	"Success": true
}
```

