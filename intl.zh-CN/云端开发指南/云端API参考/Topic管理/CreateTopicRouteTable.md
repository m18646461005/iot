# CreateTopicRouteTable

调用该接口新建Topic间的消息路由关系。

## 限制说明

-   一个源Topic最多可对应100个目标Topic。
-   源Topic所属的设备必须为已激活设备。
-   源Topic和目标Topic均仅支持自定义Topic。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为50。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=CreateTopicRouteTable&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateTopicRouteTable|系统规定参数。取值：CreateTopicRouteTable。 |
|DstTopic.N|RepeatList|是|/x7aWKW9\*\*\*\*/deviceNameTest1/user/add|目标Topic列表，即从**SrcTopic**订阅消息的Topic列表。即使只有一个Topic，也使用数组格式。如`DstTopic.1=/x7aWKW9****/deviceNameTest1/user/add`，`DstTopic.2=/x7aWKW9****/deviceNameTest2/user/delete`。 |
|SrcTopic|String|是|/x7aWKW9\*\*\*\*/testDataToDataHub/user/update|源Topic，即被订阅的Topic。如`SrcTopic=/x7aWKW9****/testDataToDataHub/user/update`。 |
|IotInstanceId|String|否|iot-cn-0pp1n8t\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|ErrorMessage|String|iot.system.SystemException|调用失败时，返回的出错信息。 |
|FailureTopics|List|\["/2Fx7aWKW9\*\*\*\*/FdeviceNameTest2/user/delete"\]|未能成功创建路由关系的Topic列表。 |
|IsAllSucceed|Boolean|true|指定的Topic间的消息路由关系是否全部新建成功。

 -   **true**表示全部新建成功。
-   **false**表示未全部新建成功。 |
|RequestId|String|FCC27691-9151-4B93-9622-9C90F30542EC|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=CreateTopicRouteTable
&SrcTopic=%2Fx7aWKW9****%2FtestDataToDataHub%2Fuser%2Fupdate
&DstTopic.1=%2Fx7aWKW9****%2FdeviceNameTest1%2Fuser%2Fadd
&DstTopic.2=%2Fx7aWKW9****%2FdeviceNameTest2%2Fuser%2Fdelete
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CreateTopicRouteTableResponse>
  <RequestId>32B9828A-25DD-48E2-8E26-D1664B341940</RequestId>
  <FailureTopics></FailureTopics>
  <Success>true</Success>
</CreateTopicRouteTableResponse>
```

`JSON` 格式

```
{
	"RequestId": "32B9828A-25DD-48E2-8E26-D1664B341940",
	"FailureTopics": {
		"Topic": []
	},
	"Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。

