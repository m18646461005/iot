# QueryTopicRouteTable

调用该接口查询向指定自定义Topic订阅消息的目标Topic，即指定Topic的路由表。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为50。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryTopicRouteTable&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryTopicRouteTable|系统规定参数。取值：QueryTopicRouteTable。 |
|Topic|String|是|/x7aWKW94bb8/testDataToDataHub/user/update|要查询的源Topic，即发布消息的Topic。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|DstTopics|List|\["/CXi4\*\*\*/device2/get","/CXi4\*\*\*/device3/get"\]|调用成功时，返回的目标Topic列表，即向源Topic订阅消息的Topic列表。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|FCC27691-9151-4B93-9622-9C90F30542EC|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryTopicRouteTable
&Topic=%2Fx7aWKW94bb8%2FtestDataToDataHub%2Fuser%2Fupdate
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryTopicRouteTableResponse>
  <DstTopics>
        <Topic>/a1T27vz****/${deviceName}/user/submit/update</Topic>
  </DstTopics>
  <RequestId>D6CB2387-0D65-4240-9436-A2E18B434E31</RequestId>
  <Success>true</Success>
</QueryTopicRouteTableResponse>
```

`JSON` 格式

```
{
	"DstTopics": {
		"Topic": [
			"/a1T27vz****/${deviceName}/user/submit/update"
		]
	},
	"RequestId": "D6CB2387-0D65-4240-9436-A2E18B434E31",
	"Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。

