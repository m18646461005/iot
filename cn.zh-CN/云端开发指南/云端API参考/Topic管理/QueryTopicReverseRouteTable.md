# QueryTopicReverseRouteTable

调用该接口查询指定自定义Topic订阅的源Topic，即反向路由表。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为50。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryTopicReverseRouteTable&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryTopicReverseRouteTable|系统规定参数。取值：QueryTopicReverseRouteTable。 |
|Topic|String|是|/x7aWKW94bb8/testDataToDataHub/user/update|要查询的目标Topic，即接收消息的Topic。 |
|IotInstanceId|String|否|iot-cn-0pp1n8t\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|RegionId|String|否|cn-shanghai|设备所在地域（与控制台上的地域对应），如cn-shanghai。

 **说明：** 目前此参数已包含在公共请求参数中，不再作为API特有参数传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|FCC27691-9151-4B93-9622-9C90F30542EC"|阿里云为该请求生成的唯一标识符。 |
|SrcTopics|List|\["/CXi4\*\*\*/device1/user/get","/CXi4\*\*\*/device4/user/get"\]|调用成功时，返回的源Topic列表，即被订阅的Topic列表。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryTopicReverseRouteTable
&Topic=%2Fx7aWKW94bb8%2FtestDataToDataHub%2Fuser%2Fupdate
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryTopicReverseRouteTableResponse>
  <SrcTopics>
        <Topic>/CXi4***/device1/user/get</Topic>
        <Topic>/CXi4***/device4/user/get</Topic>
  </SrcTopics>
  <RequestId>C5515170-3C1F-4004-A7C1-181E7955BC73</RequestId>
  <Success>true</Success>
</QueryTopicReverseRouteTableResponse>
```

`JSON` 格式

```
{
	"SrcTopics": {
		"Topic": ["/CXi4***/device1/user/get","/CXi4***/device4/user/get"]
	},
	"RequestId": "C5515170-3C1F-4004-A7C1-181E7955BC73",
	"Success": true
}
```

