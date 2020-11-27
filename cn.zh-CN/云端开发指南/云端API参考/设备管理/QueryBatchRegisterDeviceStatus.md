# QueryBatchRegisterDeviceStatus

调用该接口查询批量注册设备申请的处理状态和结果。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为30。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryBatchRegisterDeviceStatus&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryBatchRegisterDeviceStatus|系统规定参数。取值：QueryBatchRegisterDeviceStatus。 |
|ApplyId|Long|是|1295006|要查询的申请批次ID。申请批次ID在成功调用[BatchRegisterDeviceWithApplyId](~~69514~~)或[BatchRegisterDevice](~~69473~~)接口的返回结果中。 |
|ProductKey|String|是|a1BwAGV\*\*\*\*|要查询的设备所隶属的产品ProductKey。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。

 **说明：** 目前仅华东2（cn-shanghai）地域支持设备X.509证书，如果地域不是华东2（cn-shanghai），则不能生成X.509证书，返回错误码iot.device.RegionNotSupportX509。 |
|Data|Struct| |调用成功时，返回的状态信息。 |
|InvalidList|List|\{ "Name": \[\] \}|-   当返回**Status**参数值为**CHECK\_FAILED**或**CREATE\_FAILED**时，返回创建失败的设备名称集合。
-   当返回**Status**参数值为**CHECK\_SUCCESS**或**CREATE\_SUCCESS**时，该参数为空数组。 |
|Status|String|CREATE\_SUCCESS|申请单的处理状态和结果，取值：

 -   **CHECK**：正在校验设备名称。
-   **CHECK\_SUCCESS**：申请单中的所有设备名称校验成功。
-   **CHECK\_FAILED**：申请单中有设备名称校验失败。
-   **CREATE**：正在创建设备。
-   **CREATE\_SUCCESS**：申请单中的所有设备创建成功。

**说明：** 当设备所属产品的认证类型是X.509证书时，表示所有设备和对应的X.509证书都创建成功。

-   **CREATE\_FAILED**：申请单中有设备创建失败。

**说明：** 当设备所属产品的认证类型是X.509时，只要当前批次中，任意一个设备或X.509证书创建失败，则返回创建失败。 |
|ValidList|List|\{ "Name": \[\] \}|-   当返回**Status**参数值为**CHECK\_FAILED**或**CREATE\_FAILED**时，返回创建成功的设备名称集合。
-   当返回**Status**参数值为**CHECK\_SUCCESS**或**CREATE\_SUCCESS**时，该参数为空数组。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryBatchRegisterDeviceStatus
&ProductKey=a1BwAGV****
&ApplyId=1234567
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryBatchCheckDeviceNamesStatusResponse>
  <Data>
        <Status>CREATE_SUCCESS</Status>
        <ValidList></ValidList>
        <InvalidList></InvalidList>
  </Data>
  <RequestId>F731C7F3-A86C-4039-9FCA-5F802F3C59A1</RequestId>
  <Success>true</Success>
</QueryBatchCheckDeviceNamesStatusResponse>
```

`JSON` 格式

```
{
	"Data": {
		"Status": "CREATE_SUCCESS",
		"ValidList": {
			"Name": []
		},
		"InvalidList": {
			"Name": []
		}
	},
	"RequestId": "F731C7F3-A86C-4039-9FCA-5F802F3C59A1",
	"Success": true
}
```

