# QueryPageByApplyId

调用该接口查询批量注册的设备信息。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为50。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryPageByApplyId&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryPageByApplyId|系统规定参数。取值：QueryPageByApplyId。 |
|ApplyId|Long|是|1295006|要查询的申请批次ID。申请批次ID可在[BatchRegisterDeviceWithApplyId](~~69514~~)和[BatchRegisterDevice](~~69473~~)接口返回结果中查看。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|CurrentPage|Integer|否|1|指定从返回结果中的第几页开始显示。默认值是1。 |
|PageSize|Integer|否|10|指定返回结果中每页显示的记录数量。数量限制：每页最多可显示50条。默认值是10。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|ApplyDeviceList|Array of ApplyDeviceInfo| |调用成功时，生成的已注册的设备列表（**ApplyDeviceInfo**）。 |
|ApplyDeviceInfo| | | |
|DeviceId|String|gQG2GJ2y10m6hIk8\*\*\*\*|设备ID（旧版参数）。

 **说明：** 该参数是旧版本遗留参数，已无实际作用，不能用来标识设备。目前有效的设备标识符为**IotId**和**ProductKey**与**DeviceName**组合。 |
|DeviceName|String|light|设备名称。 |
|DeviceSecret|String|SkfeXXKrTgp1DbDxYr74mfJ5cnui\*\*\*\*|设备密钥。 |
|IotId|String|vWxNur6BUApsqjv9\*\*\*\*000100|设备ID，物联网平台为该设备颁发的唯一标识符。 |
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|Page|Integer|1|当前页面号。 |
|PageCount|Integer|1|总页数。 |
|PageSize|Integer|10|每页显示的设备数。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |
|Total|Integer|2|该批次的设备总数。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryPageByApplyId
&ApplyId=1234567
&PageSize=10
&CurrentPage=1
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryPageByApplyIdResponse>
  <PageCount>1</PageCount>
  <ApplyDeviceList>
        <ApplyDeviceInfo>
              <DeviceId>vWxNur6BUApsqjv9****</DeviceId>
              <DeviceName>APItest</DeviceName>
              <DeviceSecret>tXXEtily4XuV7WS1fosJoDkhRIIU****</DeviceSecret>
              <IotId>vWxNur6BUApsqjv****4000100</IotId>
        </ApplyDeviceInfo>
        <ApplyDeviceInfo>
              <DeviceId>hoiwszKPYmHk074H****</DeviceId>
              <DeviceName>awfg</DeviceName>
              <DeviceSecret>BYpg1b2nmuq21BO7fxOogYQQZd9z****</DeviceSecret>
              <IotId>hoiwszKPYmHk074HA****000100</IotId>
        </ApplyDeviceInfo>
  </ApplyDeviceList>
  <Page>1</Page>
  <PageSize>10</PageSize>
  <RequestId>762F7AAD-8B87-4C65-BBF3-4575B002B384</RequestId>
  <Success>true</Success>
  <Total>2</Total>
</QueryPageByApplyIdResponse>
```

`JSON` 格式

```
{
	"PageCount": 1,
	"ApplyDeviceList": {
		"ApplyDeviceInfo": [
			{
				"DeviceId": "vWxNur6BUApsqjv9****",
				"DeviceName": "APItest",
				"DeviceSecret": "tXXEtily4XuV7WS1fosJoDkhRIIU****",
				"IotId": "vWxNur6BUApsqjv****4000100"
			},
			{
				"DeviceId": "hoiwszKPYmHk074H****",
				"DeviceName": "awfg",
				"DeviceSecret": "BYpg1b2nmuq21BO7fxOogYQQZd9z****",
				"IotId": "hoiwszKPYmHk074HA****000100"
			}
		]
	},
	"Page": 1,
	"PageSize": 10,
	"RequestId": "762F7AAD-8B87-4C65-BBF3-4575B002B384",
	"Success": true,
	"Total": 2
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。

