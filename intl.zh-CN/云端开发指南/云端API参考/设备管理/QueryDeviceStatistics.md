# QueryDeviceStatistics

调用该接口查询设备统计数据。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为50。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryDeviceStatistics&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryDeviceStatistics|系统规定参数。取值：QueryDeviceStatistics。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|ProductKey|String|否|a1BwAGV\*\*\*\*|要查询的设备所隶属的产品Key。

 -   传入产品Key，将返回该产品下的设备统计数据。
-   不传入该参数，则返回账号下所有设备统计数据。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见 [公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Struct| |调用成功时，返回的设备统计信息。 |
|activeCount|Long|10|已激活的设备数量。 |
|deviceCount|Long|100|设备总数。 |
|onlineCount|Long|10|在线的设备数量。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryDeviceStatistics
&ProductKey=a1BwAGV****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryDeviceStatisticsResponse>
  <Data>
        <deviceCount>2</deviceCount>
        <activeCount>2</activeCount>
        <onlineCount>0</onlineCount>
  </Data>
  <RequestId>8AC026D2-6F16-4719-A396-969D63DCA138</RequestId>
  <Success>true</Success>
</QueryDeviceStatisticsResponse>
```

`JSON` 格式

```
{
	"Data": {
		"deviceCount": 2,
		"activeCount": 2,
		"onlineCount": 0
	},
	"RequestId": "8AC026D2-6F16-4719-A396-969D63DCA138",
	"Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。

